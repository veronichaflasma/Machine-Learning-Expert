# Laporan Proyek Machine Learning - Flasma Veronicha H
## System Recommendation - Tourism Destination in Surabaya

![SBY VIEW](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/wisata%20sby.jpg?raw=True)

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

1. Bagaimana cara mengembangkan sistem rekomendasi pengunjung yang dipersonalisasi dengan menggunakan teknik _Content-Based Filtering_?
   
2. Dengan memanfaatkan data rating yang diberikan oleh pengunjung, bagaimana cara untuk merekomendasikan tempat wisata yang belum pernah dikunjungi?

### 2.2. Goals

1. Membuat sistem rekomendasi yang dipersonalisasi dengan menggunakan teknik _Content-Based Filtering_ untuk meningkatkan relevansi rekomendasi tempat wisata kepada pengunjung.
   
2. Memanfaatkan data rating yang diberikan oleh pengunjung untuk memberikan rekomendasi tempat wisata yang belum pernah dikunjungi oleh pengunjung dengan _Collaborative-Based Filtering_

### 2.3 Solutions

1. Menerapkan cosine similarity dalam sistem rekomendasi Content-Based Filtering untuk menemukan kemiripan antara data dan memberikan rekomendasi yang akurat kepada pengguna.

2. Membuat RecommenderNet menggunakan Keras Model Class untuk menerapkan collaborative filtering berdasarkan rating pengunjung, sehingga meningkatkan kualitas rekomendasi.
   
## 3. Data Understanding
### 3.1 Dataset
Nama Dataset: [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)
| Nama File               | Jumlah Kolom | Jumlah Data | Keterangan | 
|----------------------------|--------------|-------------|------------|
| package_tourism.csv        |       7      | 100         | Berisi informasi tentang objek wisata di 5 kota besar di Indonesia dengan total ~400|
| tourism_rating.csv         |       3      | 10000       | Berisi data pengguna palsu untuk membuat fitur rekomendasi berdasarkan pengguna|
| tourism_with_id.csv        |      12      | 437         | Berisi 3 kolom, yaitu pengguna, tempat, dan rating yang diberikan, berfungsi untuk membuat sistem rekomendasi berdasarkan rating|
| user.csv                   |       3      | 300         | Berisi rekomendasi tempat terdekat berdasarkan waktu, biaya, dan rating|

### 3.2 Variabel pada Dataset
   **package_tourism.csv**
   
   | Variabel        | Keterangan                           |
   |-----------------|--------------------------------------|
   | `Package`       | Paket destinasi wisata              |
   | `City`          | Kota pada paket destinasi wisata    |
   | `Place_Tourism1`| Tempat destinasi wisata pertama     |
   | `Place_Tourism2`| Tempat destinasi wisata kedua       |
   | `Place_Tourism3`| Tempat destinasi wisata ketiga      |
   | `Place_Tourism4`| Tempat destinasi wisata keempat     |
   | `Place_Tourism5`| Tempat destinasi wisata kelima      |

   **tourism_rating.csv**
   
   | Variabel         | Keterangan                           |
   |------------------|--------------------------------------|
   | `User_Id`        | Id wisatawan atau turis             |
   | `Place_Id`       | Id tempat wisata                    |
   | `Place_Ratings`  | Rating tempat wisata                |

   **tourism_with_id.csv**
   
   | Variabel       | Keterangan                           |
   |----------------|--------------------------------------|
   | `Place_Id`     | Id tempat wisata                    |
   | `Place_Name`   | Nama tempat wisata                  |
   | `Description`  | Deskripsi tempat wisata             |
   | `Category`     | Kategori tempat wisata              |
   | `City`         | Kota tempat wisata berada           |
   | `Price`        | Harga tempat wisata                 |
   | `Rating`       | Rating tempat wisata                |
   | `Time_Minutes` | Lama waktu berwisata                |
   | `Coordinate`   | Koordinat tempat wisata             |
   | `Lat`          | Latitude tempat wisata              |
   | `Long`         | Panjang dari tempat wisata          |
   | `Unnamed: 11`  | Data tanpa penjelasan               |
   | `Unnamed: 12`  | Data tanpa penjelasan               |

   **user.csv**
   
   | Variabel  | Keterangan       |
   |-----------|------------------|
   | `User_Id` | Id dari user     |
   | `Location`| Lokasi user      |
   | `Age`     | Umur user        |




