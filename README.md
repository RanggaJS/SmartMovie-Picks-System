backend/
├── app/                           # Direktori utama aplikasi Flask
│   ├── __init__.py                # Inisialisasi aplikasi Flask
│   ├── ml/                        # Modul machine learning
│   │   ├── __init__.py
│   │   ├── advanced_recommendation_engine.py
│   │   ├── diet_progress_analyzer.py
│   │   ├── food_database.py
│   │   ├── model_serializer.py
│   │   ├── recommendation_engine.py
│   │   ├── tensorflow_models.py
│   │   └── tensorflow_ncf_lstm_example.py
│   ├── models/                    # Model database SQLAlchemy
│   │   ├── __init__.py
│   │   ├── food.py
│   │   ├── recommendation.py
│   │   └── user.py
│   ├── routes/                    # Definisi endpoint API
│   │   ├── __init__.py
│   │   ├── activities.py
│   │   ├── auth.py
│   │   ├── profile.py
│   │   ├── progress.py
│   │   ├── recommendations.py
│   │   └── user.py
│   └── utils/                     # Utilitas umum
│       └── __init__.py
│
├── config.py                      # Konfigurasi aplikasi
├── data/                          # Data untuk model dan database
│   ├── FoodData_Central_foundation_food_json_2025-04-24.json
│   └── FoodData_Central_foundation_food_json_2025-04-24.zip
│
├── migrations/                    # Migrasi database Flask-Migrate
│   ├── alembic.ini
│   ├── env.py
│   ├── README
│   ├── script.py.mako
│   └── versions/
│
├── models/                        # Model machine learning terlatih
│   └── tfidf_vectorizer.joblib
│
├── scripts/                       # Script utilitas dan inisialisasi
│   ├── import_usda_data.py
│   ├── initialize_food_database.py
│   ├── README.md
│   ├── rebuild_food_database.py
│   └── sqlite_tools.py
│
├── .dockerignore                  # File untuk konfigurasi Docker
├── .env~                          # Template file environment
├── .flaskenv                      # Konfigurasi Flask
├── app_minimal.py                 # Versi minimal aplikasi
├── Dockerfile                     # Konfigurasi Docker
├── food_data.csv                  # Data makanan
├── food_database.db               # Database SQLite untuk makanan
├── food_database.log              # Log database makanan
├── init_db.py                     # Script inisialisasi database
├── measure_model_accuracy.py      # Script pengukuran akurasi model
├── mealmind_dev.db                # Database SQLite untuk development
├── mealmind_prod.db               # Database SQLite untuk production
├── README.md                      # Dokumentasi backend
├── requirements.txt               # Dependensi Python
├── run.py                         # Script utama untuk menjalankan aplikasi
├── run_lightweight.py             # Versi ringan untuk menjalankan aplikasi
├── simple_recommendations.py      # Implementasi sederhana rekomendasi
├── simple_test.py                 # Script pengujian sederhana
├── SQLITE_README.md               # Dokumentasi SQLite
├── test_meal_variety.py           # Pengujian variasi makanan
├── test_recommendations.py        # Pengujian rekomendasi
└── train_models.py                # Script pelatihan model

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

