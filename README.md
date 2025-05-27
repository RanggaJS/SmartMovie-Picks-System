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

Pada tahap ini dilakukan proses data preparation untuk memastikan data yang digunakan dalam sistem rekomendasi bersih, relevan, dan siap untuk dianalisis baik menggunakan pendekatan Content-Based Filtering maupun Collaborative Filtering. Berikut adalah tahapan yang dilakukan secara berurutan:

### 1. Filtering Film dan Pengguna

Langkah pertama adalah menyaring data film dan pengguna berdasarkan jumlah rating. Film yang memiliki kurang dari lima rating dihapus dari dataset untuk memastikan hanya film yang memiliki cukup banyak penilaian yang dianalisis. Hal ini penting agar sistem rekomendasi tidak memberikan hasil yang bias terhadap film dengan informasi yang minim. Demikian pula, hanya pengguna yang memberikan minimal lima rating yang dipertahankan dalam dataset. Tujuannya adalah agar hanya pengguna aktif yang digunakan dalam analisis, karena mereka cenderung memiliki profil preferensi yang lebih jelas dan representatif.

### 2. Ekstraksi Tahun dari Judul Film

Langkah kedua adalah mengekstraksi informasi tahun rilis dari judul film. Sebagian besar judul film memuat tahun rilis dalam tanda kurung (misalnya "Toy Story (1995)"). Dengan menggunakan regular expression, informasi tahun ini diambil dan disimpan dalam kolom baru bernama year. Penambahan informasi ini bertujuan untuk memperkaya dataset dan bisa digunakan dalam analisis lanjutan, seperti menyaring film berdasarkan dekade atau mengevaluasi tren film dari waktu ke waktu.

### 3. Preprocessing untuk Content-Based Filtering

Langkah ketiga adalah preprocessing untuk pendekatan Content-Based Filtering. Genre pada data film diolah dengan mengganti tanda pemisah | menjadi spasi agar dapat diproses sebagai teks biasa. Selanjutnya, teks genre diubah menjadi representasi numerik menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency), yang mencerminkan pentingnya suatu genre pada masing-masing film. Kemudian, dihitung kemiripan antar film menggunakan cosine similarity berdasarkan TF-IDF matrix yang terbentuk. Tahapan ini memungkinkan sistem untuk memberikan rekomendasi berdasarkan kesamaan genre antar film. Di tahap ini juga dibuat pemetaan antara movieId dan indeks baris dalam data untuk mempermudah proses pencarian dan pengolahan data.

### 4. Preprocessing untuk Collaborative Filtering

Langkah keempat adalah persiapan data untuk pendekatan Collaborative Filtering. Dataset yang telah difilter sebelumnya dibagi menjadi data training (80%) dan testing (20%) agar model dapat diuji kemampuannya dalam merekomendasikan film pada data yang belum dilihat sebelumnya. Setelah itu, dilakukan mapping dari userId dan movieId ke indeks numerik berurutan, yang selanjutnya digunakan untuk membentuk format data baru dalam bentuk list of dictionaries. Setiap entri berisi indeks pengguna, indeks film, dan nilai rating, sehingga data siap digunakan untuk pelatihan model berbasis Collaborative Filtering.

## Modeling

Pada tahap ini, dilakukan pemodelan sistem rekomendasi film menggunakan pendekatan Content-Based Filtering, yang memanfaatkan informasi konten film—dalam hal ini genre—untuk memberikan rekomendasi. Sistem ini tidak menggunakan algoritma pembelajaran mesin konvensional seperti klasifikasi atau regresi, melainkan memanfaatkan teknik representasi teks dan pengukuran kemiripan antar dokumen (film) untuk menyelesaikan permasalahan rekomendasi.

### 1. Content-Based Filtering (CBF)

Pendekatan Content-Based Filtering memanfaatkan informasi konten film—khususnya genre—untuk memberikan rekomendasi film yang serupa dengan film referensi.

#### Ekstraksi Fitur

Genre film, yang semula berbentuk teks dengan pemisah "|", diubah menjadi bentuk string kalimat agar dapat diproses oleh algoritma TF-IDF. Teknik TF-IDF (Term Frequency-Inverse Document Frequency) digunakan untuk mengubah genre menjadi vektor numerik, yang merepresentasikan seberapa penting suatu genre dalam masing-masing film. TF-IDF efektif dalam menekan pengaruh genre yang terlalu umum dan memperkuat genre yang lebih unik, sehingga mampu membedakan film berdasarkan informasi kontennya.

#### Perhitungan Kemiripan Antar Film

Setelah mendapatkan representasi vektor dari genre tiap film, digunakan Cosine Similarity untuk menghitung tingkat kemiripan antara film satu dengan yang lainnya. Cosine similarity dipilih karena mampu mengukur kesamaan arah dari dua vektor, sehingga cocok untuk mengukur kemiripan konten berdasarkan TF-IDF.

