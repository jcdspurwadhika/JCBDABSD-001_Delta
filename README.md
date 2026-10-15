# Optimasi Kampanye Telemarketing Deposito

Analisis data untuk mengevaluasi efisiensi kampanye telemarketing deposito berjangka. Project ini mencari pola penggunaan panggilan, mengidentifikasi kelompok nasabah yang lebih potensial, dan mensimulasikan aturan pembatasan panggilan untuk mengurangi aktivitas yang kurang efektif.

## Latar Belakang

Kampanye telemarketing pada dataset Bank Marketing menghasilkan conversion rate yang relatif rendah dibandingkan total upaya panggilan. Analisis ini berfokus pada dua pertanyaan bisnis:

- Nasabah mana yang sebaiknya dihubungi lebih dahulu?
- Berapa kali nasabah perlu dihubungi agar penggunaan panggilan lebih efisien tanpa mengurangi terlalu banyak hasil deposito?

## Tujuan Project

- Mengukur kondisi awal kampanye melalui conversion rate dan panggilan per deposito.
- Membandingkan kinerja kampanye massal dengan kampanye selektif.
- Menganalisis hubungan karakteristik nasabah dan riwayat kampanye dengan keberhasilan pembukaan deposito.
- Mengelompokkan nasabah ke tingkat prioritas P1 sampai P4.
- Mensimulasikan beberapa batas panggilan dan membandingkan efisiensi serta jumlah deposito yang dipertahankan.
- Menyusun rekomendasi operasional yang bisa diuji oleh tim telemarketing.

## Dataset

- Nama dataset: Bank Marketing (`bank-full.csv`)
- Sumber yang dicatat pada notebook: UCI Machine Learning Repository, diakses melalui Kaggle
- Periode kampanye: Mei 2008 sampai November 2010
- Format file: CSV dengan pemisah titik koma (`;`)
- Ukuran awal: 45.211 baris dan 17 kolom
- Ukuran setelah preprocessing: 45.208 baris
- Target analisis: kolom `y`, yaitu apakah nasabah membuka deposito berjangka (`yes` atau `no`)

Dataset memuat informasi profil nasabah, kondisi keuangan, kanal kontak, riwayat kampanye sebelumnya, jumlah panggilan selama kampanye berjalan, dan hasil penawaran. Dataset tidak memiliki ID unik nasabah. Karena itu, analisis tidak dapat melacak individu yang sama secara langsung antar-kampanye.

## Teknologi yang Digunakan

- Python
- Jupyter Notebook
- pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy

## Alur Analisis

1. Business understanding dan perumusan business questions.
2. Import dataset dan pemeriksaan struktur data.
3. Exploratory Data Analysis (EDA), termasuk statistik deskriptif, nilai kategori, nilai `unknown`, duplikat, outlier, anomali, dan korelasi.
4. Data cleaning dan preprocessing.
5. Feature engineering untuk membuat kelompok usia, beban pinjaman, intensitas panggilan, tahun, mode kampanye, dan tingkat prioritas nasabah.
6. Analisis statistik, termasuk Chi-Square, Cramér's V, uji dua proporsi, serta pemeriksaan distribusi variabel numerik.
7. Perbandingan hasil berdasarkan waktu kampanye, mode kampanye, jumlah panggilan, profil nasabah, dan tingkat prioritas.
8. Simulasi batas panggilan, interpretasi KPI, penyusunan kesimpulan, rekomendasi, dan batasan analisis.

## Aturan Prioritas Nasabah

Notebook mengelompokkan nasabah menggunakan informasi yang tersedia sebelum panggilan dilakukan.

| Prioritas | Kriteria |
|---|---|
| P1 | Nasabah pernah membuka deposito pada kampanye sebelumnya. |
| P2 | Tidak memiliki KPR maupun pinjaman pribadi, serta berstatus pelajar/pensiunan atau memiliki saldo minimal €1.000. |
| P3 | Tidak memiliki KPR maupun pinjaman pribadi, tetapi tidak memenuhi kriteria P2. |
| P4 | Memiliki KPR atau pinjaman pribadi. |

Jika nasabah memenuhi kriteria P1, kelompok tersebut menjadi prioritas utama.

## Temuan Utama

Angka berikut berasal dari hasil analisis yang tercatat di notebook.

| Metrik | Hasil awal |
|---|---:|
| Catatan nasabah setelah cleaning | 45.208 |
| Nasabah yang membuka deposito | 5.289 |
| Conversion rate keseluruhan | 11,7% |
| Total panggilan | 124.935 |
| Panggilan per deposito | 23,6 |
| Panggilan kepada nasabah yang akhirnya menolak | 90,9% dari seluruh panggilan |

### Kampanye Massal dan Selektif

