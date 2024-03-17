# Laporan Proyek Machine Learning - Flasma Veronicha H

## 1. Project Overview

Dalam era modern ini, kemajuan teknologi telah membawa perubahan besar dalam berbagai aspek kehidupan, termasuk dalam industri pariwisata. Semakin banyak orang yang mencari pengalaman unik dan berkesan dalam perjalanan mereka, membuat permintaan akan sistem rekomendasi destinasi wisata semakin meningkat.

Projek ini bertujuan untuk membangun sistem rekomendasi destinasi wisata di Surabaya, kota metropolitan terbesar kedua di Indonesia setelah Jakarta. Surabaya menawarkan beragam atraksi wisata mulai dari sejarah, budaya, kuliner, hingga hiburan modern. Dengan jumlah destinasi wisata yang begitu banyak, seringkali wisatawan merasa kesulitan untuk memilih tempat yang sesuai dengan preferensi mereka.

**Keunggulan dan Kepentingan Proyek:**
- Membantu wisatawan dalam menemukan destinasi wisata yang sesuai dengan minat dan preferensi mereka.
- Mengurangi kebingungan dan waktu yang terbuang dalam mencari informasi destinasi wisata yang tepat.
- Meningkatkan pengalaman wisatawan dengan memberikan rekomendasi yang relevan dan personal.
- Mendukung perkembangan industri pariwisata di Surabaya dengan meningkatkan kunjungan ke destinasi-destinasi yang kurang terkenal namun menarik.

**Riset Terkait:**
- Menurut survei yang dilakukan oleh Badan Pusat Statistik (BPS) pada tahun 2019, sektor pariwisata di Surabaya terus mengalami pertumbuhan signifikan dengan jumlah kunjungan wisatawan domestik maupun mancanegara yang terus meningkat setiap tahunnya [[1]]().
- Penelitian oleh Universitas Airlangga [[2]](http://www.unair.ac.id/) menunjukkan bahwa sebagian besar wisatawan mengalami kesulitan dalam menemukan informasi tentang destinasi wisata di Surabaya yang sesuai dengan minat mereka.
- Berdasarkan Data Kemendagri [[3]](https://www.kemendagri.go.id/), sektor pariwisata di Surabaya memiliki potensi besar untuk terus berkembang dengan adanya dukungan infrastruktur dan promosi yang lebih baik.

Dengan menggabungkan teknologi dan informasi, sistem rekomendasi destinasi wisata di Surabaya akan menjadi solusi yang efektif untuk memenuhi kebutuhan wisatawan dalam menjelajahi keindahan kota ini dengan lebih mudah dan menyenangkan.

## 2. Business Understanding
### 2.1. Problem Statements

1. Banyaknya destinasi wisata di Surabaya menyebabkan kebingungan bagi wisatawan dalam memilih tempat yang sesuai dengan minat dan preferensi mereka.
   
2. Kurangnya informasi yang tersedia secara terperinci dan relevan tentang destinasi wisata di Surabaya membuat wisatawan kesulitan dalam merencanakan perjalanan mereka.

### 2.2. Goals

1. Membangun sistem rekomendasi destinasi wisata yang dapat memberikan rekomendasi yang akurat dan personal kepada wisatawan berdasarkan minat dan preferensi mereka.
   
2. Menyediakan informasi yang lengkap dan terperinci tentang setiap destinasi wisata di Surabaya, termasuk deskripsi, fasilitas, harga, dan ulasan pengunjung.

### 2.3 Solutions

1. Sistem Rekomendasi _Content-Based Filtering_: Menggunakan metode analisis konten untuk merekomendasikan destinasi wisata berdasarkan kesesuaian antara profil wisatawan dan deskripsi destinasi.

2. Sistem Rekomendasi _Collaborative-Based Filtering_: Menggunakan data historis kunjungan wisatawan untuk menyajikan rekomendasi destinasi wisata kepada pengguna berdasarkan preferensi yang serupa.

## 3. Data Understanding
Data yang digunakan dalam proyek ini adalah dataset yang berisi informasi tentang destinasi wisata di Surabaya, termasuk penilaian, kategori, nama tempat, dan harga. Dataset ini akan digunakan untuk membangun sistem rekomendasi destinasi wisata di Surabaya [Kaggle](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)

**Variabel pada Dataset:**

1. `User_Id`: ID pengguna yang memberikan penilaian terhadap destinasi wisata.
   
2. `Place_Id`: ID unik untuk setiap destinasi wisata.
   
3. `Place_Ratings`: Penilaian yang diberikan oleh pengguna untuk destinasi wisata tertentu. Nilai ini berupa skala tertentu dari 1 hingga 5.
   
4. `Category`: Kategori atau jenis dari destinasi wisata
   
5. `Place_Name`: Nama destinasi wisata.
   
6. `Price`: Harga dari destinasi wisata

### 3.1 Univariate - EDA

* Total Tempat Wisata di Surabaya berdasarkan _Category_
  ![UEDA - Category](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/uni1.png)
* Total Rating berdasarka _Category_ tempat wisata
  ![UEDA - Rating](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/uni2.png)

### 3.2 Multivariate - EDA
* Top 10 Destinasi Wisata dengan Rating Tertinggi
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/multi1.png)
* Top 5 Destinasi Wisata dengan Penilaian Rata-rata Tertinggi
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/meda3.png)
* Top 5 Destinasi Wisata di Surabaya dengan Harga Tiket Masuk Tertinggi:
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/multi3.png)

