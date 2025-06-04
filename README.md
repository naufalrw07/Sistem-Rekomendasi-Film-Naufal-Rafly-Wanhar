# Laporan Proyek Machine Learning Sistem Rekomendasi Film - Naufal Rafly Wanhar

## Project Overview

Di era digital saat ini, pengguna dihadapkan pada ledakan informasi, terutama dalam platform hiburan seperti layanan streaming film. Ketersediaan pilihan film yang sangat melimpah, meskipun pada awalnya tampak menguntungkan, seringkali justru membuat pengguna kesulitan dalam menemukan tontonan yang benar-benar sesuai dengan selera dan preferensi unik mereka. Fenomena ini dikenal sebagai paradox of choice, di mana terlalu banyak pilihan dapat menyebabkan kebingungan, kecemasan dalam mengambil keputusan, dan pada akhirnya mengurangi kepuasan pengguna [1]. Sistem rekomendasi hadir sebagai solusi teknologi yang bertujuan untuk mengatasi masalah ini dengan menyaring secara cerdas dan menyajikan sejumlah kecil item, dalam hal ini film, yang paling relevan dan berpotensi disukai oleh masing-masing pengguna.

Implementasi sistem rekomendasi yang efektif telah menjadi krusial bagi keberhasilan platform digital, khususnya di industri hiburan. Dengan memberikan rekomendasi yang dipersonalisasi, platform dapat secara signifikan meningkatkan pengalaman pengguna, yang berujung pada peningkatan engagement, loyalitas, dan retensi pelanggan [2]. Lebih jauh lagi, sistem rekomendasi juga memainkan peran penting dalam strategi bisnis dengan membantu platform memonetisasi konten secara lebih efektif, mempromosikan item dari long-tail katalog yang mungkin sulit ditemukan pengguna, serta meningkatkan diversitas konten yang dikonsumsi [3]. Kemampuan untuk menghubungkan pengguna dengan konten yang tepat pada waktu yang tepat adalah nilai tambah kompetitif yang signifikan.

Secara umum, terdapat beberapa pendekatan utama dalam pengembangan sistem rekomendasi, di antaranya adalah Content-Based Filtering, Collaborative Filtering, dan pendekatan Hybrid yang mengkombinasikan keduanya atau dengan teknik lain [4]. Content-Based Filtering menganalisis atribut atau konten dari item untuk merekomendasikan item serupa dengan yang disukai pengguna di masa lalu. Di sisi lain, Collaborative Filtering bekerja dengan mengidentifikasi pola dari sejumlah besar pengguna (kolaborasi) untuk menemukan pengguna dengan selera serupa dan merekomendasikan item yang disukai oleh pengguna-pengguna serupa tersebut. Setiap pendekatan memiliki kelebihan dan kekurangannya masing-masing, serta tantangan implementasi yang unik.

Proyek ini bertujuan untuk melakukan eksplorasi mendalam dan implementasi praktis dari dua pendekatan fundamental tersebut, yaitu Content-Based Filtering dan Collaborative Filtering, dalam konteks sistem rekomendasi film. Dengan memanfaatkan dataset publik yang berisi informasi film dan rating pengguna, akan dibangun model-model yang mampu menghasilkan daftar rekomendasi yang dipersonalisasi. Diharapkan melalui proyek ini, dapat diperoleh pemahaman yang lebih baik mengenai mekanisme kerja, aspek teknis, serta potensi dan keterbatasan dari masing-masing metode dalam memberikan rekomendasi film yang relevan dan bermanfaat bagi pengguna.

## Business Understanding

Pada bagian ini, akan dijelaskan proses klarifikasi masalah yang melatarbelakangi kebutuhan akan sistem rekomendasi film, serta tujuan spesifik yang ingin dicapai melalui proyek ini. Pemahaman yang jelas terhadap masalah dan tujuan bisnis adalah fondasi penting dalam merancang solusi yang efektif dan relevan.

### Problem Statements

Berikut adalah beberapa pernyataan masalah utama yang diidentifikasi:

1. **Kesulitan Pengguna dalam Penemuan Konten (Information Overload):** Pengguna platform film seringkali dihadapkan pada katalog berisi ribuan hingga puluhan ribu judul film. Volume pilihan yang sangat besar ini dapat menyulitkan pengguna untuk menemukan film yang benar-benar sesuai dengan preferensi unik dan mood mereka saat itu, yang berpotensi menyebabkan decision fatigue dan penurunan kepuasan.

2. **Kebutuhan Personalisasi untuk Meningkatkan User Engagement:** Dalam industri layanan streaming yang kompetitif, kemampuan untuk memberikan pengalaman yang dipersonalisasi menjadi kunci. Platform perlu menyajikan konten yang relevan secara proaktif untuk menjaga pengguna tetap terlibat (engaged), meningkatkan durasi kunjungan, dan pada akhirnya membangun loyalitas serta mengurangi churn rate.

