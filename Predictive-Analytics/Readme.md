# Laporan Proyek Machine Learning Terapan - Flasma Veronicha H
## _Credit Scoring Classification_

## 1. Domain Proyek & _Background_
Dalam industri keuangan, _Credit Scoring_ memainkan peran krusial dalam menilai risiko kredit peminjam. Metode ini memanfaatkan data keuangan dan profil kredit untuk memprediksi sejauh mana seseorang atau entitas bisnis akan membayar kembali pinjaman atau membayar kewajiban keuangan tepat waktu. Keputusan pemberian kredit merupakan pertimbangan yang kompleks, dan Bank harus memilih dengan hati-hati kepada siapa mereka akan memberikan kredit [1].

**Mengapa Analisis _Credit Scoring_ Penting?**
1. **Keputusan Pemberian Kredit:** Bank harus memutuskan apakah akan memberikan kredit kepada pelanggan atau tidak. _Credit Scoring_ membantu mengidentifikasi peminjam yang kredibel dan dapat membayar kembali pinjaman dengan tepat waktu.
2. **Risiko Kredit:** Meminimalkan risiko kredit adalah tujuan utama Bank. Dengan menggunakan model _Credit Scoring_ yang baik, Bank dapat mengurangi risiko kredit yang mungkin timbul dari peminjam yang gagal membayar.
3. **Efisiensi Proses:** Dalam skala besar, manual menilai kredit setiap pelanggan akan sangat tidak efisien. _Credit Scoring_ memungkinkan proses otomatisasi dan pengambilan keputusan yang lebih cepat.

## 2. _Business Understanding_
### 2.1 _Problem Statements_
1. Bagaimana cara mengklasifikasikan calon debitur dalam pengajuan kredit berdasarkan data yang disediakan oleh Bank dalam _Credit Scoring_?
2. Model Machine Learning apa yang memiliki tingkat akurasi yang tinggi untuk melakukan klasifikasi _Credit Scoring_ pada calon debitur di Bank?
3. Apa metode evaluasi yang tepat untuk menilai kinerja model Machine Learning yang dibangun untuk klasifikasi _Credit Scoring_?

### 2.2 _Goals_
1. Melakukan klasifikasi _Credit Scoring_ terhadap calon debitur menggunakan model Machine Learning.
2. Mengevaluasi model Machine Learning untuk mencari tingkat akurasi terbaik dalam klasifikasi _Credit Scoring_.
3. Melakukan evaluasi dengan menghitung nilai **Accuracy, Recall, Precission, dan F1-Score.**

### 2.3 _Solutions Statement_
Solusi yang dapat diimplementasikan untuk mencapai tujuan tersebut adalah sebagai berikut:
1. Melakukan analisis, eksplorasi, dan preprocessing pada data untuk mendapatkan pemahaman yang mendalam tentang karakteristiknya. Langkah-langkah yang dapat diambil termasuk:
   - Menangani nilai yang hilang dalam dataset.
   - Mengidentifikasi korelasi antara variabel-variabel untuk memahami hubungan antara variabel dependen dan independen.
   - Melakukan normalisasi data, terutama pada fitur-fitur numerik, untuk memastikan data memiliki skala yang seragam.
2. Menggunakan model klasifikasi untuk _Credit Scoring_ calon debitur. Beberapa model atau algoritma yang dapat dievaluasi dalam konteks ini adalah **K-Nearest Neighbors (KNN), Random Forest, dan Naive Bayes.**
3. Melakukan evaluasi model menggunakan metrik-metrik kinerja yang relevan seperti akurasi, presisi, dan F1-Score. Hal ini memungkinkan untuk mengevaluasi kinerja model secara komprehensif dan memastikan bahwa model yang dibangun dapat memberikan hasil yang dapat diandalkan dalam klasifikasi _Credit Scoring_ calon debitur.
   