#### Pemetaan dan Pencarian Rekomendasi

Mapping movieId ke indeks digunakan untuk memudahkan pencarian film referensi. Berdasarkan hasil kemiripan cosine, dipilih sejumlah film yang paling mirip (dalam hal genre) sebagai kandidat rekomendasi. Film tersebut disusun berdasarkan skor kemiripan tertinggi dan dikembalikan dalam bentuk daftar rekomendasi.

**Contoh Hasil Rekomendasi Berdasarkan Konten:**
Film Referensi: Interstellar (2014) (ID Film: 109487)
Daftar rekomendasi film yang dihasilkan mengandung genre dan tema yang sangat mirip dengan Interstellar, terutama Drama, Sci-Fi, dan film berformat IMAX.

| No  | Judul Film                            | ID Film | Genre  |          |          |      |
| --- | ------------------------------------- | ------- | ------ | -------- | -------- | ---- |
| 1   | Transcendence (2014)                  | 110730  | Drama  | Sci-Fi   | IMAX     |      |
| 2   | Cloud Atlas (2012)                    | 97752   | Drama  | Sci-Fi   | IMAX     |      |
| 3   | Contagion (2011)                      | 89470   | Sci-Fi | Thriller | IMAX     |      |
| 4   | Gravity (2013)                        | 104841  | Action | Sci-Fi   | IMAX     |      |
| 5   | The Amazing Spider-Man 2 (2014)       | 110553  | Action | Sci-Fi   | IMAX     |      |
| 6   | Edge of Tomorrow (2014)               | 111759  | Action | Sci-Fi   | IMAX     |      |
| 7   | Day the Earth Stood Still, The (2008) | 64497   | Drama  | Sci-Fi   | Thriller | IMAX |
| 8   | Elysium (2013)                        | 103253  | Action | Drama    | Sci-Fi   | IMAX |
| 9   | Real Steel (2011)                     | 90249   | Action | Drama    | Sci-Fi   | IMAX |
| 10  | Men in Black III (2012)               | 94777   | Action | Comedy   | Sci-Fi   | IMAX |

**Interpretasi Hasil**

Kesamaan Genre:
Film-film yang direkomendasikan sebagian besar memiliki genre Sci-Fi yang kuat, seringkali dikombinasikan dengan Drama dan Action, sangat mirip dengan genre Interstellar yang merupakan film fiksi ilmiah dengan elemen emosional dan drama yang kental.

Format IMAX:
Banyak film dalam daftar ini juga memiliki tag IMAX, menandakan film dengan kualitas visual dan audio yang tinggi, cocok bagi penonton yang menyukai pengalaman sinematik serupa Interstellar.

Tema dan Suasana:
Film-film seperti Transcendence, Cloud Atlas, dan Gravity juga mengangkat tema ilmiah dan futuristik, menjadikan rekomendasi ini relevan untuk penonton yang ingin melanjutkan menonton film dengan suasana dan konten serupa.

Variasi Genre Tambahan:
Beberapa film memasukkan genre tambahan seperti Thriller (Contagion, Day the Earth Stood Still) dan Comedy (Men in Black III), memberikan variasi untuk memperkaya pengalaman penonton sekaligus tetap menjaga kesamaan utama di genre Sci-Fi.

### 2. Collaborative Filtering (CF)

Collaborative Filtering merekomendasikan film berdasarkan pola rating dan preferensi pengguna lain yang memiliki kesamaan preferensi dengan pengguna target. Pada proyek ini, digunakan model Neural Collaborative Filtering (NCF) dengan arsitektur berbasis embedding.

**Implementasi Model NCF:**

• Input layer untuk user ID dan movie ID
• Embedding layer dengan ukuran 50 untuk user dan film
• Flatten layer untuk mengubah embedding menjadi vektor satu dimensi
• Concatenate layer untuk menggabungkan embedding user dan film
• Dua dense layer berturut-turut (128 dan 64 unit) dengan aktivasi ReLU dan dropout 0.2 untuk mencegah overfitting
• Output layer tunggal untuk prediksi rating film

Model dilatih menggunakan Mean Squared Error (MSE) sebagai fungsi loss dan optimizer Adam dengan learning rate 0.001. Early stopping diterapkan untuk menghentikan pelatihan ketika validasi loss tidak membaik selama 5 epoch berturut-turut.

**Hasil Pelatihan Model:**

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