3. **Tantangan dalam Merekomendasikan Konten secara Efektif untuk Berbagai Skenario:** Tidak semua film atau pengguna memiliki jumlah data historis yang sama. Platform menghadapi tantangan dalam merekomendasikan film-film baru yang belum banyak mendapatkan rating (masalah item cold start) atau memberikan rekomendasi berkualitas kepada pengguna baru dengan sedikit riwayat interaksi (masalah user cold start). Selain itu, preferensi pengguna bisa jadi kompleks dan tidak selalu mudah ditangkap hanya dari satu jenis informasi.

### Goals

Untuk menjawab pernyataan masalah yang telah diuraikan, proyek ini memiliki tujuan-tujuan berikut:

1. **Mengembangkan Sistem Rekomendasi Berbasis Konten:** Membangun sebuah model sistem rekomendasi yang mampu menganalisis atribut intrinsik film (seperti genre, judul, atau deskripsi) untuk mengidentifikasi dan menyarankan film-film yang memiliki kemiripan konten dengan film yang disukai pengguna atau sesuai dengan profil preferensi konten pengguna.

2. **Mengimplementasikan Sistem Rekomendasi Berbasis Kolaborasi Pengguna:** Membuat sebuah model sistem rekomendasi yang dapat mempelajari pola dari data interaksi historis pengguna (khususnya data rating) untuk menemukan pengguna dengan selera serupa dan merekomendasikan film yang populer di antara kelompok pengguna tersebut, atau memprediksi rating pengguna untuk film yang belum mereka tonton.

3. **Menyediakan Daftar Rekomendasi Top-N yang Relevan:** Menghasilkan output berupa daftar sejumlah N film teratas (Top-N recommendations) yang paling relevan untuk pengguna tertentu atau sebagai kelanjutan dari film tertentu, menggunakan kedua pendekatan yang dikembangkan, sehingga memberikan solusi praktis yang dapat langsung dirasakan manfaatnya.

### Solution statements

Untuk mencapai tujuan-tujuan yang telah ditetapkan, diajukan dua pendekatan solusi utama yang akan diimplementasikan dan dieksplorasi dalam proyek ini, sesuai dengan praktik umum dalam pengembangan sistem rekomendasi:

1. **Pendekatan Content-Based Filtering:**
    
    Solusi ini akan fokus pada karakteristik atau atribut dari film itu sendiri. Rencananya adalah:

    - Menggabungkan informasi tekstual dari judul film dan genrenya untuk membuat representasi konten yang komprehensif.

    - Melakukan pra-pemrosesan teks untuk membersihkan dan menstandarisasi data konten.

    - Menggunakan teknik TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengubah representasi teks konten film menjadi vektor numerik yang dapat diukur kemiripannya.

    - Menghitung kemiripan antar film menggunakan metrik Cosine Similarity pada vektor TF-IDF tersebut.

    - Berdasarkan skor kemiripan, sistem akan merekomendasikan film-film yang paling mirip dengan film yang dijadikan input atau disukai pengguna.

2. **Pendekatan Collaborative Filtering (menggunakan Matrix Factorization dengan Neural Network):**

    Solusi ini akan memanfaatkan data interaksi pengguna-film, khususnya rating yang diberikan pengguna. Rencananya adalah:

    - Melakukan pra-pemrosesan data rating, termasuk encoding ID pengguna dan ID film menjadi format numerik yang sesuai untuk model.

    - Mengimplementasikan model Matrix Factorization menggunakan arsitektur Neural Network. Model ini akan mempelajari representasi laten (embeddings) untuk setiap pengguna dan setiap film.

    - Interaksi antara pengguna dan film (prediksi rating) akan dimodelkan sebagai hasil dari operasi (misalnya, dot product) antara embedding pengguna dan embedding film, ditambah dengan komponen bias.

    - Model akan dilatih untuk meminimalkan error antara rating yang diprediksi dan rating aktual yang diberikan pengguna, menggunakan data latih.

    - Setelah model dilatih, model tersebut dapat digunakan untuk memprediksi rating film yang belum pernah ditonton oleh pengguna, dan kemudian merekomendasikan film dengan prediksi rating tertinggi.

## Data Understanding
Dataset yang digunakan dalam proyek sistem rekomendasi film ini adalah "Movie Recommendation System" yang bersumber dari platform Kaggle. Dataset ini menyediakan informasi mengenai berbagai film beserta rating yang diberikan oleh para pengguna. Data ini sangat cocok untuk membangun dan menguji model rekomendasi berbasis konten maupun kolaboratif. Dataset dapat diakses dan diunduh melalui tautan berikut: Movie Recommendation System Kaggle Dataset.

Berdasarkan pemuatan dan inspeksi awal dataset menggunakan kode Python yang telah disiapkan, diperoleh informasi kuantitatif sebagai berikut:

- Jumlah data film unik (movies.movieId.unique()): 62.423 film.

- Jumlah total data penilaian film (len(ratings)): 25.000.095 rating.

- Jumlah pengguna unik yang memberikan penilaian (ratings.userId.unique()): 162.541 pengguna.

