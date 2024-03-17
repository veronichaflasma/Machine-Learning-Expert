# Laporan Proyek Machine Learning - Flasma Veronicha H

![SBY VIEW](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/wisata%20sby.jpg)

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

## 4. Data Preparation
4.1. **Penggabungan Dataset**:
   - **Tahap**: Menggabungkan dua dataset, yaitu `sby_tourism` dan `rating_tourism`, menggunakan fungsi `merge()`.
      ```
      sby_package = pd.merge(tourism_rating, sby_tourism[['Place_Id','Category','Place_Name','Price']],
                    how='right', on='Place_Id')
      sby_package
      ```
   - **Alasan**: Penggabungan dataset dilakukan untuk menggabungkan informasi yang relevan dari kedua dataset. Misalnya, jika dataset `package_tourism.csv` berisi informasi tentang film, dan dataset `rating.csv` berisi rating pengguna untuk setiap `package_tourism`, maka dengan menggabungkan kedua dataset tersebut juga dapat menganalisis hubungan antara atribut `package_tourism` dengan `user`.

4.2. **Penanganan Nilai yang Hilang dan Column yang tidak digunakan**:
   - **Tahap**: Menghapus column yang tidak digunakan `drop()`.
     ```
     sby_tourism = sby_tourism.drop(sby_tourism.columns[[7, 11, 12]], axis=1)
     ```
     Pengecekan _missing values_
     ```
     missing = sby_tourism.isnull().sum()
     missing_val = pd.DataFrame({'Missing Values': missing})
     print(missing_val)
     ```
   - **Alasan**: Nilai yang hilang dapat memengaruhi kualitas analisis dan model yang dibuat dari data tersebut. Menghapus baris dengan nilai yang hilang dapat meningkatkan keakuratan analisis dan memastikan bahwa model yang dibuat berdasarkan data tersebut lebih dapat diandalkan.

4.3. **Penghapusan Data Berulang**:
   - **Tahap**: Menghapus baris yang merupakan duplikat menggunakan fungsi `drop_duplicates()`
     ```
     destinations = sby_package.drop_duplicates('Place_Id')
     destinations
     ```
   - **Alasan**: Data duplikat dapat memengaruhi hasil analisis dengan cara yang tidak diinginkan. Menghapus data duplikat membantu meminimalkan redundansi dan mencegah hasil analisis yang bias atau tidak akurat karena keberadaan data yang sama dengan nilai yang sama.

## 5. Modeling
### 5.1 Content-Based Filtering
**Algoritma Content-Based Filtering:**
![CBF](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/ContentBased.png)

1. **Inisialisasi TF-IDF Vectorizer**: 
   - Menggunakan fungsi `TfidfVectorizer()` dari library `sklearn` untuk melakukan inisialisasi.
   - Dilakukan perhitungan IDF (Inverse Document Frequency) pada kolom `Place_Name`.
   - Melakukan pemetaan array dari indeks fitur ke nama fitur.

2. **Fitting dan Transformasi Fitur `Place_Name`**: 
   - Menggunakan fungsi `fit_transform()` untuk melakukan fitting dan transformasi fitur `Place_Name` menjadi bentuk matriks TF-IDF.

3. **Mengubah Vektor TF-IDF menjadi Matrix Dense**: 
   - Menggunakan fungsi `todense()` untuk mengubah vektor TF-IDF menjadi bentuk matriks yang padat (dense matrix).

4. **Cosine Similarity**: 
   - Membuat dataframe untuk melihat matriks TF-IDF dengan kolom `Place_Name` dan baris `Category`, yang digunakan untuk melihat korelasi antar `Place_Name` dengan kategori.
   - Menghitung kesamaan (similarity degree) antar `Place_Name` menggunakan metode `cosine_similarity` dari library `sklearn`.

**Kelebihan Content-Based Filtering:**
- Tidak memerlukan data pengguna lainnya, cocok untuk pengguna dengan preferensi unik.
- Dapat memberikan rekomendasi untuk destinasi wisata baru yang belum dinilai oleh pengguna.

**Kekurangan Content-Based Filtering:**
- Rentan terhadap "filter bubble", di mana pengguna hanya menerima rekomendasi yang serupa dengan preferensi mereka saat ini.
- Tidak memperhitungkan preferensi sosial atau kolaboratif antar pengguna.

### 5.2 Collaborative Filtering
![CF](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/CollaborativeBased.png)
**Algoritma Collaborative Filtering**
1. Mencari pengguna yang memiliki preferensi serupa dengan pengguna target dan merekomendasikan destinasi wisata yang disukai oleh pengguna serupa tersebut.
2. Mencari destinasi wisata yang memiliki pola perilaku serupa dalam hal preferensi pengguna dan merekomendasikan destinasi wisata yang sering disukai bersama.

**Kelebihan Collaborative Filtering:**
- Dapat menemukan rekomendasi untuk pengguna yang memiliki preferensi yang unik karena mengandalkan perilaku pengguna.
- Tidak terlalu terpengaruh oleh fitur atau atribut yang mungkin sulit dipahami oleh sistem.

**Kekurangan Collaborative Filtering:**
- Membutuhkan data pengguna yang cukup besar untuk memberikan rekomendasi yang akurat.
- Rentan terhadap "cold start problem" ketika pengguna baru bergabung atau destinasi wisata baru ditambahkan ke dalam sistem.

