# Analisis Prediktif Customer Churn dan Strategi Retensi Pelanggan

## Ringkasan Proyek

Proyek ini bertujuan untuk menganalisis faktor-faktor yang menyebabkan *customer churn* (pelanggan berhenti berlangganan) menggunakan dataset dari Kaggle. Dengan memahami penyebab utama churn, kita dapat membangun model prediktif untuk mengidentifikasi pelanggan yang berisiko dan merumuskan strategi bisnis yang efektif untuk meningkatkan retensi pelanggan.

Customer churn adalah metrik krusial yang berdampak langsung pada pendapatan dan pertumbuhan perusahaan. Analisis ini fokus pada bagaimana data seperti demografi, durasi berlangganan, frekuensi penggunaan, dan interaksi dengan layanan pelanggan dapat memprediksi kemungkinan seorang pelanggan untuk churn.

---

## Dataset

Dataset yang digunakan adalah **Customer Churn Dataset** yang tersedia di Kaggle.

- **Sumber**: [Kaggle Customer Churn Dataset](https://www.kaggle.com/datasets/muhammadshahidazeem/customer-churn-dataset)
- **Volume Data**: 440,832 baris data pelanggan.

### Struktur Data (Fitur)

| Nama Kolom         | Tipe Data | Deskripsi                                             |
| ------------------ | --------- | ----------------------------------------------------- |
| `CustomerID`       | float64   | ID unik untuk setiap pelanggan.                       |
| `Age`              | float64   | Usia pelanggan.                                       |
| `Gender`           | object    | Jenis kelamin pelanggan.                              |
| `Tenure`           | float64   | Lama waktu pelanggan telah berlangganan (dalam bulan). |
| `Usage Frequency`  | float64   | Seberapa sering pelanggan menggunakan layanan.         |
| `Support Calls`    | float64   | Jumlah panggilan yang dibuat ke pusat bantuan.        |
| `Payment Delay`    | float64   | Rata-rata keterlambatan pembayaran (dalam hari).      |
| `Subscription Type`| object    | Jenis langganan yang dipilih (e.g., Basic, Standard, Premium). |
| `Contract Length`  | object    | Durasi kontrak (e.g., Monthly, Quarterly, Annual).    |
| `Total Spend`      | float64   | Total uang yang dihabiskan oleh pelanggan.            |
| `Last Interaction` | float64   | Jumlah hari sejak interaksi terakhir pelanggan.       |
| `Churn`            | float64   | **Target Variable**: 1 jika pelanggan churn, 0 jika tidak. |

---

## Alur Kerja Proyek

1.  **Eksplorasi Data (EDA)**: Memahami distribusi data, mengidentifikasi nilai yang hilang, dan melihat korelasi antar fitur.
2.  **Pra-pemrosesan Data**: Mengubah fitur kategorikal (seperti `Gender`, `Subscription Type`) menjadi format numerik menggunakan *one-hot encoding* atau *label encoding*.
3.  **Pemodelan**: Membangun model klasifikasi (misalnya, Regresi Logistik) untuk memprediksi variabel target `Churn`.
4.  **Evaluasi Model**: Mengukur performa model menggunakan metrik seperti Akurasi, Presisi, Recall, dan F1-Score.
5.  **Interpretasi & Analisis**: Menganalisis koefisien model untuk memahami faktor-faktor pendorong utama churn.
6.  **Rekomendasi Bisnis**: Merumuskan strategi yang dapat ditindaklanjuti berdasarkan temuan dari model.

---

## Hasil Analisis Model: Faktor Pendorong Churn

Analisis ini menggunakan model regresi logistik untuk memahami pengaruh setiap fitur terhadap kemungkinan churn. Koefisien positif menunjukkan peningkatan kemungkinan churn, sedangkan koefisien negatif menunjukkannya penurunan.

| Fitur                 | Koefisien  | Interpretasi                                                                                                                                 | Tingkat Dampak |
| --------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| **Support Calls**     | **+2.12**  | Peningkatan jumlah panggilan ke pusat bantuan secara signifikan **meningkatkan kemungkinan churn**. Ini adalah indikator terkuat dari ketidakpuasan pelanggan. | **Sangat Tinggi** |
| **Payment Delay**     | **+0.85**  | Keterlambatan pembayaran **meningkatkan risiko churn**, bisa disebabkan oleh ketidakpuasan, masalah finansial, atau friksi dalam proses pembayaran. | **Tinggi** |
| **Last Interaction**  | **+0.48**  | Semakin lama waktu sejak interaksi terakhir, **semakin besar kemungkinan churn**. Ini menandakan pelanggan yang mulai tidak terlibat (*disengaged*). | **Sedang** |
| **Age**               | **+0.41**  | Usia yang lebih tua **sedikit meningkatkan kemungkinan churn**, mungkin karena perubahan kebutuhan atau preferensi layanan. | **Sedang** |
| **Gender**            | **−0.52**  | Pria (direpresentasikan dengan 1) cenderung **lebih kecil kemungkinannya untuk churn** dibandingkan wanita. | **Sedang** |
| **Total Spend**       | **−1.34**  | Pelanggan yang menghabiskan lebih banyak uang memiliki **kemungkinan churn lebih rendah**. Ini menunjukkan nilai dan loyalitas yang tinggi. | **Tinggi** |
| **Tenure**            | **−0.12**  | Pelanggan yang sudah lama bergabung **cenderung lebih setia** dan lebih kecil kemungkinannya untuk churn. | **Rendah** |
| **Usage Frequency**   | **−0.11**  | Pelanggan yang lebih sering menggunakan layanan **cenderung bertahan**, karena mereka merasakan manfaat dari produk. | **Rendah** |
| **Subscription Type** | **−0.04**  | Tipe langganan memiliki pengaruh kecil terhadap churn. | **Sangat Rendah** |
| **Contract Length**   | **−0.002** | Durasi kontrak hampir tidak berpengaruh terhadap churn dalam model ini. | **Sangat Rendah** |

---

## Solusi Bisnis dan Rekomendasi Strategis

Berdasarkan temuan di atas, berikut adalah rekomendasi strategis untuk mengurangi *customer churn*:

### 1. **Prioritas Utama: Revitalisasi Layanan Pelanggan (Customer Support)**
- **Fokus pada Pelanggan Berisiko**: Identifikasi pelanggan dengan jumlah `Support Calls` yang tinggi (misalnya, >2 panggilan dalam sebulan). Tim *customer success* dapat secara proaktif menghubungi mereka untuk menyelesaikan masalah sebelum mereka memutuskan untuk churn.
- **Analisis Akar Masalah**: Analisis tiket bantuan untuk menemukan keluhan yang paling sering muncul. Jika banyak panggilan terkait masalah teknis, perbaiki produknya. Jika terkait penagihan, perbaiki sistemnya.

### 2. **Ciptakan "Golden Handcuffs" untuk Pelanggan Bernilai Tinggi**
- **Program Loyalitas Berjenjang**: Pelanggan dengan `Total Spend` tinggi adalah aset. Buat program loyalitas eksklusif (misal: Platinum Tier) yang memberikan keuntungan seperti akses prioritas ke layanan pelanggan, diskon khusus, atau akses awal ke fitur baru.
- **Personalisasi Penawaran**: Gunakan data `Usage Frequency` dan `Total Spend` untuk memberikan penawaran yang relevan, membuat mereka merasa dihargai.

### 3. **Minimalkan Kendala Pembayaran**
- **Sistem Pembayaran Fleksibel**: Untuk mengatasi `Payment Delay`, sediakan berbagai metode pembayaran (e-wallet, transfer bank, kartu kredit) dan kirim pengingat pembayaran otomatis (H-3, H-1, hari H).
- **Kampanye Re-engagement**: Targetkan pelanggan dengan `Last Interaction` yang sudah lama. Kirim email berisi rangkuman fitur baru, studi kasus, atau penawaran khusus untuk "membangunkan" mereka kembali.

### 4. **Pemasaran Tersegmentasi Berbasis Demografi**
- **Segmentasi Usia & Gender**: Karena `Age` dan `Gender` memiliki pengaruh, buat kampanye pemasaran yang disesuaikan. Misalnya:
    - **Wanita**: Tawarkan konten atau promosi yang lebih sesuai dengan persona mereka.
    - **Pelanggan Lebih Tua**: Pastikan antarmuka produk mudah digunakan dan tawarkan panduan atau webinar untuk membantu adaptasi.

Dengan menerapkan strategi ini secara terarah, perusahaan dapat secara efektif menekan angka churn, meningkatkan loyalitas, dan mengamankan pendapatan jangka panjang.

---

## Teknologi yang Digunakan

- **Bahasa**: Python 
- **Library**: Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn
- **Tools**: Jupyter Notebook, Git, GitHub