Dataset ini terdiri dari dua file utama yang digunakan dalam analisis, yaitu movies.csv dan ratings.csv.

**Variabel pada Dataset movies.csv**

File movies.csv berisi informasi detail mengenai setiap film.

<img width="134" alt="image" src="https://github.com/user-attachments/assets/6277310b-b65a-484f-8921-3372a6edac7b" />

Output dari movies.info() menunjukkan:

<img width="256" alt="image" src="https://github.com/user-attachments/assets/d44b17aa-4810-462d-a3ce-5f8b524eb2e1" />

Dari output di atas, diketahui bahwa file ini memiliki 62.423 entri dan 3 kolom, tanpa ada nilai yang hilang (non-null).

Variabel-variabel pada movies.csv adalah sebagai berikut:

- movieId: Merupakan ID unik yang merepresentasikan setiap film. Tipe data: int64. Terdapat 62.423 ID film unik.
  
- title: Merupakan judul dari film, seringkali menyertakan tahun rilis dalam tanda kurung. Tipe data: object (string). Terdapat 62.320 judul film unik.
  
- genres: Merupakan genre atau beberapa genre yang diklasifikasikan untuk film tersebut, dipisahkan oleh karakter |. Tipe data: object (string). Terdapat 1.639 kombinasi genre unik.

**Variabel pada Dataset ratings.csv**

File ratings.csv berisi informasi mengenai rating yang diberikan oleh pengguna terhadap film. Kolom timestamp pada dataset ini tidak digunakan dalam analisis model dan telah dihapus pada tahap awal.

<img width="102" alt="image" src="https://github.com/user-attachments/assets/3c735fee-68e7-4713-8c04-bf40f74455f6" />

Output dari ratings.info()

<img width="299" alt="image" src="https://github.com/user-attachments/assets/23f65206-234e-4c11-ac7b-dda4e0f1dc69" />

File ini memiliki 25.000.095 entri rating dan 3 kolom relevan setelah penghapusan timestamp, tanpa ada nilai yang hilang.

Variabel-variabel pada ratings.csv (setelah modifikasi) adalah sebagai berikut:

- userId: Merupakan ID unik yang merepresentasikan setiap pengguna. Tipe data: int64.

- movieId: Merupakan ID unik film yang dirating. Tipe data: int64.

- rating: Merupakan nilai rating yang diberikan oleh pengguna untuk film tertentu. Skala rating berkisar antara 0.5 hingga 5.0, dengan interval 0.5. Tipe data: float64.

Statistik deskriptif untuk data rating (ratings.describe()):

<img width="287" alt="image" src="https://github.com/user-attachments/assets/9369a6b4-aa63-49af-81e2-7668fc56b8f1" />

Dari statistik ini, terlihat bahwa rata-rata rating yang diberikan adalah 3.53. Rating minimum adalah 0.5 dan maksimum adalah 5.0.

**Eksplorasi Data Awal (EDA) - Visualisasi Genre**

Untuk mendapatkan pemahaman lebih lanjut mengenai distribusi genre film dalam dataset, dilakukan visualisasi untuk menampilkan 20 kombinasi genre dengan jumlah film terbanyak.

Berikut adalah kode yang digunakan untuk visualisasi:

<img width="708" alt="image" src="https://github.com/user-attachments/assets/44f66225-8bdb-4708-bad4-fd2ef7cd9120" />

<img width="949" alt="image" src="https://github.com/user-attachments/assets/67c31b76-12ad-465e-b07e-590c46c480c9" />

**Insight dari Visualisasi Genre:**

Visualisasi bar plot di atas menunjukkan distribusi frekuensi dari 20 kombinasi genre yang paling sering muncul dalam dataset movies.csv. Dari plot tersebut, dapat ditarik beberapa insight:

- Genre tunggal seperti "Drama" dan "Comedy" memiliki jumlah film yang sangat signifikan, mendominasi daftar teratas. Ini mengindikasikan bahwa sebagian besar film dalam dataset dikategorikan setidaknya sebagai Drama atau Komedi.
  
- Kombinasi genre seperti "Drama|Romance", "Comedy|Romance", atau "Comedy|Drama|Romance" juga cukup populer, menunjukkan adanya banyak film yang mencakup beberapa kategori genre sekaligus.

- Genre "Documentary", "Action", dan genre spesifik lainnya juga muncul dalam 20 besar, meskipun dengan frekuensi yang lebih rendah dibandingkan Drama atau Comedy murni. Pemahaman mengenai distribusi genre ini penting karena genre merupakan salah satu fitur utama yang akan digunakan dalam pendekatan Content-Based Filtering. Genre yang paling umum mungkin lebih sering muncul dalam rekomendasi jika tidak ada penanganan khusus untuk diversifikasi.

## Data Preparation

