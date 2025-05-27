# Laporan Proyek Machine Learning - Rangga Julian Syaputra

## Domain Proyek

### Latar Belakang

Di era digital saat ini, pengguna menghadapi tantangan dalam memilih film yang sesuai dengan preferensi mereka akibat banyaknya konten film yang tersedia di berbagai platform streaming. Dengan ribuan film yang dapat diakses, sangat tidak praktis bagi pengguna untuk mencari dan memilih film secara manual. Oleh karena itu, diperlukan sistem rekomendasi film yang dapat memberikan saran personal berdasarkan perilaku dan preferensi pengguna.

Sistem rekomendasi merupakan komponen penting dalam meningkatkan pengalaman pengguna pada platform hiburan dengan membantu mereka menemukan konten yang relevan secara cepat dan tepat. Proyek ini mengembangkan sistem rekomendasi hibrida yang menggabungkan metode Collaborative Filtering dan Content-Based Filtering, yang memanfaatkan interaksi pengguna dengan film serta atribut film itu sendiri untuk menghasilkan rekomendasi yang lebih akurat dan beragam.

### Mengapa Masalah Ini Perlu Diselesaikan

Volume besar film yang tersedia dapat menyebabkan kebingungan dan kelelahan dalam pengambilan keputusan bagi pengguna. Tanpa rekomendasi yang personal, pengguna berpotensi melewatkan film yang sesuai dengan minat mereka, sehingga menurunkan tingkat kepuasan dan loyalitas terhadap platform.

Penyelesaian masalah ini memberikan manfaat ganda: pengguna dapat menemukan film yang cocok dengan lebih mudah, sementara penyedia platform dapat meningkatkan waktu tontonan dan pendapatan. Selain itu, pemahaman preferensi pengguna melalui model berbasis data memungkinkan pengembangan algoritma rekomendasi yang terus ditingkatkan.

### Hasil Riset dan Referensi Terkait

Metode sistem rekomendasi telah banyak diteliti dan diterapkan di berbagai bidang. Collaborative filtering mengandalkan pola interaksi pengguna untuk memprediksi preferensi (Su & Khoshgoftaar, 2009), sedangkan content-based filtering menggunakan fitur dari item (seperti genre dan deskripsi film) untuk merekomendasikan item serupa (Lops, de Gemmis, & Semeraro, 2011).

Sistem hibrida mengkombinasikan kedua metode tersebut guna mengatasi keterbatasan masing-masing, seperti masalah cold start dan sparsity pada collaborative filtering, serta keterbatasan variasi rekomendasi pada content-based filtering (Burke, 2002). Perkembangan terbaru menggunakan deep learning untuk memodelkan hubungan kompleks antara pengguna dan item dalam ruang laten (He et al., 2017).

### Referensi

Su, X., & Khoshgoftaar, T. M. (2009). A survey of collaborative filtering techniques. Advances in Artificial Intelligence, 2009, Article ID 421425. https://doi.org/10.1155/2009/421425

Lops, P., de Gemmis, M., & Semeraro, G. (2011). Content-based Recommender Systems: State of the Art and Trends. Recommender Systems Handbook, 73–105. https://doi.org/10.1007/978-0-387-85820-3_3

Burke, R. (2002). Hybrid Recommender Systems: Survey and Experiments. User Modeling and User-Adapted Interaction, 12(4), 331–370. https://doi.org/10.1023/A:1021240730564

He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T.-S. (2017). Neural Collaborative Filtering. Proceedings of the 26th International Conference on World Wide Web, 173–182. https://doi.org/10.1145/3038912.3052569

## Business Understanding

### Problem Statements

Berdasarkan latar belakang di atas, berikut adalah beberapa permasalahan yang perlu diselesaikan dalam proyek ini:

1. Keterbatasan dalam Menemukan Film yang Sesuai dengan Preferensi Pengguna
   Pengguna sering kesulitan menemukan film yang sesuai dengan selera dan preferensi mereka di antara ribuan pilihan yang tersedia.

2. Kurangnya Personalisasi Rekomendasi yang Akurat
   Sistem rekomendasi film yang ada belum mampu memberikan rekomendasi yang cukup relevan dan personal bagi setiap pengguna.

