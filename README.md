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
