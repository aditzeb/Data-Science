# Bagian 1: Matematika & Statistika untuk Data Science

Statistika adalah fondasi utama dari Data Science. Sebelum kita membangun model machine learning yang rumit, kita harus memahami data kita menggunakan statistika deskriptif dan mengambil keputusan atau kesimpulan menggunakan statistika inferensial.

---

## 1. Statistika Deskriptif (Descriptive Statistics)

Statistika deskriptif digunakan untuk merangkum, menggambarkan, dan menyajikan data agar lebih mudah dipahami tanpa menarik kesimpulan umum untuk populasi.

### A. Ukuran Pemusatan Data (Measures of Central Tendency)
Ukuran pemusatan data menentukan nilai tengah atau pusat dari suatu dataset.

1. **Mean (Rata-rata)**
   Rata-rata aritmatika dari semua nilai dalam dataset.
   $$\mu = \frac{\sum_{i=1}^{N} X_i}{N}$$
   *Penggunaan:* Cocok untuk data numerik yang berdistribusi normal (simetris) tanpa pencilan (outliers).

2. **Median (Nilai Tengah)**
   Nilai tengah setelah data diurutkan dari terkecil ke terbesar.
   *Penggunaan:* Sangat baik untuk data yang memiliki pencilan (skewed data), seperti data gaji karyawan.

3. **Mode (Modus)**
   Nilai yang paling sering muncul dalam dataset.
   *Penggunaan:* Cocok untuk data kategorikal atau nominal (misalnya: warna favorit, jenis kelamin).

### B. Ukuran Penyebaran Data (Measures of Dispersion)
Ukuran penyebaran mengukur seberapa jauh data menyebar dari nilai pusatnya.

1. **Variance (Varians)**
   Rata-rata dari kuadrat selisih setiap titik data dengan mean.
   - Varians Populasi ($\sigma^2$):
     $$\sigma^2 = \frac{\sum (X_i - \mu)^2}{N}$$
   - Varians Sampel ($s^2$, menggunakan koreksi Bessel $N-1$):
     $$s^2 = \frac{\sum (X_i - \bar{X})^2}{N - 1}$$

2. **Standard Deviation (Deviasi Standar)**
   Akar kuadrat dari varians. Deviasi standar memiliki satuan yang sama dengan data asli.
   $$\sigma = \sqrt{\sigma^2} \quad \text{dan} \quad s = \sqrt{s^2}$$

3. **Coefficient of Variation (Koefisien Variasi - CV)**
   Ukuran penyebaran relatif yang dinyatakan dalam persentase. Digunakan untuk membandingkan variabilitas antar kelompok data dengan skala yang berbeda.
   $$CV = \left( \frac{s}{\bar{X}} \right) \times 100\%$$

### C. Bentuk Distribusi Data (Shape of Distribution)
1. **Skewness (Kemiringan):** Mengukur ketidaksimetrisan distribusi data.
   - *Skewness = 0:* Distribusi simetris (Normal).
   - *Skewness > 0 (Positive Skew):* Ekor distribusi memanjang ke kanan (banyak nilai kecil, sedikit nilai sangat besar).
   - *Skewness < 0 (Negative Skew):* Ekor distribusi memanjang ke kiri.
2. **Kurtosis (Keruncingan):** Mengukur keruncingan atau ketebalan ekor distribusi.
   - *Mesokurtik:* Distribusi normal.
   - *Leptokurtik:* Distribusi runcing dengan ekor tebal (outliers banyak).
   - *Platikurtik:* Distribusi datar/landai.

---

## 2. Statistika Inferensial (Inferential Statistics)

Statistika inferensial digunakan untuk mengambil kesimpulan atau membuat generalisasi tentang suatu populasi berdasarkan analisis sampel data.

### A. Uji Hipotesis (Hypothesis Testing)
Uji hipotesis adalah prosedur formal untuk menentukan apakah klaim (hipotesis) tentang populasi didukung oleh bukti sampel.

- **Hipotesis Nol ($H_0$):** Pernyataan bahwa tidak ada efek, perbedaan, atau hubungan (status quo).
- **Hipotesis Alternatif ($H_1$ atau $H_a$):** Klaim yang ingin kita buktikan (ada efek, perbedaan, atau hubungan).

### B. P-value dan Significance Level ($\alpha$)
- **Significance Level ($\alpha$):** Batas probabilitas untuk menolak $H_0$. Biasanya diatur sebesar $0.05$ (5%).
- **P-value:** Probabilitas mendapatkan hasil sampel ekstrem jika $H_0$ benar.
  - Jika **P-value $\le \alpha$**: Tolak $H_0$ (Hasil signifikan secara statistik).
  - Jika **P-value $> \alpha$**: Gagal menolak $H_0$ (Hasil tidak signifikan secara statistik).

### C. Jenis Uji Hipotesis yang Sering Digunakan

| Nama Uji | Kegunaan | Contoh Kasus |
| :--- | :--- | :--- |
| **One-Sample t-Test** | Membandingkan rata-rata 1 sampel dengan rata-rata populasi teoritis. | Apakah rata-rata tinggi badan siswa kelas A = 165 cm? |
| **Independent Two-Sample t-Test** | Membandingkan rata-rata dari 2 kelompok independen. | Apakah ada perbedaan signifikan nilai ujian antara kelas A dan kelas B? |
| **Paired Sample t-Test** | Membandingkan rata-rata dari kelompok yang sama sebelum dan sesudah perlakuan. | Uji efektivitas obat penurun berat badan sebelum vs sesudah konsumsi. |
| **ANOVA (Analysis of Variance)** | Membandingkan rata-rata dari 3 kelompok atau lebih. | Apakah ada perbedaan hasil panen menggunakan Pupuk A, B, dan C? |
| **Chi-Square Test** | Menguji hubungan/asosiasi antara dua variabel kategorikal. | Hubungan antara jenis kelamin dengan pilihan produk belanja online. |

---

## 3. Implementasi Singkat dengan Python

Berikut cara melakukan analisis statistika sederhana menggunakan library Python standard:

```python
import numpy as np
from scipy import stats
import statistics

# Dataset Contoh
data = [77, 50, 99, 60, 90, 82, 93, 75, 86, 99, 55, 79]

# 1. Statistika Deskriptif
mean_val = statistics.mean(data)
median_val = statistics.median(data)
mode_val = statistics.mode(data)
std_sample = statistics.stdev(data) # ddof=1
variance_sample = statistics.variance(data) # ddof=1

print(f"Mean: {mean_val}")
print(f"Median: {median_val}")
print(f"Mode: {mode_val}")
print(f"Sample Std Dev: {std_sample:.4f}")
print(f"Sample Variance: {variance_sample:.4f}")

# 2. Uji Hipotesis (Contoh: One-Sample t-Test)
# Kita uji apakah rata-rata populasi data ini sama dengan 70 (H0: mu = 70)
t_stat, p_val = stats.ttest_1samp(data, popmean=70)
print(f"\nt-Statistic: {t_stat:.4f}")
print(f"P-value: {p_val:.4f}")

alpha = 0.05
if p_val <= alpha:
    print("Kesimpulan: Tolak H0 (Rata-rata tidak sama dengan 70)")
else:
    print("Kesimpulan: Gagal menolak H0 (Rata-rata sama dengan 70 secara statistik)")
```

*Untuk melihat implementasi lengkap beserta visualisasi distribusinya, silakan buka file notebook:*
👉 [01_descriptive_and_inferential_statistics.ipynb](file:///c:/Users/Adit%20Victus/Desktop/Github/Data-Science/notebooks/01_descriptive_and_inferential_statistics.ipynb)
