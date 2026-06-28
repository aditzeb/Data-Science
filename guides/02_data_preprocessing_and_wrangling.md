# Bagian 2: Data Preprocessing & Wrangling

Dalam dunia nyata, data mentah (raw data) sangat jarang berada dalam kondisi bersih dan siap pakai. Lebih dari 70% waktu seorang Data Scientist dihabiskan untuk melakukan data cleaning, preprocessing, dan data wrangling. Bagian ini menjelaskan teknik-teknik wajib untuk mempersiapkan data Anda.

---

## 1. Pengenalan Pandas & Numpy

- **Numpy (Numerical Python):** Library dasar untuk komputasi numerik berkinerja tinggi menggunakan array multi-dimensi (`ndarray`).
- **Pandas:** Library analisis data yang menyediakan struktur data tingkat tinggi:
  - `Series`: Array 1-dimensi berlabel.
  - `DataFrame`: Tabel data 2-dimensi yang menyerupai spreadsheet atau tabel SQL.

---

## 2. Pembersihan Data (Data Cleaning)

### A. Mengatasi Missing Values (Data Hilang)
Penyebab hilangnya data bisa bermacam-macam (alat rusak, kesalahan input, dll). Cara mengatasinya:
1. **Deteksi:** Menggunakan `.isnull()` atau `.info()`.
2. **Penanganan:**
   - **Drop (Hapus):** Menghapus baris atau kolom (`.dropna()`). Lakukan jika persentase missing values sangat kecil (< 5%).
   - **Imputasi (Mengisi):** Mengisi nilai kosong (`.fillna()`) dengan:
     - Mean atau Median (untuk data numerik).
     - Mode / Modus (untuk data kategorikal).
     - Forward Fill / Backward Fill (untuk data time-series).

### B. Mengatasi Duplikasi Data
Duplikasi data dapat mengacaukan analisis statistik dan membuat model overfitting.
- **Deteksi:** `.duplicated().sum()`
- **Penanganan:** `.drop_duplicates(inplace=True)`

### C. Mengatasi Outliers (Pencilan)
Outliers adalah nilai data yang menyimpang secara signifikan dari mayoritas data lainnya.
- **Deteksi:**
  - **Metode IQR (Interquartile Range):**
    $$IQR = Q_3 - Q_1$$
    $$\text{Batas Bawah} = Q_1 - 1.5 \times IQR$$
    $$\text{Batas Atas} = Q_3 + 1.5 \times IQR$$
  - **Metode Z-Score:** Nilai data dengan $Z > 3$ atau $Z < -3$ dikategorikan sebagai outlier.
- **Penanganan:**
  - Menghapus baris pencilan.
  - Capping/Flooring (mengganti outlier dengan batas atas/bawah IQR).

---

## 3. Rekayasa Fitur (Feature Engineering)

### A. Feature Scaling (Penskalaan Fitur)
Algoritma machine learning yang mengandalkan perhitungan jarak (seperti KNN, SVM, K-Means, Gradient Descent) sangat sensitif terhadap perbedaan skala antar variabel.

1. **Standardization (Standard Scaler):**
   Mengubah data sehingga memiliki rata-rata ($\mu$) = 0 dan standar deviasi ($\sigma$) = 1.
   $$X_{new} = \frac{X - \mu}{\sigma}$$
   *Sifat:* Tidak membatasi data pada rentang tertentu, cocok untuk algoritma yang mengasumsikan data terdistribusi normal.

2. **Normalization (Min-Max Scaler):**
   Mengubah data ke dalam rentang tertentu, biasanya 0 sampai 1.
   $$X_{new} = \frac{X - X_{min}}{X_{max} - X_{min}}$$
   *Sifat:* Sangat berguna ketika kita tahu batas atas dan bawah data, tetapi rentan terhadap pencilan (outliers).

### B. Categorical Encoding (Encoding Variabel Kategorikal)
Komputer hanya memahami angka. Oleh karena itu, variabel teks/kategori harus diubah menjadi numerik.

1. **Label Encoding (Ordinal Encoding):**
   Mengubah setiap kategori menjadi integer unik (misalnya: Rendah = 0, Sedang = 1, Tinggi = 2).
   *Kapan digunakan:* Jika kategori memiliki urutan logis (ordinal).

2. **One-Hot Encoding:**
   Membuat kolom biner baru (0 atau 1) untuk setiap kategori unik.
   *Kapan digunakan:* Jika kategori tidak memiliki urutan logis (nominal, misalnya: Warna - Merah, Hijau, Biru).
   *Fungsi Pandas:* `pd.get_dummies(df, columns=['NamaKolom'])`

---

## 4. Contoh Pemrosesan Data dengan Python

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Membuat dummy DataFrame
data = {
    'Nama': ['Budi', 'Siti', 'Joko', 'Siti', 'Rini'],
    'Umur': [25, 30, np.nan, 30, 45],
    'Gaji': [5000000, 7000000, 6000000, 7000000, 25000000], # Gaji Rini outlier
    'Kota': ['Jakarta', 'Bandung', 'Jakarta', 'Bandung', 'Surabaya']
}
df = pd.DataFrame(data)

# 1. Hapus Duplikat
df.drop_duplicates(inplace=True)

# 2. Imputasi Missing Value di kolom 'Umur' dengan median
median_umur = df['Umur'].median()
df['Umur'].fillna(median_umur, inplace=True)

# 3. Handling Outlier Gaji dengan IQR
Q1 = df['Gaji'].quantile(0.25)
Q3 = df['Gaji'].quantile(0.75)
IQR = Q3 - Q1
upper_bound = Q3 + 1.5 * IQR
# Filter outlier
df_clean = df[df['Gaji'] <= upper_bound]

# 4. Feature Scaling (Standardization)
scaler = StandardScaler()
df_clean['Gaji_Scaled'] = scaler.fit_transform(df_clean[['Gaji']])

# 5. One-Hot Encoding untuk kolom 'Kota'
df_final = pd.get_dummies(df_clean, columns=['Kota'], drop_first=True)

print("DataFrame Final Setelah Preprocessing:")
print(df_final)
```

*Untuk melakukan latihan langsung dengan dataset nyata, buka notebook berikut:*
👉 [02_data_preprocessing_and_wrangling.ipynb](file:///c:/Users/Adit%20Victus/Desktop/Github/Data-Science/notebooks/02_data_preprocessing_and_wrangling.ipynb)