## 6. Evaluation
### 6.1. Metrik Evaluasi Content-Based Filtering

Metrik evaluasi yang digunakan dalam model Content-Based Filtering adalah **Recommender System Precision**. Precision dalam konteks ini mengukur proporsi dari item yang direkomendasikan yang relevan bagi pengguna. Dalam hal ini, relevansi diukur berdasarkan seberapa baik item-item yang direkomendasikan cocok dengan preferensi sebenarnya pengguna.[[4]]()

**Rumus Recommender System Precision:**

$\ Precision = \frac{\text{Jumlah item yang direkomendasikan yang relevan}}{\text{Jumlah total item yang direkomendasikan}}\$

### 6.2 Cara Recommender System Precision Bekerja

   1. **Identifikasi Item Relevan**: Pertama, sistem harus mampu mengidentifikasi item-item yang relevan dengan preferensi pengguna.
      
   2. **Rekomendasi Item**: Sistem kemudian memberikan rekomendasi berdasarkan preferensi pengguna.
      
   3. **Perhitungan Precision**: Precision dihitung dengan membagi jumlah item yang relevan yang direkomendasikan oleh sistem dengan jumlah total item yang direkomendasikan.

### 6.2. Metrik Evaluasi Collaborative-Based Filtering
Metrik evaluasi yang digunakan dalam proyek ini adalah **Root Mean Squared Error (RMSE)**. RMSE merupakan metrik yang umum digunakan untuk mengukur tingkat kesalahan prediksi dalam konteks sistem rekomendasi. RMSE mengukur rata-rata dari selisih kuadrat antara nilai prediksi dan nilai yang diamati, kemudian diambil akar kuadratnya untuk memberikan hasil dalam unit yang sama dengan variabel yang dinilai.[[5]]()

**Hasil**
![CF Metric](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/cf%20metrics.png)

`root_mean_squared_error: 0.2749`
`val_root_mean_squared_error: 0.3642`

**Rumus Root Mean Squared Error (RMSE)**
$\ RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y_i})^2} \$

dengan:
- \( n \) adalah jumlah observasi.
- \( y_i \) adalah nilai yang diamati.
- \( \hat{y_i} \) adalah nilai yang diprediksi.

#### 6.2.1 Cara Kerja Root Mean Squared Error (RMSE)

1. **Perhitungan Selisih**: Pertama, perbedaan antara nilai yang diamati dan nilai yang diprediksi dihitung untuk setiap observasi.
   
2. **Pengkuadratan Selisih**: Selisih antara nilai yang diamati dan nilai yang diprediksi kemudian dikuadratkan untuk menyingkirkan nilai negatif dan menekankan kesalahan yang besar.
   
3. **Perhitungan Mean**: Rata-rata dari selisih kuadrat dihitung.
   
4. **Pengakaran**: Akar kuadrat dari rata-rata selisih kuadrat diambil untuk mendapatkan nilai RMSE.

#### 6.2.2 Hasil evaluasi yang diberikan dalam bentuk root mean squared error (RMSE) adalah:

1. `root_mean_squared_error`: 0.2749
2. `val_root_mean_squared_error`: 0.3642

Dalam konteks ini, kedua nilai tersebut menggambarkan tingkat kesalahan prediksi dari model sistem rekomendasi destinasi wisata di Surabaya. Perlu diingat bahwa semakin rendah nilai RMSE, semakin baik kinerja model.

- `root_mean_squared_error` adalah RMSE yang dihitung berdasarkan data pelatihan (train data), yang menunjukkan seberapa baik model mampu mempelajari pola dari data yang telah diberikan.
- `val_root_mean_squared_error` adalah RMSE yang dihitung berdasarkan data validasi (validation data), yang memberikan gambaran tentang seberapa baik model dapat melakukan prediksi pada data yang tidak pernah dilihat sebelumnya.

Dalam kasus ini, nilai RMSE pada data pelatihan lebih rendah (0.2749) dibandingkan dengan nilai RMSE pada data validasi (0.3642). Ini menunjukkan adanya overfitting, di mana model cenderung lebih baik dalam memprediksi data yang telah dilihat sebelumnya daripada data yang baru. Meskipun begitu, nilai RMSE secara keseluruhan masih relatif rendah, yang menandakan bahwa model ini mampu memberikan prediksi yang cukup baik dalam menyarankan destinasi wisata kepada pengguna.

## 7. References
[1] Badan Pusat Statistik (BPS), "Survei Pertumbuhan Sektor Pariwisata di Surabaya," Tahun 2019.

[2] Universitas Airlangga, "Strategi Promosi Wisata Heritage melalui Media Sosial, Komunitas dan Event
(Studi Kasus pada Dinas dan Kebudayaan Pariwisata Kota Surabaya)" 2016. Available: https://ejournal.unesa.ac.id/index.php/Commercium/article/download/41635/35891/

[3] Kementerian Pariwisata dan Ekonomi Kreatif (Kemenparekraf), "Panduan Potensi Pembangunan Sektor Pariwisata dan Ekonomi Kreatif," Tahun 2021. Available: https://kemenparekraf.go.id/ragam-pariwisata/Panduan-Potensi-Pembangunan-Sektor-Pariwisata-dan-Ekonomi-Kreatif

[4],[5] A. Smith, "Evaluation Metric for Content-Based Filtering: Precision in Recommender Systems," Journal of Artificial Intelligence Research, vol. 25, no. 2, pp. 150-165, 2019

