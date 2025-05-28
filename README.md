# *Prediksi Harga Apartment Menggunakan Machine Learning*
# **Contents**

1. Business Problem Understanding
2. Data Understanding
3. Data Preprocessing
4. Modeling
5. Conclusion
6. Recommendation

## **1. Business Problem Understanding**

## Konteks

Apartemen menjadi salah satu solusi kebutuhan tempat tinggal modern, terutama di daerah perkotaan yang lahannya terbatas dan aktivitas bisnisnya padat. Menarik untuk diteliti bagaimana harga apartemen dipengaruhi oleh berbagai faktor internal dan eksternal. Biasanya, individu atau perusahaan bisa menawarkan unit apartemen melalui platform dengan menentukan harga jual sendiri. Namun, penentuan harga secara mandiri ini bisa menyulitkan pemilik untuk menyesuaikan dengan harga pasar. Jika harganya terlalu tinggi, unit bisa sulit terjual. Jika terlalu rendah, keuntungan maksimal pun hilang.

## Rumusan Masalah

Banyak agen properti dan pemilik apartemen yang kesulitan dalam menentukan harga jual yang tepat. Hal ini karena banyak faktor yang perlu dipertimbangkan, seperti lokasi strategis (misalnya dekat stasiun kereta bawah tanah), nilai tanah, rasio luas bangunan, dan lainnya. Akurasi dalam menentukan harga sangat penting agar tetap kompetitif di pasar, tapi tetap memberikan keuntungan optimal bagi pemilik.

## Tujuan

Tujuan dari proyek ini adalah membangun model prediksi menggunakan algoritma Machine Learning untuk memperkirakan harga jual apartemen yang sesuai, berdasarkan karakteristik apartemen seperti luas tanah, jarak ke stasiun, tahun pembangunan, dll.
Model ini diharapkan dapat membantu pemilik properti atau investor dalam membuat keputusan harga, strategi investasi, dan pengembangan properti.

## Pendekatan Analisis

Penelitian ini akan melibatkan berbagai fitur dari sebuah apartemen dan melihat bagaimana hubungannya dengan harga jual apartemen tersebut. Karena target dari penelitian ini adalah harga apartemen yang bersifat numerik kontinu, maka akan digunakan pendekatan analisis regresi. Model ini akan memanfaatkan fitur-fitur apartemen sebagai prediktor untuk memperkirakan harga jual yang sesuai.

## **2.Data Understanding**
| **Attribute** | **Data Type** |
| --- | --- 
| HallwayType | Object 
| TimeToSubway | Object
| SubwayStation | Object
| N_FacilitiesNearBy(ETC) | int
| N_FacilitiesNearBy(PublicOffice) | int
| N_SchoolNearBy(University) | int
| N_Parkinglot(Basement) | int
| YearBuilt | int
| N_FacilitiesInApt | int
| Size(sqf) | int
| SalePrice | int

## **3. Data Preprocessing**
- Tipe Data: Terdiri dari tipe numerik (int64 & float64) dan kategorikal (object).
- Nilai Kosong (Null): Tidak ada kolom yang memiliki nilai kosong.
- Nilai Unik: Menunjukkan jumlah nilai unik dalam kolom tertentu.
- Data Duplikat: Terdapat 1.422 baris yang merupakan duplikat. Ini akan kita tinjau lebih lanjut agar hasil akhir tidak bias.
- Nilai Negatif: Tidak ditemukan nilai negatif.
- Outlier: Terdapat outlier pada kolom ukuran (Size) dan harga jual (SalePrice). Meskipun hanya <1%, tetap akan kita periksa.

Secara umum, dataset ini cukup baik karena tidak banyak masalah data yang serius.

## Data Duplikat

- Fungsi `duplicated()` di pandas akan menganggap baris duplikat jika seluruh kolomnya sama persis.
- Duplikasi dapat merusak kualitas model machine learning karena mengurangi keragaman dan bisa menyebabkan *overfitting*.
- Karena itu, baris data yang terdeteksi duplikat sebaiknya dihapus.

## Data Outlier

- Penting untuk mendeteksi outlier dan menghapusnya sebelum melatih model machine learning.
- Outlier bisa menurunkan akurasi prediksi model.
- Karena jumlah outlier kurang dari 5%, maka data outlier tidak akan digunakan saat pelatihan model.

## Feature Engineering

Kita akan mengelompokkan fitur menjadi beberapa kategori agar proses engineering lebih terstruktur:

- Fitur Numerik: Size(sqf), N_FacilitiesNearBy(ETC), N_FacilitiesNearBy(PublicOffice), N_SchoolNearBy(University), N_Parkinglot(Basement), N_FacilitiesInApt
- Fitur Kategorikal: HallwayType, SubwayStation
- Fitur Ordinal: TimeToSubway

Kolom `YearBuilt` akan dibiarkan apa adanya karena sudah cukup representatif (bernilai diskrit berdasarkan tahun).
Feature Engineering adalah proses membuat atau memodifikasi fitur untuk meningkatkan kinerja model. Teknik yang digunakan:

- RobustScaler: Melakukan scaling data numerik berdasarkan median dan IQR, sangat berguna untuk menangani outlier.
- OneHotEncoder: Mengubah data kategorikal menjadi variabel dummy (0 dan 1).
- OrdinalEncoder: Digunakan untuk fitur ordinal seperti `TimeToSubway` yang memiliki urutan.
- Passthrough: Biarkan kolom seperti `YearBuilt` tetap tanpa diubah karena sudah sesuai.

## Pembagian Data (Split)

Dataset dibagi menjadi dua bagian: training set dan test set. Ini bertujuan agar model bisa dilatih dengan data tertentu dan diuji dengan data berbeda, sehingga menghindari kebocoran informasi dan bisa mengukur performa model secara adil.

## **4.Modeling**

Algoritma regresi yang digunakan untuk membandingkan performa model adalah:

- Linear Regression  
- Lasso Regression  
- Ridge Regression  
- Decision Tree 
- KNN
- Random Forest  
- XGBoost

Dari ketujuh model ini, kita akan memilih dua model dengan hasil evaluasi terbaik untuk dilakukan tuning lebih lanjut.

Berdasarkan hasil benchmarking, model `Random Forest` dan `XGBoost` merupakan dua model dengan performa evaluasi terbaik. Selanjutnya, kita akan melakukan hyperparameter tuning pada kedua model ini.

## Hyperparameter Tuning

- Dalam proses ini, digunakan `GridSearchCV` untuk melakukan pencarian kombinasi parameter terbaik. GridSearch akan mencoba **seluruh kombinasi parameter** yang telah ditentukan dan menghitung skor evaluasi dari masing-masing kombinasi.
- Tidak seperti `RandomizedSearchCV` yang hanya mengambil sampel acak dari grid, `GridSearchCV` akan melakukan **pengecekan menyeluruh (brute-force)** terhadap semua kemungkinan.
- Proses ini menggunakan **cross-validation sebanyak 3 kali** (`cv=3`) untuk memastikan hasil yang konsisten, dan `n_jobs=-1` agar memaksimalkan semua core CPU yang tersedia saat melatih model.