Tahap data preparation merupakan proses penting sebelum membangun model machine learning, termasuk sistem rekomendasi. Dalam studi kasus ini, data perlu disiapkan agar sesuai dengan kebutuhan dua pendekatan yang digunakan, yaitu content-based filtering dan collaborative filtering. Masing-masing pendekatan memiliki karakteristik dan kebutuhan data yang berbeda, sehingga proses persiapan dilakukan secara terpisah untuk memastikan setiap model dapat bekerja secara optimal.

Secara umum, langkah-langkah awal berikut dilakukan sebelum masuk ke persiapan spesifik per pendekatan:

- Penghapusan data film dengan genre kosong: Baris film yang memiliki nilai genres = (no genres listed) dihapus karena tidak memiliki informasi yang berguna untuk content-based filtering. Langkah ini dilakukan dengan perintah:

<img width="429" alt="image" src="https://github.com/user-attachments/assets/3c76a117-b682-4f1f-9bec-b4ed1b7f3a55" />

- Penghapusan kolom yang tidak relevan: Kolom timestamp pada dataset ratings dihapus karena tidak dibutuhkan dalam proses pemodelan, baik untuk content-based maupun collaborative filtering. Langkah ini dilakukan dengan:

<img width="416" alt="image" src="https://github.com/user-attachments/assets/c3a05e25-526b-4802-976b-57e316c089e3" />

Selanjutnya, bagian ini akan menguraikan tahapan-tahapan data preparation untuk masing-masing pendekatan secara terstruktur.

### Preparation Data Content-Based Filtering

- **Menggabungkan data movies dengan ratings:** Langkah awal adalah menggabungkan DataFrame movies dengan data ratings (disalin ke all_movies_rate) berdasarkan kolom movieId. Penggabungan ini dilakukan menggunakan pd.merge() dengan metode how='left', menghasilkan DataFrame all_movies. Ini memastikan semua film dari dataset movies tetap ada, dan informasi rating ditambahkan jika tersedia.

- **Membuat dataset film unik untuk fitur konten (preparation):** Untuk keperluan Content-Based Filtering, kita memerlukan daftar film unik beserta metadata-nya. DataFrame preparation dibuat dengan mengambil DataFrame all_movies (hasil merge) dan menghapus baris duplikat berdasarkan movieId menggunakan all_movies.drop_duplicates('movieId'). Ini memastikan setiap film hanya direpresentasikan satu kali. Meskipun pada tahap selanjutnya ada penanganan NaN untuk fitur teks, preparation sendiri mengambil data dari all_movies yang mungkin masih mengandung NaN di kolom userId atau rating untuk film tanpa rating (namun kolom title dan genres berasal dari movies.csv dan akan ditangani kemudian jika missing).

- **Sampling data film unik:** Untuk efisiensi komputasi pada tahap pengembangan, dilakukan pengambilan sampel dari DataFrame preparation. Data film unik diacak terlebih dahulu (preparation.sample(frac=1, random_state=42)), kemudian diambil 10.000 data film pertama (preparation[:10000]). Setelah sampling, indeks DataFrame di-reset menggunakan .reset_index(drop=True) untuk menyusun ulang indeks secara berurutan. Sampel ini kemudian disusun kembali menjadi DataFrame baru movies_new (kemudian di-assign ke variabel data) yang berisi kolom id (dari movieId), title, dan genre.

- **Penanganan nilai hilang (NaN) pada kolom title dan genre saat penggabungan fitur:** Meskipun preparation dibuat sebelum dropna() pada all_movies, pada saat pembuatan fitur gabungan untuk TF-IDF (pada DataFrame data), potensi nilai NaN pada kolom title atau genre ditangani. Kode data['combined'] = (data['title'].fillna('') + ' ' + data['genre'].fillna('')) (meskipun kolom combined ini tidak secara langsung digunakan untuk TF-IDF akhir di kode yang diberikan) menunjukkan strategi mengisi NaN dengan string kosong. Untuk kolom cleaned yang menjadi input TF-IDF, operasi string seperti .str.lower() pada title dan genre akan secara inheren menangani NaN dengan tidak error atau mengubahnya sesuai perilaku metode string pandas (biasanya NaN tetap NaN tapi tidak menghentikan proses pada kolom lain, dan TF-IDF akan mengabaikannya atau TfidfVectorizer bisa memiliki parameter untuk ini).

- **Pembersihan dan Pembobotan Fitur Teks (title dan genre):**

  - **Pembersihan Genre:** Kolom genre diproses terlebih dahulu: dikonversi ke huruf kecil dan karakter | (pipe) yang memisahkan antar genre diganti dengan spasi. Hasilnya disimpan di kolom data['genre_cleaned']. Ini bertujuan agar setiap genre dapat dikenali sebagai token individual oleh TF-IDF.

  - **Penggabungan dan Pembobotan Fitur:** Fitur teks utama yang akan digunakan (data['cleaned']) dibuat dengan menggabungkan kolom title (yang dikonversi ke huruf kecil) dengan genre_cleaned. Pada tahap ini, genre_cleaned diulang sebanyak tiga kali ((data['genre_cleaned'] + ' ') * 3). Ini merupakan teknik weighting sederhana untuk memberikan bobot atau penekanan yang lebih besar pada informasi genre dibandingkan judul dalam menentukan kemiripan konten.

  - Meskipun fungsi clean_text (yang melakukan penghapusan karakter non-alfanumerik dan konversi ke huruf kecil) didefinisikan dalam notebook, kolom cleaned yang akhirnya menjadi input untuk TfidfVectorizer secara spesifik dibentuk melalui proses di atas (konversi ke huruf kecil untuk title dan genre, penggantian | pada genre, dan pembobotan genre).