![heatmap_correlation](https://github.com/user-attachments/assets/ccadaf71-1dbc-4560-be1c-0e97be167348)

Visualisasi ini menunjukkan hubungan antara jumlah rating dan rata-rata rating per film.
Insight: Nilai korelasi yang sangat lemah (0.13) menunjukkan bahwa film yang banyak dirating belum tentu memiliki nilai rating tinggi — popularitas tidak selalu berbanding lurus dengan kualitas.

#### 3. Boxplot Distribusi Rating per Genre

![boxplot_rating_per_genre](https://github.com/user-attachments/assets/5b359b24-81d7-4a53-9637-711211c0524c)

Boxplot ini menunjukkan sebaran rating berdasarkan genre utama.
Insight: Genre seperti Documentary dan Animation cenderung memiliki rating lebih tinggi, sedangkan genre seperti Horror memiliki distribusi yang lebih menyebar dan banyak outlier.

#### 4. Wordcloud Genre Film

![wordcloud_genre](https://github.com/user-attachments/assets/8efc4f53-6796-494c-9dd9-540d0f8af2fb)

Wordcloud menggambarkan frekuensi kemunculan genre dalam dataset.
Insight: Genre seperti Drama, Comedy, dan Romance adalah yang paling umum dalam data.

#### 5. Scatter Plot: Rating per User

![scatter_user_rating](https://github.com/user-attachments/assets/0be3fb1b-5c99-4eb1-8658-b765f2888ee6)

Plot ini menunjukkan hubungan antara jumlah film yang dirating oleh user dan rata-rata rating yang mereka berikan.
Insight: User yang memberikan rating dalam jumlah besar cenderung memberi rating yang lebih stabil/moderat, sedangkan user dengan sedikit rating cenderung ekstrem.

#### 6. Barplot: 10 Film Paling Banyak Dirating

![top10_movies_rating_count](https://github.com/user-attachments/assets/3a18ed01-ed60-47cb-b892-de77665a1d4c)

Grafik ini menunjukkan 10 film dengan jumlah rating terbanyak.
Insight: Film klasik seperti Forrest Gump dan The Shawshank Redemption menempati peringkat teratas, mencerminkan tingkat popularitas yang sangat tinggi.

#### 7. Treemap: Genre Film Terpopuler

![treemap_genre](https://github.com/user-attachments/assets/4c34acee-39ae-406f-9860-f2d6d78d6622)

Grafik ini menampilkan genre film berdasarkan tingkat popularitasnya dalam bentuk treemap, di mana ukuran setiap kotak mencerminkan jumlah film atau tingkat popularitas genre tersebut.

Insight: Genre Drama, Comedy, dan Action mendominasi tampilan ini, menandakan ketertarikan penonton yang tinggi terhadap genre-genre tersebut.

#### 8. Radar Chart: Genre Film Terpopuler

![radar_genre](https://github.com/user-attachments/assets/3ed5d461-2e7f-48aa-b31c-e67fe590efb0)

Grafik radar ini memvisualisasikan popularitas berbagai genre film dalam bentuk area yang melebar ke berbagai arah sesuai skala nilai popularitas.

Insight: Drama muncul sebagai genre paling populer, disusul oleh Comedy dan Thriller. Genre seperti Animation dan Documentary memiliki nilai popularitas lebih rendah.

#### 9. Bubble Chart: Popularitas vs Kualitas Film

![bubble_rating](https://github.com/user-attachments/assets/a16ad5f7-a3de-4177-98d7-2c76e6748166)

Grafik ini menggabungkan jumlah rating (sumbu X) dan rata-rata rating (sumbu Y) dari film, dengan ukuran dan warna gelembung mewakili jumlah dan kualitas ulasan.

Insight: Terlihat bahwa beberapa film memiliki rating sangat tinggi meski tidak terlalu populer, dan sebaliknya ada film populer namun dengan rating rendah—menunjukkan bahwa popularitas tidak selalu mencerminkan kualitas.

#### 10. Donut Chart: Distribusi Genre Film

![donut_genre](https://github.com/user-attachments/assets/38a582b2-fb3b-4489-9aef-7ac0cb9d39e6)

Grafik berbentuk donat ini menunjukkan distribusi persentase film berdasarkan genre.

Insight: Drama mendominasi dengan porsi 23.7%, diikuti oleh Comedy dan Action. Genre Horror dan Romance menempati porsi yang lebih kecil.

#### 11. Barplot: Top 15 Film Berdasarkan Rating Rata-rata (Min 100 Rating)

![lollipop_top_movies](https://github.com/user-attachments/assets/b71a1282-a29c-41bc-a22d-8013e62eb1b7)

Grafik ini menunjukkan 15 film dengan rating rata-rata tertinggi, dengan syarat minimal 100 rating agar hasil lebih representatif.

Insight: Film-film dalam grafik ini mendapatkan apresiasi tinggi dari penonton, menunjukkan kualitas konten yang konsisten dan kuat berdasarkan ulasan.

## Data Preparation

Tahap ini memastikan data yang digunakan dalam sistem rekomendasi bersih, relevan, dan siap dianalisis, baik dengan pendekatan **Content-Based Filtering** maupun **Collaborative Filtering**. Berikut langkah-langkahnya:

### 1. Filtering Film dan Pengguna

- Film dengan kurang dari 5 rating dihapus untuk menghindari bias terhadap film yang minim informasi.
- Hanya pengguna dengan minimal 5 rating yang dipertahankan agar analisis berbasis preferensi lebih representatif.

### 2. Ekstraksi Tahun dari Judul Film

- Tahun rilis diekstraksi dari judul film menggunakan **regular expression** (contoh: `"Toy Story (1995)" → 1995`).
- Tahun disimpan dalam kolom `year`, berguna untuk analisis tren atau segmentasi berdasarkan dekade.

### 3. Preprocessing untuk Content-Based Filtering

- Genre film diubah dari format `Action|Adventure` menjadi teks biasa.
- Representasi numerik genre dibentuk dengan **TF-IDF**.
- Kemiripan antar film dihitung dengan **Cosine Similarity**.
- Dibuat pemetaan `movieId` ke indeks baris untuk efisiensi pencarian.

### 4. Preprocessing untuk Collaborative Filtering

- Dataset dibagi menjadi **80% training** dan **20% testing**.
- `userId` dan `movieId` dipetakan ke indeks numerik.
- Format data diubah menjadi **list of dictionaries**, masing-masing berisi: indeks user, indeks film, dan rating.

---

## Modeling

Tahap ini membangun sistem rekomendasi dengan dua pendekatan: **Content-Based Filtering (CBF)** dan **Collaborative Filtering (CF)**.

### 1. Content-Based Filtering (CBF)

Pendekatan ini menggunakan informasi konten (genre) untuk merekomendasikan film serupa.

#### Ekstraksi Fitur

- Genre diformat sebagai teks utuh, lalu diolah dengan **TF-IDF** untuk menghasilkan vektor numerik.
- TF-IDF membantu memperkuat genre unik dan menekan genre umum.

#### Perhitungan Kemiripan

- Digunakan **Cosine Similarity** untuk mengukur kemiripan antar film berdasarkan vektor TF-IDF.

#### Pemetaan dan Rekomendasi

- Menggunakan hasil kemiripan untuk mengurutkan dan memilih film dengan skor tertinggi sebagai rekomendasi.

**Contoh Rekomendasi Berdasarkan Film "Interstellar (2014)"**

| No  | Judul Film                       | ID Film | Genre                         |
| --- | -------------------------------- | ------- | ----------------------------- |
| 1   | Transcendence (2014)             | 110730  | Drama\|Sci-Fi\|IMAX           |
| 2   | Cloud Atlas (2012)               | 97752   | Drama\|Sci-Fi\|IMAX           |
| 3   | Contagion (2011)                 | 89470   | Sci-Fi\|Thriller\|IMAX        |
| 4   | Gravity (2013)                   | 104841  | Action\|Sci-Fi\|IMAX          |
| 5   | The Amazing Spider-Man 2 (2014)  | 110553  | Action\|Sci-Fi\|IMAX          |
| 6   | Edge of Tomorrow (2014)          | 111759  | Action\|Sci-Fi\|IMAX          |
| 7   | Day the Earth Stood Still (2008) | 64497   | Drama\|Sci-Fi\|Thriller\|IMAX |
| 8   | Elysium (2013)                   | 103253  | Action\|Drama\|Sci-Fi\|IMAX   |
| 9   | Real Steel (2011)                | 90249   | Action\|Drama\|Sci-Fi\|IMAX   |
| 10  | Men in Black III (2012)          | 94777   | Action\|Comedy\|Sci-Fi\|IMAX  |

**Analisis Hasil:**

- Mayoritas film bergenre **Sci-Fi** dan **Drama**, selaras dengan Interstellar.
- Banyak film memiliki tag **IMAX**, menyiratkan kualitas sinematik tinggi.
- Tema ilmiah dan futuristik tetap terjaga dengan variasi tambahan seperti Thriller dan Comedy.

### 2. Collaborative Filtering (CF)

Menggunakan **Neural Collaborative Filtering (NCF)** untuk merekomendasikan film berdasarkan kesamaan preferensi antar pengguna.

#### Arsitektur Model NCF

- **Input Layer**: `userId`, `movieId`
- **Embedding Layer**: ukuran 50 untuk user dan film
- **Flatten Layer**: mengubah embedding menjadi vektor 1D
- **Concatenate Layer**: menggabungkan user dan movie vector
- **Dense Layer**: dua layer (128 dan 64 unit) dengan ReLU dan dropout 0.2
- **Output Layer**: memprediksi rating

- **Loss Function**: Mean Squared Error (MSE)
- **Optimizer**: Adam (lr = 0.001)
- **Early Stopping**: diterapkan bila tidak ada perbaikan validasi loss selama 5 epoch

#### Hasil Training

| Epoch | Training Loss | Validation Loss |
| ----- | ------------- | --------------- |
| 1     | 2.4559        | 0.7519          |
| 2     | 0.8333        | 0.7326          |
| 3     | 0.7791        | 0.7177          |
| 4     | 0.7241        | 0.7186          |
| 5     | 0.6840        | 0.7238          |
| 6     | 0.6373        | 0.7294          |
| 7     | 0.6027        | 0.7357          |
| 8     | 0.5517        | 0.7560          |

> Model menunjukkan tren konvergensi dengan validasi loss relatif stabil.

### 3. Contoh Rekomendasi untuk User ID: 414

**Histori Rating Pengguna:**

| Judul Film                     | Rating |
| ------------------------------ | ------ |
| Hell or High Water (2016)      | 5.0    |
| American President, The (1995) | 5.0    |
| High Fidelity (2000)           | 5.0    |
| Usual Suspects, The (1995)     | 5.0    |
| Gladiator (2000)               | 5.0    |

**Rekomendasi Hasil Collaborative Filtering:**

| Judul Film                                      | Genre                         |
| ----------------------------------------------- | ----------------------------- |
| Persuasion (1995)                               | Drama\|Romance                |
| Philadelphia Story, The (1940)                  | Comedy\|Drama\|Romance        |
| Seventh Seal, The (Sjunde inseglet, Det) (1957) | Drama                         |
| Jules and Jim (Jules et Jim) (1961)             | Drama\|Romance                |
| Thomas Crown Affair, The (1968)                 | Action\|Crime\|Drama\|Romance |

> Rekomendasi menunjukkan kecenderungan pada film dengan genre **Drama** dan **Romance**, sesuai preferensi pengguna terhadap film-film berkualitas dengan elemen naratif yang kuat.

### 4. Kelebihan dan Kekurangan Pendekatan

#### Content-Based Filtering

- **Kelebihan:**
  - Tidak membutuhkan data perilaku pengguna lain, cocok untuk masalah cold-start.
  - Memberikan rekomendasi yang transparan berdasarkan konten film.
  - Dapat merekomendasikan film dengan fitur unik meskipun belum populer.
- **Kekurangan:**
  - Terbatas pada fitur konten (genre), sehingga kurang eksplorasi variasi rekomendasi.
  - Rentan terhadap efek filter bubble (rekomendasi serupa terus-menerus).
  - Tidak mempertimbangkan tren atau preferensi kolektif pengguna lain.

#### Collaborative Filtering

- **Kelebihan:**
  - Memanfaatkan data interaksi pengguna, bisa menangkap preferensi kompleks.
  - Mampu memberikan rekomendasi yang beragam sesuai pola perilaku kolektif.
- **Kekurangan:**
  - Membutuhkan data interaksi pengguna yang cukup, rentan masalah cold-start untuk pengguna dan film baru.
  - Model lebih kompleks dan memerlukan waktu pelatihan serta tuning parameter.

### 5. Saran Pengembangan

Untuk meningkatkan performa sistem rekomendasi, disarankan menggabungkan kedua pendekatan tersebut menjadi sistem **hybrid filtering**. Sistem hybrid akan mengombinasikan kekuatan Content-Based Filtering (berdasarkan fitur film) dan Collaborative Filtering (berdasarkan interaksi pengguna) sehingga dapat menghasilkan rekomendasi yang lebih akurat dan beragam. Selain itu, fitur konten bisa diperkaya dengan metadata tambahan seperti deskripsi film, sutradara, dan pemeran untuk memperkaya representasi konten.

---

## Evaluation

**Metrik Evaluasi yang Digunakan**
Dalam proyek sistem rekomendasi film ini, kami menggunakan dua jenis metrik evaluasi yang sesuai dengan karakteristik masing-masing metode rekomendasi:

### 1. Precision@k (Precision at 10)

Precision@k adalah metrik yang mengukur seberapa banyak dari k rekomendasi teratas yang benar-benar relevan atau sesuai dengan preferensi pengguna.
Secara matematis, precision@k untuk seorang pengguna dihitung dengan rumus:

```javascript
Precision@k = (Jumlah Rekomendasi Relevan di Top k) / k
```

Metrik ini cocok untuk sistem Content-Based Filtering yang fokus pada relevansi item yang direkomendasikan berdasarkan kesamaan konten.

### 2. Root Mean Squared Error (RMSE)

RMSE mengukur rata-rata akar kuadrat selisih antara rating yang diprediksi model dan rating asli yang diberikan pengguna.
Formula RMSE adalah:

```javascript
RMSE = sqrt(((1 / n) * Σ(y_pred_i - y_true_i)) ^ 2);
```

di mana:

- y_pred_i = rating prediksi ke-i
- y_true_i = rating asli ke-i
- n = jumlah data evaluasi

RMSE digunakan untuk mengukur akurasi model Collaborative Filtering yang memprediksi rating numerik.

#### Hasil Evaluasi Proyek

![evaluation_metrics_alt](https://github.com/user-attachments/assets/37545aa1-de8c-404b-b3f6-3d5b0004bccd)

Evaluasi sistem rekomendasi film dilakukan dengan menggunakan metrik yang sesuai untuk masing-masing pendekatan. Untuk Content-Based Filtering, hasil evaluasi menunjukkan nilai Precision@10 sebesar 0.0230, yang mengindikasikan bahwa sekitar 2,3% dari 10 rekomendasi teratas relevan dengan preferensi pengguna berdasarkan kesamaan konten film. Nilai ini menunjukkan bahwa pendekatan ini masih memiliki keterbatasan dalam memberikan rekomendasi yang sangat tepat. Sedangkan pada Collaborative Filtering, model yang digunakan berhasil mencapai nilai Root Mean Squared Error (RMSE) sebesar 0.8472, menunjukkan tingkat akurasi prediksi rating pengguna yang cukup baik. RMSE yang rendah ini menandakan bahwa model mampu memprediksi preferensi pengguna dengan kesalahan yang relatif kecil, sehingga memberikan rekomendasi yang lebih personal dan akurat dibandingkan Content-Based Filtering.

## Kesimpulan

Dalam proyek ini, telah diimplementasikan dua pendekatan sistem rekomendasi film, yaitu Content-Based Filtering dan Collaborative Filtering. Content-Based Filtering memberikan rekomendasi berdasarkan kesamaan konten film, cocok untuk mengatasi masalah cold-start dan memberikan rekomendasi yang transparan. Namun, dengan nilai Precision@10 sebesar 0,0230, efektivitasnya masih sangat terbatas dan cenderung menghasilkan rekomendasi yang kurang relevan. Sebaliknya, Collaborative Filtering dengan model Neural Collaborative Filtering menunjukkan performa yang lebih baik dengan RMSE sebesar 0,8472, menandakan akurasi prediksi rating pengguna yang cukup baik dan rekomendasi yang lebih personal serta akurat.

Pengembangan selanjutnya disarankan untuk menggabungkan kedua pendekatan menjadi sistem hybrid filtering guna meningkatkan akurasi dan variasi rekomendasi, serta memperkaya fitur konten dan menambahkan fitur kontekstual. Dengan penerapan sistem rekomendasi yang optimal, platform streaming dapat meningkatkan pengalaman pengguna, mempercepat pencarian film, serta meningkatkan engagement dan retensi pengguna.
