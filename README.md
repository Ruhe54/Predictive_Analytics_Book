# Laporan Proyek Machine Learning - Nama Anda

## Domain Proyek

Buku adalah salah satu medium utama untuk menyampaikan pengetahuan, cerita, dan pengalaman dari satu generasi ke generasi berikutnya. Dalam era digital, munculnya platform seperti Goodreads telah memungkinkan pembaca di seluruh dunia untuk berbagi ulasan, memberikan penilaian, dan merekomendasikan buku kepada komunitas pembaca lainnya. Goodreads, sebagai salah satu platform terbesar untuk komunitas pembaca, menghubungkan jutaan pengguna dengan koleksi buku yang luar biasa dari berbagai genre, kategori, dan bahasa. Oleh karena itu saya ingin membuat sebuah clustering untuk mengelompokkan buku-buku yang berada di platform Goodreads sehingga kita dapat menganalisa lebih lanjut tentang bagaimana para pembaca diseluruh dunia memberi rating.

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Apakah buku dengan jumlah halaman yang lebih banyak cenderung mendapatkan rating lebih tinggi atau lebih rendah?
- Apa distribusi rating untuk semua buku? Apakah ada pola tertentu?
- Apakah buku yang ditulis oleh penulis yang sama cenderung memiliki rating yang mirip?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui apakah pembaca cenderung menyukai buku yang lebih panjang atau lebih pendek berdasarkan rating yang diberikan. Ini bisa memberikan wawasan tentang pola konsumsi literatur
- Mengetahui tren umum selera pembaca terhadap koleksi buku dalam dataset.
- Untuk melihat apakah nama penulis mempunyai pengaruh yang besar pada setiap buku yang ditulisnya.


## Data Understanding

Data yang akan saya gunakan adalah dataset buku yang terdapat pada website goodreadsbooks yang berisikan daftar buku sebanyak 11.000 judul buku. 
Berikut adalah link dari kaggle
(https://www.kaggle.com/datasets/jealousleopard/goodreadsbooks)

### Variabel-variabel pada Goodreads-books0 dataset adalah sebagai berikut:
- BookID               : Code unik untuk mengidentifikasi setiap buku
- Title                : Judul buku yang dipublikasikan
- Authors              : Nama-nama penulis buku
- Average_rating       : rating rata-rata yang diberikan oleh user
- Isbn                 : Code unik buku yang digunakan sebagai code buku internasional
- Isbn13               : Code unik buku yang terdiri dari 13 digit yang diterbitkan secara internasional
- language_code        : bahasa yang digunakan pada buku
- num_pages            : jumlah halaman yang terdapat pada buku biasanya belum termasuk bagian awal buku yang berisikan informasi penerbit
- ratings_count        : Jumlah User yang melakukan rating
- text_reviews_count   : Jumlah User yang memberikan ulasan terhadap buku
- Publication_date     : Tanggal dimana buku pertama kali terbit
- Publisher            : Nama lembaga yang menerbitkan buku

**Rubrik/Kriteria Tambahan (Opsional)**:
Untuk mendalami tentang data yang diolah terdapat beberapa langkah yang dilakuakan:
1. mencari informasi secara menyeluruh tentang dataset dengan menggunakan .info().
2. selanjutnya melakukan .describe untuk melihat berapa banyak data, nilai minimal, nilai maksimal serta melihat apakah ada keganjilan pada data.

## Data Preparation
Dalam tahap ini berikut adalah tahapan yang saya lakukan:
1. Menghilangkan nilai 0.
   pada tahapan sebelumnya terdapat beberapa keganjilan pada data yaitu terdapat nilai 0 pada setiap colomn
   oleh karena itu dilakukan drop pada colomn yang memiliki nilai 0.
2. Menghapus colomn Isbn,Isbn13, dan Publisher.
   colom Isb, Isbn13 ,serta Publisher kurang memiliki hubungan dengan colomn yang lain, sehingga dilakukan drop colomn pada ketiga column tersebut.
3. Melakuakn visualisasi pada rating semua buku.
   pada tahap ini dilakukan visualisasi pada average_rating dengan menggunakan plot barchart untuk melihat sebaran buku dengan sumbu X adalah rating dan sumbu Y adalah jumlah buku.
4. Melakukan visualisasi rating VS count.
   selanjutnya adalah melakukan visualisasi menggunakan scatter plot untuk melihat bagaimana penyebaran average_rating dengan Rating_count.
5. Visualisasi Heatmap
   pada tahap ini visualisasi akan dilakukan pada data yang berjenis angka saja karena data-data yang lain tidak cocok jika dilakukan encorder.

## Modeling

Dalam melakukan modeling untuk dataset ini akan menggunakan clustering dengan methode DBSCAN dan KMeans
1. DBSCAN
   - Sebelum melakukan modeling dilakukan Standardscaler dan fit_transform pada dataframe yang telah di olah.
   - selanjutnya membuat model DBSCAN dengan menggunakan nilai ephoch 0.1 dan minimal samples adalah 10 yang ternyata mendapatkan nilai silhoutte coefficient -0.251.
   - setelah mendapatkan nilai yang kurang memuaskan dilanjutkan menggunakan gridsearch untuk mendapatkan nilai yang lebih baik dimana rentang nilai epoch adalah 1-2 dengan setiap step bertambah 0,1 dan min_sample 10-21.
   - dan nilai terbaik yang didapatkan adalah epoch 1,9 dengan min_sample 10 dan nilai silhouette score adalah 0,895 tetapi cluster yang didapatkan hanya 2.

2.KMean
  - Dilakukan KelbowVisualizer untuk menemukan nilai cluster yang cocok dengan rentang 1-10
  - selanjutnya membuat modeling dengan KMean N_cluster 4 dan didapatkan nilai silhouette score 0,956 dengan cluster 4.

## Evaluation

Pada modeling ini digunakan metrik evaluasi berupa silhoutte score dimana matrik evaluasi ini berguna untuk menentukan jumlah cluster yang optimal dimana nilai yang didapatkan berkisar antara -1 dan 1 dengan nilai positif yang menunjukkan tingkat kesesuaian object dengan clusternya dan nilai negatif yang kurang cocok antara object dan clusternya.
Sehingga pada dataset ini digunakanlah dua methode untuk mendapatkan nilai paling tinggi dimana DBSCAN hanya mendapatkan nilai 0,895 dengan total cluster hanya 2 sedangkan pada methode KMean didapatkan nilai hampir mendekati 1 yaitu 0,956 dengan total cluster 4.
dari kedua methode yang digunakan diterapkanlah methode KMean karena nilai silhoutte score yang tinggi dan jumlah cluster yang cukup.