Dengan menerapkan langkah-langkah di atas, diharapkan dapat berhasil dalam mencapai tujuan klasifikasi _Credit Scoring_ pada Bank dengan menggunakan model Machine Learning yang tepat.

## 3. _Data Understanding_
Datasets yang digunakan pada proyek ini didapatkan dari [Kaggle](https://www.kaggle.com/code/sudhanshu2198/multi-class-credit-score-classification).
### 3.1 Credit Scoring Datasets

Dalam konteks analisis kredit, klasifikasi _Credit Scoring_ menjadi 3 kategori - Good, Poor, and Standard - berfungsi sebagai dasar untuk mengevaluasi kelayakan kredit calon debitur. Proses klasifikasi ini melibatkan penilaian berbagai indikator keuangan dan pola perilaku yang terkait dengan peminjam untuk menentukan tingkat risiko kredit mereka.

![Credit Score](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Predictive-Analytics/Images/Credit%20Score%20Class.png)

### 3.2 **Variabel klasifikasi _Credit Scoring_**
* `Delay_from_due_date`: jumlah hari terlambat dari tanggal pembayaran
* `Num_of_Delayed_Payment`: jumlah pembayaran yang terlambat
* `Num_Credit_Inquiries`: jumlah pertanyaan kartu kredit
* `Credit_Utilization_Ratio`: rasio pemanfaatan kartu kredit
* `Credit_History_Age`:  usia histori kredit
* `Amount_invested_monthly`: jumlah bulanan yang diinvestasikan oleh pelanggan (dalam USD)
* `Monthly_Balance`: jumlah saldo bulanan pelanggan (dalam USD)
* `Age`: usia seseorang
* `Annual_Income`: pendapatan tahunan seseorang
* `Num_Bank_Accounts`: jumlah rekening bank yang dimiliki
* `Num_Credit_Card`: jumlah kartu kredit lain yang dimiliki
* `Interest_Rate`: tingkat bunga pada kartu kredit
* `Num_of_Loan`: jumlah pinjaman yang diambil dari bank
* `Monthly_Inhand_Salary`: gaji bulanan dasar
* `Outstanding_Debt`: hutang yang tersisa untuk dibayar (dalam USD)
* `Total_EMI_per_month`: pembayaran EMI bulanan (dalam USD)

### 3.3 EDA - Univariate Analysis
_Univariate Analysis_ univariat adalah proses menganalisis satu variabel pada suatu waktu. Dalam konteks analisis _Credit Score_, analisis univariat dapat dilakukan pada setiap variabel yang disediakan untuk memahami distribusi dan karakteristiknya secara individual.
![Univariate Analysis](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/main/Predictive-Analytics/Images/Univariate%20Analysis.png)

### 3.4 EDA - Analisis Relation _Credit Score_
Skor kredit memiliki tiga kelas utama: Good, Poor, dan Standard, yang mencerminkan tingkat kesehatan keuangan seseorang dan risiko kredit yang terkait. Berikut adalah poin-poin kunci untuk setiap _class_:

1. **Good**:
   - Individu dengan skor kredit "Good" memiliki riwayat pembayaran yang Good, rendahnya jumlah utang, dan pengelolaan keuangan yang bertanggung jawab.
   - Mereka sering memiliki pendapatan tahunan yang tinggi, saldo bulanan yang seimbang, dan tingkat kredit yang rendah.
   - Biasanya mendapatkan suku bunga yang lebih rendah dan akses lebih mudah ke produk keuangan dengan syarat yang lebih Good.

2. **Poor**:
   - Skor kredit "Poor" menunjukkan riwayat pembayaran yang buruk, jumlah utang yang tinggi, dan kesulitan dalam mengelola keuangan.
   - Mereka cenderung memiliki keterlambatan pembayaran, jumlah kartu kredit yang tinggi, dan tingkat kredit yang tinggi.
   - Kesulitan dalam mendapatkan pinjaman baru dan mungkin dikenakan suku bunga yang lebih tinggi.

3. **Standard**:
   - Skor kredit "Standar" berada di tengah antara "Good" dan "Poor" dalam hal risiko kredit.
   - Mereka memiliki riwayat pembayaran yang cukup Good tetapi ada area yang perlu diperbaiki.
   - Biasanya memiliki jumlah pinjaman yang moderat, saldo bulanan yang stabil, dan riwayat pembayaran yang cukup baik.
   - Diberikan produk keuangan dengan syarat yang standar dan suku bunga yang moderat.
     
![Korelasi Credit Score](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/6b20101c038390b4dad9dd3ee9e8f53f158955e0/Predictive-Analytics/Images/Relation%20Credit%20Score.png)

### 3.5 EDA - Analisis Korelasi Numerik
![Korelasi Matrix](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/acbf2f969f47f7e3e61b3548fa1ac1a3252177b2/Predictive-Analytics/Images/Correlation%20Matrix.png)

## 4. Data Preparation
Data preparation adalah proses persiapan data sebelum data tersebut dapat digunakan untuk analisis atau pemodelan, dalam proyek ini ada beberapa tahapan yaitu:
### 4.1 **_Data Cleaning_**:
   - Pemeriksaan _missing values_ dilakukan untuk memastikan tidak ada nilai yang hilang atau jika ada, harus ditangani dengan strategi tertentu seperti pengisian nilai rata-rata atau median, atau dengan menghapus baris atau kolom yang mengandung nilai yang hilang.
   - Pemeriksaan duplikat data dilakukan untuk memastikan setiap baris data unik.
### 4.2 **Transformasi Data**:
   - Transformasi data melibatkan konversi atau pengubahan data ke dalam format yang lebih sesuai atau lebih mudah diproses oleh model.
   - Salah satu transformasi umum adalah encoding variabel kategorikal menjadi format numerik agar bisa diproses oleh model. Dalam proyek ini menggunakan metode label encoding.
### 4.3 **Pembagian Data**:
   - Training set digunakan untuk melatih model, sedangkan Test set digunakan untuk menguji performa model dengan pembagian 20%.
   - Pembagian ini bertujuan untuk menghindari overfitting dan memastikan bahwa model dapat menggeneralisasi dengan baik pada data yang belum pernah dilihat sebelumnya.
   - Pembagian dalam proyek ini dilakukan secara acak.
## 5. Modelling
Dalam proyek pembuatan model machine learning untuk credit scoring classification, penggunaan tiga model yaitu K-Nearest Neighbors (KNN), Random Forest, dan Naive Bayes dapat memberikan beragam kelebihan dan kekurangan. Berikut adalah penjelasan mengenai ketiga model tersebut:

### 5.1. **K-Nearest Neighbors (KNN)**:
KNN cocok digunakan dalam proyek credit scoring classification karena sifatnya yang sederhana dan kemampuannya untuk menangani pola yang cukup jelas dalam data kredit[[2]()]
   - **Kelebihan**:
     - Tidak memerlukan pembelajaran yang rumit atau pemahaman yang mendalam terhadap data.
     - KNN cocok untuk dataset dengan pola yang sederhana atau distribusi yang tidak terlalu kompleks.
   - **Kekurangan**:
     - KNN cenderung lambat dalam fase prediksi, terutama pada dataset besar.
     - Rentan terhadap data pencilan (outliers) karena pengaruh langsung dari titik-titik _Nearest Neighbors_.
     - Sensitif terhadap skala dan jarak yang digunakan dalam menghitung _Nearest Neighbors_.
### 5.2. **Random Forest**:
Random Forest merupakan pilihan yang baik karena kemampuannya dalam menangani kompleksitas dan variabilitas data kredit yang terjadi.[[3]()]
   - **Kelebihan**:
     - Mampu menangani masalah klasifikasi dan regresi dengan baik.
     - Tidak terlalu rentan terhadap overfitting karena membangun banyak pohon keputusan secara acak.
     - Mampu menangani data yang tidak seimbang (imbalanced data) dengan baik.
   - **Kekurangan**:
     - Random Forest bisa menjadi kompleks dan sulit untuk diinterpretasi karena melibatkan banyak pohon keputusan.
     - Waktu pembelajaran mungkin lebih lama daripada model yang lebih sederhana seperti KNN.
     - Memerlukan pemrosesan yang lebih besar karena membangun banyak pohon keputusan.
### 5.3. **Naive Bayes**:
Naive Bayes sering digunakan dalam klasifikasi credit scoring karena sifatnya yang cepat dan efisien, serta kemampuannya menangani data yang memiliki banyak fitur dan korelasi yang relatif rendah.[[4]()]
   - **Kelebihan**:
     - Cocok untuk dataset dengan fitur-fitur yang saling bebas (independen).
     - Tidak memerlukan banyak data pelatihan untuk memberikan hasil yang baik.
     - Cenderung tahan terhadap overfitting.
   - **Kekurangan**:
     - Naive Bayes mengasumsikan independensi antara fitur, yang mungkin tidak selalu terjadi dalam praktiknya.
     - Tidak cocok untuk dataset dengan hubungan kompleks antara fitur.
     - Performa Naive Bayes bisa terpengaruh oleh fitur yang memiliki distribusi yang sangat berbeda.
## 6. Evaluation
Dalam konteks evaluasi pada proyek klasifikasi _Credit Score_, beberapa metrik yang digunakan adalah **Accuracy, Recall, Precission, dan F1-Score[5].**

### 6.1. **Accuracy**
   - **Accuracy** mengukur sejauh mana model mampu memprediksi dengan benar, dan dihitung sebagai persentase dari total prediksi yang benar (TP dan TN) dibagi dengan total data.
   - **Accuracy** memberikan gambaran umum seberapa baik model _Credit Score_ classification dapat mengklasifikasikan data dengan benar. Semakin tinggi nilai akurasi, semakin baik kinerja model.
$$\text{Akurasi} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}} \%$$
  **Ket:**
  - TP (True Positive): Jumlah data positif yang diprediksi dengan benar sebagai positif.
  - TN (True Negative): Jumlah data negatif yang diprediksi dengan benar sebagai negatif.
  - FP (False Positive): Jumlah data negatif yang diprediksi secara tidak benar sebagai positif.
  - FN (False Negative): Jumlah data positif yang diprediksi secara tidak benar sebagai negatif.