![model_loss_ggplot_style](https://github.com/user-attachments/assets/7a34c14e-54fb-410b-89f0-f499ef216c5c)

Model menunjukkan penurunan loss yang signifikan di awal, validasi loss relatif stabil menandakan model mulai konvergen dan belum overfitting parah.

### 3. Contoh Rekomendasi untuk Pengguna dengan ID: 414

Pengguna dengan ID 414 memiliki histori rating film sebagai berikut:

| Judul Film                     | Rating |
| ------------------------------ | ------ |
| Hell or High Water (2016)      | 5.0    |
| American President, The (1995) | 5.0    |
| High Fidelity (2000)           | 5.0    |
| Usual Suspects, The (1995)     | 5.0    |
| Gladiator (2000)               | 5.0    |

Berdasarkan model Collaborative Filtering, rekomendasi film yang diberikan adalah:

| Judul Film                                      | Genre                           |
| ----------------------------------------------- | ------------------------------- |
| Persuasion (1995)                               | Drama\|Romance                  |
| Philadelphia Story, The (1940)                  | Comedy\|Drama\|Romance          |
| Seventh Seal, The (Sjunde inseglet, Det) (1957) | Drama                           |
| Jules and Jim (Jules et Jim) (1961)             | Drama\|Romance                  |
| Thomas Crown Affair, The (1968)                 | Crime\|Drama\|Romance\|Thriller |
| Yojimbo (1961)                                  | Action\|Adventure               |
| Guess Who's Coming to Dinner (1967)             | Drama                           |
| Trial, The (Procès, Le) (1962)                  | Drama                           |
| Louis C.K.: Live at the Beacon Theater (2011)   | Comedy                          |
| Captain Fantastic (2016)                        | Drama                           |

Rekomendasi ini menunjukkan film-film dengan genre Drama, Romance, dan Comedy mendominasi, yang konsisten dengan film-film yang pernah diberi rating tinggi oleh pengguna.

### 4 Kelebihan dan Kekurangan Pendekatan

Content-Based Filtering
• Kelebihan:
o Tidak membutuhkan data perilaku pengguna lain, cocok untuk masalah cold-start.
o Memberikan rekomendasi yang transparan berdasarkan konten film.
o Dapat merekomendasikan film dengan fitur unik meskipun belum populer.
• Kekurangan:
o Terbatas pada fitur konten (genre), sehingga kurang eksplorasi variasi rekomendasi.
o Rentan terhadap efek filter bubble (rekomendasi serupa terus-menerus).
o Tidak mempertimbangkan tren atau preferensi kolektif pengguna lain.
Collaborative Filtering
• Kelebihan:
o Memanfaatkan data interaksi pengguna, bisa menangkap preferensi kompleks.
o Mampu memberikan rekomendasi yang beragam sesuai pola perilaku kolektif.
• Kekurangan:
o Membutuhkan data interaksi pengguna yang cukup, rentan masalah cold-start untuk pengguna dan film baru.
o Model lebih kompleks dan memerlukan waktu pelatihan serta tuning parameter.

### 5. Saran Pengembangan

Untuk meningkatkan performa sistem rekomendasi, disarankan menggabungkan kedua pendekatan tersebut menjadi sistem hybrid filtering. Sistem hybrid akan mengombinasikan kekuatan Content-Based Filtering (berdasarkan fitur film) dan Collaborative Filtering (berdasarkan interaksi pengguna) sehingga dapat menghasilkan rekomendasi yang lebih akurat dan beragam. Selain itu, fitur konten bisa diperkaya dengan metadata tambahan seperti deskripsi film, sutradara, dan pemeran untuk memperkaya representasi konten.

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

Dalam proyek ini, telah berhasil diimplementasikan dua pendekatan sistem rekomendasi film, yaitu Content-Based Filtering dan Collaborative Filtering.
• Content-Based Filtering mampu memberikan rekomendasi berdasarkan kesamaan genre film, cocok untuk mengatasi masalah cold-start pada item baru dan memberikan rekomendasi yang transparan. Namun, pendekatan ini terbatas dalam menangkap preferensi pengguna yang kompleks dan rawan menghasilkan rekomendasi yang monoton (filter bubble). Nilai Precision@10 sebesar 0.35 menunjukkan efektivitas yang moderat.
• Collaborative Filtering dengan model Neural Collaborative Filtering dapat mempelajari pola preferensi pengguna secara lebih personal dan kompleks. Model ini menunjukkan performa yang baik dengan RMSE sekitar 0.87, yang menandakan akurasi prediksi rating yang cukup baik.
Saran pengembangan selanjutnya meliputi penggabungan kedua pendekatan menjadi sistem hybrid filtering untuk meningkatkan akurasi dan variasi rekomendasi, memperkaya fitur konten film, dan mengadopsi teknik machine learning yang lebih canggih serta penambahan fitur kontekstual.
Dengan penerapan sistem rekomendasi yang optimal, platform streaming dapat meningkatkan pengalaman pengguna, mempersingkat waktu pencarian film, serta meningkatkan engagement dan retensi pengguna.