- **Membuat vektor fitur menggunakan TF-IDF:** Kolom data['cleaned'] yang berisi gabungan teks dari judul dan genre (dengan genre yang telah dibersihkan dan diberi bobot lebih) kemudian diolah menjadi representasi vektor numerik. Ini dilakukan menggunakan TfidfVectorizer, dengan mengabaikan stop words bahasa Inggris. Matriks TF-IDF (tfidf_matrix) yang dihasilkan merepresentasikan setiap film sebagai vektor fitur berdasarkan kekhasan kata-kata dalam deskripsi kontennya.

### Preparation Data Collaborative Filtering

- **Pengambilan sampel acak sebanyak 10.000 data rating:** Pengambilan data dilakukan secara acak dengan menetapkan random_state agar hasilnya konsisten. Hal ini bertujuan membatasi jumlah data agar proses pelatihan model neural network lebih efisien dan tidak memakan sumber daya komputasi yang terlalu besar.

- **Label encoding untuk userId dan movieId:** Karena model deep learning tidak dapat memproses data string, dilakukan label encoding untuk mengubah userId dan movieId menjadi nilai numerik. Ini memungkinkan model mengenali entitas pengguna dan film secara matematis.

- **Mapping kembali ID hasil encoding ke ID asli:** Setelah proses encoding, dibuat mapping dari ID numerik kembali ke ID aslinya. Hal ini penting untuk tahap inference, agar hasil rekomendasi dapat dikonversi kembali ke bentuk asli seperti movieId dan title film yang dikenali oleh pengguna.

- **Mengonversi kolom rating ke tipe data float:** Tipe data rating dikonversi ke float untuk memastikan kesesuaian dengan format input yang diharapkan model neural network. Hal ini juga memastikan operasi matematis berjalan dengan presisi selama proses pelatihan.

- **Normalisasi rating dan split data:** Rating dinormalisasi ke dalam skala 0–1 untuk menjaga kestabilan proses pembelajaran model serta menghindari bias karena perbedaan skala. Data kemudian dibagi menjadi 80% data latih dan 20% data validasi guna mengevaluasi performa model secara objektif dan mengurangi risiko overfitting.

## Modeling

Pada tahap ini, dilakukan pembangunan dan evaluasi dua model sistem rekomendasi yang bertujuan untuk membantu pengguna menemukan film sesuai dengan preferensi mereka. Model dikembangkan berdasarkan dua pendekatan utama, yaitu Content-Based Filtering dan Collaborative Filtering berbasis Neural Network.

Pendekatan pertama fokus pada konten film itu sendiri, seperti judul dan genre, serta memanfaatkan kemiripan antar item untuk menghasilkan rekomendasi. Sementara pendekatan kedua memanfaatkan pola interaksi antara pengguna dan film melalui data historis rating, dan menggunakan pembelajaran mesin untuk memprediksi ketertarikan pengguna terhadap film yang belum mereka tonton.

Berikut adalah penjelasan masing-masing pendekatan:

### Content-Based Filtering

Pendekatan Content-Based Filtering merekomendasikan item (film) berdasarkan kemiripan fitur antar item itu sendiri. Dalam studi kasus ini, fitur yang digunakan adalah title dan genre film yang telah diproses pada tahap Data Preparation menggunakan TF-IDF Vectorization, dan kemiripannya dihitung menggunakan cosine similarity. Matriks kemiripan kosinus (cosine_sim_df) yang dihasilkan pada tahap tersebut menjadi dasar untuk menghasilkan rekomendasi.

**Mekanisme Pemberian Rekomendasi:**

Fungsi movie_recommendations digunakan untuk menghasilkan daftar film yang direkomendasikan. Prosesnya adalah sebagai berikut:

Untuk mendapatkan rekomendasi bagi sebuah film, sistem akan:

1. Input Judul Film: Sistem menerima judul_film sebagai input, yaitu film yang ingin dicari rekomendasinya oleh pengguna.

2. Validasi Judul: Dilakukan pengecekan apakah judul_film yang dimasukkan terdapat dalam matriks kemiripan cosine_sim_df. Jika tidak ditemukan, sistem akan memberikan pesan bahwa judul tidak ditemukan.

3. Pengambilan Skor Kemiripan: Jika judul ditemukan, sistem akan mengambil seri skor kemiripan yang bersesuaian dengan judul_film tersebut dari cosine_sim_df. Seri ini berisi skor kemiripan film input dengan semua film lain dalam dataset.

