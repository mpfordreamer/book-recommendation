# Laporan Proyek Machine Learning - I Dewa Gede Mahesta Parawangsa
Proyek Sistem Rekomendasi ini mengembangkan model content-based filtering untuk menghasilkan top-N rekomendasi buku, serta memanfaatkan K-Means clustering untuk menganalisis pengelompokan buku berdasarkan fitur-fiturnya.

## Project Overview

<img src="https://github.com/user-attachments/assets/0fc41268-0865-4095-b6dd-7e11e691f1ca" alt="Buku Self Development" width="600">

<br>[Referensi Gambar](https://digitalskola.com/blog/home/buku-self-development)

Book Recommendation System
*Konsep Sistem Rekomendasi Buku (Sumber: Diadaptasi dari berbagai sumber)*

Di era sekarang yang identik dengan era literasi, kemampuan untuk mengakses dan memanfaatkan pengetahuan menjadi krusial, terutama bagi para intelektual muda sebagai agen perubahan dalam menghadapi tantangan global [[1](https://jurnal.unissula.ac.id/index.php/ELIC/article/view/1282/)]. Perpustakaan, sebagai pusat koleksi buku dan bahan bacaan, memegang peran penting dalam mendukung literasi dan penyediaan informasi [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

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

### Eksploratory Data Analysis (EDA)

Analisis data eksploratif (EDA) dilakukan untuk mendapatkan pemahaman mendalam mengenai karakteristik dan distribusi data dalam dataset buku (`book.xlsx`). EDA ini membantu mengidentifikasi pola, anomali, dan bias dalam data yang dapat mempengaruhi pengembangan sistem rekomendasi. Berikut adalah temuan utama:

1.  **Distribusi Kategori Buku:**
    ![image](https://github.com/user-attachments/assets/579a7e0f-8de2-4922-a27e-106f2f472237)
    *   **Visualisasi:** *Bar chart* menampilkan 10 kategori buku teratas berdasarkan frekuensinya.
    *   **Pengamatan:**
        *   **Dominasi Fiksi:** Kategori **Fiksi (`fiction`)** sangat dominan, muncul lebih dari 2500 kali, jauh mengungguli kategori lainnya.
        *   **Kategori Populer Berikutnya:** Fiksi Remaja (`juvenile fiction`) dan Biografi/Autobiografi (`biography & autobiography`) menempati posisi kedua dan ketiga dengan frekuensi masing-masing sekitar 540 dan 400 kali.
        *   **Ketidakseimbangan Data:** Kategori populer lainnya (seperti `history`, `literary criticism`, dll.) muncul dengan frekuensi yang jauh lebih rendah.
    *   **Interpretasi:** Distribusi kategori yang sangat tidak seimbang ini penting untuk diketahui. Hal ini berpotensi menyebabkan model rekomendasi cenderung lebih banyak menyarankan buku fiksi dibandingkan kategori lain yang kurang terwakili, kecuali jika ditangani secara khusus dalam pemodelan.

2.  **Tren Tahun Publikasi:**
    ![image](https://github.com/user-attachments/assets/f954c04f-30de-4763-9b79-4aa7f07e1ba6)

    *   **Visualisasi:** Histogram menunjukkan distribusi jumlah buku yang diterbitkan per tahun.
    *   **Pengamatan:**
        *   **Konsentrasi pada Era Modern:** Sebagian besar buku dalam dataset diterbitkan dalam beberapa dekade terakhir.
        *   **Puncak Distribusi:** Jumlah buku terbanyak diterbitkan sekitar **awal tahun 2000-an**.
        *   **Distribusi Miring ke Kiri:** Terdapat "ekor" panjang ke arah kiri, menunjukkan jumlah buku yang jauh lebih sedikit dari tahun-tahun yang lebih lama (misalnya, sebelum 1975).
        *   **Peningkatan Signifikan:** Jumlah penerbitan buku mulai meningkat secara signifikan sejak sekitar tahun 1970-an.
    *   **Interpretasi:** Dataset ini didominasi oleh buku-buku yang relatif modern. Sistem rekomendasi mungkin akan lebih efektif dalam merekomendasikan buku-buku baru atau yang terbit setelah tahun 1970-an karena representasi data yang lebih kaya untuk periode tersebut.


3.  **Popularitas Penulis:**
    ![image](https://github.com/user-attachments/assets/cdb33eaa-ceb6-4d76-b038-155d584df720)
    *   **Visualisasi:** *Bar chart* menampilkan 10 penulis dengan jumlah buku terbanyak dalam dataset.
    *   **Pengamatan:**
        *   **Penulis Teratas:** **Agatha Christie** dan **Stephen King** memiliki representasi buku terbanyak (masing-masing lebih dari 35 buku). William Shakespeare juga sangat terwakili.
        *   **Representasi Tinggi Lainnya:** Penulis populer lain seperti J.R.R. Tolkien, Virginia Woolf, dan Sandra Brown juga memiliki jumlah buku yang signifikan (umumnya antara 17 hingga 26 buku).
    *   **Interpretasi:** Dataset ini memiliki bias terhadap penulis-penulis yang sangat populer dan produktif. Rekomendasi yang dihasilkan mungkin cenderung mengulang penulis-penulis ini, kecuali jika ada mekanisme untuk meningkatkan keberagaman penulis.



4.  **Distribusi Rata-Rata Rating:**
    ![image](https://github.com/user-attachments/assets/55423b12-730c-48a1-84fa-4e8ce9aadc27)
    *   **Visualisasi:** Histogram menunjukkan distribusi rata-rata rating buku. *Catatan: Skala pada sumbu X (0-500) tampaknya tidak sesuai dengan skala rating buku standar (misalnya 1-5). Ini perlu diperhatikan.*
    *   **Pengamatan:**
        *   **Distribusi Bimodal:** Terdapat dua puncak utama dalam distribusi.
        *   **Puncak Rating Tinggi:** Puncak utama (mayoritas buku) berada di sekitar **rating 380-420** (pada skala 0-500 yang tertera), menandakan kecenderungan buku memiliki rating tinggi dalam skala tersebut.
        *   **Puncak Kecil Rating Rendah:** Terdapat puncak kedua yang jauh lebih kecil di sekitar rating 0-50, menunjukkan adanya sekelompok buku dengan rating sangat rendah.
    *   **Interpretasi:** Adanya dua kelompok rating (tinggi dan rendah) ini menarik. Namun, **skala rating yang tidak standar (0-491?) memerlukan klarifikasi atau normalisasi** sebelum fitur ini dapat digunakan secara efektif dalam pemodelan, karena interpretasi nilai absolutnya menjadi sulit. Pola bimodal mungkin menunjukkan adanya segmen buku yang sangat disukai dan yang sangat tidak disukai.



5.  **Distribusi Jumlah Halaman:**
    ![image](https://github.com/user-attachments/assets/d18202a3-8504-4dfe-a478-d35d4291ef17)
    *   **Visualisasi:** *Box plot* menunjukkan sebaran jumlah halaman buku.
    *   **Pengamatan:**
        *   **Konsentrasi Utama (Kotak/Box):** 50% buku di tengah dataset memiliki jumlah halaman antara sekitar 150-200 hingga 350-400 halaman.
        *   **Median:** Garis di dalam kotak (median) berada di sekitar 250-300 halaman, artinya setengah dari buku memiliki halaman lebih sedikit dari ini, dan setengahnya lebih banyak.
        *   **Banyaknya Outlier:** Terdapat sangat banyak titik (*outlier*) di sebelah kanan *whisker*, menunjukkan adanya sejumlah besar buku dengan jumlah halaman yang sangat tinggi (bisa mencapai lebih dari 1000, 2000, bahkan 3000 halaman).
        *   **Distribusi Miring ke Kanan:** Keberadaan banyak *outlier* ini membuat distribusi jumlah halaman menjadi sangat miring ke kanan (*right-skewed*).
    *   **Interpretasi:** Sebagian besar buku memiliki ketebalan standar, namun keberadaan buku-buku yang sangat tebal sebagai *outlier* signifikan. Jika fitur jumlah halaman digunakan dalam pemodelan (misalnya, untuk clustering), pengaruh *outlier* ini perlu diperhatikan, dan penggunaan teknik *scaling* yang tahan *outlier* (seperti `RobustScaler`) mungkin diperlukan.



6.  **Keunikan Judul:**
    *   **Pengamatan:** Dari total 6810 entri buku, terdapat 6397 judul yang unik.
    *   **Persentase:** Ini berarti **93.9%** dari buku dalam dataset memiliki judul yang berbeda satu sama lain.
    *   **Interpretasi:** Tingkat keunikan judul yang tinggi ini menunjukkan kualitas data yang baik dari segi identifikasi buku dan minimnya duplikasi pencatatan berdasarkan judul yang sama persis. Ini memudahkan proses pencocokan judul yang dimasukkan pengguna dengan data yang ada.

    ```
    Unique Titles: 6397/6810 (93.9%)
    ```

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

Pada tahap ini, dikembangkan model sistem rekomendasi buku berdasarkan data yang telah disiapkan. Tujuan utamanya adalah untuk memberikan rekomendasi buku yang relevan kepada pengguna. Dalam proyek ini, disajikan dua pendekatan atau solusi rekomendasi yang berbeda:

1.  **Content-Based Filtering (CBF) Murni:** Menggunakan kemiripan konten antar buku.
2.  **Rekomendasi Berbasis Konten yang Disempurnakan dengan Cluster (CBF + K-Means):** Menggabungkan kemiripan konten dengan informasi dari pengelompokan (clustering) buku untuk memberikan rekomendasi tambahan yang berpotensi lebih beragam atau populer.

Kedua pendekatan ini dibangun untuk mengatasi permasalahan dalam menemukan buku yang sesuai dengan preferensi pengguna.

### 1. Content-Based Filtering (TF-IDF & Cosine Similarity)

Pendekatan pertama adalah sistem rekomendasi berbasis konten murni. Ide dasarnya adalah merekomendasikan buku yang memiliki kemiripan fitur atau konten dengan buku yang disukai pengguna di masa lalu atau buku yang sedang dilihat.

**Implementasi:**

1.  **Penggabungan Fitur Konten:** Fitur-fitur tekstual dan kategorikal yang relevan seperti `title`, `categories`, `authors`, dan `published_year` digabungkan menjadi satu representasi teks tunggal untuk setiap buku. Ini menciptakan deskripsi komprehensif dari konten setiap buku.
2.  **TF-IDF Vectorization:** Teks gabungan tersebut kemudian diubah menjadi representasi vektor numerik menggunakan `TfidfVectorizer` dari `sklearn`. TF-IDF (Term Frequency-Inverse Document Frequency) mengukur seberapa penting sebuah kata dalam sebuah dokumen (buku) relatif terhadap keseluruhan koleksi dokumen (semua buku). Hasilnya adalah matriks TF-IDF di mana setiap baris mewakili buku dan setiap kolom mewakili kata unik, dengan nilai sel adalah skor TF-IDF.
3.  **Cosine Similarity:** Kemiripan antar buku dihitung berdasarkan vektor TF-IDF mereka menggunakan metrik Cosine Similarity. Metrik ini mengukur kosinus sudut antara dua vektor, menghasilkan skor antara 0 (tidak mirip) hingga 1 (sangat mirip). Matriks kemiripan (similarity matrix) persegi dihasilkan, di mana `similarity[i][j]` menunjukkan skor kemiripan antara buku ke-i dan buku ke-j.
4.  **Pemberian Rekomendasi Top-N:** Ketika pengguna memberikan input judul buku, sistem mencari kecocokan terdekat dalam dataset, mengambil baris skor kemiripan yang sesuai dari matriks similarity, mengurutkannya secara menurun, dan menyajikan N buku teratas (tidak termasuk buku input itu sendiri) sebagai rekomendasi.

**Contoh Output Top-5 Rekomendasi (untuk input 'Gilead'):**

| Rank | Title            | Authors               | Categories   | Published Year | Cosine Similarity |
| :--- | :--------------- | :-------------------- | :----------- | :------------- | :---------------- |
| 1    | the martians     | kim stanley robinson  | fiction      | 2000           | 0.32              |
| 2    | robinson crusoe  | daniel defoe          | fiction      | 2003           | 0.31              |
| 3    | kilo class       | patrick robinson      | fiction      | 1999           | 0.31              |
| 4    | uss seawolf      | patrick robinson      | fiction      | 2001           | 0.30              |
| 5    | pacific edge     | kim stanley robinson  | fiction      | 1995           | 0.30              |

**Kelebihan Content-Based Filtering:**

*   **Tidak Memerlukan Data Pengguna Lain:** Rekomendasi dibuat berdasarkan profil item dan preferensi satu pengguna, tidak bergantung pada data pengguna lain (mengatasi *user cold-start*).
*   **Transparansi:** Relatif mudah menjelaskan mengapa suatu item direkomendasikan (karena mirip dengan item lain yang disukai).
*   **Mampu Merekomendasikan Item Baru/Kurang Populer:** Selama item memiliki deskripsi fitur yang memadai, item tersebut dapat direkomendasikan meskipun belum pernah dirating oleh siapa pun (mengatasi *item cold-start*).

**Kekurangan Content-Based Filtering:**

*   **Keterbatasan Analisis Konten:** Membutuhkan data fitur item yang baik. Jika fitur tidak cukup deskriptif atau sulit diekstrak (misalnya, kualitas tulisan, nuansa plot), kualitas rekomendasi menurun.
*   **Overspecialisasi:** Cenderung merekomendasikan item yang sangat mirip dengan apa yang sudah disukai pengguna, sehingga sulit menemukan item dari genre atau tipe yang benar-benar baru (*serendipity* rendah).
*   **Membutuhkan Pengetahuan Domain:** Proses *feature engineering* (memilih dan menggabungkan fitur) seringkali memerlukan pemahaman domain yang baik.

### 2. Rekomendasi Berbasis Konten yang Disempurnakan dengan Cluster (CBF + K-Means)

Pendekatan kedua bertujuan untuk menambahkan dimensi lain pada rekomendasi dengan memanfaatkan struktur kelompok dalam data buku. Selain memberikan rekomendasi berdasarkan kemiripan konten murni, pendekatan ini juga mempertimbangkan popularitas atau karakteristik kelompok buku.

**Implementasi:**

1.  **Seleksi Fitur Clustering:** Fitur numerik yang mencerminkan popularitas atau karakteristik umum buku seperti `average_rating`, `num_pages`, dan `ratings_count` dipilih.
2.  **Scaling Fitur:** Fitur-fitur tersebut di-scaling menggunakan `RobustScaler` agar nilainya berada dalam rentang yang sebanding dan tidak didominasi oleh fitur dengan skala besar. RobustScaler dipilih karena ketahanannya terhadap *outlier*.
3.  **K-Means Clustering:** Algoritma K-Means diterapkan pada data fitur yang telah di-scaling untuk mengelompokkan buku ke dalam cluster. Berdasarkan analisis Elbow Method dan Silhouette Score, jumlah cluster optimal (k) ditetapkan menjadi 2. Hasil clustering ini (misalnya, Cluster 0 dan Cluster 1) kemudian ditambahkan sebagai fitur baru ke DataFrame utama. Dalam proyek ini, cluster-cluster tersebut diinterpretasikan sebagai representasi, misalnya, buku "Underrated" (Cluster 0) dan buku "Best Seller / Popular" (Cluster 1).
4.  **Pemberian Rekomendasi Gabungan:** Fungsi `recommend_with_cluster_info` dikembangkan. Fungsi ini:
    *   Mengambil input judul buku dan menentukan clusternya.
    *   Menampilkan Top-N rekomendasi berdasarkan **kemiripan konten (CBF)** murni (sama seperti pendekatan pertama).
    *   Secara terpisah, mengidentifikasi buku-buku dari **cluster "populer" (Cluster 1)**, menghitung kemiripan kontennya dengan buku input (menggunakan matriks similarity CBF), dan menampilkan Top-3 buku populer yang paling mirip. Ini memberikan opsi rekomendasi tambahan yang mungkin tidak muncul di Top-N CBF murni jika buku input berasal dari cluster yang berbeda.

**Contoh Output Top-3 Rekomendasi Populer (untuk input 'bali'/'bliss' dari Cluster 0):**

| Rank | Title                        | Authors         | Categories   | Published Year | Content Similarity |
| :--- | :--------------------------- | :-------------- | :----------- | :------------- | :----------------- |
| 1    | the alchemist                | paulo coelho    | fiction      | 2006           | 0.158              |
| 2    | the giver                    | lois lowry      | juvenile fiction | 2006           | 0.151              |
| 3    | the fellowship of the ring | j r r tolkien | fiction      | 2003           | 0.151              |

**Kelebihan Pendekatan CBF + K-Means:**

*   **Potensi Peningkatan Keberagaman/Serendipity:** Dengan menyarankan item populer dari cluster lain (meskipun kemiripan kontennya mungkin lebih rendah daripada rekomendasi CBF murni), sistem dapat membantu pengguna menemukan item di luar "gelembung filter" mereka.
*   **Memanfaatkan Struktur Data:** Menggunakan informasi implisit dari interaksi pengguna (rating, jumlah halaman/rating) melalui clustering untuk menginformasikan rekomendasi.
*   **Memberikan Konteks Tambahan:** Informasi cluster ("Underrated", "Best Seller") memberikan konteks tambahan pada buku yang direkomendasikan.

**Kekurangan Pendekatan CBF + K-Means:**

*   **Ketergantungan pada Kualitas Cluster:** Efektivitas rekomendasi tambahan sangat bergantung pada seberapa baik dan bermakna hasil clustering K-Means. Jika cluster tidak terpisah dengan baik atau tidak merepresentasikan konsep yang berguna (seperti popularitas), manfaatnya berkurang.
*   **Kompleksitas Tambahan:** Memerlukan langkah tambahan untuk clustering dan interpretasi cluster.
*   **Masih Berbasis Konten:** Rekomendasi "populer" masih diurutkan berdasarkan kemiripan konten (CBF) dengan input, hanya saja difilter dari cluster tertentu. Ini bukan pendekatan kolaboratif murni.
*   **Ketidakseimbangan Cluster:** Seperti yang terlihat pada evaluasi, jika satu cluster sangat dominan (Cluster 0: 99.7%), kemampuan untuk merekomendasikan item dari cluster minoritas (Cluster 1: 0.3%) menjadi terbatas atau kurang berdampak luas.

## Evaluation

Pada bagian ini, dilakukan evaluasi terhadap model-model sistem rekomendasi yang telah dikembangkan: Content-Based Filtering (CBF) murni dan K-Means Clustering yang digunakan untuk memperkaya rekomendasi. Evaluasi bertujuan untuk mengukur relevansi, keberagaman, dan kualitas struktur data yang ditemukan oleh model.

Metrik evaluasi yang digunakan disesuaikan dengan tugas masing-masing model:

1.  **Evaluasi Content-Based Filtering (CBF):**
    *   Skor Kemiripan (Cosine Similarity - sebagai proxy Relevansi)
    *   Intra-List Similarity (sebagai metrik Keberagaman)
2.  **Evaluasi K-Means Clustering:**
    *   Silhouette Score
    *   Calinski-Harabasz Index
    *   Davies-Bouldin Index
3.  **Evaluasi Model Hybrid (CBF + K-Means):**
    *   Analisis Keselarasan Cluster (Cluster Alignment)

### Evaluasi Content-Based Filtering (CBF)

Metrik berikut digunakan untuk mengevaluasi rekomendasi yang dihasilkan oleh model CBF murni (TF-IDF & Cosine Similarity).

#### 1. Skor Kemiripan (Relevansi)

*   **Metrik:** Rata-rata Skor Kemiripan dan Skor Kemiripan Tertinggi (Average & Highest Similarity Score).
*   **Tujuan:** Mengukur seberapa mirip (relevan) buku-buku yang direkomendasikan dengan buku input berdasarkan kontennya.
*   **Cara Kerja:** Metrik ini menggunakan skor Cosine Similarity yang dihasilkan pada tahap modeling.
    *   `Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||)`
    *   Skor berkisar antara 0 (tidak mirip) hingga 1 (identik). Skor yang lebih tinggi untuk rekomendasi teratas menunjukkan relevansi konten yang lebih baik. Rata-rata skor memberikan gambaran umum kemiripan daftar rekomendasi, sedangkan skor tertinggi menunjukkan item paling mirip.
*   **Hasil Proyek:**
    *   Untuk input 'Gilead', Rata-rata Skor: 0.31, Skor Tertinggi: 0.32.
    *   Untuk input 'The Four Loves', Rata-rata Skor: 0.49, Skor Tertinggi: 0.64.
    *   Untuk input 'Rage of Angels', Rata-rata Skor: 0.48, Skor Tertinggi: 0.51.
    *   Untuk input 'The One Tree', Rata-rata Skor: 0.41, Skor Tertinggi: 0.48.
    *   Untuk input '1984', Rata-rata Skor: 0.50, Skor Tertinggi: 0.63.
*   **Interpretasi:** Skor kemiripan rata-rata dan tertinggi menunjukkan tingkat relevansi yang moderat hingga cukup baik. Rekomendasi yang diberikan memiliki hubungan konten yang jelas dengan buku input, namun tidak terlalu identik, yang mungkin diinginkan untuk penemuan.

#### 2. Intra-List Similarity (Keberagaman)

*   **Metrik:** Rata-rata Intra-List Similarity.
*   **Tujuan:** Mengukur seberapa mirip buku-buku *di dalam* daftar rekomendasi satu sama lain. Skor yang lebih rendah menunjukkan keberagaman yang lebih tinggi (buku-buku yang direkomendasikan tidak terlalu mirip satu sama lain).
*   **Cara Kerja:** Metrik ini menghitung rata-rata Cosine Similarity untuk semua pasangan buku unik dalam daftar rekomendasi Top-N. Skor 0 berarti tidak ada kemiripan sama sekali antar rekomendasi (sangat beragam), skor 1 berarti semua rekomendasi identik (tidak beragam). Dihitung menggunakan fungsi `calculate_cbf_diversity`
    *   Konsep: `Avg(CosineSim(Item_i, Item_j))` untuk semua `i != j` dalam daftar rekomendasi.
*   **Hasil Proyek:**
    *   Untuk input 'Gilead': 0.34
    *   Untuk input 'The Four Loves': 0.47
    *   Untuk input 'Rage of Angels': 0.32
    *   Untuk input 'The One Tree': 0.20
    *   Untuk input '1984': 0.35
*   **Interpretasi:** Nilai Intra-List Similarity yang dihasilkan relatif rendah (jauh di bawah 0.7), menunjukkan bahwa rekomendasi yang dihasilkan oleh model CBF memiliki **keberagaman yang baik**. Sistem tidak hanya menyarankan buku yang sangat mirip satu sama lain.

### Evaluasi K-Means Clustering

Metrik berikut digunakan untuk menilai kualitas pengelompokan (clustering) data buku ke dalam 2 cluster menggunakan K-Means, *sebelum* cluster ini digunakan dalam rekomendasi hybrid. Evaluasi ini penting karena kualitas rekomendasi tambahan bergantung pada kualitas cluster yang terbentuk.

#### 1. Silhouette Score

*   **Tujuan:** Mengukur seberapa baik setiap objek (buku) cocok dengan clusternya sendiri dibandingkan dengan cluster tetangga terdekat.
*   **Cara Kerja:** Skor berkisar antara -1 hingga 1.
    *   Nilai mendekati +1: Objek sangat cocok dengan clusternya sendiri dan jauh dari cluster lain.
    *   Nilai sekitar 0: Objek berada dekat dengan batas antar cluster.
    *   Nilai mendekati -1: Objek mungkin salah diklasifikasikan ke dalam cluster.
    *   Rumus ini membandingkan jarak rata-rata objek ke titik lain dalam clusternya (a) dengan jarak rata-rata objek ke titik dalam cluster terdekat berikutnya (b): `(b - a) / max(a, b)`. Skor keseluruhan adalah rata-rata skor Silhouette untuk semua objek.
*   **Hasil Proyek:** 0.976.
*   **Interpretasi:** Skor yang sangat tinggi (mendekati 1) menunjukkan bahwa K-Means berhasil menciptakan **cluster yang sangat padat dan terpisah dengan baik**. Buku-buku dalam satu cluster sangat mirip satu sama lain (berdasarkan fitur clustering) dan sangat berbeda dari buku di cluster lain.

#### 2. Calinski-Harabasz Index (Variance Ratio Criterion)

*   **Tujuan:** Mengukur rasio antara varians antar-cluster (seberapa jauh pusat cluster satu sama lain) dan varians intra-cluster (seberapa padat titik data dalam satu cluster).
*   **Cara Kerja:** Skor yang lebih tinggi menunjukkan cluster yang lebih baik (lebih padat dan lebih terpisah). Tidak ada batas atas, tetapi nilai yang lebih tinggi secara relatif lebih baik.
    *   Formula: `(SSB / SSW) * ((N - k) / (k - 1))` di mana SSB adalah Sum of Squares Between clusters, SSW adalah Sum of Squares Within clusters, N jumlah data, k jumlah cluster.
*   **Hasil Proyek:** 10063.465.
*   **Interpretasi:** Nilai yang sangat tinggi ini mengindikasikan bahwa **struktur cluster yang ditemukan sangat jelas**, dengan varians antar-cluster jauh lebih besar daripada varians intra-cluster.

#### 3. Davies-Bouldin Index

*   **Tujuan:** Mengukur rata-rata 'kemiripan' antara setiap cluster dengan cluster yang paling mirip dengannya, di mana kemiripan adalah rasio jarak intra-cluster terhadap jarak antar-cluster.
*   **Cara Kerja:** Skor yang lebih rendah menunjukkan pemisahan cluster yang lebih baik, dengan 0 sebagai skor terendah yang mungkin. Indeks menghitung rasio penyebaran dalam cluster terhadap pemisahan antar cluster untuk setiap cluster, lalu merata-ratakannya.
    *   Formula: `(1/k) * Σ max( (Si + Sj) / Dij )` dimana k jumlah cluster, Si simpangan rata-rata cluster i dari centroidnya, Dij jarak antar centroid cluster i dan j. Dicari rasio maksimum untuk setiap cluster i terhadap cluster lain j.
*   **Hasil Proyek:** 0.353.
*   **Interpretasi:** Skor yang relatif rendah (mendekati 0) ini juga menunjukkan bahwa **cluster terpisah dengan baik**.

**Kesimpulan Evaluasi Clustering:** Ketiga metrik (Silhouette, Calinski-Harabasz, Davies-Bouldin) secara konsisten menunjukkan bahwa algoritma K-Means dengan k=2 berhasil menemukan struktur cluster yang kuat dan jelas dalam data berdasarkan fitur `average_rating`, `num_pages`, dan `ratings_count`. Ini memberikan dasar yang baik untuk menggunakan label cluster dalam pendekatan rekomendasi hybrid.

### Evaluasi Model Hybrid (CBF + K-Means)

Metrik ini melihat bagaimana rekomendasi CBF murni berinteraksi dengan struktur cluster yang ditemukan.

#### 1. Keselarasan Cluster (Cluster Alignment)

*   **Tujuan:** Menganalisis dari cluster mana rekomendasi CBF berasal, relatif terhadap cluster buku input.
*   **Cara Kerja:** Untuk buku input dari cluster tertentu, dihitung persentase rekomendasi Top-N CBF yang berasal dari cluster yang sama. Dihitung menggunakan fungsi `analyze_cluster_alignment`.
*   **Hasil Proyek:**
    *   Untuk buku input dari Cluster 0 ("Underrated"): 100% (5/5) rekomendasi berasal dari Cluster 0.
    *   Untuk buku input dari Cluster 1 ("Best Seller"): 0% (0/5) rekomendasi berasal dari Cluster 1 (semua dari Cluster 0).
*   **Interpretasi:** Hasil ini menunjukkan bahwa rekomendasi CBF sangat dipengaruhi oleh cluster asal buku input, terutama cluster dominan (Cluster 0). Ketika input berasal dari cluster minoritas (Cluster 1), CBF murni cenderung tetap merekomendasikan buku dari cluster mayoritas (Cluster 0) karena kemungkinan besar memiliki lebih banyak tetangga dekat secara konten di sana. Hal ini menyoroti potensi manfaat dari fungsi `recommend_with_cluster_info` yang secara eksplisit menyajikan rekomendasi buku populer dari Cluster 1 sebagai tambahan, meskipun kemiripan kontennya mungkin lebih rendah.

## Referensi

1.  Linden, G., Smith, B., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. *IEEE Internet Computing*, 7(1), 76-80. Tersedia: [tautan.](https://ieeexplore.ieee.org/document/1167344)
2.  Smith, B., & Linden, G. (2017). Two decades of recommender systems at Amazon.com. *IEEE Internet Computing*, 21(3), 12-18.
3.  Martinez, M. (2017). Amazon: Everything you wanted to know about its algorithm and innovation. *IEEE Computer Society Tech News*. Tersedia: [tautan.](https://www.computer.org/publications/tech-news/trends/amazon-all-the-research-you-need%20about-its-algorithm-and-innovation)
4.  Gomez-Uribe, A., & Neil, N. (2015). The Netflix Recommender System: Algorithms, Business Value, and Innovation. *ACM Transactions on Management Information Systems*, 6(4), 1-19. Tersedia: [tautan.](https://dl.acm.org/doi/10.1145/2843948)
5.  Isinkaye, F. O., Folajimi, Y. O., & Ojokoh, B. (2015). Recommendation systems: Principles, methods and evaluation. *Egyptian Informatics Journal*, 16(3), 261-273. Tersedia: [tautan.](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)
6.  Khusro, S., Ali, Z., & Ullah, I. (2016). Recommender Systems: Issues, Challenges, and Research Opportunities. *In Information Science and Applications (ICISA), Ho Chi Minh*.
7.  Azizi, M., & Do, H. (2018). A Collaborative Filtering Recommender System for Test Case Prioritization in Web Applications. *In Proceedings of SAC 2018: Symposium on Applied Computing, Pau*.