3. Dampak Negatif dari Rekomendasi yang Tidak Tepat
   Rekomendasi yang tidak sesuai dapat mengurangi kepuasan pengguna dan menurunkan keterlibatan mereka dalam menggunakan platform.

### Goals

Tujuan dari proyek ini adalah:

1. Mengembangkan sistem rekomendasi film yang mampu memberikan rekomendasi personal berdasarkan preferensi pengguna.

2. Meningkatkan akurasi rekomendasi melalui penerapan metode Content-Based Filtering dan Collaborative Filtering.

3. Mengoptimalkan pengalaman pengguna dengan menampilkan rekomendasi yang relevan, sehingga meningkatkan kepuasan dan interaksi pengguna.

### Solution Statements

Untuk mencapai tujuan di atas, berikut adalah solusi yang akan diimplementasikan:

**1. Mengimplementasikan Content-Based Filtering**
Menggunakan fitur film seperti genre dan metadata lain untuk merekomendasikan film serupa yang sesuai dengan film favorit pengguna, dengan metrik evaluasi menggunakan Precision@10.

**2. Mengembangkan Collaborative Filtering dengan Neural Collaborative Filtering (NCF)**
Menggunakan model deep learning NCF untuk mempelajari preferensi pengguna berdasarkan interaksi pengguna-film dan menghasilkan prediksi rating yang lebih akurat, dievaluasi menggunakan metrik RMSE.

**2. Penggabungan Model dan Pengujian Kinerja**
Melakukan evaluasi dan perbandingan performa kedua metode untuk memilih solusi terbaik yang dapat diterapkan secara efektif. Peningkatan hasil evaluasi menjadi tolok ukur keberhasilan proyek.

## Data Understanding

