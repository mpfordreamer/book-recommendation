# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Book Recommendation System
*Konsep Sistem Rekomendasi Buku (Sumber: Diadaptasi dari berbagai sumber)*

Di era sekarang yang identik dengan era literasi, kemampuan untuk mengakses dan memanfaatkan pengetahuan menjadi krusial, terutama bagi para intelektual muda sebagai agen perubahan dalam menghadapi tantangan global [[1](https://jurnal.unissula.ac.id/index.php/ELIC/article/view/1282/0)]. Perpustakaan, sebagai pusat koleksi buku dan bahan bacaan, memegang peran penting dalam mendukung literasi dan penyediaan informasi [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

Namun, seiring berkembangnya koleksi perpustakaan dan sistem informasi seperti *Online Public Access Catalog* (OPAC), pengunjung seringkali mengalami kesulitan. Sistem yang ada saat ini umumnya hanya menampilkan informasi dasar buku yang dicari dan belum mampu memberikan saran buku lain yang relevan atau mirip [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)]. Pengunjung memerlukan waktu lebih lama untuk mencari alternatif ketika buku yang diinginkan tidak tersedia atau saat ingin menjelajahi judul-judul serupa.

Untuk mengatasi tantangan ini, proyek ini mengembangkan **Sistem Rekomendasi Buku**. Sistem ini bertujuan membantu pengguna memfilter informasi dan menemukan buku yang kemungkinan besar menarik bagi mereka [[3](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [4](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)]. Pendekatan utama yang diimplementasikan adalah **Content-Based Filtering**, yang merekomendasikan buku berdasarkan kemiripan fitur atau konten buku itu sendiri, seperti `title`, `authors`, `categories`, dan `published_year` [[3](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System)]. Pendekatan ini efektif bahkan ketika data rating pengguna terbatas, karena memanfaatkan metadata buku [[5](https://www.researchgate.net/publication/317382367_Amazon_Everything_you_wanted_to_know_about_its_algorithm_and_innovation)].

Untuk meningkatkan kualitas rekomendasi dan mengatasi potensi *cold start problem* (kesulitan merekomendasikan item baru atau kepada pengguna baru) [[6](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [7](https://www.researchgate.net/publication/221563070_Amazoncom_recommendations_item-to-item_collaborative_filtering)], proyek ini juga mengintegrasikan **Collaborative Filtering**, khususnya metode **User-Based CF**. Pendekatan ini bekerja dengan menganalisis pola rating dari banyak pengguna untuk menemukan pengguna dengan selera serupa dan kemudian merekomendasikan buku yang disukai oleh *peer group* tersebut [[8](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [9](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)]. Dengan menggabungkan kedua metode ini (Hybrid System), diharapkan sistem dapat memberikan rekomendasi yang lebih akurat, beragam, dan relevan, seperti yang telah sukses diterapkan oleh platform seperti Netflix [[10](https://dl.acm.org/doi/10.1145/2843948)] dan Amazon [[11](https://ieeexplore.ieee.org/document/1167344), [2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

Penerapan sistem rekomendasi ini diharapkan dapat meningkatkan kualitas layanan perpustakaan (atau platform buku lainnya), memudahkan pengguna menemukan buku yang sesuai minat, mempersingkat waktu pencarian, dan secara keseluruhan meningkatkan pengalaman membaca serta mendukung budaya literasi [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

## Business Understanding

Pada bagian ini, akan dijelaskan latar belakang masalah yang dihadapi, tujuan yang ingin dicapai melalui proyek sistem rekomendasi buku ini, serta pendekatan solusi yang akan digunakan.

### Problem Statements

Permasalahan utama yang mendorong pengembangan sistem rekomendasi buku ini adalah:

1.  **Kesulitan Menemukan Buku yang Relevan (Information Overload):**
    *   Perpustakaan modern dan platform buku digital memiliki koleksi yang sangat besar dan terus bertambah.
    *   Pengguna seringkali merasa kewalahan dengan banyaknya pilihan dan kesulitan menemukan buku yang benar-benar sesuai dengan minat atau kebutuhan spesifik mereka di antara ribuan atau jutaan judul yang tersedia.
    *   Proses pencarian manual atau hanya berdasarkan kategori umum seringkali tidak efisien dan memakan waktu.

2.  **Kesulitan Menemukan Buku Serupa:**
    *   Setelah selesai membaca buku yang disukai, pengguna seringkali ingin membaca buku lain dengan tema, gaya penulisan, genre, atau penulis yang mirip.
    *   Sistem katalog perpustakaan atau toko buku online yang ada saat ini mungkin tidak secara efektif menyarankan buku-buku serupa ini, sehingga pengguna harus melakukan pencarian tambahan yang mungkin tidak membuahkan hasil.

3.  **Kurangnya Personalisasi dan Penemuan (Serendipity):**
    *   Pengguna cenderung mencari atau memilih buku dari penulis atau genre yang sudah mereka kenal, sehingga membatasi eksplorasi mereka pada judul-judul baru atau berbeda yang mungkin juga mereka sukai.
    *   Pengalaman mencari buku seringkali bersifat generik dan kurang disesuaikan dengan preferensi unik masing-masing individu, mengurangi kemungkinan *serendipity* (penemuan tak terduga yang menyenangkan).

4.  **Keterbatasan Sistem Informasi Perpustakaan/Platform Saat Ini:**
    *   Sistem *Online Public Access Catalog* (OPAC) atau platform serupa yang ada seringkali hanya menyediakan fungsi pencarian dasar (berdasarkan judul, penulis, ISBN) dan informasi deskriptif buku, tanpa kemampuan proaktif untuk menyarankan item lain yang relevan.
    *   Hal ini mengakibatkan pengalaman pengguna yang kurang optimal dan potensi koleksi buku yang relevan namun kurang populer menjadi tidak terlihat.

### Goals

Berdasarkan permasalahan di atas, tujuan utama dari proyek sistem rekomendasi buku ini adalah:

1.  **Meningkatkan Efisiensi Penemuan Buku:**
    *   Mengembangkan sistem yang dapat membantu pengguna menyaring koleksi buku yang besar dan dengan cepat menemukan judul-judul yang paling mungkin sesuai dengan preferensi mereka, menjawab *Problem Statement 1*.

2.  **Menyediakan Rekomendasi Buku yang Relevan dan Serupa:**
    *   Membangun model yang mampu mengidentifikasi dan menyarankan buku-buku lain yang memiliki kemiripan konten (genre, tema, penulis, dll.) atau pola minat pengguna (berdasarkan rating pengguna lain) dengan buku yang sedang dilihat atau disukai pengguna, menjawab *Problem Statement 2*.

3.  **Meningkatkan Personalisasi dan Memfasilitasi Penemuan Buku Baru:**
    *   Memberikan rekomendasi yang lebih personal dan sesuai dengan selera unik setiap pengguna, serta membantu mereka menemukan buku-buku menarik di luar zona nyaman mereka (meningkatkan *serendipity*), menjawab *Problem Statement 3*.

4.  **Menyempurnakan Layanan Sistem Informasi yang Ada:**
    *   Menambahkan fungsionalitas rekomendasi pada sistem pencarian buku yang sudah ada (seperti OPAC atau platform digital) untuk meningkatkan kualitas layanan dan pengalaman pengguna secara keseluruhan, menjawab *Problem Statement 4*.

### Solution Statements

Untuk mencapai tujuan-tujuan tersebut, pendekatan solusi berikut akan diimplementasikan dan dievaluasi:

1.  **Content-Based Filtering:**
    *   Mengembangkan model yang menganalisis fitur-fitur intrinsik dari buku (seperti `title`, `authors`, `categories`, `published_year`, dan mungkin `description`).
    *   Menggunakan teknik seperti **TF-IDF (Term Frequency-Inverse Document Frequency)** untuk merepresentasikan konten buku sebagai vektor numerik.
    *   Menghitung kemiripan antar buku menggunakan metrik seperti **Cosine Similarity** berdasarkan vektor fitur tersebut.
    *   Rekomendasi dihasilkan dengan menyarankan buku yang paling mirip secara konten dengan buku yang disukai pengguna.

2.  **Collaborative Filtering (User-Based):**
    *   Mengimplementasikan model yang memanfaatkan data historis rating atau interaksi pengguna terhadap buku (`average_rating`, `ratings_count`, atau idealnya data rating per pengguna).
    *   Mengidentifikasi pengguna-pengguna yang memiliki pola rating atau preferensi serupa dengan pengguna target.
    *   Merekomendasikan buku-buku yang disukai (memiliki rating tinggi) oleh pengguna-pengguna serupa tersebut, tetapi belum pernah dibaca atau di-rate oleh pengguna target. Metode yang mungkin digunakan adalah **K-Nearest Neighbors (KNN)** pada matriks user-item atau perhitungan **User Similarity** (misalnya Cosine Similarity antar vektor rating pengguna).

3.  **Pendekatan Hybrid (Kombinasi):**
    *   Menggabungkan hasil dari Content-Based Filtering dan Collaborative Filtering untuk menghasilkan rekomendasi akhir.
    *   Strategi kombinasi dapat berupa:
        *   **Weighted Hybrid:** Memberikan bobot pada skor dari masing-masing metode.
        *   **Switching Hybrid:** Menggunakan salah satu metode tergantung konteks (misalnya, CF untuk pengguna lama, CB untuk pengguna baru/buku baru).
        *   **Mixed Hybrid:** Menampilkan rekomendasi dari kedua sistem secara bersamaan.
    *   Tujuan hybrid adalah memanfaatkan kelebihan masing-masing pendekatan dan menutupi kekurangannya (misal, mengatasi *cold start problem* dari CF dengan CB).

## Data Understanding

### EDA - Deskripsi Variabel

| Jenis      | Keterangan                                                                                                     |
|------------|----------------------------------------------------------------------------------------------------------------|
| Title      | Books Dataset                                                                                                  |
| Source     | [Kaggle](https://www.kaggle.com/datasets/abdallahwagih/books-dataset/code/)                                      |
| Maintainer | [Abdallah Wagih](https://www.kaggle.com/abdallahwagih)                                                            |
| License    | Community Data License Agreement - Sharing - Version 1.0                                                       |
| Visibility | Publik                                                                                                         |
| Tags       | books, recommendation system, chatbot development, literature, classification, clustering                      |
| Usability  | 10.00                                                                                                           |

Berikut informasi pada dataset: Kumpulan data ini adalah kumpulan informasi komprehensif tentang buku, yang dikumpulkan dari berbagai sumber dan dirancang untuk digunakan dalam sistem rekomendasi dan pengembangan chatbot. Ini mencakup detail tentang berbagai macam buku, membuatnya cocok untuk berbagai aplikasi di bidang pembelajaran mesin, pemrosesan bahasa alami, dan kecerdasan buatan. Dataset yang digunakan pada proyek kali ini disediakan secara publik di Kaggle dengan nama dataset yaitu: _Books Dataset_. Dataset ini dapat diunduh di Kaggle: [Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset/code/).

**Berikut informasi pada dataset**:
 - Dataset berupa file `.xlsx` (Excel Spreadsheet).
 - Dataset terdiri dari 1 buah file XLSX yaitu: `book.xlsx`.
 - Dataset memiliki **6810 sampel** (baris data) dengan **12 fitur** awal.
 - Dataset memiliki 4 fitur `float64`, 1 fitur `int64`, dan 7 fitur `object`.
 - Terdapat *Missing value* pada beberapa fitur awal seperti `subtitle` (signifikan), `authors`, `categories`, `thumbnail`, `description`, `published_year`, `average_rating`, `num_pages`, dan `ratings_count`. Namun, setelah *data preparation* (pembersihan dan imputasi/konversi tipe data), fitur-fitur kunci yang digunakan untuk *content-based filtering* (`title`, `authors`, `categories`, `published_year`, `combined_features`) **tidak memiliki *missing value***.
 - Tidak ada data yang duplikat dalam dataset.

### Variabel - variabel pada dataset

Berikut adalah penjelasan singkat untuk setiap kolom dalam dataset book.xlsx:

*   **`isbn13`**: Nomor ISBN (International Standard Book Number) 13 digit, kode unik pengenal buku secara internasional. (Dihapus pada Data Preparation).
*   **`isbn10`**: Nomor ISBN 10 digit, kode unik pengenal buku (versi standar lama sebelum ISBN 13). Bertipe `object` (teks) karena bisa mengandung karakter 'X'. (Dihapus pada Data Preparation).
*   **`title`**: Judul utama dari buku. *Digunakan sebagai fitur.*
*   **`subtitle`**: Subjudul atau judul tambahan buku (kolom ini memiliki banyak nilai kosong/`null`).
*   **`authors`**: Nama penulis atau para penulis buku. Bisa berisi lebih dari satu nama. *Digunakan sebagai fitur.*
*   **`categories`**: Kategori atau genre buku (misalnya, Fiksi, Sejarah, Komputer). Bisa berisi lebih dari satu kategori. *Digunakan sebagai fitur.*
*   **`thumbnail`**: Tautan (URL) ke gambar sampul kecil (thumbnail) buku. (Dihapus pada Data Preparation).
*   **`description`**: Ringkasan, sinopsis, atau deskripsi singkat mengenai isi buku.
*   **`published_year`**: Tahun buku pertama kali diterbitkan. (Bertipe `float64` awalnya, dibersihkan dan dikonversi ke string). *Digunakan sebagai fitur.*
*   **`average_rating`**: Rata-rata skor penilaian (rating) yang diberikan oleh pengguna untuk buku tersebut (skala tidak standar, perlu normalisasi jika digunakan).
*   **`num_pages`**: Jumlah total halaman dalam buku. (Bertipe `float64` awalnya).
*   **`ratings_count`**: Jumlah total pengguna yang telah memberikan penilaian (rating) pada buku. (Bertipe `float64` awalnya).
*   **`combined_features`**: Kolom baru yang dibuat saat *data preparation*, berisi gabungan teks dari `title`, `authors`, `categories`, dan `published_year` yang telah dibersihkan. Ini adalah input utama untuk TF-IDF.

### EDA - Eksploratory Data Analysis

Analisis data eksploratif dilakukan untuk memahami karakteristik dataset buku:

*   **Distribusi Kategori Buku:** Visualisasi menunjukkan bahwa kategori **Fiksi (`fiction`)** sangat mendominasi dataset (lebih dari 2500 buku), diikuti oleh Fiksi Remaja (`juvenile fiction`) dan Biografi/Autobiografi. Distribusi kategori sangat tidak seimbang.
*   **Tren Tahun Publikasi:** Sebagian besar buku diterbitkan dalam beberapa dekade terakhir, dengan puncak distribusi berada di **awal tahun 2000-an**. Distribusi ini miring ke kiri (ekor panjang ke masa lalu), menunjukkan lebih sedikit buku tua dalam dataset.
*   **Popularitas Penulis:** **Agatha Christie** dan **Stephen King** adalah penulis yang paling banyak karyanya muncul dalam dataset ini, diikuti oleh William Shakespeare dan J.R.R. Tolkien. Ini menandakan representasi kuat dari penulis populer/produktif.
*   **Distribusi Rata-Rata Rating:** Histogram menunjukkan distribusi **bimodal**, dengan puncak utama di sekitar **rating 4.0** (menandakan mayoritas buku dinilai positif) dan puncak kecil di dekat rating 0-1 (menunjukkan sejumlah kecil buku dengan rating sangat buruk).
*   **Distribusi Jumlah Halaman:** *Box plot* menunjukkan bahwa sebagian besar buku memiliki panjang moderat (median sekitar 250-300 halaman), tetapi terdapat **banyak *outlier* buku yang sangat tebal** (lebih dari 1000 halaman), membuat distribusi miring ke kanan.
*   **Keunikan Judul:** Sekitar **93.9%** judul buku dalam dataset adalah unik, menunjukkan duplikasi judul yang minimal.

## Data Preparation

Tahap persiapan data (Data Preparation) merupakan langkah penting untuk memastikan data yang digunakan dalam membangun sistem rekomendasi buku ini berkualitas dan siap untuk diolah. Mengingat sistem ini berfokus pada kemiripan konten (Content-Based Filtering), persiapan data ditujukan untuk membersihkan dan menggabungkan fitur-fitur tekstual yang relevan (seperti judul, penulis, kategori, dan tahun terbit) menjadi satu representasi yang dapat diolah oleh model TF-IDF. Proses ini juga melibatkan penanganan nilai yang hilang pada fitur-fitur kunci dan penghapusan kolom yang tidak relevan untuk perhitungan kemiripan konten. Berdasarkan analisis kode pada notebook, berikut adalah langkah-langkah persiapan data yang dilakukan:

### 1. Pembersihan Fitur Teks (`title`, `authors`, `categories`)

*   **Proses:**
    *   Iterasi dilakukan pada fitur-fitur teks yang dipilih (`title`, `authors`, `categories`).
    *   Setiap fitur dikonversi ke tipe data string untuk konsistensi.
    *   Semua karakter yang bukan alfanumerik (huruf dan angka) atau spasi dihapus menggunakan ekspresi reguler (`[^a-zA-Z0-9\\s]`).
    *   Seluruh teks dikonversi menjadi huruf kecil (`lower()`) untuk menghilangkan sensitivitas terhadap huruf besar/kecil.
*   **Alasan:**
    *   **Standarisasi:** Mengubah semua teks ke huruf kecil dan menghapus karakter non-alfanumerik memastikan bahwa kata-kata yang sama (misalnya, "Fiction" dan "fiction") atau variasi karena tanda baca tidak dianggap berbeda oleh algoritma TF-IDF.
    *   **Noise Reduction:** Menghilangkan tanda baca dan simbol mengurangi "noise" dalam data teks yang dapat mengganggu perhitungan frekuensi kata dan kemiripan.
    *   **Persiapan Tokenisasi:** Teks yang bersih lebih mudah untuk dipecah menjadi unit-unit kata (token) pada langkah vektorisasi.

### 2. Pembersihan dan Konversi Fitur `published_year`

*   **Proses:**
    *   Kolom `published_year` dikonversi ke tipe data string.
    *   Semua karakter yang bukan digit (angka) dihapus.
    *   String kosong yang mungkin dihasilkan (jika nilai asli tidak valid atau hilang) diganti dengan '0'.
    *   Hasilnya dikonversi menjadi tipe integer (untuk memastikan validitas numerik) dan kemudian kembali dikonversi menjadi tipe string.
*   **Alasan:**
    *   **Konsistensi Format:** Memastikan kolom tahun publikasi memiliki format string numerik yang konsisten dan bebas dari karakter non-numerik atau format tanggal yang tidak standar.
    *   **Kombinasi Fitur:** Mengubahnya menjadi string memungkinkan tahun publikasi untuk digabungkan dengan fitur teks lainnya dan diperlakukan sebagai "kata" atau token yang merepresentasikan era penerbitan dalam analisis TF-IDF.
    *   **Penanganan Missing Value Implisit:** Dengan mengganti string kosong (hasil dari nilai non-numerik atau NaN asli) dengan '0', secara implisit menangani potensi nilai hilang atau tidak valid pada kolom ini sebelum konversi akhir ke string.

### 3. Kombinasi Fitur (`combined_features`)

*   **Proses:**
    *   Sebuah kolom baru bernama `combined_features` dibuat.
    *   Nilai pada kolom ini merupakan hasil penggabungan (konkatenasi) dari string yang telah dibersihkan pada kolom `title`, `authors`, `categories`, dan `published_year`, dengan spasi sebagai pemisah antar fitur.
*   **Alasan:**
    *   **Representasi Konten Tunggal:** Menciptakan satu representasi tekstual yang komprehensif untuk setiap buku, yang mencakup informasi konten utama dari fitur-fitur kunci.
    *   **Input untuk TF-IDF:** Kolom `combined_features` ini menjadi input utama ("dokumen") untuk TfidfVectorizer. Vektorisasi akan dilakukan pada teks gabungan ini untuk menangkap profil konten keseluruhan dari setiap buku dalam bentuk vektor numerik.

### 4. Penanganan Nilai Hilang pada Fitur Kunci (Safeguard)

*   **Proses:**
    *   Meskipun langkah pembersihan sebelumnya secara efektif menangani nilai hilang pada `title`, `authors`, `categories`, dan `published_year` (misalnya, dengan mengonversi NaN menjadi string 'nan' atau '0' untuk tahun), kode `df.dropna(subset=selected_features, how='any')` dijalankan.
    *   Langkah ini secara teoritis akan menghapus baris mana pun yang *masih* memiliki nilai hilang pada *salah satu* dari fitur-fitur kunci yang dipilih (`selected_features`).
*   **Alasan:**
    *   **Integritas Data Inti:** Meskipun langkah pembersihan sebelumnya sudah efektif (seperti terlihat pada output `df.isnull().sum()` yang menunjukkan 0 missing values untuk fitur-fitur ini), langkah `dropna` ini berfungsi sebagai **lapisan pengaman (safeguard)** untuk memastikan absolut tidak ada nilai hilang pada fitur-fitur yang paling krusial (`title`, `authors`, `categories`, `published_year`) sebelum fitur tersebut digunakan untuk membuat `combined_features` dan diumpankan ke model. Ini menjamin bahwa setiap buku yang masuk ke tahap vektorisasi memiliki profil konten dasar yang lengkap.

### 5. Penghapusan Kolom yang Tidak Diperlukan

*   **Proses:** Kolom `isbn13`, `isbn10`, dan `thumbnail` dihapus dari DataFrame.
*   **Alasan:**
    *   **Relevansi untuk Model:** Kolom-kolom ini (nomor identifikasi unik buku dan tautan gambar) tidak secara langsung memberikan informasi tentang *konten* buku yang relevan untuk pendekatan *content-based filtering* menggunakan TF-IDF pada fitur tekstual.
    *   **Efisiensi:** Menghilangkan kolom yang tidak digunakan membuat dataset lebih ringkas dan memfokuskan analisis pada fitur-fitur yang memang berkontribusi pada perhitungan kemiripan konten.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

## Referensi

1.  Linden, G., Smith, B., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. *IEEE Internet Computing*, 7(1), 76-80. Tersedia: [tautan.](https://ieeexplore.ieee.org/document/1167344)
2.  Smith, B., & Linden, G. (2017). Two decades of recommender systems at Amazon.com. *IEEE Internet Computing*, 21(3), 12-18.
3.  Martinez, M. (2017). Amazon: Everything you wanted to know about its algorithm and innovation. *IEEE Computer Society Tech News*. Tersedia: [tautan.](https://www.computer.org/publications/tech-news/trends/amazon-all-the-research-you-need%20about-its-algorithm-and-innovation)
4.  Gomez-Uribe, A., & Neil, N. (2015). The Netflix Recommender System: Algorithms, Business Value, and Innovation. *ACM Transactions on Management Information Systems*, 6(4), 1-19. Tersedia: [tautan.](https://dl.acm.org/doi/10.1145/2843948)
5.  Isinkaye, F. O., Folajimi, Y. O., & Ojokoh, B. (2015). Recommendation systems: Principles, methods and evaluation. *Egyptian Informatics Journal*, 16(3), 261-273. Tersedia: [tautan.](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)
6.  Khusro, S., Ali, Z., & Ullah, I. (2016). Recommender Systems: Issues, Challenges, and Research Opportunities. *In Information Science and Applications (ICISA), Ho Chi Minh*.
7.  Azizi, M., & Do, H. (2018). A Collaborative Filtering Recommender System for Test Case Prioritization in Web Applications. *In Proceedings of SAC 2018: Symposium on Applied Computing, Pau*.

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