4. Pengurutan Skor: Skor kemiripan tersebut diurutkan dari nilai tertinggi ke terendah untuk mengidentifikasi film-film yang paling mirip.

5. Eksklusi Film Input: Film input itu sendiri (yang memiliki skor kemiripan 1.0 dengan dirinya) akan dihapus dari daftar hasil pengurutan agar tidak muncul dalam rekomendasinya sendiri.

6. Pemilihan Top-K Judul: Sejumlah k judul film teratas (misalnya, k=10) diambil dari daftar yang telah diurutkan dan disaring.
Pengambilan Detail Film: Informasi detail (seperti title dan genre) untuk k judul film teratas tersebut diambil dari DataFrame data (yang berisi daftar film unik beserta metadatanya).

7. Output Rekomendasi: DataFrame berisi k film yang direkomendasikan (lengkap dengan judul dan genrenya) akan ditampilkan kepada pengguna.

**Top-N Rekomendasi Content-Based Filtering:**

Berikut adalah  output rekomendasi Top-N yang dihasilkan oleh fungsi movie_recommendations untuk film "Johnny English Strikes Again (2018)":

| No | Judul Film                    | Genre                                             | Relevan ✅ |
|----|-------------------------------|---------------------------------------------------|------------|
| 1  | Twigson (2009)                | Adventure, Children, Comedy                       | ✅         |
| 2  | Spy Kids (2001)               | Action, Adventure, Children, Comedy               | ✅         |
| 3  | Inspector Gadget 2 (2003)     | Action, Adventure, Children, Comedy               | ✅         |
| 4  | Big Red (1962)                | Action, Adventure, Children, Drama                | ✅         |
| 5  | Goonies, The (1985)           | Action, Adventure, Children, Comedy, Fantasy      | ✅         |
| 6  | Bejewelled (1991)             | Action, Adventure, Children                       | ✅         |
| 7  | Camp Nowhere (1994)           | Adventure, Children, Comedy                       | ✅         |
| 8  | Incredibles 2 (2018)          | Action, Adventure, Animation, Children            | ✅         |
| 9  | Dadnapped (2009)              | Action, Adventure, Children, Comedy               | ✅         |
| 10 | Cop Dog (2008)                | Action, Adventure, Children                       | ✅         |

- Kelebihan:

  - Tidak bergantung pada data dari pengguna lain.

  - Tetap dapat memberikan rekomendasi meskipun pengguna baru (cold-start user) jika film acuannya jelas.

  - Dapat merekomendasikan item yang spesifik dan kurang populer jika memiliki kemiripan konten yang tinggi.

- Kekurangan:

  - Terbatas pada kemiripan konten; tidak bisa merekomendasikan film yang secara konten berbeda namun mungkin disukai pengguna (serendipity rendah).

  - Memerlukan fitur konten yang baik dan deskriptif. Jika fitur konten buruk, rekomendasi juga akan buruk.

  - Cenderung merekomendasikan item yang terlalu mirip (overspecialization).

### Collaborative Filtering

Pendekatan Collaborative Filtering yang digunakan di sini berbasis neural network. Model ini fokus pada pola interaksi antara pengguna dan film melalui data rating historis. Model memanfaatkan embedding layer untuk mengubah userId dan movieId menjadi representasi vektor padat (embedding) dalam ruang laten.

Selama pelatihan, model belajar memprediksi rating yang mungkin diberikan seorang pengguna terhadap suatu film. Setelah model terlatih, sistem dapat menghitung prediksi rating untuk semua film yang belum ditonton pengguna, lalu memilih Top-N film dengan prediksi tertinggi sebagai rekomendasi.

**Mekanisme Pemberian Rekomendasi:**

Setelah model dilatih, proses untuk menghasilkan rekomendasi bagi seorang pengguna (userId) adalah sebagai berikut, sesuai dengan implementasi kode:

1. Pemilihan Pengguna: Seorang userId dipilih sebagai target untuk diberikan rekomendasi (dalam kode contoh, userId dipilih secara acak dari data rating yang telah disampling).

2. Identifikasi Film yang Belum Ditonton: Sistem mengidentifikasi daftar film dari movie_df (DataFrame yang berisi metadata 10.000 film sampel) yang belum pernah ditonton atau diberi rating oleh userId tersebut. Ini dilakukan dengan membandingkan daftar semua film dengan film-film yang ada dalam catatan rating pengguna (movies_watch_by_user).

3. Filter Film yang Dikenal Model: Dari daftar film yang belum ditonton, sistem menyaringnya lebih lanjut untuk hanya menyertakan film-film yang ID-nya memiliki representasi encoded yang dikenal oleh model Collaborative Filtering (yaitu, movieId yang ada dalam mapping movie_to_movie_encoded). Ini memastikan model hanya membuat prediksi untuk item yang pernah "dilihat" atau memiliki embedding selama pelatihan.

