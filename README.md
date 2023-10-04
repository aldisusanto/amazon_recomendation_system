# Laporan Proyek Machine Learning - Aldi Susanto

---

## Project Overview

---

##### Latar Belakang

![Amazon Book Shop](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Amazon_Books_logo.svg/2560px-Amazon_Books_logo.svg.png)

Amazon, sebagai salah satu perusahaan terbesar di dunia telah mengubah cara berbelanja dan berinteraksi dengan
produk. Dengan beroperasi dalam berbagai bidang, termasuk
_e-commerce_ [[1]](https://www.aboutamazon.com/news/operations/the-faces-of-amazon-operations). Amazon memiliki banyak
produk, termasuk buku yang menjadi salah satu kategori produk paling populer di platform mereka. Dengan jutaan judul
yang tersedia dalam berbagai genre dan
format. [[2]](https://self-publishingschool.com/most-popular-book-genres-on-amazon/).

Amazon menjadi platform utama bagi pembaca untuk menemukan dan membeli buku. Namun, jumlah buku yang begitu banyak,
mencari buku yang tepat adalah sesuatu yang sulit dilakukan.

Dalam platform amazon, banyak pengguna meninggalkan ulasan dan peringkat untuk buku yang mereka baca. Ulasan tersebut
memberikan wawasan yang berharga tentang konten, gaya penulisan, dan kualitas buku, serta memberikan gambaran tentang
apakah buku tersebut mungkin sesuai dengan preferensi pembaca
lainnya[[3]](https://www.junglescout.com/blog/importance-of-amazon-reviews/).

Data ulasan tersebut sangatlah berharga dan dapat digunakan untuk membangun sistem rekomendasi yang dapat membantu
pengguna menemukan buku-buku yang sesuai preferensi mereka.

----

## Business Understanding

---

### Problem Statements

- Bagaimana cara melakukan pra-pemrosesan pada data books dan rating yang akan digunakan untuk membuat sistem
  rekomendasi?
- Bagaimana cara membuat sebuah sistem rekomendasi buku yang dapat memberikan rekomendasi kepada pengguna
  berdasarkan kategori buku yang spesifik dengan mempertimbangkan minat pengguna dalam kategori tertentu?
- Bagaimana cara mengembangkan sistem rekomendasi buku yang dapat memberikan rekomendasi berdasarkan ulasan dan rating
  pengguna, dengan memastikan bahwa buku yang direkomendasikan belum pernah dibaca oleh pengguna?

### Goals

- Melakukan pra-pemrosesan dengan baik agar dapat digunakan dalam pembuatan sistem rekomendasi.
- Mengetahui cara membuat sebuah sistem rekomendasi buku yang dapat memberikan rekomendasi kepada pengguna berdasarkan
  kategori buku.
- Mengetahui cara membuat sistem rekomendasi buku berdasarkan ulasan dan rating pengguna, dengan memastikan bahwa buku
  yang direkomendasikan belum pernah dibaca oleh pengguna.

### Solution statements

Solusi yang dapat dilakukan untuk memenuhi tujuan dari _project_ ini adalah sebagai berikut:

* Menggunakan **_Content Based Filtering_ & _Collaborative Filtering_**.
* Untuk **Pra-Pemrosesan Data** dilakukan beberapa tahapan, diantaranya :
    * Menghapus fitur yang tidak digunakan pada books dan ratings.
    * Mengganti nama pada kolom books dan ratings
* **Persiapan Data.** Pada persiapan data dilakukan beberapa tahapan, sebagai berikut:.
    * Content Based Filtering.
        * Menangani Missing Value
        * Extraction Feature
    * Collaborative Filtering.
        * Merge data books dan ratings.
        * Menangani missing value pada data hasil merge.
        * Filtrasi berbasis jumlah (Jumlah user yang memberi ratings lebih dari 20 kali).
        * Encoding dan Decoding.
        * Shuffle data.
        * Train & Split data.

## Data Understanding

---
![Dataset](https://i.imgur.com/9ELRD7G.png)

Informasi dataset dapat dilihat pada _table_ dibawah ini :

Tabel 1. Informasi Dataset

| Jenis                   | Keterangan                                                                                                  |
|-------------------------|-------------------------------------------------------------------------------------------------------------|
| Sumber                  | [Kaggle Dataset : Amazon Books Reviews](https://www.kaggle.com/datasets/mohamedbakhet/amazon-books-reviews) |
| Lisensi                 | Creative Commons CC0 1.0 DEED                                                                               |
| Kategori                | Tabular, NLP, Literature, Recommendation System                                                             |
| Jenis dan Ukuran Berkas | Zip (3.4 GB)                                                                                                |

---

Pada berkas zip yang di unduh, terdapat dua berkas CSV yaitu Books_rating dan Books_data. Dengan masing-masing berjumlah
3 Juta dan 212.404 data. Berikut penjelasan variabel-variabel nya:

**Books_ratings**

* `Id` merupakan id dari books.
* `Title` merupakan judul buku.
* `Price` merupakan harga buku.
* `User_id` merupakan id user yang melakukan rating pada buku.
* `profileName` merupakan nama user yang melakukan rating pada buku.
* `review/helpfulness` merupakan rating yang diberikan oleh pengguna terhadap sebuah ulasan.
* `review/scoew` merupakan rating yang diberikan oleh pengguna terhadap buku.
* `review/time` merupakan waktu yang diberikan untuk sebuah ulasan.
* `review/summary` merupakan singkatan dari ulasan yang diberikan.
* `review/text` merupakan keseluruhan text ulasan.

**Books_ratings**

* `Title` merupakan judul buku.
* `description` merupakan detail dari buku.
* `authors` merupakan nama-nama penulis pada buku.
* `image` merupakan url untuk cover buku.
* `previewLink` merupakan link untuk akses buku di platform google books.
* `publisher` merupakan nama yang mempublikasikan buku tersebut.
* `publishedDate` merupakan tahun dipublikasikannya buku tersebut.
* `infoLink` merupakan tautan untuk mendapatkan informasi lebih lanjut tentang buku di Google Buku.
* `categories` merupakan genre-genre pada buku.
* `ratingCounts` merupakan rata-rata rating pada buku.

### _Univariate Analysis_:

___

* Mengecek jumlah data unik kolom Title dan User_id pada data ratings, berikut visualisasi-nya:

  Gambar 1. Judul dan User Unik pada ratings

  ![Judul dan Kategori Unik pada Books](https://github.com/aldisusanto/video/blob/main/gambar/userUnique.png?raw=true)

  Berdasarkan gambar diatas terdapat 212404 judul yang unik dan 1008973 user yang unik.


* Mengecek jumlah data unik kolom Title dan categories pada data books, berikut visualisasi-nya:

  Gambar 2. Judul dan Kategori Unik pada books

  ![Judul dan Kategori Unik pada Books](https://github.com/aldisusanto/video/blob/main/gambar/book_unique.png?raw=true)

  Berdasarkan gambar diatas terdapat 212404 judul yang unik dan 10884 user yang unik.

![]()

## Data Preparation

___

Berikut merupakan tahapan-tahapan dalam melakukan persiapan data:

* **Menghapus kolom/fitur yang tidak diperlukan**. Pada data terdapat kolom/fitur yang tidak diperlukan karena tidak
  memberikan pengaruh pada proses pembuatan model sistem rekomendasi sehingga bisa dihapus atau dibuang. Kolom-kolom
  tersebut yaitu kolom 'Id', 'Price', 'review/helpfulness', 'review/time', 'review/text' pada data _**ratings**_.
  Sedangkan untuk data books yang dihapus adalah 'Image', 'previewLink', 'infoLink', 'publishedDate', 'publisher', '
  infoLink', dan 'description'

* **Mengganti nama kolom/fitur pada data** **_ratings_** dan **_books_**, berikut pergantian-nya:

  Tabel 2. Pergantian nama fitur ratings.

  | Sebelum        | Sesudah |
  |----------------|---------|
  | Title          | title   |
  | User_id        | userId  |
  | review/score   | score   |
  | review/summary | summary |

  Tabel 3. Pergantian nama fitur books.

  | Sebelum        | Sesudah |
  |----------------|---------|
  | Title          | title   |

* **Persiapan data untuk Content Based Filtering**

  Pada persiapan data untuk **_Content Based Filtering_**, dilakukan 2 tahapan sebagai berikut:
    * Menangani missing value, untuk mendeteksi missing value digunakan isna().sum() pada data books.

      Tabel 4. Missing Value Books.

      | Fitur          | Jumlah _Missing Value_ | 
      |----------------|------------------------|
      | `title`        | 1                      |
      | `authors`      | 31413                  |
      | `categories`   | 41199                  |
      | `ratingCounts` | 162652                 |

      Berdasakan table diatas, dilakukan penghapusan data yang kosong menggunakan fungsi 'dropna'. Sehingga sisa buku
      sebanyak 47269 dari 212404. Penghapusan data dilakukan karena data tersebut dapat menyebabkan ketidak-konsistensi
      dalam analisis dan permodelan, serta mempercepat proses analisis dan pemodelan.


* **Extraction fitur menggunakan TfidfVectorizer**.

  Sebelum masuk pembuatan model terlebih dahulu, dilakukan reshaping data books ke dalam array dua dimensi. Dengan baris
  mewakili `title` dan kolom mewakili `categories`. Dengan cara ini juga dapat diketahui korelasi antara kedua fitur.
  Berikut samplenya:

  ![](https://github.com/aldisusanto/video/blob/main/gambar/Screenshot%20(327).png?raw=true)


* **Persiapan data untuk Collaborative Filtering**, dilakukan 6 tahapan sebagai berikut:
    * **Merge data books dan ratings**. merge dilakukan berdasarkan fitur `title` yang hasilnya ditampung di dalam
      variable
      rating_books dengan nilai baris **1.549.923**.
    * **Menangani missing value**, untuk mendeteksi missing value digunakan isna().sum() pada data rating_books.

      | Fitur          | Jumlah _Missing Value_ | 
      |----------------|------------------------|
      | `title`        | 0                      |
      | `authors`      | 0                      |
      | `categories`   | 0                      |
      | `ratingCounts` | 0                      |
      | `userId`       | 305701                 |
      | `profileName`  | 305631                 |
      | `score`        | 0                      |
      | `summary`      | 228                    |

      Berdasakan table diatas, dilakukan penghapusan data yang kosong menggunakan fungsi 'dropna'. Sehingga sisa
      rating_books sebanyak 1.244.003 dari 1.549.923.

    * **Filtrasi berbasiskan jumlah user yang memberi rating terhadap buku lebih dari 20 kali**. Hal ini, dilakukan
      untuk menghilangkan noise pada data. Dalam kasus ini, ada banyak pengguna
      yang hanya memberikan sedikit skor, dan skor tersebut bisa jadi menyesatkan model. Sehingga sisa data pada
      rating_books adalah **211447** data.
    * **Encoding dan Decoding**. Pada tahap ini akan dilakukan proses encoding yaitu proses mengubah data non-numerik
      menjadi data numerik agar model dapat memproses data tersebut. Pada proyek ini, proses encoding dilakukan pada
      fitur `userId` dan `title` dengan memanfaatkan fungsi enumerate. Kemudian memetakan `userId` dan `title` ke
      dataframe yang
      berkaitan. Dimana numeric `title` diberi nama `bookId`, sedangkan `userId` diberi nama `user`.
    * **Mengacak dataset menggunakan Shuffle**. Hal ini, dilakukan untuk mengurangi bias, meningkatkan keragaman, dan
      menghindari overfitting. Serta mendapatkan hasil random yang sama jika di run lagi dengan nilai random yang sama.
    * **Train dan split data**. Pada tahap ini dilakukan pembagian data menjadi data training dan validasi. Kemudian
      membuat
      variabel x untuk mencocokkan data user dan buku menjadi satu value, lalu membuat variabel y untuk membuat rating
      dari hasil. Setelah itu membagi menjadi 60% data train dan 40% data validasi. Setelah melakukan pembagian dataset,
      maka data siap dikonsumsi model.

      | Jumlah Total Data | Jumlah Data Latih | Jumlah Data Validation |
      |-------------------|-------------------|------------------------|
      | 211477            | 126886            | 84591                  |

## Modeling

___

Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah modeling terhadap data. Pada tahap ini
menggunakan 2 model development yaitu Content Based Filtering dan Collaborative Filtering.

### a. Content Based Filtering,

___

* **Kelebihan**, memberikan rekomendasi yang personal dan sesuai dengan preferensi pengguna berdasarkan item yang sudah
  dikenal.
* **Kekurangannya**, terbatas dalam menghadirkan variasi karena hanya merekomendasikan item yang serupa dengan yang
  sudah dikenal oleh pengguna.
* **Cara kerjanya**, dengan mengekstrak fitur dari item, kemudian mencocokkan item dengan kesamaan fitur.

_Similarity measure_ yang digunakan adalah _Cosine Similarity_. Dimana teknik ini mengukur kesamaan yang bekerja dengan
mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan
menghitung sudut _cosinus_ antara dua vector. Semakin kecil sudut _cosinus_, semakin besar nilai _cosine similarity_.
Fungsi _cosine similarity_ antara item A dan B adalah sebagai berikut:

$$\\text{cosine\\_similarity}(A, B) = \\frac{A \\cdot B}{||A||_2 \\times ||B||_2}$$

di mana:

- $A$ dan $B$ adalah dua vektor yang ingin kita hitung kesamaannya.
- $A \\cdot B$ adalah dot product (produk titik) dari $A$ dan $B$.
- $||A||_2$ dan $||B||_2$ adalah norma L2 (atau panjang) dari vektor $A$ dan $B$, masing-masing.

Jika kedua objek memiliki nilai similaritas 1, maka kedua objek dikatakan identik dan sebaliknya. Semakin besar hasil
dari fungsi similarity, maka kedua objek yang dievaluasi dianggap semakin mirip dan sebaliknya.

Berikut hasil uji coba menggunakan teknik _cosine similarity_:

* Judul untuk uji coba yaitu "The dark on the other side", dengan detail sebagai berikut:

  | title                      | categories           | authors               | ratingCounts |  
  |----------------------------|----------------------|-----------------------|--------------|
  | The dark on the other side | ['Juvenile Fiction'] | ['Joan Lowery Nixon'] | 2.0          |

* 10 hasil rekomendasi:

  | title                              | categories           | authors                                        | ratingCounts |  
  |------------------------------------|----------------------|------------------------------------------------|--------------|
  | Which Witch?                       | ['Juvenile Fiction'] | ['Eva Ibbotson']                               | 1.0          |
  | The alphabet book                  | ['Juvenile Fiction'] | ['Philip D. Eastman']                          | 4.0          |
  | The Man in the Moon                | ['Juvenile Fiction'] | ['William Joyce']                              | 17.0         |
  | REM WORLD                          | ['Juvenile Fiction'] | ['Rodman Philbrick']                           | 2.0          |
  | Shaoey And Dot: Bug Meets Bundle   | ['Juvenile Fiction'] | ['Mary Beth Chapman', 'Steven Curtis Chapman'] | 1.0          |
  | Dragonslayers                      | ['Juvenile Fiction'] | ['Bruce Coville']                              | 3.0          |
  | Wordles                            | ['Juvenile Fiction'] | ['Amy Krouse Rosenthal']                       | 2.0          |
  | Little Bears Friend                | ['Juvenile Fiction'] | ['Else Holmelund Minarik']                     | 5.0          |
  | The Watsons Go to Birmingham: 1963 | ['Juvenile Fiction'] | ['Else Holmelund Minarik']                     | 7.0          |
  | Auntie Claus                       | ['Juvenile Fiction'] | ['Elise Primavera']                            | 8.0          |

Berdasarkan hasil diatas, terlihat bahwa metode content based filtering hanya memberikan konten yang relevan.

### b. Collaborative Filtering,

___

* **Kelebihan**, menghasilkan rekomendasi yang berdasarkan perilaku dan preferensi sebenarnya dari pengguna, tanpa
  memerlukan pengetahuan ekspplisit tentang konten item.
* **Kekurangannya**, bergantung pada data perilaku pengguna, sehingga memerlukan jumlah pengguna yang cukup besar dan
  item yang cukup banyak untuk memberikan rekomendasi yang akurat.
* **Cara Kerjanya**, mencari kesamaan antara pengguna atau item berdasarkan data perilaku, seperti score dan membuat
  kesamaan ini untuk membuat rekomendasi yang sesuai.

Langkah kerja yang dilakukan, yaitu

1. Membuat Class ImprovedRecommenderNet, dengan beberapa tambahan parameter, yaitu dropout untuk menghindari
   overfitting, dan L1 dan L2 untuk mengendalikan kompleksitas pada model. Sehingga model ini dirancang untuk memberikan
   rekomendasi yang lebih baik dan mengatasi overfitting.
2. lalu menginisialisasi model menggunakan class tersebut dengan 6 parameter (num_user, num_book, dan embedding_size,
   dropout_rate, l1_strength, dan l2_strength).
3. Selanjutnya melakukan compile model dengan menentukan fungsi loss (Binary Crossentropy), optimizer (Adam), dan
   metrik (Root Mean Squared Error). Lalu melakukan fit dengan 10 epoch.
4. Terakhir melakukan prediction terhadap user yang random.

Berikut hasil dari collaborative filtering:

* Buku yang diberikan rating oleh pengguna:

  | Title                                           | Categories           |
  |-------------------------------------------------|----------------------|
  | The Long Dark Tea-Time of the Soul              | ['Fiction']          |
  | The Importance of Being Earnest and Other Plays | ['Drama']            |
  | Lion, the Witch, and the Wardrobe               | ['Fiction']          |
  | Ripley's Game                                   | ['Fiction']          |
  | The grapes of wrath, (The living library)       | ['California']       |
  | George Orwell 1984                              | ['Fiction']          |
  | Severed Wasp: A Novel                           | ['Fiction']          |
  | The Importance of Being Earnest                 | ['Fiction']          |
  | The hitchhiker's guide to the galaxy            | ['Science']          |
  | Tale of Despereaux                              | ['Juvenile Fiction'] |

* 20 hasil rekomendasi:

  | Title                                                                              | Categories                    |
  |------------------------------------------------------------------------------------|-------------------------------|
  | Jane Eyre (New Windmill)                                                           | ['Charity-schools']           |
  | When We Were Very Young                                                            | ["Children's poetry"]         |
  | Pride and Prejudice                                                                | ['Fiction']                   |
  | The Hobbit                                                                         | ['Juvenile Fiction']          |
  | The Lord of the Rings - Boxed Set                                                  | ['Young Adult Fiction']       |
  | Leaves of grass                                                                    | ['Poetry']                    |
  | Harry Potter and The Sorcerer's Stone                                              | ['Juvenile Fiction']          |
  | THE RISE AND FALL ON THE THIRD REICH                                               | ['History']                   |
  | The defence of Duffer's Drift                                                      | ['Guerrilla warfare']         |
  | The Rise and Fall of the Third Reich                                               | ['History']                   |
  | Narrative of the Life of Frederick Douglass, An American Slave. Written by Himself | ['Biography & Autobiography'] |
  | In the Heart of the Sea                                                            | ['History']                   |
  | Gone with the Wind                                                                 | ['Fiction']                   |
  | Animal Farm 50TH Anniversary Edition                                               | ['Fiction']                   |
  | Narrative of the Life of Frederick Douglass                                        | ['Biography & Autobiography'] |
  | The Hobbit There and Back Again                                                    | ['Adventure stories']         |
  | The Complete Calvin and Hobbes                                                     | ['Comics & Graphic Novels']   |
  | To Kill a Mocking Bird                                                             | ['Drama']                     |
  | No Such Thing As A Secret: A Brandy Alexander Mystery                              | ['Fiction']                   |
  | A Christmas Carol (Enriched Classics (Pocket))                                     | ['Fiction']                   |

Berdasarkan hasil diatas, terlihat bahwa metode collaborative filtering memberikan konten yang relevan dan beragam.

## Evaluasi

___

Pada _project_ ini, evaluasi yang dilakukan ada 2 yaitu menggunakan metrik "Precision at K" untuk Content Based
Filtering dan menggunakan "RMSE" untuk Collaborative Filltering.

### Content Based Filltering.

___
Untuk evaluasi _Content Based Filtering_ yang digunakan adalah precision@k.

Precision@k adalah metrik evaluasi yang digunakan untuk mengukur seberapa baik model dalam memberikan K rekomendasi atau
hasil teratas yang relevan.

Rumus untuk menghitung precision@k adalah sebagai berikut:

$$Precision@K = \\frac{\\text{Jumlah item relevan dalam K item teratas}}{K}$$

Langkah tersebut dilakukan dalam beberapa tahap:

* Menghitung presisi pada k peringkat teratas dalam hasil rekomendasi.
* Kemudian, mengambil sample buku.
* Lalu menghitung P@k untuk setiap sample menggunakan rekomendasi categories, dan menghasilkan nilai rata-rata untuk
  sample tersebut.
* Terakhir, mencetak hasil evaluasinya. Berikut hasilnya:

  | Nilai Precision@k |
  |-------------------|
  | 100.0             |
  | 60.0              |
  | 100.0             |
  | 100.0             |
  | 100.0             |
  | 100.0             |
  | 100.0             |
  | 100.0             |
  | 100.0             |
  | 100.0             |

Berdasarkan hasil evaluasi tersebut menunjukkan sistem rekomendasi berhasil memberikan rekomendasi yang sempurna sesuai
dengan
preferensi kategori buku yang sesuai dengan pengguna.

### Collaborative Fiiltering.

___

_Metric_ yang digunakan untuk mengevaluasi model adalah RMSE (_Root Mean Squared Error_). RMSE menghitung akar dari
rata-rata selisih kuadrat antara nilai prediksi dan nilai aktual. Nilai RMSE yang kecil menunjukkan performa model yang
lebih baik dan akurat.

Rumus untuk menghitung RMSE adalah sebagai berikut:

$$RMSE = \\sqrt{\\frac{1}{n}\\sum_{i=1}^{n}(y_i - \\hat{y}_i)^2}$$

di mana:

- $y_i$ adalah nilai observasi aktual.
- $\\hat{y}_i$ adalah nilai prediksi oleh model.
- $n$ adalah jumlah total observasi atau titik data.

Berikut visualisasi evaluasinya:

![Hasil Evaluasi Metric](https://github.com/aldisusanto/video/blob/main/gambar/3.png?raw=true)

Berdasarkan gambar diatas, proses training cukup smooth. Dari proses tersebut diperoleh nilai eror akhir sebesar 0.21
dan eror validasi sebesar 0.22. Nilai tersebut cukup baik untuk sistem rekomendasi. Kemudian setelah dilakukan evaluasi
menggunakan seluruh data diperoleh nilai sebesar 0.24

### Kesimpulan

---
Dengan demikian, kedua goals berhasil diselesaikan dengan menggunakan 2 metode yaitu Content Based Filtering dan
Collaborative Filtering. Setalah diujikan kedua metode berhasil memberikan 10 top recommended dengan cukup baik.

## Referensi

___

[1]    “The faces of Amazon operations,” US About Amazon. Accessed: Oct. 04, 2023. [Online].
Available: https://www.aboutamazon.com/news/operations/the-faces-of-amazon-operations

[2]    “What Are the Most Popular Book Genres on Amazon?” Accessed: Oct. 04, 2023. [Online].
Available: https://self-publishingschool.com/most-popular-book-genres-on-amazon/

[3]    “Why Product Reviews Are Important for Amazon Sellers.” Accessed: Oct. 04, 2023. [Online].
Available: https://www.junglescout.com/blog/importance-of-amazon-reviews/