### 6.2 Precision:
  - **Precision** mengukur seberapa banyak dari prediksi positif model yang benar, dan dihitung sebagai persentase dari TP dibagi dengan jumlah prediksi positif yang benar dan yang salah (TP dan FP).
  - **Precision** berguna ketika penting untuk meminimalkan kesalahan dalam memprediksi kelas positif. Misalnya, berapa persen dari pelanggan yang diprediksi sebagai kredit baik yang sebenarnya memang memiliki kredit baik.
  $$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}} \%$$
### 6.3. Recall:
  - **Recall** (Sensitivitas atau True Positive Rate) mengukur sejauh mana model mampu mengidentifikasi semua instance dari kelas yang benar, dan dihitung sebagai persentase dari TP dibagi dengan jumlah sebenarnya dari kelas positif (TP dan FN).
  - **Recall**  penting jika fokus pada mendeteksi sebanyak mungkin instance dari kelas positif. Sebagai contoh, berapa persen pelanggan yang memiliki kredit baik berhasil terdeteksi oleh model.
$$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}} \%$$

### 6.4. F1-score:
  - F1 Score adalah harmonic mean dari precision dan recall, memberikan perpaduan yang baik antara kedua metrik tersebut. F1 Score bermanfaat ketika ada trade-off antara precision dan recall.
  - F1 Score memberikan gambaran holistik kinerja model, terutama jika terdapat ketidakseimbangan antara kelas positif dan negatif.
