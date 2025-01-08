# Laporan Proyek Machine Learning - Dicky Ary Setiawan

## Domain Proyek

Buku adalah salah satu medium utama untuk menyampaikan pengetahuan, cerita, dan pengalaman dari satu generasi ke generasi berikutnya. Dalam era digital, munculnya platform seperti Goodreads telah memungkinkan pembaca di seluruh dunia untuk berbagi ulasan, memberikan penilaian, dan merekomendasikan buku kepada komunitas pembaca lainnya. Goodreads, sebagai salah satu platform terbesar untuk komunitas pembaca, menghubungkan jutaan pengguna dengan koleksi buku yang luar biasa dari berbagai genre, kategori, dan bahasa. Oleh karena itu saya ingin membuat sebuah labeling untuk mengelompokkan buku-buku yang berada di platform Goodreads sehingga kita dapat menganalisa lebih lanjut tentang bagaimana para pembaca diseluruh dunia memberi rating.

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Apakah buku dengan jumlah halaman yang lebih banyak cenderung mendapatkan rating lebih tinggi atau lebih rendah?
- bagaimana distribusi rating untuk semua buku? Apakah ada pola tertentu?
- Apakah buku yang ditulis oleh penulis yang sama cenderung memiliki rating yang mirip?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui apakah pembaca cenderung menyukai buku yang lebih panjang atau lebih pendek berdasarkan rating yang diberikan. Ini bisa memberikan wawasan tentang pola konsumsi literatur
- Mengetahui tren umum selera pembaca terhadap koleksi buku dalam dataset.
- Untuk melihat apakah nama penulis mempunyai pengaruh yang besar pada setiap buku yang ditulisnya.


## Data Understanding