Kampanye massal ditetapkan sebagai kampanye dengan sedikitnya 1.000 nasabah dalam satu bulan. Kampanye di bawah ambang tersebut dikategorikan sebagai kampanye selektif.

| Metrik | Massal | Selektif |
|---|---:|---:|
| Conversion rate | 6,7% | 45,8% |
| Persentase seluruh panggilan | 91,4% | 8,6% |
| Persentase seluruh deposito | 49,7% | 50,3% |
| Panggilan per deposito | 43,4 | 4,0 |

### Conversion Rate per Prioritas

| Prioritas | Conversion rate | Panggilan per deposito |
|---|---:|---:|
| P1 | 64,7% | 2,8 |
| P2 | 19,7% | 13,8 |
| P3 | 11,2% | 26,9 |
| P4 | 6,8% | 40,1 |

P1 memiliki conversion rate tertinggi. Pada kampanye massal, P2 juga menunjukkan hasil yang lebih baik dibandingkan P3 dan P4.

## Simulasi Rekomendasi

Skenario yang direkomendasikan pada notebook adalah tidak membatasi panggilan untuk P1, lalu membatasi P2 sampai P4 hingga maksimal tiga panggilan.

| Metrik | Kondisi awal | Skenario rekomendasi |
|---|---:|---:|
| Total panggilan | 124.935 | 88.304 |
| Perubahan jumlah panggilan | 0% | Turun 29,3% |
| Deposito yang dipertahankan | 100% | 87,7% |
| Panggilan per deposito | 23,6 | 19,0 |

Simulasi ini menggunakan data historis. Deposito yang tercatat setelah batas panggilan diperlakukan sebagai hasil yang berisiko hilang. Angka tersebut merupakan estimasi, bukan hasil implementasi pada kampanye baru.

## Rekomendasi Bisnis

- Susun daftar kontak berdasarkan prioritas P1, P2, P3, lalu P4.
- Batasi panggilan maksimal tiga kali untuk P2 sampai P4, dengan pengecualian P1.
- Pertimbangkan mengalihkan kapasitas panggilan yang dihemat untuk menghubungi calon nasabah baru.
- Uji aturan baru pada satu kampanye massal melalui A/B test sebelum menerapkannya secara luas.
- Lengkapi pencatatan data, terutama ID nasabah, tanggal kontak, hasil setiap panggilan, durasi, sumber daftar, dan kanal kontak.

## Cara Menjalankan

1. Siapkan Python dan Jupyter Notebook.
2. Install library yang digunakan:

   ```bash
   pip install pandas numpy matplotlib seaborn scipy notebook
   ```

3. Simpan `bank-full.csv` di folder yang sama dengan notebook.
4. Buka notebook `Final_Project_Telemarketing_Deposito (1).ipynb` melalui Jupyter Notebook.
5. Jalankan sel notebook secara berurutan untuk meninjau analisis, tabel, dan visualisasi.

Notebook membaca file data menggunakan pemisah titik koma, sesuai format `bank-full.csv`.

## Batasan Analisis

- Hasil penghematan dan retensi deposito berasal dari simulasi historis, bukan uji coba operasional.
- Tahun direkonstruksi dari urutan bulan karena kolom tahun tidak tersedia secara langsung pada dataset.
- Data tidak menyediakan ID unik nasabah atau riwayat lengkap setiap panggilan.
- Data biaya telemarketing dan nilai setiap deposito tidak tersedia, sehingga dampak finansial belum dapat dihitung.
- Dataset berasal dari satu bank di Portugal pada periode 2008 sampai 2010. Hasilnya belum tentu berlaku dengan pola yang sama pada bank atau periode lain.
- Beberapa fungsi helper pada notebook perlu diperiksa sebelum menjalankan ulang seluruh sel dari kernel kosong. Contohnya, `uji_chi_square` dipanggil dengan jumlah argumen yang berbeda dari definisinya, sementara fungsi `uji_dua_proporsi` dan `tabel_kpi` digunakan tanpa definisi yang terlihat di file. Fungsi `chi2_contingency` juga perlu diimpor secara eksplisit atau dipanggil melalui `stats.chi2_contingency`.

## Referensi

- Moro, S., Laureano, R., & Cortez, P. (2011). *Using data mining for bank direct marketing: An application of the CRISP-DM methodology*. Proceedings of the European Simulation and Modelling Conference (ESM 2011), 117–121.
- Moro, S., Cortez, P., & Rita, P. (2014). *A data-driven approach to predict the success of bank telemarketing*. Decision Support Systems, 62, 22–31.
- Dataset: *Bank Marketing*, UCI Machine Learning Repository.

---

Project ini berfokus pada analisis bisnis dan statistik deskriptif-inferensial. Notebook saat ini tidak membangun atau melatih model machine learning untuk prediksi.
