# Bagian 3: Exploratory Data Analysis (EDA) & Visualisasi

Exploratory Data Analysis (EDA) adalah pendekatan analisis data untuk memahami karakteristik utama dari suatu dataset, seringkali secara visual. EDA membantu kita menemukan pola, mendeteksi anomali, menguji hipotesis, dan memeriksa asumsi dasar sebelum pemodelan machine learning.

---

## 1. Jenis-jenis Analisis Data dalam EDA

### A. Univariate Analysis (Analisis Satu Variabel)
Fokus pada distribusi dan statistik dari satu variabel tunggal.
- **Variabel Numerik:**
  - **Histogram:** Menampilkan frekuensi nilai numerik dalam interval tertentu (bins).
  - **KDE Plot (Kernel Density Estimate):** Menunjukkan estimasi kurva probabilitas kepadatan data (versi halus dari histogram).
  - **Boxplot:** Menampilkan visualisasi ringkasan lima angka (Minimum, Q1, Median, Q3, Maksimum) serta outlier.
- **Variabel Kategorikal:**
  - **Bar Chart (Countplot):** Menunjukkan jumlah atau frekuensi setiap kategori.
  - **Pie Chart:** Menunjukkan proporsi persentase dari setiap kategori.

### B. Bivariate Analysis (Analisis Dua Variabel)
Menganalisis hubungan atau korelasi antara dua variabel yang berbeda.
- **Numerik vs Numerik:**
  - **Scatter Plot:** Menunjukkan titik-titik koordinat data untuk mendeteksi korelasi linier atau pola spasial.
  - **Line Plot:** Menunjukkan tren variabel numerik sepanjang waktu atau sekuens tertentu.
- **Kategorik vs Numerik:**
  - **Boxplot Terkelompok:** Membandingkan distribusi nilai numerik di berbagai kategori.
  - **Bar Plot Rata-rata:** Membandingkan nilai rata-rata variabel numerik antar kategori.
- **Kategorik vs Kategorik:**
  - **Stacked Bar Chart:** Memperlihatkan proporsi kategori kedua di dalam kategori pertama.

### C. Multivariate Analysis (Analisis Banyak Variabel)
Melihat hubungan antara tiga atau lebih variabel secara bersamaan.
- **Heatmap Korelasi:** Menampilkan matriks koefisien korelasi Pearson/Spearman antar variabel numerik menggunakan warna.
- **Pairplot:** Grid scatter plot yang memetakan hubungan berpasangan untuk seluruh variabel dalam dataset sekaligus.
- **Scatter Plot dengan Hue/Size:** Scatter plot 2D tradisional tetapi menggunakan warna (`hue`) atau ukuran titik (`size`) untuk merepresentasikan variabel ketiga/keempat.

---

## 2. Koefisien Korelasi (Correlation Coefficient)

Mengukur kekuatan dan arah hubungan linear antara dua variabel numerik.
- **Nilai Korelasi ($r$):** Berada di rentang $-1$ hingga $1$.
  - $r = 1$: Korelasi positif sempurna (jika X naik, Y pasti naik).
  - $r = 0$: Tidak ada korelasi linier.
  - $r = -1$: Korelasi negatif sempurna (jika X naik, Y pasti turun).
- **Korelasi $\neq$ Kausalitas:** Adanya hubungan statistik (korelasi) tidak berarti satu variabel menyebabkan variabel lainnya terjadi.

---

## 3. Best Practices Visualisasi Data Premium

Untuk membuat grafik yang mengesankan (WOW factor) dan profesional:
1. **Selalu Beri Label:** Setiap sumbu wajib memiliki label sumbu X, sumbu Y, judul grafik (`title`), dan legenda jika menggunakan warna.
2. **Pilih Palette Warna yang Harmonis:** Hindari warna dasar murni (seperti merah/biru terang bawaan). Gunakan palette bawaan Seaborn seperti `viridis`, `plasma`, `coolwarm`, atau `muted`.
3. **Gunakan Grid Garis Tipis:** Mempermudah pembaca membaca nilai koordinat tanpa membuat layar terasa penuh.
4. **Sederhanakan Layout:** Hapus garis bingkai atas dan kanan yang tidak diperlukan menggunakan `sns.despine()`.

---

## 4. Contoh Kode Visualisasi dengan Matplotlib & Seaborn

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# Mengatur tema visualisasi agar terlihat estetik
sns.set_theme(style="whitegrid")
plt.rcParams['figure.figsize'] = (10, 6)

# Membuat dummy dataset
np.random.seed(42)
df = pd.DataFrame({
    'Luas_Rumah': np.random.normal(120, 30, 200),
    'Harga_Jual': np.random.normal(500, 100, 200),
    'Tipe_Cluster': np.random.choice(['Ekonomis', 'Standar', 'Premium'], 200)
})

# Korelasi buatan: Luas_Rumah mempengaruhi Harga_Jual secara positif
df['Harga_Jual'] = df['Harga_Jual'] + (df['Luas_Rumah'] * 2.5)

# Visualisasi Bivariate: Scatter Plot dengan Hue (Tipe Cluster)
fig, ax = plt.subplots(figsize=(8, 5))
sns.scatterplot(
    data=df, 
    x='Luas_Rumah', 
    y='Harga_Jual', 
    hue='Tipe_Cluster', 
    palette='muted',
    alpha=0.8,
    edgecolor='w',
    ax=ax
)

# Kustomisasi Estetika
ax.set_title('Hubungan Luas Rumah terhadap Harga Jual berdasarkan Tipe Cluster', fontsize=14, fontweight='bold', pad=15)
ax.set_xlabel('Luas Rumah (meter persegi)', fontsize=12)
ax.set_ylabel('Harga Jual (Juta Rupiah)', fontsize=12)
sns.despine() # Menghilangkan border atas dan kanan

plt.tight_layout()
# Untuk menampilkan plot: plt.show()
```

*Untuk melihat grafik interaktif dan melakukan analisis eksploratif pada dataset riil, buka notebook:*
👉 [03_exploratory_data_analysis.ipynb](file:///c:/Users/Adit%20Victus/Desktop/Github/Data-Science/notebooks/03_exploratory_data_analysis.ipynb)