Data yang akan saya gunakan adalah dataset buku yang terdapat pada website goodreadsbooks yang berisikan daftar buku sebanyak 10.319  judul buku. 
Berikut adalah link dari kaggle
(https://www.kaggle.com/datasets/jealousleopard/goodreadsbooks)

### Variabel-variabel pada Goodreads-books dataset adalah sebagai berikut:
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
3. Melakuakn visualisasi pada rating semua buku.
   pada tahap ini dilakukan visualisasi pada average_rating dengan menggunakan plot barchart untuk melihat sebaran buku dengan sumbu X adalah rating dan sumbu Y adalah jumlah buku.
4. Melakukan visualisasi rating VS count.
   selanjutnya adalah melakukan visualisasi menggunakan scatter plot untuk melihat bagaimana penyebaran average_rating dengan Rating_count.
5. Visualisasi Heatmap
   pada tahap ini visualisasi akan dilakukan pada data yang berjenis angka saja karena data-data yang lain tidak cocok jika dilakukan encorder.
   
## Data Preparation
Dalam tahap ini berikut adalah tahapan yang saya lakukan:
1. Melihat apakah ada rating_count dengan jumlah 0
   ini digunakan untuk melihat apakah pada colomn rating_count terdapat nilai 0.
2. Menghilangkan nilai 0.
   pada tahapan sebelumnya terdapat beberapa keganjilan pada data yaitu terdapat nilai 0 pada setiap colomn
   oleh karena itu dilakukan drop pada colomn yang memiliki nilai 0.
3. Melakukan pengecekan apakah terdapat nilai na
   pada langkah ini dilakukan untuk menghilangkan nilai na pada column yang ada ternyata terdapat 29.
4. Melakukan Dropna
   menghilangkan baris yang mempunyai nilai na.
5. Menghapus colomn bookID,title,authors,language_code,publication_date.
   colom bookID,title,authors,language_code,publication_date kurang memiliki hubungan dengan colomn yang lain, sehingga dilakukan drop colomn pada ketiga column tersebut.


## Modeling

1. Membuat objek scaler dari MinMaxScaler. Scaler ini digunakan untuk mereskalakan data numerik ke rentang [0,1].
2. numeric_columns digunakan untuk memilih kolom dari dataframe yang memiliki tipe data numerik.
3. selanjutnya melakukan fit_transform untuk menghitung nilai minimum dan maksimum dari setiap kolom numerik.
4. memisahkan fitur dari dataset dengan menghapus kolom label dengan variable X dan valiabel z berisi kolom label saja
5. selanjunya membuat lab_enc dengan membuat objek encoder dari LabelEncoder. Encoder ini digunakan untuk mengubah data kategorikal menjadi nilai numerik.
6. membagi dataset menjadi data training dan testing dengan test_size=0,2 dan random_state=42.

membuat modeling KNN :
1. Membuat model K-Nearest Neighbors (KNN) untuk klasifikasi dengan menggunakan KNeighborsClassifier() dengan menggunakan fitur pelatihan dari X_train dan label y_train.
2. membuat variable y_ped_knn dengan menggunakan model KNN yang sudah dilatih sebelumnya.
3. membuat confusion matrix yang berguna untuk membandingkan label y_test dengan label prediksi y_pred_knn untuk menghasilkan matriks kebingungan.
4. mengakses elemen confusion matrix dengan 4 variable yang berbeda.
5. selanjunya menghitung dan menampilkan metrik evaluasi diantara lain accuracy score, precision score, recall score dan F1-score.
6. menampilakn heatmap dengan menggunakan heatmap dari confusion matrix dengan anotasi angka di dalamnya. dengan cmap='Blues': Menggunakan skema warna biru. selanjutnya fmt='d': Menampilkan nilai integer. cbar=False: Menyembunyikan color bar. plt.title(), plt.xlabel(), plt.ylabel(): Memberi judul dan label pada heatmap.

membuat modeling SVM :
1. Membuat model Support Vector Machine (SVM) untuk klasifikasi dengan menggunakan SVC() dengan menggunakan fitur pelatihan dari X_train dan label y_train.
2. membuat variable y_ped_knn dengan menggunakan model SVM yang sudah dilatih sebelumnya.
3. membuat confusion matrix yang berguna untuk membandingkan label y_test dengan label prediksi y_pred_knn untuk menghasilkan matriks kebingungan.
4. mengakses elemen confusion matrix dengan 4 variable yang berbeda.
5. selanjunya menghitung dan menampilkan metrik evaluasi diantara lain accuracy score, precision score, recall score dan F1-score.
6. menampilakn heatmap dengan menggunakan heatmap dari confusion matrix dengan anotasi angka di dalamnya. dengan cmap='Blues': Menggunakan skema warna biru. selanjutnya fmt='d': Menampilkan nilai integer. cbar=False: Menyembunyikan color bar. plt.title(), plt.xlabel(), plt.ylabel(): Memberi judul dan label pada heatmap.

## Evaluation

Pada modeling ini digunakan metrik evaluasi berupa silhoutte score dimana matrik evaluasi ini berguna untuk menentukan jumlah label yang optimal dimana nilai yang didapatkan berkisar antara -1 dan 1 dengan nilai positif yang menunjukkan tingkat kesesuaian object dengan labelnya dan nilai negatif yang kurang cocok antara object dan labelnya.
Sehingga pada dataset ini digunakanlah dua methode untuk mendapatkan nilai paling tinggi dimana DBSCAN hanya mendapatkan nilai 0,895 dengan total label hanya 2 sedangkan pada methode KMean didapatkan nilai hampir mendekati 1 yaitu 0,956 dengan total label 4.
dari kedua methode yang digunakan diterapkanlah methode KMean karena nilai silhoutte score yang tinggi dan jumlah label yang cukup.

Apakah sudah menjawab problem statment?
- pada pertanyaan pertama 'Apakah buku dengan jumlah halaman yang lebih banyak cenderung mendapatkan rating lebih tinggi atau lebih rendah?':
   ternyata ketebalan halaman suatu buku tidak mempunyai pengaruh besar terhadap rating buku itu sendiri
- pada pertanyaan kedua 'Bagaimana distribusi rating untuk semua buku? Apakah ada pola tertentu?'
   dari data diatas dapat dilihat bahwa distribusi rating yang didapatkan sangat merata antara label, tetapi terdapat pola dimana label 0 memiliki rating count yang terendah yaitu dibawah 250ribu reviewer, label 1 12-25 juta reviewer , label 250ribu - 12 juta reviewer ,dan label 3 lebih dari 25 juta reviewer
- pada pertanyaan ketiga 'Apakah buku yang ditulis oleh penulis yang sama cenderung memiliki rating yang mirip?' :
  dari data diatas diambil dua pengarang terkenal yang menulis buku sendirian yaitu J.K Rowling dengan buku terkenalnya harry potter dan Agatha Cristhie yang dijuluki sebagai ratu misteri, dari data diatas memang betul bahwa buku yang ditulis oleh penulis yang sama cenderung memiliki rating yang tidak jauh berbeda antara satu dengan lainnya.
  
Apakah berhasil mencapai goals yang diharapkan?
dari goal yang dipaparkan semua goal berhasil diraih 
pada goal pertama : ternyata jumlah halaman buku tidak terlalu berpengaruh terhadap rating yang diberikan.
pada goal kedua : pada masalah ini tren buku cenderung merata.
pada goal ketiga : benar adanya nama penulis yang besar selalu mempunyai rating yang baik itu dikarenakan mereka sudah mempunyai basis pembaca.

Apakah solusi statement yang kamu rencanakan berdampak? Jelaskan!
Solusi statement yang direncanakan adalah dengan membuat labeling sehingga pada pebisnis toko buku mengetahui buku mana yang mempunyai daya jual yang baik sehingga produk bisa terjual dengan baik.

Tambahkan insight yang didapat terhadap perbedaan tiap label:

label 0 (Terendah): Jumlah reviewer berada di bawah 250 ribu, menunjukkan tingkat interaksi yang rendah.
Insight: Produk atau layanan di label ini cenderung kurang populer atau memiliki pangsa pasar yang sangat kecil.
Peluang: Perlu dilakukan strategi pemasaran yang lebih efektif atau evaluasi terhadap produk untuk meningkatkan jumlah reviewer dan eksposur.

label 1 (Menengah Tinggi): Memiliki jumlah reviewer antara 12 juta hingga 25 juta, menunjukkan keterlibatan yang lebih tinggi dibanding label lainnya.
Insight: Produk/layanan di label ini cukup populer, dengan tingkat keterlibatan yang tinggi.
Peluang: Fokus pada menjaga kepuasan pengguna yang sudah ada, serta meningkatkan loyalitas untuk mempertahankan angka ini.

label 2 (Menengah Rendah): Reviewer berada pada rentang 250 ribu hingga 12 juta, mencerminkan keterlibatan sedang.
Insight: Produk/layanan di label ini memiliki popularitas yang sedang, mungkin memiliki potensi untuk berkembang lebih lanjut.
Peluang: Perbaikan kualitas produk atau pemasaran tambahan dapat membantu meningkatkan engagement sehingga naik ke label yang lebih tinggi.

label 3 (Tertinggi): Reviewer lebih dari 25 juta, menandakan tingkat popularitas yang sangat tinggi di kategori ini.
Insight: Produk/layanan di label ini sangat populer, menjadi "market leader" di kategori tertentu.
Peluang: Fokus pada inovasi untuk menjaga posisi terdepan, sekaligus mempelajari apa yang membuat produk ini begitu sukses untuk diterapkan pada label lainnya.