4. Encoding Input untuk Prediksi: userId yang dipilih dan daftar movieId dari film yang belum ditonton (dan dikenal model) diubah ke format encoded numerik menggunakan mapping user_to_user_encoded dan movie_to_movie_encoded.

5. Persiapan Batch Data Prediksi: Pasangan [user_id_encoded, movie_id_encoded] dibentuk untuk setiap film yang akan diprediksi ratingnya oleh pengguna tersebut. Ini disusun menjadi sebuah array (user_movie_array) yang siap menjadi input bagi model.

6. Prediksi Rating: Model neural network (model) yang telah dilatih digunakan untuk memprediksi skor rating untuk setiap pasangan [user_id_encoded, movie_id_encoded] dalam user_movie_array. Output prediksi ini biasanya berupa nilai antara 0 dan 1 (hasil dari fungsi aktivasi sigmoid dan normalisasi data rating target selama persiapan data).

7. Pengurutan dan Pemilihan Top-N: Hasil prediksi rating kemudian diurutkan dari yang tertinggi ke terendah. Indeks dari k (misalnya, 10) film dengan prediksi rating tertinggi diambil.

8. Decoding Output: movieId yang masih dalam format encoded dari film-film yang direkomendasikan tersebut diubah kembali ke ID film aslinya menggunakan mapping movie_encoded_to_movie.

9. Penyajian Rekomendasi: Detail film (seperti title dan genre) untuk k film teratas tersebut diambil dari movie_df (menggunakan ID film asli) dan ditampilkan sebagai rekomendasi untuk userId tersebut. Untuk memberikan konteks tambahan tentang selera pengguna, beberapa film yang sebelumnya telah diberi rating tinggi oleh pengguna juga dapat ditampilkan (diambil dari movies_watch_by_user).

**Top-N Rekomendasi Collaborative Filtering:**

**Movies with High Ratings from User `74429`**

| Judul Film                    | Genre                         |
|------------------------------|-------------------------------|
| Apt Pupil (1998)             | Drama, Thriller               |
| Mirror Mirror (2012)         | Adventure, Comedy, Fantasy    |
| His Girl Friday (1940)       | Comedy, Romance               |
| Dream With the Fishes (1997) | Drama                        |

---

**Top 10 Movie Recommendations**

| No. | Judul Film                                | Genre                                       |
|-----|-------------------------------------------|---------------------------------------------|
| 1   | Wallace & Gromit: A Close Shave (1995)    | Animation, Children, Comedy                 |
| 2   | Jurassic World: Fallen Kingdom (2018)     | Action, Adventure, Drama, Sci-Fi, Thriller  |
| 3   | Somewhere in Time (1980)                  | Drama, Romance                              |
| 4   | Beginners (2010)                          | Drama                                       |
| 5   | Dial M for Murder (1954)                  | Crime, Mystery, Thriller                    |
| 6   | Third Man, The (1949)                     | Film-Noir, Mystery, Thriller                |
| 7   | Born Yesterday (1950)                     | Comedy                                      |
| 8   | Barry Lyndon (1975)                       | Drama, Romance, War                         |
| 9   | Ulee's Gold (1997)                        | Drama                                       |
| 10  | M (1931)                                  | Crime, Film-Noir, Thriller                  |


- Kelebihan:

  - Memanfaatkan pola kolektif antar pengguna, sehingga bisa memberikan rekomendasi yang lebih personal dan beragam (serendipity lebih tinggi).

  - Dapat menemukan hubungan "tersembunyi" antara pengguna dan film yang tidak bisa ditangkap oleh analisis konten saja.

  - Tidak memerlukan fitur konten item secara eksplisit.

- Kekurangan:

  - Membutuhkan jumlah data interaksi (rating) yang signifikan untuk bekerja optimal.

  - Sulit memberikan rekomendasi kepada pengguna baru yang belum memiliki histori rating (cold-start user problem).

  - Sulit merekomendasikan item baru yang belum memiliki interaksi (cold-start item problem).

## Evaluation

Dalam proyek ini, digunakan dua pendekatan utama untuk sistem rekomendasi, yaitu content-based filtering dan collaborative filtering. Masing-masing pendekatan dievaluasi menggunakan metrik yang sesuai dengan karakteristik metode dan tujuan bisnis yang ingin dicapai.

### Metrik Evaluasi Content-Based Filtering : Recall@K
Untuk mengevaluasi performa model content-based filtering, digunakan metrik Recall@K. Metrik ini mengukur seberapa banyak item relevan yang berhasil direkomendasikan kepada pengguna dalam daftar rekomendasi sebanyak K item.Secara matematis, Recall@K dirumuskan sebagai:

$$
\text{Recall@K} = \frac{\text{Jumlah item relevan dalam top-K}}{\text{Total item relevan untuk pengguna}}
$$

Metrik ini bekerja dengan cara menghitung proporsi item yang benar-benar relevan bagi pengguna yang muncul dalam daftar rekomendasi sebanyak K item. Semakin tinggi nilai Recall@K, semakin baik sistem dalam menemukan item yang sesuai dengan preferensi pengguna. 