Pada proyek ini, saya memanfaatkan dataset MovieLens Small yang dibuat oleh GroupLens Research. Dataset ini terdiri dari 100.836 data rating dan tag yang diberikan oleh 610 pengguna terhadap 9.742 film. Dataset tersebut dapat diunduh melalui [situs resmi GroupLens](https://grouplens.org/datasets/movielens/latest/).

Dataset MovieLens Small terdiri dari beberapa file, namun dalam proyek ini saya memfokuskan pada empat file utama berikut:

### Variabel-variabel pada dataset MovieLens:

1.  **ratings.csv**: Berisi data rating yang diberikan oleh pengguna terhadap film, meliputi:
    • userId: Identifikasi unik untuk setiap pengguna
    • movieId: Identifikasi unik untuk setiap film
    • rating: Nilai rating yang diberikan dengan rentang 0.5 hingga 5.0
    • timestamp: Waktu pemberian rating dalam format unix timestamp
2.  **movies.csv**: Berisi informasi dasar mengenai film, yang mencakup:
    • movieId: Identifikasi unik untuk setiap film
    • title: Judul film beserta tahun rilisnya
    • genres: Genre film yang dipisahkan dengan tanda "|"
3.  **tags.csv**: Berisi data tag atau label yang diberikan oleh pengguna terhadap film, terdiri dari:
    • userId: Identifikasi unik untuk setiap pengguna
    • movieId: Identifikasi unik untuk setiap film
    • tag: Tag berupa teks yang diberikan oleh pengguna
    • timestamp: Waktu pemberian tag dalam format unix timestamp
4.  **links.csv**: Berisi tautan ke sumber data eksternal terkait film, yaitu:
    • movieId: Identifikasi unik untuk setiap film
    • imdbId: ID film di database IMDb (Internet Movie Database)
    • tmdbId: ID film di database TMDb (The Movie Database)

### Exploratory Data Analysis

Berikut adalah beberapa visualisasi eksploratif yang digunakan untuk menganalisis dataset film (seperti MovieLens), termasuk genre, popularitas, dan perilaku pengguna dalam memberikan rating:

#### 1. Statistik Dasar Dataset

Dataset ratings terdiri dari 100.836 baris dan 4 kolom (userId, movieId, rating, timestamp). Sedangkan dataset movies memiliki 9.742 baris dengan 3 kolom (movieId, title, genres). Berdasarkan analisis statistik deskriptif, rata-rata rating yang diberikan adalah 3,5 dengan standar deviasi sebesar 1,04, yang mengindikasikan bahwa sebagian besar rating cenderung bernilai positif.

#### 2. Heatmap Korelasi Jumlah Rating vs Rata-rata Rating

![heatmap_correlation](https://github.com/user-attachments/assets/d1788302-7bde-4202-97c2-f461e8fae0f7)

Visualisasi ini menunjukkan hubungan antara jumlah rating dan rata-rata rating per film.
Insight: Nilai korelasi yang sangat lemah (0.13) menunjukkan bahwa film yang banyak dirating belum tentu memiliki nilai rating tinggi — popularitas tidak selalu berbanding lurus dengan kualitas.

#### 3. Boxplot Distribusi Rating per Genre

![boxplot_rating_per_genre](https://github.com/user-attachments/assets/47b0a429-4354-4d3e-9911-93e69f66ef19)

Boxplot ini menunjukkan sebaran rating berdasarkan genre utama.
Insight: Genre seperti Documentary dan Animation cenderung memiliki rating lebih tinggi, sedangkan genre seperti Horror memiliki distribusi yang lebih menyebar dan banyak outlier.

#### 4. Wordcloud Genre Film

![wordcloud_genre](https://github.com/user-attachments/assets/81f3bed0-da9b-4a7b-b58d-ff69c7be5bdb)

Wordcloud menggambarkan frekuensi kemunculan genre dalam dataset.
Insight: Genre seperti Drama, Comedy, dan Romance adalah yang paling umum dalam data.

#### 5. Scatter Plot: Rating per User

![scatter_user_rating](https://github.com/user-attachments/assets/af4b5aa7-4769-4672-b1cb-03cbff352f70)

Plot ini menunjukkan hubungan antara jumlah film yang dirating oleh user dan rata-rata rating yang mereka berikan.
Insight: User yang memberikan rating dalam jumlah besar cenderung memberi rating yang lebih stabil/moderat, sedangkan user dengan sedikit rating cenderung ekstrem.

#### 6. Barplot: 10 Film Paling Banyak Dirating

![top10_movies_rating_count](https://github.com/user-attachments/assets/6a78aa75-94a2-4e44-83ce-1d6360b57f42)

Grafik ini menunjukkan 10 film dengan jumlah rating terbanyak.
Insight: Film klasik seperti Forrest Gump dan The Shawshank Redemption menempati peringkat teratas, mencerminkan tingkat popularitas yang sangat tinggi.

#### 7. Treemap: Genre Film Terpopuler

![treemap_genre](https://github.com/user-attachments/assets/9bc10afd-2bfd-4ead-ade6-1fcf2fb1eeb5)

Grafik ini menampilkan genre film berdasarkan tingkat popularitasnya dalam bentuk treemap, di mana ukuran setiap kotak mencerminkan jumlah film atau tingkat popularitas genre tersebut.

Insight: Genre Drama, Comedy, dan Action mendominasi tampilan ini, menandakan ketertarikan penonton yang tinggi terhadap genre-genre tersebut.

#### 8. Radar Chart: Genre Film Terpopuler

![radar_genre](https://github.com/user-attachments/assets/ce2a4766-23c2-4fd5-b6f2-dd8a6fdf8616)

Grafik radar ini memvisualisasikan popularitas berbagai genre film dalam bentuk area yang melebar ke berbagai arah sesuai skala nilai popularitas.

Insight: Drama muncul sebagai genre paling populer, disusul oleh Comedy dan Thriller. Genre seperti Animation dan Documentary memiliki nilai popularitas lebih rendah.

#### 9. Bubble Chart: Popularitas vs Kualitas Film

![bubble_rating](https://github.com/user-attachments/assets/0d9eda6a-b5b3-47d5-80bd-87f7af1c5057)

Grafik ini menggabungkan jumlah rating (sumbu X) dan rata-rata rating (sumbu Y) dari film, dengan ukuran dan warna gelembung mewakili jumlah dan kualitas ulasan.

Insight: Terlihat bahwa beberapa film memiliki rating sangat tinggi meski tidak terlalu populer, dan sebaliknya ada film populer namun dengan rating rendah—menunjukkan bahwa popularitas tidak selalu mencerminkan kualitas.

#### 10. Donut Chart: Distribusi Genre Film

![donut_genre](https://github.com/user-attachments/assets/f7f0312e-1ae6-4e74-87a2-ab46a3cc5dcc)

Grafik berbentuk donat ini menunjukkan distribusi persentase film berdasarkan genre.

Insight: Drama mendominasi dengan porsi 23.7%, diikuti oleh Comedy dan Action. Genre Horror dan Romance menempati porsi yang lebih kecil.

#### 11. Barplot: Top 15 Film Berdasarkan Rating Rata-rata (Min 100 Rating)

![lollipop_top_movies](https://github.com/user-attachments/assets/30c115dd-402a-471b-aafc-1a345ef98811)

Grafik ini menunjukkan 15 film dengan rating rata-rata tertinggi, dengan syarat minimal 100 rating agar hasil lebih representatif.

Insight: Film-film dalam grafik ini mendapatkan apresiasi tinggi dari penonton, menunjukkan kualitas konten yang konsisten dan kuat berdasarkan ulasan.

## Data Preparation

Sebelum membangun model, saya melakukan beberapa tahapan persiapan data untuk memastikan kualitas dan kesesuaian data dengan algoritma yang akan digunakan:

### 1. Filtering Data

Tahap pertama adalah memfilter data untuk menghapus film dan pengguna dengan sedikit rating (kurang dari 5 rating). Tahapan ini penting untuk mengatasi masalah sparsity dan cold-start yang umum dalam sistem rekomendasi. Dengan menghapus film dan pengguna dengan sedikit rating, model dapat fokus pada pola yang lebih kuat dan reliable dalam data.

Setelah filtering, jumlah rating berkurang dari 100,836 menjadi 90,274, menunjukkan bahwa sekitar 10% data dihapus karena tidak memenuhi kriteria minimum.

### 2. Ekstraksi Tahun dari Judul Film

Selanjutnya, saya mengekstrak tahun rilis film dari judul film menggunakan ekspresi reguler. Ekstraksi tahun dari judul film memungkinkan kita untuk menggunakan informasi temporal dalam analisis dan rekomendasi. Pengguna mungkin memiliki preferensi terhadap film dari era tertentu.

### 3. Persiapan Data untuk Content-Based Filtering

Untuk Content-Based Filtering, saya menggunakan TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengekstrak fitur dari genre film. Langkah-langkah persiapan data meliputi:

- Mengisi nilai NaN pada kolom genres dengan string kosong
- Mengubah format genre dari pipe-separated (`|`) menjadi space-separated untuk diproses oleh TF-IDF Vectorizer
- Membuat matriks TF-IDF dari genre film
- Menghitung cosine similarity antar film berdasarkan matriks TF-IDF
- Membuat mapping dari movieId ke indeks dan sebaliknya untuk mempermudah pencarian film

### 4. Persiapan Data untuk Collaborative Filtering

Untuk Collaborative Filtering, data dibagi menjadi set training (80%) dan testing (20%) menggunakan fungsi train_test_split dari scikit-learn. Kemudian, userId dan movieId dipetakan ke indeks berurutan untuk digunakan dalam model neural network. Langkah-langkah persiapan data meliputi:

- Membuat mapping dari userId dan movieId ke indeks berurutan
- Mengkonversi data rating ke format yang sesuai untuk model, yaitu pasangan (user, movie, rating)
- Membuat fungsi untuk mengubah data menjadi format TensorFlow Dataset yang efisien untuk training

## Modeling

Dalam proyek ini, saya mengimplementasikan dua pendekatan untuk sistem rekomendasi: Content-Based Filtering dan Collaborative Filtering.

### 1. Content-Based Filtering

Content-Based Filtering merekomendasikan item berdasarkan kesamaan fitur atau atribut item. Dalam konteks film, fitur yang digunakan adalah genre film.

#### Implementasi Model:

Model Content-Based Filtering yang diimplementasikan menggunakan TF-IDF Vectorizer untuk mengekstrak fitur dari genre film, dan cosine similarity untuk menghitung kesamaan antar film.

Langkah-langkah implementasi:

1. Membuat matriks TF-IDF dari genre film
2. Menghitung cosine similarity antar film
3. Membuat fungsi rekomendasi yang mengambil ID film sebagai input, mencari film-film yang paling mirip berdasarkan cosine similarity, dan mengembalikan daftar film yang direkomendasikan

Fungsi `get_recommendations_content_based` mengambil ID film sebagai input dan mengembalikan daftar film yang paling mirip berdasarkan genre. Fungsi ini bekerja dengan mencari indeks film dalam matriks cosine similarity, kemudian mengurutkan semua film berdasarkan nilai kesamaan, dan mengembalikan n film teratas (tidak termasuk film itu sendiri).

#### Hasil Rekomendasi:

Sebagai contoh, berikut adalah rekomendasi untuk film "Toy Story":

| movieId | title                                              | genres                                      |
| ------- | -------------------------------------------------- | ------------------------------------------- |
| 2294    | Antz (1998)                                        | Adventure\Animation\Children\Comedy\Fantasy |
| 3114    | Toy Story 2 (1999)                                 | Adventure\Animation\Children\Comedy\Fantasy |
| 3754    | Adventures of Rocky and Bullwinkle, The (2000)     | Adventure\Animation\Children\Comedy\Fantasy |
| 4016    | Emperor's New Groove, The (2000)                   | Adventure\Animation\Children\Comedy\Fantasy |
| 4886    | Monsters, Inc. (2001)                              | Adventure\Animation\Children\Comedy\Fantasy |
| 45074   | Wild, The (2006)                                   | Adventure\Animation\Children\Comedy\Fantasy |
| 53121   | Shrek the Third (2007)                             | Adventure\Animation\Children\Comedy\Fantasy |
| 65577   | Tale of Despereaux, The (2008)                     | Adventure\Animation\Children\Comedy\Fantasy |
| 91355   | Asterix and the Vikings (Astérix et les Viking...) | Adventure\Animation\Children\Comedy\Fantasy |
| 103755  | Turbo (2013)                                       | Adventure\Animation\Children\Comedy\Fantasy |

Dari hasil rekomendasi, terlihat bahwa model berhasil merekomendasikan film-film dengan genre yang sama dengan "Toy Story", yaitu film animasi petualangan untuk anak-anak dengan unsur komedi dan fantasi.

#### Kelebihan Content-Based Filtering:

- Tidak memerlukan data dari pengguna lain, sehingga dapat mengatasi masalah cold-start untuk item baru
- Dapat memberikan rekomendasi untuk item yang belum populer (long-tail)
- Dapat memberikan penjelasan yang transparan tentang mengapa item tersebut direkomendasikan

#### Kekurangan Content-Based Filtering:

- Terbatas pada fitur yang tersedia (dalam kasus ini hanya genre)
- Tidak dapat mempelajari preferensi pengguna yang kompleks
- Cenderung merekomendasikan item yang serupa, sehingga kurang memberikan variasi (filter bubble)

### 2. Collaborative Filtering

Collaborative Filtering merekomendasikan item berdasarkan pola rating dari pengguna lain. Pendekatan ini mengasumsikan bahwa pengguna yang memiliki preferensi serupa di masa lalu akan memiliki preferensi serupa di masa depan.

#### Implementasi Model:

Model Neural Collaborative Filtering (NCF) yang diimplementasikan menggunakan TensorFlow dengan embedding layer untuk user dan item. Arsitektur model terdiri dari:

1. Input layer untuk user dan movie ID
2. Embedding layer untuk user dan movie (ukuran embedding = 50)
3. Flatten layer untuk mengubah embedding menjadi vektor
4. Concatenate layer untuk menggabungkan embedding user dan movie
5. Dense layer (128 unit) dengan aktivasi ReLU dan dropout (0.2)
6. Dense layer (64 unit) dengan aktivasi ReLU dan dropout (0.2)
7. Output layer (1 unit) untuk memprediksi rating

Model dilatih menggunakan Mean Squared Error sebagai loss function dan Adam optimizer dengan learning rate 0.001. Untuk mencegah overfitting, digunakan early stopping dengan memonitor validation loss dan patience 5 epochs.

#### Hasil Pelatihan:

Model dilatih selama 8 epoch (berhenti karena early stopping) dengan hasil akhir:

- Training loss: 0.5409
- Validation loss: 0.7529

Grafik loss selama training menunjukkan bahwa model konvergen dengan cepat dan mulai overfitting setelah epoch ke-4, yang ditandai dengan validation loss yang mulai meningkat sementara training loss terus menurun.

![model_loss](https://github.com/user-attachments/assets/d0ae9ebf-d415-48e8-a07e-7d8a821686eb)

#### Hasil Rekomendasi:

Berikut adalah contoh rekomendasi untuk pengguna dengan ID 414:

**Film yang sudah ditonton pengguna (dengan rating 5.0):**
| Judul Film | Tahun |
|------------|-------|
| Hell or High Water | 2016 |
| American President, The | 1995 |
| High Fidelity | 2000 |
| Usual Suspects, The | 1995 |
| Gladiator | 2000 |

**Rekomendasi berdasarkan Collaborative Filtering:**
| Judul Film | Genre |
|------------|-------|
| Persuasion (1995) | Drama\|Romance |
| Dead Alive (Braindead) (1992) | Comedy\|Fantasy\|Horror |
| Central Station (Central do Brasil) (1998) | Drama |
| Guess Who's Coming to Dinner (1967) | Drama |
| Hustler, The (1961) | Drama |
| Discreet Charm of the Bourgeoisie, The (Charme...) | Comedy\|Drama\|Fantasy |
| Gladiator (1992) | Action\|Drama |
| Neon Genesis Evangelion: The End of Evangelion... | Action\|Animation\|Drama\|Fantasy\|Sci-Fi |
| Louis C.K.: Live at the Beacon Theater (2011) | Comedy |
| Captain Fantastic (2016) | Drama |

Dari hasil rekomendasi, terlihat bahwa model merekomendasikan beragam film dengan genre yang bervariasi, tidak hanya terfokus pada satu genre seperti pada Content-Based Filtering. Ini menunjukkan bahwa model berhasil mempelajari preferensi pengguna yang lebih kompleks.

#### Kelebihan Collaborative Filtering:

- Dapat menemukan pola yang kompleks dan tidak eksplisit dalam preferensi pengguna
- Tidak memerlukan informasi tentang item (fitur)
- Dapat merekomendasikan item yang mungkin tidak mirip secara konten tetapi disukai oleh pengguna serupa

#### Kekurangan Collaborative Filtering:

- Menghadapi masalah cold-start untuk pengguna baru dan item baru
- Memerlukan jumlah data yang cukup besar untuk membuat rekomendasi yang akurat
- Sulit menjelaskan mengapa item tertentu direkomendasikan (black box)

## Evaluation

Untuk mengevaluasi kinerja model sistem rekomendasi, saya menggunakan metrik evaluasi yang berbeda untuk masing-masing pendekatan:

### 1. Content-Based Filtering - Precision@K

Untuk Content-Based Filtering, saya menggunakan metrik Precision@K untuk mengevaluasi relevansi rekomendasi. Precision@K mengukur proporsi item yang relevan di antara K item teratas yang direkomendasikan.

#### Formula Precision@K:

```javascript
Precision@K = (Jumlah item relevan di antara K rekomendasi) / K
```

Dalam implementasi evaluasi, saya menggunakan pendekatan berikut:

1. Pilih pengguna yang memiliki cukup banyak rating (minimal 20 rating)
2. Untuk setiap pengguna, pilih satu film yang disukai (rating ≥ 4) sebagai dasar rekomendasi
3. Dapatkan rekomendasi berdasarkan film tersebut
4. Hitung Precision@K sebagai proporsi film yang direkomendasikan yang juga disukai oleh pengguna

#### Hasil Evaluasi Content-Based Filtering:

```javascript
Content-Based Filtering - Precision@10: 0.0440
```

Hasil Precision@10 sebesar 0.0440 berarti bahwa sekitar 4.4% dari film yang direkomendasikan oleh model Content-Based Filtering relevan dengan preferensi pengguna. Nilai ini relatif rendah, yang menunjukkan bahwa rekomendasi berdasarkan kesamaan genre saja mungkin tidak cukup untuk menangkap preferensi pengguna yang kompleks.

### 2. Collaborative Filtering - RMSE

Untuk Collaborative Filtering, saya menggunakan Root Mean Squared Error (RMSE) untuk mengevaluasi akurasi prediksi rating. RMSE mengukur seberapa jauh prediksi rating menyimpang dari rating sebenarnya.

#### Formula RMSE:

```javascript
RMSE = sqrt(1/n * Σ(y_true - y_pred)²)
```

di mana:

- n adalah jumlah prediksi
- y_true adalah rating sebenarnya
- y_pred adalah rating yang diprediksi

#### Hasil Evaluasi Collaborative Filtering:

```javascript
Collaborative Filtering - RMSE: 0.8485
```

Hasil RMSE sebesar 0.8485 menunjukkan bahwa rata-rata prediksi rating menyimpang sekitar 0.85 poin dari rating sebenarnya. Mengingat skala rating adalah 0.5-5.0, error ini relatif kecil (sekitar 17% dari rentang skala), yang menunjukkan bahwa model Collaborative Filtering cukup akurat dalam memprediksi preferensi pengguna.

### Perbandingan dan Analisis Hasil

Dari hasil evaluasi, dapat disimpulkan bahwa model Collaborative Filtering memberikan kinerja yang lebih baik dalam memprediksi preferensi pengguna dibandingkan dengan model Content-Based Filtering. Hal ini dapat dijelaskan karena Collaborative Filtering dapat menangkap pola yang lebih kompleks dalam preferensi pengguna, tidak hanya berdasarkan kesamaan konten.

RMSE 0.8485 untuk Collaborative Filtering menunjukkan akurasi prediksi yang cukup baik, mengingat skala rating 0.5-5.0. Precision@10 sebesar 0.0440 untuk Content-Based Filtering menunjukkan bahwa meskipun rekomendasi berdasarkan genre dapat memberikan beberapa hasil yang relevan, namun pendekatan ini memiliki keterbatasan dalam menangkap preferensi pengguna yang kompleks.

Namun, kedua pendekatan memiliki kelebihan dan kekurangan masing-masing, dan dalam praktiknya, sistem rekomendasi yang baik sering menggabungkan kedua pendekatan ini (hybrid approach) untuk mendapatkan hasil yang optimal.

![evaluation_metrics](https://github.com/user-attachments/assets/ae448bfb-1054-47e2-b016-c17c6a2ed96b)

## Kesimpulan

Dalam proyek ini, saya telah berhasil mengimplementasikan dua pendekatan sistem rekomendasi film: Content-Based Filtering dan Collaborative Filtering.

Content-Based Filtering berhasil merekomendasikan film berdasarkan kesamaan genre, yang berguna untuk memberikan rekomendasi yang transparan dan mengatasi masalah cold-start untuk item baru. Namun, pendekatan ini memiliki keterbatasan dalam menangkap preferensi pengguna yang kompleks, yang tercermin dari nilai Precision@10 yang relatif rendah (0.0440).

Collaborative Filtering dengan model Neural Collaborative Filtering berhasil mempelajari pola preferensi pengguna yang kompleks dan memberikan rekomendasi yang lebih personal. Model ini mencapai RMSE 0.8485, yang menunjukkan akurasi prediksi yang cukup baik.

Untuk pengembangan lebih lanjut, beberapa saran yang dapat dipertimbangkan:

1. Mengembangkan sistem rekomendasi hybrid yang menggabungkan kelebihan dari kedua pendekatan
2. Memperkaya fitur film dengan menambahkan informasi seperti aktor, sutradara, atau sinopsis
3. Mengimplementasikan teknik deep learning yang lebih canggih seperti attention mechanism atau graph neural networks
4. Menambahkan fitur kontekstual seperti waktu, lokasi, atau perangkat yang digunakan pengguna
5. Mengembangkan strategi untuk mengatasi masalah cold-start, seperti content-boosted collaborative filtering

Dengan implementasi sistem rekomendasi film yang efektif, platform streaming dapat meningkatkan pengalaman pengguna, mengurangi waktu pencarian, dan pada akhirnya meningkatkan engagement dan retensi pengguna.