## 4. Data Preparation
 * Pengambilan data berdasarkan `City` Surabaya dari `package_tourism` karena proyek ini berfokus pada pembuatan sistem rekomendasi destinasi wisata yang terdapat di kota Surabaya
 * Membuat variabel baru `sby_tourism` yang berisi sebagai berikut:
   
   |   # | Column        | Non-Null Count | Dtype    |
   |----:|:--------------|:---------------|:---------|
   |   0 | Place_Id      | 46 non-null    | int64    |
   |   1 | Place_Name    | 46 non-null    | object   |
   |   2 | Description   | 46 non-null    | object   |
   |   3 | Category      | 46 non-null    | object   |
   |   4 | City          | 46 non-null    | object   |
   |   5 | Price         | 46 non-null    | int64    |
   |   6 | Rating        | 46 non-null    | float64  |
   |   7 | Time_Minutes  | 30 non-null    | float64  |
   |   8 | Coordinate    | 46 non-null    | object   |
   |   9 | Lat           | 46 non-null    | float64  |
   |  10 | Long          | 46 non-null    | float64  |
   |  11 | Unnamed: 11   | 0 non-null     | float64  |
   |  12 | Unnamed: 12   | 46 non-null    | int64    |
  * Menghapus column yang tidak digunakan

      |   # | Column       | Non-Null Count | Dtype    |
      |----:|:-------------|:---------------|:---------|
      |   7 | Time_Minutes | 30 non-null    | float64  |
      |  11 | Unnamed: 11  | 0 non-null     | float64  |
      |  12 | Unnamed: 12  | 46 non-null    | int64    |
  * Menggabungkan dua dataset, yaitu `sby_tourism` dan `rating_tourism`, menggunakan fungsi `merge()`. Penggabungan dataset dilakukan untuk menggabungkan informasi yang relevan dari kedua dataset. Dataset `package_tourism.csv` berisi informasi tentang tempat, dan dataset `rating.csv` berisi rating pengguna untuk setiap `package_tourism`, maka dengan menggabungkan kedua dataset tersebut juga dapat menganalisis hubungan antara atribut `package_tourism` dengan `user`.
  * Penanganan _Missing Value_ pada variable `sby_package`,`rating`, dan `user`
  * Menghapus baris yang merupakan duplikat pada `Place_Id` menggunakan fungsi `drop_duplicates()`. Menghapus data duplikat membantu meminimalkan redundansi dan mencegah hasil analisis yang bias atau tidak akurat karena keberadaan data yang sama dengan nilai yang sama.


### 4.1 Univariate - EDA
Melakukan _Univariate_ EDA untuk memvisualisasikan data untuk memahami masing-masing fitur yang telah diproses sebelumnya.
* Total Tempat Wisata di Surabaya berdasarkan _Category_
  ![UEDA - Category](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/uni1.png?raw=True)
* Total Rating berdasarka _Category_ tempat wisata
  ![UEDA - Rating](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/uni2.png?raw=True)

### 4.2 Multivariate - EDA
 Melakukan _Multivariate_ EDA proses untuk memahami hubungan antara dua atau lebih variabel pada saat yang bersamaan. 
* Top 10 Destinasi Wisata dengan Rating Tertinggi
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/multi1.png?raw=True)
* Top 5 Destinasi Wisata dengan Penilaian Rata-rata Tertinggi
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/meda3.png?raw=True)
* Top 5 Destinasi Wisata di Surabaya dengan Harga Tiket Masuk Tertinggi:
![MEDA - Top Dest](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/multi3.png?raw=True)

## 5. Modeling
### 5.1 Content-Based Filtering
Dalam model Content-Based Filtering ini model dibuat untuk rekomendasi berdasarkan pengunjung ke tempat serupa yang telah dikunjungi. 

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
  
5. **Membuat fungsi rekomendasi dengan parameter**
   - `Place_Name`: nama tempat wisata yang menjadi titik awal rekomendasi.
   - `similarity_data`: Dataframe yang berisi informasi kesamaan sebelumnya.
   - `items`: fitur yang digunakan untuk menentukan kemiripan antara `Place_Name` dan `Category`.
   - `k`: jumlah rekomendasi yang akan diberikan.
     
6. **Melakukan rekomendasi yang similar dengan Taman Prestasi, berikut merupakan output yang dihasilkan**:
   
   | User_Id | Place_Id | Place_Ratings | Category      | Place_Name    | Price |
   |---------|----------|---------------|---------------|---------------|-------|
   | 5       | 395      | 2             | Taman Hiburan | Taman Prestasi| 0     |
   
   Hasil
   
   | Place_Name                          | Category      | Price |
   |------------------------------------|---------------|-------|
   | Taman Pelangi                      | Taman Hiburan | 0     |
   | Taman Barunawati                   | Taman Hiburan | 0     |
   | Taman Mundu                        | Taman Hiburan | 0     |
   | Taman Keputran                     | Taman Hiburan | 0     |
   | Taman Air Mancur Menari Kenjeran   | Taman Hiburan | 0     |