$$\text{F1-score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} \%$$

### Berikut hasil _Confusion Matrix_ KNN, Random Forest, dan Naive Bayes

<img src="https://github.com/veronichaflasma/Machine-Learning-Expert/blob/541575183b11586413504f43924b43a8801c7ae8/Predictive-Analytics/Images/Confusion%20Matrix%20KNN.png" alt="Confusion Matrix KNN" width="300" height="300"><img src="https://github.com/veronichaflasma/Machine-Learning-Expert/blob/541575183b11586413504f43924b43a8801c7ae8/Predictive-Analytics/Images/Confusion%20Matrix%20RF.png" alt="Confusion Matrix Random Forest" width="300" height="300"><img src="https://github.com/veronichaflasma/Machine-Learning-Expert/blob/541575183b11586413504f43924b43a8801c7ae8/Predictive-Analytics/Images/Confusion%20Matrix%20NB.png" alt="Confusion Matrix Random Naive Bayes" width="300" height="300">

### Berikut Perbandingan hasil Accuracy, Precision, Recall and F1-Score dari Model **KNN,Random Forest, dan Naive Bayes.**
![Acc Results](https://github.com/veronichaflasma/Machine-Learning-Expert/blob/ec34382c23c661f28bdea1f0e27620a8bfe5415d/Predictive-Analytics/Images/Accuracy%20Results.png)

- Dari ketiga model yang dievaluasi, **Random Forest** memiliki akurasi tertinggi **(0.8130)**, diikuti oleh **KNN (0.7626)**, dan terakhir **Naive Bayes (0.6343)**.
- **Random Forest** juga memiliki nilai precision, recall, dan F1-score yang lebih baik untuk kebanyakan kelas dibandingkan dengan **KNN dan Naive Bayes**.
- **Naive Bayes**  memiliki nilai recall yang rendah untuk kelas 0, sehingga menunjukkan bahwa model cenderung mengabaikan sejumlah besar contoh yang sebenarnya positif.

Dengan menggunakan model **Random Forest**, para perbankan dapat dengan mudah mengklasifikasikan _Credit Score_ untuk calon debitur yang ingin melakukan kredit. Dengan demikian, model ini dapat membantu perbankan dalam pengambilan keputusan yang lebih akurat dan efisien terkait dengan pemberian pinjaman atau layanan keuangan lainnya kepada calon debitur.

## 7. References
[1] R. Anderson, The Handbook of Credit Scoring, New York, NY, USA: Wiley, 2001.

[2] A. Alizadeh, M. B. Shargh, and S. M. M. Kahani, "A Novel Approach for Fault Detection in Power Distribution Networks Using K-Nearest Neighbor Algorithm," IEEE Transactions on Power Systems, vol. 36, no. 6, pp. 4404-4415, Nov. 2021. [Online]. Available: https://doi.org/10.1109/TPWRS.2021.3064704

[3] S. Liu, Y. Wang, and X. Zhou, "An Improved Random Forest Model for Traffic Flow Prediction," IEEE Access, vol. 9, pp. 13539-13549, 2021. [Online]. Available: https://doi.org/10.1109/ACCESS.2021.3055815

[4] A. H. Alhadi, M. A. Othman, and A. N. Abdul Manaf, "A Comparative Study of Naive Bayes, K-Nearest Neighbor, and Random Forest Classifiers for Intrusion Detection System," 2020 International Conference on Computer and Information Sciences (ICCIS), pp. 1-6, Dec. 2020. [Online]. Available: https://doi.org/10.1109/ICCIS52050.2020.9321589

[5] M. Sokolova and G. Lapalme, "A systematic analysis of performance measures for classification tasks," Information Processing & Management, vol. 45, no. 4, pp. 427-437, Jul. 2009. [Online]. Available: https://doi.org/10.1016/j.ipm.2009.03.002