$$
Recall@10 = \frac{10}{10} = 1.0
$$

**Hasil Evaluasi Content-Based Filtering:** 

Berdasarkan hasil evaluasi, sistem rekomendasi berhasil memberikan 10 item teratas (top-10 recommendations) yang seluruhnya relevan terhadap film input pengguna, yaitu Johnny English Strikes Again (2018). Dengan demikian, diperoleh nilai Recall@10 sebesar 1.0, yang menunjukkan bahwa semua item relevan berhasil direkomendasikan dalam daftar top-10. Ini menandakan bahwa model content-based filtering bekerja sangat baik dalam menangkap kesamaan konten berdasarkan preferensi pengguna.

### Metrik Evaluasi Collaborative Filtering : RMSE (Root Mean Squared Error)

Untuk pendekatan collaborative filtering, digunakan metrik Root Mean Square Error (RMSE). RMSE mengukur deviasi rata-rata antara rating yang diprediksi sistem dan rating aktual dari pengguna. Rumus RMSE dituliskan sebagai:

$$
\text{RMSE} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (r_i - \hat{r}_i)^2}
$$

di mana 𝑟𝑖 adalah rating aktual dan 𝑟^𝑖 adalah rating prediksi. Metrik ini bekerja dengan mengukur selisih kuadrat antara prediksi dan nilai sebenarnya, kemudian mengambil akar dari rata-ratanya. Semakin kecil nilai RMSE, semakin akurat prediksi yang dihasilkan oleh sistem.

Hasil: 

<img width="456" alt="image" src="https://github.com/user-attachments/assets/ce1b8e80-695a-4aae-ab93-8f30347b113e" />

Berdasarkan grafik di atas, nilai Root Mean Squared Error (RMSE) pada data latih menunjukkan penurunan yang konsisten seiring bertambahnya jumlah epoch. Hal ini menandakan bahwa model berhasil mempelajari pola preferensi pengguna terhadap film secara efektif selama proses pelatihan.

Sementara itu, nilai RMSE pada data uji berada di kisaran 0.265 dan cenderung stabil sepanjang pelatihan, tanpa menunjukkan peningkatan berarti. Ini mengindikasikan bahwa model tidak mengalami overfitting, karena performanya pada data uji tetap terjaga meskipun error pada data latih terus menurun.

Secara keseluruhan, performa model collaborative filtering dalam merekomendasikan film dapat dikatakan cukup baik, dengan tingkat kesalahan prediksi yang relatif rendah dan generalisasi yang stabil terhadap data yang belum pernah dilihat sebelumnya.

### Kesimpulan

Dalam proyek ini, dua pendekatan telah digunakan untuk membangun sistem rekomendasi film:

1. Content-Based Filtering berhasil memberikan rekomendasi film yang relevan berdasarkan kemiripan konten seperti genre dan judul. Evaluasi kuantitatif menggunakan metrik Recall@10 menunjukkan performa yang sangat baik, dengan nilai Recall@10 sebesar 1.0, yang berarti semua item relevan berhasil masuk dalam daftar rekomendasi. Pendekatan ini efektif dalam menjaga relevansi rekomendasi dengan histori tontonan pengguna.

2. Collaborative Filtering berbasis Neural Network berhasil memberikan prediksi rating dengan cukup akurat. Dengan nilai RMSE sekitar 0.265, model menunjukkan performa yang stabil dan tidak mengalami overfitting, yang berarti model mampu memprediksi preferensi pengguna baru berdasarkan interaksi pengguna lain.

Secara keseluruhan, kombinasi kedua pendekatan ini mampu meningkatkan kualitas sistem rekomendasi yang dikembangkan. Pendekatan content-based menjaga relevansi berdasarkan histori pengguna, sementara collaborative filtering memperluas rekomendasi dengan mengenalkan film-film baru yang belum dikenal oleh pengguna. Dengan demikian, sistem ini dapat memberikan pengalaman yang lebih personal, bervariasi, dan bernilai tambah bagi pengguna dalam menemukan film yang sesuai dengan selera mereka.

## Referensi
[1] Schwartz, B. (2004). The Paradox of Choice: Why More Is Less. Harper Perennial.
[2] Jannach, D., Zanker, M., Felfernig, A., & Friedrich, G. (2010). Recommender Systems: An Introduction. Cambridge University Press. (Catatan: Buku ini secara umum membahas dampak dan implementasi)
[3] Resnick, P., & Varian, H. R. (1997). Recommender systems. Communications of the ACM, 40(3), 56–58. (Artikel klasik yang mengenalkan konsep)
[4] Adomavicius, G., & Tuzhilin, A. (2005). Toward the Next Generation of Recommender Systems: A Survey of the State-of-the-Art and Possible Extensions. IEEE Transactions on Knowledge and Data Engineering, 17(6), 734–749.

**---Ini adalah bagian akhir laporan---**