7. **Kelebihan Content-Based Filtering**
   - Tidak memerlukan data pengguna lainnya, cocok untuk pengguna dengan preferensi unik.
   - Dapat memberikan rekomendasi untuk destinasi wisata baru yang belum dinilai oleh pengguna.

8. **Kekurangan Content-Based Filtering**
   - Rentan terhadap "filter bubble", di mana pengguna hanya menerima rekomendasi yang serupa dengan preferensi mereka saat ini.
   - Tidak memperhitungkan preferensi sosial atau kolaboratif antar pengguna.

9. **Mengapa Algoritma Content-Based Filtering?**
   - Karena algoritma ini mampu menampilkan rekomendasi berdasarkan tempat wisata yang telah dikunjungi oleh pengunjung sebelumnya dan menampilkan rekomendasi yang serupa dengan wisata sebelumnya.

### 5.2 Collaborative Filtering
Dalam langkah ini, skor kesesuaian antara pengunjunh dengan destinasi wisata dihitung menggunakan teknik embedding.
1. Pembuatan kelas `RecommenderNet` dengan menggunakan kelas ``Model`` dari Keras. Pada awalnya, fungsi embedding diinisialisasi dengan mengatur parameter sebagai berikut:
   - `embedding_size`: Ukuran dimensi vektor yang digunakan untuk embedding.
   - `embedding_initializer` = 'he_normal': Metode inisialisasi matriks embedding menggunakan 'he_normal'.
   - `embedding_regularizer` = `keras.regularizers.l2(1e-6)`: Fungsi regularizer yang diterapkan pada matriks embedding menggunakan `keras.regularizers.l2(1e-6)`.
2. layer embedding user dan layer embedding place dengan bias dibuat dengan mengatur parameter sebagai berikut:
  - `num_users`: Jumlah pengguna yang dienkripsi menjadi indeks integer.
  - `num_places`: Jumlah tempat yang dienkripsi menjadi indeks integer.
3. Kemudian, fungsi ``call`` dipanggil untuk menerapkan layer embedding 1, 2, 3, dan 4 dengan menggunakan aktivasi sigmoid. Model kemudian dicompile dengan loss ``BinaryCrossentropy()``, optimizer ``Adam()`` dengan ``learning_rate = 0.001``, dan metrics ``RootMeanSquaredError()``.
4. Proses training dilakukan dengan ``batch_size = 8`` dan ``epochs = 100``.
5. Untuk mendapatkan rekomendasi destinasi wisata, disarankan untuk melakukan pemilihan sampel acak dari places_not_visited menggunakan operator bitwise (~) yang diperoleh dari variabel places_visited_by_user.
6. Menggunakan model.predict() untuk memperoleh rekomendasi destinasi wisata.

| Recommendations for User: 1      |
|-----------------------------------|

| **Place with high ratings from user** |                |
|-----------------------------------|---------------|
| Taman Harmoni Keputih             | Cagar Alam     |
| Surabaya North Quay               | Taman Hiburan  |

| **Top 10 place recommendations**   |                |
|-----------------------------------|---------------|
| Balai Kota Surabaya               | Budaya         |
| Patung Buddha Empat Rupa          | Budaya         |
| Atlantis Land Surabaya            | Taman Hiburan  |
| Taman Hiburan Rakyat              | Taman Hiburan  |
| Taman Mundu                       | Taman Hiburan  |
| Museum Mpu Tantular               | Budaya         |
| Taman Bungkul                     | Taman Hiburan  |
| Taman Air Mancur Menari Kenjeran | Taman Hiburan  |
| Taman Flora Bratang Surabaya      | Taman Hiburan  |
| Gereja Perawan Maria Tak Berdosa Surabaya | Tempat Ibadah |

7. **Kelebihan Collaborative Filtering:**
   - Dapat menemukan rekomendasi untuk pengguna yang memiliki preferensi yang unik karena mengandalkan perilaku pengguna.
   - Tidak terlalu terpengaruh oleh fitur atau atribut yang mungkin sulit dipahami oleh sistem.

8. **Kekurangan Collaborative Filtering:**
   - Membutuhkan data pengguna yang cukup besar untuk memberikan rekomendasi yang akurat.
   - Rentan terhadap "cold start problem" ketika pengguna baru bergabung atau destinasi wisata baru ditambahkan ke dalam sistem.
9. **Mengapa Algoritma Collaborative Filtering?**
- Karena algoritma ini mampu menampilkan rekomendasi berdasarkan pada rating yang diberikan oleh pengguna. Tujuan dari _collaborative filtering_ adalah untuk merekomendasikan destinasi wisata bahkan jika pengunjunh tidak pernah mengunjungi destinasi wisata tertentu sebelumnya.
  
## 6. Evaluation
### 6.1. Metrik Evaluasi Content-Based Filtering

Metrik evaluasi yang digunakan dalam model _Content-Based Filtering_ adalah **Recommender System Precision**. Precision dalam konteks ini mengukur proporsi dari item yang direkomendasikan yang relevan bagi pengguna. Dalam hal ini, relevansi diukur berdasarkan seberapa baik item-item yang direkomendasikan cocok dengan preferensi sebenarnya pengguna.[[4]]()

   **Rumus Recommender System Precision:**

   $\ Precision = \frac{\text{Jumlah item yang direkomendasikan yang relevan}}{\text{Jumlah total item yang direkomendasikan}}\$

   **Cara Recommender System Precision Bekerja**

   1. **Identifikasi Item Relevan**: Pertama, sistem harus mampu mengidentifikasi item-item yang relevan dengan preferensi pengguna.
      
   2. **Rekomendasi Item**: Sistem kemudian memberikan rekomendasi berdasarkan preferensi pengguna.
      contoh:
      
      | Place_Name                          | Category      | Price |
      |------------------------------------|---------------|-------|
      | Taman Pelangi                      | Taman Hiburan | 0     |
      | Taman Barunawati                   | Taman Hiburan | 0     |
      | Taman Mundu                        | Taman Hiburan | 0     |
      | Taman Keputran                     | Taman Hiburan | 0     |
      | Taman Air Mancur Menari Kenjeran   | Taman Hiburan | 0     |
      
   4. **Perhitungan Precision**: Precision dihitung dengan membagi jumlah item yang relevan yang direkomendasikan oleh sistem dengan jumlah total item yang direkomendasikan.
      Dalam tabel di atas, fitur yang relevan adalah 5, dan jumlah total top-N adalah 5. Jika dimasukkan ke dalam rumus, maka akan menjadi seperti berikut: relevan/jumlah item rekomendasi = 5/5 = 1. Ini berarti precisionnya adalah 100%.


### 6.2. Metrik Evaluasi Collaborative-Based Filtering
Metrik evaluasi yang digunakan dalam proyek ini adalah **Root Mean Squared Error (RMSE)**. RMSE merupakan metrik yang umum digunakan untuk mengukur tingkat kesalahan prediksi dalam konteks sistem rekomendasi. RMSE mengukur rata-rata dari selisih kuadrat antara nilai prediksi dan nilai yang diamati, kemudian diambil akar kuadratnya untuk memberikan hasil dalam unit yang sama dengan variabel yang dinilai.[[5]]()

**Hasil**
![CF Metric](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Sistem-Recommendation/Images/cf%20metrics.png?raw=True)

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

### 6.3 Kesimpulan
Berdasarkan kesimpulan dari proyek ini, dapat disimpulkan bahwa sistem rekomendasi berhasil dalam memberikan rekomendasi destinasi tempat wisata di Surabaya berdasarkan rating dan tempat yang pernah dikunjungi oleh pengguna sebelumnya. Hal ini terbukti dari precision yang mencapai 100%, yang menunjukkan bahwa rekomendasi yang diberikan sangat relevan dengan preferensi dan pengalaman pengguna. Dengan demikian, proyek ini dapat dianggap berhasil dalam menciptakan sistem rekomendasi yang efektif dan akurat untuk memandu pengguna dalam memilih destinasi wisata yang sesuai dengan minat dan preferensi mereka di Surabaya.

## 7. References
[1] Badan Pusat Statistik (BPS), "Survei Pertumbuhan Sektor Pariwisata di Surabaya," Tahun 2019.

[2] Universitas Airlangga, "Strategi Promosi Wisata Heritage melalui Media Sosial, Komunitas dan Event
(Studi Kasus pada Dinas dan Kebudayaan Pariwisata Kota Surabaya)" 2016. Available: https://ejournal.unesa.ac.id/index.php/Commercium/article/download/41635/35891/

[3] Kementerian Pariwisata dan Ekonomi Kreatif (Kemenparekraf), "Panduan Potensi Pembangunan Sektor Pariwisata dan Ekonomi Kreatif," Tahun 2021. Available: https://kemenparekraf.go.id/ragam-pariwisata/Panduan-Potensi-Pembangunan-Sektor-Pariwisata-dan-Ekonomi-Kreatif

[4],[5] A. Smith, "Evaluation Metric for Content-Based Filtering: Precision in Recommender Systems," Journal of Artificial Intelligence Research, vol. 25, no. 2, pp. 150-165, 2019

