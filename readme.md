# Laporan Proyek Machine Learning - M. Taufiq Hidayat Pohan

## Domain Proyek

<p  style='text-align: justify;'>

Di era yang serba digital ini, orang-orang semakin mudah dalam memiliki banyak pilihan untuk mendapatkan hiburan. Salah satu hiburan yang banyak diminati adalah _anime_ ​(Jayaperwira et al., 2023)​. Dengan gambar yang bagus dan cerita yang menarik membuat orang menyukai _anime_. Pertumbuhan popularitas animasi asal Jepang di Indonesia dapat dilihat dari banyaknya orang ingin pergi ke Jepang karena menonton _anime_ dan dapat dilihat melihat salah satu _Youtube Channel Muse Indonesia_ yang kini mencapai lebih dari 7 Juta _Subscribers_ ​(Reynaldi & Istiono, 2023)​. Berdasarkan _Japan Animation  Assosiation_, jumlah judul _anime_ di bulan Juli 2022 telah menembus angka 14.710 judul dan berdasarkan _MyAnimeList_, jumlah judul _anime_ yang tercatat sebesar 24.777 judul yang terdiri dari anime buatan Jepang maupun buatan di luar Jepang. Selain itu terdapat banyak genre dan banyaknya _anime_ yang telah ada membuat orang yang sering maupun baru ingin menonton mengalami kesulitan dalam menentukan pilihan mereka, sehingga diperlukan sebuah sistem yang dapat memberikan rekomendasi _anime_ ke penonton ​(Jayaperwira  et  al., 2023)​.

</p>

<p  style='text-align: justify;'>

Sistem rekomendasi adalah sebuah algoritma atau program yang dapat membantu keputusan pengguna dengan memberikan informasi atau rekomendasi yang dibutuhkan​(Girsang et  al., 2020)​. Sistem rekomendasi dapat memberikan rekomendasi berdasarkan data yang sudah dimiliki oleh pengguna maupun data yang dimasukkan oleh pengguna ​(Jayaperwira  et  al., 2023)​.

</p>

<p  style='text-align: justify;'>

Banyak peneliti yang telah melakukan penelitian mengenai sistem rekomendasi untuk _anime_. Penelitian yang dilakukan oleh ​(Jayaperwira  et  al., 2023)​ menjelaskan sistem rekomendasi yang dibangun menggunakan _KNNWithMeans_ mendapatkan hasil _MAE_ dengan nilai 0.8989. Pada penelitian yang dilakukan oleh ​(Girsang et  al., 2020)​ menjelaskan sistem rekomendasi yang dibangun menggunakan model _Alternating  Least  Squares (ALS)_ memberikan hasil _RMSE_ dengan nilai 2.537. Dan pada penelitian yang dilakukan oleh ​(Reynaldi & Istiono, 2023)​ menjelaskan sistem rekomendasi yang dibangun dengan metode _Content-Based  Filtering_ memberikan hasil _Precission_ dan _Accuration_ sebesar 100% dan skor kepuasan pengguna menggunakan perhitungan _DeLone  and  McLean  Method_ dengan skor sebesar 74.23%.

</p>

## Business Understanding

### Problem Statement

Berdasarkan uraian diatas, dapat ditarik sebagai berikut

- Bagaimana perkembangan tren _anime_ saat ini?
- Sistem rekomendasi seperti apa yang dapat membantu pengguna dalam memilih _anime_ yang diinginkan?

### Goal

Tujuan dari proyek ini adalah:

- Melakukan analisis pada _dataset_ dengan teknik _Exploratory Data Analysis (EDA)_ untuk mendapatkan perkembangan tren _anime_ saat ini
- Membangun sistem rekomendasi _anime_ yang menggunakan pendekatan _Content Based Filtering_ dan _Colaborative Based Filtering_ sehingga penonton ataupun calon penonton mendapatkan rekomendasi _Anime_ yang sesuai dengan _anime_ yang terakhir ditonton ataupun berdasarkan preferensi dirinya.


### Solution Approach

Tahapan untuk menyelesaikan tujuan dari proyek ini adalah sebagai berikut.

1. Melakukan *Exploratory Data Analysis (EDA)* untuk melakukan pembersihan data, visualisasi diagram dan analisis mengenai tren _Anime_ hingga tahun 2020

2. Membangun model sistem prediksi dimana akan menggunakan dua pendekatan, yaitu **_Content Based Filtering_** yaitu dengan memberikan rekomendasi berdasarkan _Anime_ yang pernah ditonton pengguna dengan mengukur kesamaan _anime_ berdasarkan genre dan **_Collaborative Based Filtering_** yaitu dengan memberikan rekomendasi berdasarkan _Anime_ yang pernah ditonton dan di-_rating_ oleh pengguna lainnya

3.  Untuk model dengan pendekatan **_Content Based Filtering_**, model akan dibangun menggunakan 2 metode, yaitu menggunakan **_Cosine Similarity_** dan **_euclidean Distance_**. Sedangkan untuk model dengan pendekatan **_Collaborative Based Filtering_** akan dibangun menggunakan model **RecommenderNet** dengan  _Optimizer_ yang berbeda, yaitu **_Adam_** dan **_RMSprop_**

4. Pengujian akan menggunakan metode **_Precission_** untuk pendekatan **_Content Based Filtering_** dan **_Root Mean Square Error_** untuk pendekatan **_Collaborative Based Filtering_**

## Data Understanding

_Dataset_ yang digunakan adalah _dataset Anime Recommendation Database 2020_ dari _kaggle_ [berikut] (https://www.kaggle.com/datasets/hernan4444/anime-recommendation-database-2020).

![Sumber Dataset](https://cdn.discordapp.com/attachments/1121095008926302358/1126199942441086996/image.png)

<p align = "center">  
Gambar 1. Sumber _dataset_ dalam proyek ini
</p>

Data ini merupakan data yang dikumpulkan dari _[MyAnimeList.net](https://myanimelist.net/)_ sebuah situs yang berisi berbagai informasi mengenai _Anime_ dan _Manga_. _Dataset_ ini memiliki data pengguna sebesar 320.000 dan 16.000 _Anime_ hingga tahun 2020 dimana informasi yang disimpan sebagai berikut.

* Daftar _anime_ tiap pengguna, termasuk _anime_ yang memiliki status _dropped_, ditamatkan, direncanakan untuk di tonton, sedang ditonton atau _on hold_
* Penilaian yang diberikan oleh pengguna terhadap _anime_ yang sudah tamat di tonton, sedang ditonton ataupun _on hold_
* Informasi mengenai _anime_ seperti genre, stats, studio_, dan sebagainya
* _HTML file_ dengan informasi _anime_ hasil _scrapping_

Untuk file  _csv_, terdapat 5 file  _csv_, yaitu

1.  `anime.csv`
2.  `anime_with_synopsis.csv`
3.  `animelist.csv`
4.  `rating_complete.csv`
5.  `watching_status.csv`

dimana jumlah data yang disimpan untuk 4 variabel (kecuali `watching_status` karena berisi indeks `watching_status` akan dibahas nanti) sebagai berikut.

```
Jumlah Seluruh Data Anime : 17562
Jumlah Data Anime dengan Sinopsis : 16214
Jumlah Data Anime yang Ditambah User : 17562
Jumlah Data Anime yang Dirating User Setelah Tamat : 16872
```

### Univariate Exploratory Data Analysis

Variabel-variabel pada dataset ini adalah

-   **anime_df**  - Berisi informasi  _anime_  secara general seperti  _genre, stats, studio_, dan sebagainya
-   **anime_sypnopsis_df**  - Berisi informasi  _anime_  yang lebih ringkas dibandingkan dengan  **anime_df**  namun ditambah dengan sinopsis setiap  _anime_
-   **anime_list_df**  - Berisi daftar  _anime_  yang didaftarkan oleh pengguna dengan skor  _rating_, status  _watching_  dan jumlah episode yang sudah ditonton
-   **rating_complete_df**  - Berisi daftar  _rating_  setiap  _anime_  dengan  _watching status_  adalah  **2**  yang berarti tamat ditonton
-   **watching_status_df**  - Berisi daftar kode status  _watching_  untuk kolom "watching_list" di variabel  **anime_list_df**

Tahapan-tahapan yang dilakukan pada _Exploratory Data Analysis_ ini adalah

- Penjelasan setiap variabel
- Analisis 20 _anime_ paling populer, paling banyak ditamatkan, paling banyak di-_drop_, dan _anime_ dengan skor tertinggi
- Analisis distribusi _anime_ berdasarkan musim dan distribusi skor
- Analisis fitur _genre, type_, dan _watching status_

#### Anime Variable
```
RangeIndex: 17562 entries, 0 to 17561
Data columns (total 35 columns):
 #   Column         Non-Null Count  Dtype 
---  ------         --------------  ----- 
 0   MAL_ID         17562 non-null  int64 
 1   Name           17562 non-null  object
 2   Score          17562 non-null  object
 3   Genres         17562 non-null  object
 4   English name   17562 non-null  object
 5   Japanese name  17562 non-null  object
 6   Type           17562 non-null  object
 7   Episodes       17562 non-null  object
 8   Aired          17562 non-null  object
 9   Premiered      17562 non-null  object
 10  Producers      17562 non-null  object
 11  Licensors      17562 non-null  object
 12  Studios        17562 non-null  object
 13  Source         17562 non-null  object
 14  Duration       17562 non-null  object
 15  Rating         17562 non-null  object
 16  Ranked         17562 non-null  object
 17  Popularity     17562 non-null  int64 
 18  Members        17562 non-null  int64 
 19  Favorites      17562 non-null  int64 
 20  Watching       17562 non-null  int64 
 21  Completed      17562 non-null  int64 
 22  On-Hold        17562 non-null  int64 
 23  Dropped        17562 non-null  int64 
 24  Plan to Watch  17562 non-null  int64 
 25  Score-10       17562 non-null  object
 26  Score-9        17562 non-null  object
 27  Score-8        17562 non-null  object
 28  Score-7        17562 non-null  object
 29  Score-6        17562 non-null  object
 30  Score-5        17562 non-null  object
 31  Score-4        17562 non-null  object
 32  Score-3        17562 non-null  object
 33  Score-2        17562 non-null  object
 34  Score-1        17562 non-null  object
dtypes: int64(9), object(26)
```

Berdasarkan variabel dari  _file anime_, terdapat 17562 data dan terdapat 35 kolom dimana variabel dimana penjelasan kolomnya adalah sebagai berikut

-   **MAL_ID**  : ID  _anime_  yang dicatat di  _MyAnimeList_
-   **Name**  : Judul lengkap  _anime_
-   **Score**  :  _Rating_  rata-rata dari seluruh pengguna yang telah menilai  _anime_  tersebut
-   **Genres**  : Kumpulan  _genre_  dari sebuah  _anime_
-   **English name**  : Judul  _anime_  dalam Bahasa Inggris
-   **Japanese name**  : Judul  _anime_  dalam aksara Jepang
-   **Type**  : Tipe/format penayangan  _anime_, seperti  **TV, Movie, OVA**
-   **Episodes**  : Jumlah episode
-   **Aired**  : Tanggal rilis/penayangan perdana
-   **Premiered**  : Musim penayangan perdana
-   **Producers**  : Produser yang menaungi produksi  _anime_
-   **Studios**  : Studio utama  _anime_  tersebut diproduksi
-   **Source**  : Sumber material dari  _anime_, seperti  _Manga, Visual Novel, Light Novel_  atau  _Original_
-   **Duration**  : Durasi  _anime_  dalam sekali tayang per episode
-   **Rating**  :  _Rating_  usia penonton
-   **Ranked**  : Posisi ranking berdasarkan skor  _rating_  rata-rata
-   **Popularity**  : Posisi popularitas berdasarkan jumlah pengguna yang menambahkan  _anime_  tersebut di dalam daftar  _anime_-nya
-   **Members**  : Jumlah pengguna yang menambahkan  _anime_  tersebut di daftar  _anime_  pada akun mereka
-   **Favorites**  : Jumlah pengguna yang memfavoritkan  _anime_  tersebut
-   **Watching**  : Jumlah pengguna yang menonton  _anime_  tersebut
-   **Completed**  : Jumlah pengguna yang menamatkan  _anime_  tersebut
-   **On-Hold**  : Jumlah pengguna yang berhenti sementara menonton  _anime_  tersebut
-   **Dropped**  : Jumlah pengguna yang tidak melanjutkan menonton  _anime_  tersebut
-   **Plan to Watch**  : Jumlah pengguna yang berencana menonton  _anime_  tersebut
-   **Score-10**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 10
-   **Score-9**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 9
-   **Score-8**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 8
-   **Score-7**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 7
-   **Score-6**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 6
-   **Score-5**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 5
-   **Score-4**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 4
-   **Score-3**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 3
-   **Score-2**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 2
-   **Score-1**  : Jumlah pengguna yang memberikan skor /  _rating_  dengan nilai 1

#### Anime With Sypnopsis Variable

```
RangeIndex: 16214 entries, 0 to 16213
Data columns (total 5 columns):
 #   Column     Non-Null Count  Dtype 
---  ------     --------------  ----- 
 0   MAL_ID     16214 non-null  int64 
 1   Name       16214 non-null  object
 2   Score      16214 non-null  object
 3   Genres     16214 non-null  object
 4   sypnopsis  16206 non-null  object
dtypes: int64(1), object(4)
```

Berdasarkan dari variabel berikut, terdapat 16214 data dan terdapat 5 kolom dimana variabel dimana penjelasan kolomnya adalah sebagai berikut

-   **MAL_ID**  : ID  _anime_  yang dicatat di  _MyAnimeList_
-   **Name**  : Judul lengkap  _anime_
-   **Score**  :  _Rating_  rata-rata dari seluruh pengguna yang telah menilai  _anime_  tersebut
-   **Genres**  : Kumpulan  _genre_  dari sebuah  _anime_
-   **synopsis**  : Sinopsis dari  _anime_

#### Anime List Variable

```
RangeIndex: 109224747 entries, 0 to 109224746
Data columns (total 5 columns):
 #   Column            Dtype
---  ------            -----
 0   user_id           int64
 1   anime_id          int64
 2   rating            int64
 3   watching_status   int64
 4   watched_episodes  int64
dtypes: int64(5)
```

Berdasarkan dari variabel berikut, jika melihat dari  _RangeIndex_  terdapat 109.224.747 data dan terdapat 5 kolom dimana variabel dimana penjelasan kolomnya adalah sebagai berikut

-   **user_id**  : ID pengguna secara  _random_  dan tidak terkait dengan id pengguna di  _MyAnimeList_
-   **anime_id**  : ID  _anime_  di  _MyAnimeList_
-   **score**  : Skor atau  _rating_  yang diberi pengguna terhadap  _anime_  tersebut. Skor 0 menunjukkan pengguna tidak memberikan skor/_rating_
-   **watching_status**  : ID Status nonton dari pengguna berdasarkan variabel  **watching_status_df**
-   **watched_episodes**  : Jumlah episode yang sudah ditonton pengguna

#### Watching Status Variable

```
RangeIndex: 5 entries, 0 to 4
Data columns (total 2 columns):
 #   Column        Non-Null Count  Dtype 
---  ------        --------------  ----- 
 0   status        5 non-null      int64 
 1    description  5 non-null      object
dtypes: int64(1), object(1)
```

Berdasarkan dari variabel berikut, terdapat 5 data dan terdapat 2 kolom dimana variabel dimana penjelasan kolomnya adalah sebagai berikut

-   **status**  : ID status nonton dari pengguna untuk kolom "watching_status" di variabel  **anime_list_df**
-   **description**  : Deskripsi dari ID status

Variabel ini dipakai sebagai  _indexing_  atau penanda untuk kolom "watching_status" di variabel  **anime_list_df**

#### Rating Complete Variable

```
RangeIndex: 57633278 entries, 0 to 57633277
Data columns (total 3 columns):
 #   Column    Dtype
---  ------    -----
 0   user_id   int64
 1   anime_id  int64
 2   rating    int64
dtypes: int64(3)
```

Berdasarkan dari variabel berikut, terdapat 57.633.278 data dan terdapat 3 kolom dimana variabel dimana penjelasan kolomnya adalah sebagai berikut

-   **user_id**  : ID pengguna secara  _random_  dan tidak terkait dengan id pengguna di  _MyAnimeList_
-   **anime_id**  : ID  _anime_  di  _MyAnimeList_
-   **rating**  :  _rating_  atau skor yang diberikan pengguna

#### 20 _Anime_ Terbaik Berdasarkan Popularitas

|       | Name                             |   Score | Genres                                                              | Type   |   Episodes | Aired                        | Premiered   |   Popularity |
|------:|:---------------------------------|--------:|:--------------------------------------------------------------------|:-------|-----------:|:-----------------------------|:------------|-------------:|
|  1393 | Death Note                       |    8.63 | Mystery, Police, Psychological, Supernatural, Thriller, Shounen     | TV     |         37 | Oct 4, 2006 to Jun 27, 2007  | Fall 2006   |            1 |
|  7449 | Shingeki no Kyojin               |    8.48 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         25 | Apr 7, 2013 to Sep 29, 2013  | Spring 2013 |            2 |
|  3971 | Fullmetal Alchemist: Brotherhood |    9.19 | Action, Military, Adventure, Comedy, Drama, Magic, Fantasy, Shounen | TV     |         64 | Apr 5, 2009 to Jul 4, 2010   | Spring 2009 |            3 |
|  6614 | Sword Art Online                 |    7.25 | Action, Game, Adventure, Romance, Fantasy                           | TV     |         25 | Jul 8, 2012 to Dec 23, 2012  | Summer 2012 |            4 |
| 10451 | One Punch Man                    |    8.57 | Action, Sci-Fi, Comedy, Parody, Super Power, Supernatural           | TV     |         12 | Oct 5, 2015 to Dec 21, 2015  | Fall 2015   |            5 |
| 11185 | Boku no Hero Academia            |    8.11 | Action, Comedy, School, Shounen, Super Power                        | TV     |         13 | Apr 3, 2016 to Jun 26, 2016  | Spring 2016 |            6 |
|  8646 | Tokyo Ghoul                      |    7.81 | Action, Mystery, Horror, Psychological, Supernatural, Drama, Seinen | TV     |         12 | Jul 4, 2014 to Sep 19, 2014  | Summer 2014 |            7 |
|    10 | Naruto                           |    7.91 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen       | TV     |        220 | Oct 3, 2002 to Feb 8, 2007   | Fall 2002   |            8 |
|  5683 | Steins;Gate                      |    9.11 | Thriller, Sci-Fi                                                    | TV     |         24 | Apr 6, 2011 to Sep 14, 2011  | Spring 2011 |            9 |
|  8148 | No Game No Life                  |    8.2  | Game, Adventure, Comedy, Supernatural, Ecchi, Fantasy               | TV     |         12 | Apr 9, 2014 to Jun 25, 2014  | Spring 2014 |           10 |
| 11308 | Kimi no Na wa.                   |    8.96 | Romance, Supernatural, School, Drama                                | Movie  |          1 | Aug 26, 2016                 | Unknown     |           11 |
|  6474 | Hunter x Hunter (2011)           |    9.1  | Action, Adventure, Fantasy, Shounen, Super Power                    | TV     |        148 | Oct 2, 2011 to Sep 24, 2014  | Fall 2011   |           12 |
| 11914 | Boku no Hero Academia 2nd Season |    8.33 | Action, Comedy, Super Power, School, Shounen                        | TV     |         25 | Apr 1, 2017 to Sep 30, 2017  | Spring 2017 |           13 |
|  1431 | Code Geass: Hangyaku no Lelouch  |    8.72 | Action, Military, Sci-Fi, Super Power, Drama, Mecha, School         | TV     |         25 | Oct 6, 2006 to Jul 29, 2007  | Fall 2006   |           15 |
|  4636 | Angel Beats!                     |    8.15 | Action, Comedy, Drama, School, Supernatural                         | TV     |         13 | Apr 3, 2010 to Jun 26, 2010  | Spring 2010 |           15 |
|  9383 | Shingeki no Kyojin Season 2      |    8.45 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         12 | Apr 1, 2017 to Jun 17, 2017  | Spring 2017 |           16 |
|  3564 | Toradora!                        |    8.24 | Slice of Life, Comedy, Romance, School                              | TV     |         25 | Oct 2, 2008 to Mar 26, 2009  | Fall 2008   |           17 |
|  8292 | Noragami                         |    8.01 | Action, Adventure, Comedy, Supernatural, Shounen                    | TV     |         12 | Jan 5, 2014 to Mar 23, 2014  | Winter 2014 |           18 |
|  1574 | Naruto: Shippuuden               |    8.16 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen       | TV     |        500 | Feb 15, 2007 to Mar 23, 2017 | Winter 2007 |           18 |
|  6295 | Mirai Nikki                      |    7.54 | Action, Mystery, Psychological, Shounen, Supernatural, Thriller     | TV     |         26 | Oct 9, 2011 to Apr 15, 2012  | Fall 2011   |           19 |

<p align = "center">  
Tabel 1. 20 <i>anime</i> yang paling populer
</p>

Berdasarkan tabel 1 berikut, mayoritas _anime_ yang paling populer adalah _anime_ dengan _genre Action_ , selain itu hampir seluruh _anime_ yang populer dibuat dalam format TV dan hanya satu _Movie_ yaitu _Kimi no Na Wa_. Kemudian _score_ untuk _anime_ di tabel berikut berada diatas 7 dengan skor terendah adalah 7.2 yang dimiliki oleh _Sword Art Online_ dan rata-rata skor adalah 8.346.

#### 20 _Anime_ yang Paling Banyak Ditamatin

|       | Name                             |   Score | Genres                                                              | Type   |   Episodes | Aired                       | Premiered   |   Completed |
|------:|:---------------------------------|--------:|:--------------------------------------------------------------------|:-------|-----------:|:----------------------------|:------------|------------:|
|  7449 | Shingeki no Kyojin               |    8.48 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         25 | Apr 7, 2013 to Sep 29, 2013 | Spring 2013 |     2182587 |
|  1393 | Death Note                       |    8.63 | Mystery, Police, Psychological, Supernatural, Thriller, Shounen     | TV     |         37 | Oct 4, 2006 to Jun 27, 2007 | Fall 2006   |     2146116 |
|  6614 | Sword Art Online                 |    7.25 | Action, Game, Adventure, Romance, Fantasy                           | TV     |         25 | Jul 8, 2012 to Dec 23, 2012 | Summer 2012 |     1907261 |
| 10451 | One Punch Man                    |    8.57 | Action, Sci-Fi, Comedy, Parody, Super Power, Supernatural           | TV     |         12 | Oct 5, 2015 to Dec 21, 2015 | Fall 2015   |     1841220 |
| 11185 | Boku no Hero Academia            |    8.11 | Action, Comedy, School, Shounen, Super Power                        | TV     |         13 | Apr 3, 2016 to Jun 26, 2016 | Spring 2016 |     1655900 |
|  3971 | Fullmetal Alchemist: Brotherhood |    9.19 | Action, Military, Adventure, Comedy, Drama, Magic, Fantasy, Shounen | TV     |         64 | Apr 5, 2009 to Jul 4, 2010  | Spring 2009 |     1644938 |
|  8646 | Tokyo Ghoul                      |    7.81 | Action, Mystery, Horror, Psychological, Supernatural, Drama, Seinen | TV     |         12 | Jul 4, 2014 to Sep 19, 2014 | Summer 2014 |     1594880 |
|    10 | Naruto                           |    7.91 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen       | TV     |        220 | Oct 3, 2002 to Feb 8, 2007  | Fall 2002   |     1462223 |
| 11308 | Kimi no Na wa.                   |    8.96 | Romance, Supernatural, School, Drama                                | Movie  |          1 | Aug 26, 2016                | Unknown     |     1462143 |
|  8148 | No Game No Life                  |    8.2  | Game, Adventure, Comedy, Supernatural, Ecchi, Fantasy               | TV     |         12 | Apr 9, 2014 to Jun 25, 2014 | Spring 2014 |     1426896 |
| 11914 | Boku no Hero Academia 2nd Season |    8.33 | Action, Comedy, Super Power, School, Shounen                        | TV     |         25 | Apr 1, 2017 to Sep 30, 2017 | Spring 2017 |     1389299 |
|  9383 | Shingeki no Kyojin Season 2      |    8.45 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         12 | Apr 1, 2017 to Jun 17, 2017 | Spring 2017 |     1337762 |
|  4636 | Angel Beats!                     |    8.15 | Action, Comedy, Drama, School, Supernatural                         | TV     |         13 | Apr 3, 2010 to Jun 26, 2010 | Spring 2010 |     1229098 |
|  1431 | Code Geass: Hangyaku no Lelouch  |    8.72 | Action, Military, Sci-Fi, Super Power, Drama, Mecha, School         | TV     |         25 | Oct 6, 2006 to Jul 29, 2007 | Fall 2006   |     1209288 |
|  8551 | Sword Art Online II              |    6.79 | Action, Game, Adventure, Romance, Fantasy                           | TV     |         24 | Jul 5, 2014 to Dec 20, 2014 | Summer 2014 |     1199824 |
|  3564 | Toradora!                        |    8.24 | Slice of Life, Comedy, Romance, School                              | TV     |         25 | Oct 2, 2008 to Mar 26, 2009 | Fall 2008   |     1191775 |
|  8292 | Noragami                         |    8.01 | Action, Adventure, Comedy, Supernatural, Shounen                    | TV     |         12 | Jan 5, 2014 to Mar 23, 2014 | Winter 2014 |     1181215 |
|  6295 | Mirai Nikki                      |    7.54 | Action, Mystery, Psychological, Shounen, Supernatural, Thriller     | TV     |         26 | Oct 9, 2011 to Apr 15, 2012 | Fall 2011   |     1154210 |
|  9886 | Koe no Katachi                   |    9    | Drama, School, Shounen                                              | Movie  |          1 | Sep 17, 2016                | Unknown     |     1151644 |
|  9011 | Nanatsu no Taizai                |    7.89 | Action, Adventure, Ecchi, Fantasy, Magic, Shounen, Supernatural     | TV     |         24 | Oct 5, 2014 to Mar 29, 2015 | Fall 2014   |     1151443 |

<p align = "center">  
Tabel 2. 20 <i>anime</i> yang paling banyak ditamatin
</p>

Berdasarkan tabel berikut, seperti pada bagian 20 _anime_ yang paling populer, mayoritas _anime_ yang paling paling banyak ditamatin adalah _anime_ dengan _genre Action_ . Selain itu hampir seluruh _anime_ yang paling banyak ditamatin dibuat dalam format TV dan hanya dua _Movie_ yaitu _Kimi no Na Wa_ dan _Koe no Katachi_. Kedua _movie_ tersebut adalah film dengan skor yang tinggi, yaitu 8.96 dan 9.0. Kemudian _score_ untuk _anime_ di tabel berikut berada diatas 6 dengan skor terendah adalah 6.79 yang dimiliki oleh _Sword Art Online II_ dan rata-rata skor adalah 8.2115. Beberapa _anime_ di daftar ini juga termasuk dalam 20 _anime_ paling populer, terutama 6 besar di tabel tersebut.

#### 20 _Anime_ yang paling banyak di-_drop_

|       | Name                            |   Score | Genres                                                                                        | Type   | Episodes   | Aired                        | Premiered   |   Dropped |
|------:|:--------------------------------|--------:|:----------------------------------------------------------------------------------------------|:-------|:-----------|:-----------------------------|:------------|----------:|
|   245 | Bleach                          |    7.8  | Action, Adventure, Comedy, Super Power, Supernatural, Shounen                                 | TV     | 366        | Oct 5, 2004 to Mar 27, 2012  | Fall 2004   |    174710 |
|  4707 | Fairy Tail                      |    7.68 | Action, Adventure, Comedy, Magic, Fantasy, Shounen                                            | TV     | 175        | Oct 12, 2009 to Mar 30, 2013 | Fall 2009   |    148408 |
|    11 | One Piece                       |    8.52 | Action, Adventure, Comedy, Super Power, Drama, Fantasy, Shounen                               | TV     | Unknown    | Oct 20, 1999 to ?            | Fall 1999   |    136245 |
|  1574 | Naruto: Shippuuden              |    8.16 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen                                 | TV     | 500        | Feb 15, 2007 to Mar 23, 2017 | Winter 2007 |    124253 |
| 12492 | Boruto: Naruto Next Generations |    5.81 | Action, Adventure, Super Power, Martial Arts, Shounen                                         | TV     | Unknown    | Apr 5, 2017 to ?             | Spring 2017 |    113677 |
|    10 | Naruto                          |    7.91 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen                                 | TV     | 220        | Oct 3, 2002 to Feb 8, 2007   | Fall 2002   |     99806 |
|  6614 | Sword Art Online                |    7.25 | Action, Game, Adventure, Romance, Fantasy                                                     | TV     | 25         | Jul 8, 2012 to Dec 23, 2012  | Summer 2012 |     90661 |
| 12493 | Black Clover                    |    7.38 | Action, Comedy, Magic, Fantasy, Shounen                                                       | TV     | 170        | Oct 3, 2017 to Mar 30, 2021  | Fall 2017   |     89594 |
|  1393 | Death Note                      |    8.63 | Mystery, Police, Psychological, Supernatural, Thriller, Shounen                               | TV     | 37         | Oct 4, 2006 to Jun 27, 2007  | Fall 2006   |     80834 |
|  7939 | Kill la Kill                    |    8.11 | Action, Comedy, Super Power, Ecchi, School                                                    | TV     | 24         | Oct 4, 2013 to Mar 28, 2014  | Fall 2013   |     67845 |
|  8551 | Sword Art Online II             |    6.79 | Action, Game, Adventure, Romance, Fantasy                                                     | TV     | 24         | Jul 5, 2014 to Dec 20, 2014  | Summer 2014 |     67243 |
|  3155 | Soul Eater                      |    7.88 | Action, Fantasy, Comedy, Supernatural, Shounen                                                | TV     | 51         | Apr 7, 2008 to Mar 30, 2009  | Spring 2008 |     65962 |
|  6295 | Mirai Nikki                     |    7.54 | Action, Mystery, Psychological, Shounen, Supernatural, Thriller                               | TV     | 26         | Oct 9, 2011 to Apr 15, 2012  | Fall 2011   |     55337 |
| 13292 | Darling in the FranXX           |    7.33 | Action, Drama, Mecha, Romance, Sci-Fi                                                         | TV     | 24         | Jan 13, 2018 to Jul 7, 2018  | Winter 2018 |     53880 |
|  8585 | Fairy Tail (2014)               |    7.73 | Action, Adventure, Comedy, Fantasy, Magic, Shounen                                            | TV     | 102        | Apr 5, 2014 to Mar 26, 2016  | Spring 2014 |     50700 |
|  6376 | Guilty Crown                    |    7.52 | Action, Sci-Fi, Super Power, Drama, Romance, Mecha                                            | TV     | 22         | Oct 14, 2011 to Mar 23, 2012 | Fall 2011   |     48643 |
|   494 | Pokemon                         |    7.34 | Action, Adventure, Comedy, Kids, Fantasy                                                      | TV     | 276        | Apr 1, 1997 to Nov 14, 2002  | Spring 1997 |     47875 |
|   225 | InuYasha                        |    7.85 | Action, Adventure, Comedy, Historical, Demons, Supernatural, Magic, Romance, Fantasy, Shounen | TV     | 167        | Oct 16, 2000 to Sep 13, 2004 | Fall 2000   |     47273 |
|  3873 | Kuroshitsuji                    |    7.75 | Action, Mystery, Comedy, Historical, Demons, Supernatural, Shounen                            | TV     | 24         | Oct 3, 2008 to Mar 27, 2009  | Fall 2008   |     46856 |
|  8625 | Akame ga Kill!                  |    7.53 | Action, Adventure, Drama, Fantasy, Shounen                                                    | TV     | 24         | Jul 7, 2014 to Dec 15, 2014  | Summer 2014 |     45684 |

<p align = "center">  
Tabel 3. 20 <i>anime</i> yang paling banyak di-<i>drop</i>
</p>

_Dropping_ atau _Anime_ yang di-_drop_ merupakan suatu kondisi atau status dimana penonton berhenti melanjutkan menonton judul _anime_ tersebut. Banyak faktor yang menyebabkan seseorang berhenti menonton judul _anime_ tertentu, seperti cerita yang membosankan, grafis yang kurang baik, ataupun cerita yang tidak sesuai dengan ekspektasi dan selera penonton, terutama jika _anime_ tersebut merupakan adaptasi dari media lainnya seperti _manga, Light Novel_ atau _Visual Novel_. 

Berdasarkan tabel 3 diatas, mayoritas _anime_ yang paling paling banyak di-_drop_ adalah _anime_ dengan _genre Action_. Fakta yang cukup menarik adalah 5 _anime_ yang paling banyak di-_drop_ adalah _anime_ yang populer, yaitu _Bleach, Fairy Tail, One Piece, Naruto: Shipuuden,_ dan _Boruto: Naruto Next Generations_. Kemudian _score_ untuk _anime_ di tabel berikut berada diatas 6 dengan skor terrendah adalah 5.81 yang dimiliki oleh _Boruto: Naruto Next Generations_ dan rata-rata skor adalah 7.6255. 

#### Distribusi Penayangan _Anime_ Berdasarkan Musim Tayang

_Anime_ biasanya akan ditayangkan berdasarkan musim tayang. Musim tayang tersebut diambil dari 4 musim yang terjadi di Jepang, yaitu musim semi, panas, gugur dan dingin.

![Grafik distribusi musim penayangan](https://media.discordapp.net/attachments/1121095008926302358/1126206133644824627/distribusi_musim_tayang.png)

<p align = "center">  
Gambar 2. Grafik Distribusi <i>Anime</i> Berdasarkan Musim Tayang
</p>

Berdasarkan grafik diatas, _anime_ paling banyak ditayangkan di musim semi dengan persentase 34% dan 1611 judul. Diikuti dengan musim gugur dengan persentase 29.3% dan 1389 judul. Kemudian musim dingin dengan persentase 19.9% dan 942. Dan terakhir musim panas dengan persentase 16.9% dan 803 judul.

#### 20 _Anime_ yang Paling Banyak Ditambahkan ke Daftar _Anime_

|       | Name                             |   Score | Genres                                                              | Type   |   Episodes | Aired                        | Premiered   |   Members |
|------:|:---------------------------------|--------:|:--------------------------------------------------------------------|:-------|-----------:|:-----------------------------|:------------|----------:|
|  1393 | Death Note                       |    8.63 | Mystery, Police, Psychological, Supernatural, Thriller, Shounen     | TV     |         37 | Oct 4, 2006 to Jun 27, 2007  | Fall 2006   |   2589552 |
|  7449 | Shingeki no Kyojin               |    8.48 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         25 | Apr 7, 2013 to Sep 29, 2013  | Spring 2013 |   2531397 |
|  3971 | Fullmetal Alchemist: Brotherhood |    9.19 | Action, Military, Adventure, Comedy, Drama, Magic, Fantasy, Shounen | TV     |         64 | Apr 5, 2009 to Jul 4, 2010   | Spring 2009 |   2248456 |
|  6614 | Sword Art Online                 |    7.25 | Action, Game, Adventure, Romance, Fantasy                           | TV     |         25 | Jul 8, 2012 to Dec 23, 2012  | Summer 2012 |   2214395 |
| 10451 | One Punch Man                    |    8.57 | Action, Sci-Fi, Comedy, Parody, Super Power, Supernatural           | TV     |         12 | Oct 5, 2015 to Dec 21, 2015  | Fall 2015   |   2123866 |
| 11185 | Boku no Hero Academia            |    8.11 | Action, Comedy, School, Shounen, Super Power                        | TV     |         13 | Apr 3, 2016 to Jun 26, 2016  | Spring 2016 |   1909814 |
|  8646 | Tokyo Ghoul                      |    7.81 | Action, Mystery, Horror, Psychological, Supernatural, Drama, Seinen | TV     |         12 | Jul 4, 2014 to Sep 19, 2014  | Summer 2014 |   1895488 |
|    10 | Naruto                           |    7.91 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen       | TV     |        220 | Oct 3, 2002 to Feb 8, 2007   | Fall 2002   |   1830540 |
|  5683 | Steins;Gate                      |    9.11 | Thriller, Sci-Fi                                                    | TV     |         24 | Apr 6, 2011 to Sep 14, 2011  | Spring 2011 |   1771162 |
|  8148 | No Game No Life                  |    8.2  | Game, Adventure, Comedy, Supernatural, Ecchi, Fantasy               | TV     |         12 | Apr 9, 2014 to Jun 25, 2014  | Spring 2014 |   1751054 |
| 11308 | Kimi no Na wa.                   |    8.96 | Romance, Supernatural, School, Drama                                | Movie  |          1 | Aug 26, 2016                 | Unknown     |   1726660 |
|  6474 | Hunter x Hunter (2011)           |    9.1  | Action, Adventure, Fantasy, Shounen, Super Power                    | TV     |        148 | Oct 2, 2011 to Sep 24, 2014  | Fall 2011   |   1673924 |
| 11914 | Boku no Hero Academia 2nd Season |    8.33 | Action, Comedy, Super Power, School, Shounen                        | TV     |         25 | Apr 1, 2017 to Sep 30, 2017  | Spring 2017 |   1611771 |
|  4636 | Angel Beats!                     |    8.15 | Action, Comedy, Drama, School, Supernatural                         | TV     |         13 | Apr 3, 2010 to Jun 26, 2010  | Spring 2010 |   1591773 |
|  9383 | Shingeki no Kyojin Season 2      |    8.45 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         12 | Apr 1, 2017 to Jun 17, 2017  | Spring 2017 |   1591506 |
|  1431 | Code Geass: Hangyaku no Lelouch  |    8.72 | Action, Military, Sci-Fi, Super Power, Drama, Mecha, School         | TV     |         25 | Oct 6, 2006 to Jul 29, 2007  | Fall 2006   |   1583882 |
|  3564 | Toradora!                        |    8.24 | Slice of Life, Comedy, Romance, School                              | TV     |         25 | Oct 2, 2008 to Mar 26, 2009  | Fall 2008   |   1567792 |
|  1574 | Naruto: Shippuuden               |    8.16 | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen       | TV     |        500 | Feb 15, 2007 to Mar 23, 2017 | Winter 2007 |   1543765 |
|  8292 | Noragami                         |    8.01 | Action, Adventure, Comedy, Supernatural, Shounen                    | TV     |         12 | Jan 5, 2014 to Mar 23, 2014  | Winter 2014 |   1535575 |
|  6295 | Mirai Nikki                      |    7.54 | Action, Mystery, Psychological, Shounen, Supernatural, Thriller     | TV     |         26 | Oct 9, 2011 to Apr 15, 2012  | Fall 2011   |   1533289 |

<p align = "center">  
Tabel 4. 20 <i>anime</i> yang paling banyak ditambahkan ke <i>Daftar Anime</i>
</p>

Setiap pengguna _MyAnimeList_ akan memiliki 2 daftar, yaitu daftar _anime_ dan _manga_. Daftar _anime_ berbeda dengan _favorite_ dimana pada daftar _anime_, pengguna dapat memberikan _rating_, jumlah episode yang sudah ditonton dan status tonton.

Berdasarkan tabel 4 berikut, yang paling paling banyak ditambahkan pengguna adalah _anime_ dengan _genre Action_. Mayoritas _anime_ tersebut juga merupakan _anime_ yang paling populer.

#### Score Feature

Sebelum melakukan analisis distribusi skor dan mencari _anime_ dengan skor tertinggi, perlu dilakukan analisis mengenai data skor.

```
array(['8.78', '8.39', '8.24', '7.27', '6.98', '7.95', '8.06', '7.59',
       '8.15', '8.76', '7.91', '8.52', '7.9', '6.38', '7.94', '7.42',
       '7.76', '7.32', '7.51', '8.32', '7.45', '8.51', '8.49', '8.29',
       '8.73', '8.31', '7.56', '8.17', '7.35', '6.31', '7.26', '7.14',
       '7.1', '6.53', '5.91', '7.05', '7.43', '7.66', '7.2', '6.77',
       '6.62', '7.44', '7.65', '7.98', '7.58', '7.38', '6.35', '8.07',
       '7.96', '7.3', '7.99', '7.09', '7.78', '8.03', '6.79', '7.92',
       '6.66', '7.68', '6.67', '6.76', '7.72', '7.79', '7.22', '7.7',
       '7.82', '7.46', '7.31', '7.48', '7.39', '7.23', '6.46', '7.29',
       '6.81', '7.63', '6.83', '4.95', '7.93', '6.97', '6.85', '6.56',
       '7.69', '7.64', '6.86', '6.49', '6.91', '6.96', '7.41', '7.61',
       '6.21', '8.11', '8.42', '8.33', '8.21', '6.14', '6.87', '7.11',
       '7.24', '7.12', '7.28', '6.59', '7.34', '6.34', '7.33', '6.94',
       '6.48', '8.72', '8.53', '6.93', '6.63', '6.19', '7.55', '7.18',
       '6.69', '7.21', '6.37', '8.12', '7.89', '6.11', '7.25', '6.8',
       '7.17', '6.88', '6.55', '8.83', '6.75', '8.5', '7.16', '7.4',
       '7.67', '6.26', '6.02', '6.15', '5.94', '6.28', '7.52', '5.76',
       '6.65', '6.68', '8.0', '6.92', '7.02', '6.18', '8.16', '6.64',
       '8.09', '7.36', '6.45', '8.7', '7.85', '7.07', '7.84', '7.83',
       '6.23', '6.84', '8.75', '8.23', '7.87', '7.8', '7.5', '6.7',
       '7.15', '5.74', '7.03', '6.73', '7.01', '5.93', '6.3', '6.72',
       '6.6', '6.61', '6.32', '7.57', '5.39', '6.01', '6.16', '5.98',
       '6.52', '6.5', '6.0', '7.0', '7.19', '7.49', '6.24', '7.37',
       '5.63', '6.99', '6.29', '7.47', '6.54', '8.22', '6.82', '8.45',
       '7.08', '2.23', '6.47', '6.44', '6.12', '7.88', '8.67', '5.55',
       '8.48', '8.2', '7.6', '7.06', '7.54', '8.69', '8.34', '6.71',
       '6.58', '6.13', '6.17', '5.51', '5.89', '6.06', '7.75', '6.74',
       '7.04', '8.04', '5.27', '6.78', '6.03', '8.25', '7.53', '6.07',
       '8.4', '6.25', '7.71', '7.62', '5.96', '4.93', '6.95', '5.67',
       '5.65', '6.04', '5.58', '8.27', '7.13', '6.9', '5.81', '5.22',
       '5.8', '6.36', '5.16', '6.4', '5.71', '4.75', '6.27', '5.08',
       '5.15', '6.05', '4.96', '5.69', '5.02', '6.09', '5.73', '4.39',
       '8.54', '9.07', '6.41', '5.87', '5.84', '5.77', '5.78', '6.43',
       '6.2', '5.92', '8.01', '8.46', '8.05', '6.89', '5.9', '8.96',
       '5.54', '5.44', '5.66', '4.97', '4.85', '6.57', '5.42', '5.09',
       '5.88', '5.41', '5.7', '8.02', '5.36', '7.97', '5.97', '4.59',
       '5.62', '8.26', '5.99', '5.72', '5.53', '6.51', '5.61', '5.83',
       '5.37', '7.77', '6.33', '5.85', '5.6', '6.08', '5.32', '5.03',
       '5.24', '6.1', '5.43', '5.23', '5.48', '3.15', '5.1', '8.14',
       '8.1', '8.08', '5.75', '4.74', '8.18', '7.73', '7.86', '7.81',
       '8.19', '7.74', '5.25', '8.63', 'Unknown', '5.05', '3.8', '5.64',
       '6.39', '5.49', '5.5', '4.37', '4.61', '4.18', '5.33', '5.28',
       '6.42', '5.79', '4.69', '5.57', '5.46', '5.56', '3.67', '5.18',
       '5.13', '6.22', '5.82', '5.59', '5.68', '4.21', '4.46', '4.71',
       '8.66', '5.38', '5.06', '5.47', '5.17', '4.88', '5.86', '4.49',
       '4.67', '5.29', '5.35', '4.83', '5.52', '5.26', '3.96', '5.21',
       '5.19', '5.45', '5.07', '8.28', '4.42', '5.04', '8.35', '5.14',
       '4.92', '3.35', '4.36', '4.47', '3.28', '5.12', '5.34', '8.91',
       '5.4', '4.62', '4.54', '5.31', '4.65', '4.89', '1.85', '4.98',
       '5.3', '5.95', '4.77', '4.91', '4.73', '3.81', '4.31', '5.0',
       '5.2', '4.81', '4.66', '4.78', '4.68', '8.56', '4.43', '4.86',
       '3.38', '8.57', '4.04', '4.99', '5.01', '8.13', '4.38', '4.48',
       '8.36', '9.19', '8.44', '5.11', '4.63', '4.94', '2.26', '4.12',
       '4.57', '2.5', '8.43', '4.82', '4.9', '4.26', '4.35', '4.08',
       '4.16', '4.87', '4.64', '4.52', '3.69', '2.77', '4.41', '3.61',
       '4.01', '4.8', '3.79', '8.65', '4.79', '8.38', '8.61', '4.24',
       '4.72', '9.11', '3.1', '9.08', '8.6', '4.84', '9.1', '4.29',
       '3.52', '4.19', '8.59', '3.91', '3.26', '3.23', '3.39', '8.37',
       '8.64', '8.58', '4.25', '2.01', '4.6', '9.04', '3.47', '3.51',
       '2.78', '3.55', '4.51', '3.41', '3.32', '3.09', '4.2', '3.19',
       '2.63', '4.4', '3.6', '8.41', '4.0', '8.74', '4.05', '4.58',
       '4.53', '3.72', '4.13', '9.0', '4.5', '4.44', '2.35', '4.17',
       '3.27', '3.76', '3.87', '4.7', '4.76', '4.56', '3.02', '2.3',
       '3.24', '3.82', '4.33', '3.92', '8.82', '8.3', '2.61', '4.28',
       '2.66', '8.87', '4.34', '8.79', '3.84', '3.42', '4.22', '3.58',
       '8.99', '8.93', '8.81', '8.86', '8.84', '8.71', '8.62', '8.68',
       '2.18', '8.88', '9.17', '3.89', '4.06'], dtype=object)

```

Berdasarkan hasil berikut, ditemukan sebuah skor dengan nama "Unknown". Selain itu semua skor menggunakan tipe data _**string**_ dimana terdapat simbol tanda petik di setiap nilai skor. Untuk itu perlu dilakukan 2 tahapan berikut, yaitu

1. Ambik data _anime_ dengan skor bukan "unknown"
2. Hitung rata-rata skor
3. Ganti skor _anime_ yang bernilai "unknown" dengan nilai skor rata-rata
4. Konversi kolom skor ke **_float64_**

Setelah melakukan tahapan berikut, maka sekarang dapat dilakukan analisis distribusi skor _anime_ dengan hasil histogram sebagai berikut.

![histogram skor](https://media.discordapp.net/attachments/1121095008926302358/1126206134152343622/distribusi_score.png)

<p align = "center">  
Gambar 3. Distribusi Skor <i>Anime</i>
</p>

Berdasarkan histogram berikut, mayoritas skor berada di antara 6 hingga 7, kemudian diikuti dengan skor antara 5.5 hingga 6 dan 7 hingga 8.

#### 20 Anime Dengan Skor Tertinggi

|       | Name                                                       |   Score | Genres                                                              | Type   |   Episodes | Aired                        | Premiered   |
|------:|:-----------------------------------------------------------|--------:|:--------------------------------------------------------------------|:-------|-----------:|:-----------------------------|:------------|
|  3971 | Fullmetal Alchemist: Brotherhood                           |    9.19 | Action, Military, Adventure, Comedy, Drama, Magic, Fantasy, Shounen | TV     |         64 | Apr 5, 2009 to Jul 4, 2010   | Spring 2009 |
| 15926 | Shingeki no Kyojin: The Final Season                       |    9.17 | Action, Military, Mystery, Super Power, Drama, Fantasy, Shounen     | TV     |         16 | Dec 7, 2020 to ?             | Winter 2021 |
|  5683 | Steins;Gate                                                |    9.11 | Thriller, Sci-Fi                                                    | TV     |         24 | Apr 6, 2011 to Sep 14, 2011  | Spring 2011 |
| 14963 | Shingeki no Kyojin Season 3 Part 2                         |    9.1  | Action, Drama, Fantasy, Military, Mystery, Shounen, Super Power     | TV     |         10 | Apr 29, 2019 to Jul 1, 2019  | Spring 2019 |
|  6474 | Hunter x Hunter (2011)                                     |    9.1  | Action, Adventure, Fantasy, Shounen, Super Power                    | TV     |        148 | Oct 2, 2011 to Sep 24, 2014  | Fall 2011   |
|  9913 | Gintama°                                                   |    9.1  | Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen        | TV     |         51 | Apr 8, 2015 to Mar 30, 2016  | Spring 2015 |
|  6006 | Gintama'                                                   |    9.08 | Action, Sci-Fi, Comedy, Historical, Parody, Samurai, Shounen        | TV     |         51 | Apr 4, 2011 to Mar 26, 2012  | Spring 2011 |
|   741 | Ginga Eiyuu Densetsu                                       |    9.07 | Military, Sci-Fi, Space, Drama                                      | OVA    |        110 | Jan 8, 1988 to Mar 17, 1997  | Unknown     |
|  7261 | Gintama': Enchousen                                        |    9.04 | Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen        | TV     |         13 | Oct 4, 2012 to Mar 28, 2013  | Fall 2012   |
| 12898 | 3-gatsu no Lion 2nd Season                                 |    9    | Drama, Game, Seinen, Slice of Life                                  | TV     |         22 | Oct 14, 2017 to Mar 31, 2018 | Fall 2017   |
|  9886 | Koe no Katachi                                             |    9    | Drama, School, Shounen                                              | Movie  |          1 | Sep 17, 2016                 | Unknown     |
| 12242 | Gintama.                                                   |    8.99 | Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen        | TV     |         12 | Jan 9, 2017 to Mar 27, 2017  | Winter 2017 |
|  3537 | Clannad: After Story                                       |    8.96 | Slice of Life, Comedy, Supernatural, Drama, Romance                 | TV     |         24 | Oct 3, 2008 to Mar 27, 2009  | Fall 2008   |
|   833 | Gintama                                                    |    8.96 | Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen        | TV     |        201 | Apr 4, 2006 to Mar 25, 2010  | Spring 2006 |
| 11308 | Kimi no Na wa.                                             |    8.96 | Romance, Supernatural, School, Drama                                | Movie  |          1 | Aug 26, 2016                 | Unknown     |
|  7249 | Gintama Movie 2: Kanketsu-hen - Yorozuya yo Eien Nare      |    8.96 | Action, Sci-Fi, Comedy, Historical, Parody, Samurai, Shounen        | Movie  |          1 | Jul 6, 2013                  | Unknown     |
| 12933 | Owarimonogatari 2nd Season                                 |    8.93 | Mystery, Comedy, Supernatural, Vampire                              | TV     |          7 | Aug 12, 2017 to Aug 13, 2017 | Summer 2017 |
|  2656 | Code Geass: Hangyaku no Lelouch R2                         |    8.91 | Action, Military, Sci-Fi, Super Power, Drama, Mecha                 | TV     |         25 | Apr 6, 2008 to Sep 28, 2008  | Spring 2008 |
| 15631 | Gintama: The Final                                         |    8.88 | Action, Sci-Fi, Comedy, Historical, Parody, Drama, Samurai, Shounen | Movie  |          1 | Jan 8, 2021                  | Unknown     |
| 11624 | Haikyuu!!: Karasuno Koukou vs. Shiratorizawa Gakuen Koukou |    8.87 | Comedy, Sports, Drama, School, Shounen                              | TV     |         10 | Oct 8, 2016 to Dec 10, 2016  | Fall 2016   |

<p align = "center">  
Tabel 5. 20 <i>anime</i> dengan skor tertinggi
</p>

#### Deskripsi Kolom Score dan Members

Pada bagian ini, penulis akan menampilkan deskripsi dari kolom _score_ dan _members_ dari data anime. Hasilnya dapat dilihat pada tabel berikut ini.

| | Score | Members | 
|------|------------|-----------------| 
| count | 17562 | 17562 | 
| mean | 6.51 | 34658.5 | 
| std | 0.74571 | 125282 | 
| min | 1.85 | 1 | 
| 25% | 6.2 | 336 | 
| 50% | 6.51 | 2065 | 
| 75% | 6.86 | 13223.2 | 
| max | 9.19 | 2589552 |

<p align = "center">  
Tabel 6. Deskripsi kolom Score dan Members data _anime_
</p>

Berdasarkan tabel diatas, nilai rata-rata skor pada seluruh _anime_ adalah **6.51** dengan skor terendah sebesar **1.85** dan skor tertinggi sebesar **9.19**. Kemudian rata-rata jumlah member sebesar **34658.5** dengan jumlah member terendah sebesar **1** dan maksimal sebesar **2.589.552**. Total keseluruhan data pada data _anime_ sebanyak 17.562 judul _anime_.

#### Genre Feature

![Grafik Distribusi Genre](https://media.discordapp.net/attachments/1121095008926302358/1126360683882221578/distribusi_genre.png)

<p align = "center">  
Gambar 4. Grafik distribusi <i>anime</i> berdasarkan genre
</p>

Berdasarkan grafik diatas, genre _comedy_ menempati urutan terbanyak dibandingkan genre _action_. Hal ini disebabkan karena genre komedi merupakan salah genre yang fleksibel. Fleksibel disini adalah genre ini bisa ada di berbagai genre besar, seperti _action_, drama, _slice of life_ bahkan genre olahraga dan musik.

Untuk jumlah detail judul _anime_ berdasarkan genre dapat dilihat pada tabel berikut.
|		Genre   |   Total |
|:--------------|---------:|
| Comedy        |     6029 |
| Action        |     3888 |
| Fantasy       |     3285 |
| Adventure     |     2957 |
| Kids          |     2665 |
| Drama         |     2619 |
| Sci-Fi        |     2583 |
| Music         |     2244 |
| Shounen       |     2003 |
| Slice of Life |     1914 |
| Romance       |     1899 |
| School        |     1642 |
| Supernatural  |     1479 |
| Hentai        |     1348 |
| Historical    |     1144 |
| Mecha         |     1101 |
| Magic         |     1081 |
| Seinen        |      830 |
| Ecchi         |      767 |
| Mystery       |      727 |
| Sports        |      713 |
| Shoujo        |      688 |
| Parody        |      660 |
| Super Power   |      632 |
| Military      |      576 |
| Dementia      |      512 |
| Demons        |      501 |
| Space         |      495 |
| Horror        |      462 |
| Martial Arts  |      425 |
| Harem         |      399 |
| Game          |      386 |
| Psychological |      345 |
| Police        |      247 |
| Samurai       |      202 |
| Vampire       |      136 |
| Cars          |      133 |
| Thriller      |      131 |
| Shounen Ai    |      100 |
| Josei         |       97 |
| Shoujo Ai     |       79 |
| Unknown       |       63 |
| Yaoi          |       42 |
| Yuri          |       32 |

<p align = "center">  
Tabel 7. Jumlah judul <i>anime</i> berdasarkan genre
</p>

#### Type Feature

![Grafik Distribusi judul anime dengan tipe penayangan](https://media.discordapp.net/attachments/1121095008926302358/1126360684221956157/jumlah_judul_anime_berdasarkan_tipe.png)

<p align = "center">  
Gambar 5. Grafik Jumlah Judul <i>Anime</i> Berdasarkan Tipe
</p>

Berdasarkan grafik diatas, _anime_ kebanyakan ditayangkan dalam format **TV** dengan total sebanyak 4996 judul. 

Kemudian disusul dengan format _**Original Video Animation (OVA)**_ dengan total sebanyak 3894 judul. **OVA** adalah format penayangan _anime_ yang biasanya dalam bentuk episode bonus/tambahan episode yang tidak ditayangkan di format asli _anime_ tersebut ditayangkan dan hanya tersedia ketika melakukan pembelian _anime_ dalam format fisik seperti _DVD_ atau _BluRay_ bahkan bisa didapatkan ketika membeli sumber asli dari penayangan _anime_ tersebut. Ceritanya bisa aja berupa kelanjutan dari _anime_ utamanya, atau plot cerita tambahan yang tidak mengganggu alur cerita aslinya.  Contohnya seperti **_Non Non Biyori_**  yang merupakan adaptasi dari _manga_ dengan judul yang sama dimana _anime_ tersebut terdapat sebuah _OVA_ yang berjudul **_Non Non Biyori: Okinawa e Ikukoto ni Natta_** yang bisa didapatkan ketika melakukan pembelian _manga Non Non Biyori Volume 7_.

Kemudian diikuti dengan format _**Movie**_ dengan total sebanyak 3041 judul. Kemudian diikuti dengan format _**Special**_ dengan total sebanyak 2218 Judul, yaitu format penayangan yang secara umum mirip dengan **OVA** namun secara umum memiliki alur cerita yang sangat berbeda dengan alur cerita _anime_ utamanya, memiliki durasi yang lebih singkat, dan _anime_ tersebut dapat tayang di format asli _anime_ tersebut seperti TV.

Kemudian diikuti dengan format **_Original Net Animation (ONA)_** dengan total sebanyak 1907 judul. _ONA_ secara dasarnya sama dengan _OVA_, namun _ONA_ bisa diakses secara online seperti _ Official Youtube anime_ tersebut. Kemudian terakhir diikuti dengan format _**Music**_ dengan total sebanyak 1469 judul. Dan terdapat 39 judul yang tipenya "Unknown".

#### Watching Status Feature

_Watching Status_ merupakan suatu fitur yang menjelaskan status tontonan terhadap sebuah judul anime.  Fitur ini terdapat di variabel **anime_list** dan variabel ini akan dijadikan patokan untuk pengembangan model menggunakan pendekatan _Collaborative Based Filtering_ dikarenakan variabel tersebut menampung _anime_ yang di tambah pengguna, status nonton dan juga rating. 

|    |   user_id |   anime_id |   rating |   watching_status |   watched_episodes |
|---:|----------:|-----------:|---------:|------------------:|-------------------:|
|  0 |         0 |         67 |        9 |                 1 |                  1 |
|  1 |         0 |       6702 |        7 |                 1 |                  4 |
|  2 |         0 |        242 |       10 |                 1 |                  4 |
|  3 |         0 |       4898 |        0 |                 1 |                  1 |
|  4 |         0 |         21 |       10 |                 1 |                  0 |

<p align = "center">  
Tabel 8. Sampel daftar <i>anime</i> yang ditambahkan oleh pengguna
</p>

Berdasarkan daftar _anime_ yang diambil dari variabel **anime list**, fitur **watching_status** diwakilkan dengan kode. Referensi kode tersebut berasal dari sebuah variabel **watch status**. Ada 5 kode yang tersimpan pada variabel tersebut seperti yang terlihat pada Tabel 8 berikut.

| Status | Description |
|--|--|
| 1 | Currently Watching |
| 2 | Completed |
| 3 | On Hold |
| 4 | Dropped |
| 6 | Plan to Watch |

<p align = "center">  
Tabel 9. Isi dari variabel <i>watch status</i>
</p>

Dikarenakan itu, maka akan dilakukan penggantian kode di kolom **watching_status** dengan **Description** yang ada di variabel _watch status_. Pergantian tersebut akan berguna untuk melakukan analisis distribusi _anime_ berdasarkan status tonton dan juga dapat digunakan sebagai filtering untuk _Data Preparation_. 

Sebelum melakukan penggantian kode status tersebut, perlu dilakukan pemeriksaan **watching_status** dengan memeriksa nilai unik mereka, dan hasilnya seperti berikut.

` array([ 1,  2,  3,  4,  6,  0,  5, 33, 55])`

Berdasarkan hasil berikut ditemukan beberapa id yang tidak sesuai dengan tabel 8, seperti id 0, 5 , 33, dan 55. 
Untuk itu maka perlu dilakukan normalisasi agar kode **watching_status** sesuai dengan di tabel 8 dengan ketentuan sebagai berikut

1. Untuk data dengan **watching_status** 33, maka akan di konversikan ke 3
2. Untuk data dengan **watching_status** 5 dan 55, maka akan di konversikan ke 6

Untuk data dengan status 0, sebelum dilakukan konversi, perlu dilakukan analisis sehingga dapat ditentukan tindakan yang perlu dilakukan terhadap data tersebut. Cara yang dilakukan adalah dengan melihat sampel data yang memiliki **watching_status** 0. Sehingga didapatkan hasil yang dapat dilihat di tabel berikut.

|         |   user_id |   anime_id |   rating |   watching_status |   watched_episodes |
|--------:|----------:|-----------:|---------:|------------------:|-------------------:|
| 2970875 |     10015 |       6682 |        0 |                 0 |                  0 |
| 2970876 |     10015 |      18893 |        0 |                 0 |                  0 |
| 2970877 |     10015 |       4999 |        0 |                 0 |                  0 |
| 2970878 |     10015 |       7817 |        0 |                 0 |                  0 |
| 2970879 |     10015 |       6347 |        0 |                 0 |                  0 |

 
<p align = "center">  
Tabel 10. Sampel dari data <i>anime list</i> dengan <i>watching status</i> 0
</p>

Seperti yang dilihat pada tabel tersebut, ketika kolom watching_status bernilai 0, kolom rating dan watched_episodes juga bernilai 0. Untuk memastikan apakah ketika watching_status bernilai kolom rating dan watched_episodes juga bernilai 0, maka perlu untuk melihat desribe() pada _dataframe_ tersebut.

|       |    rating |   watching_status |   watched_episodes |
|:------|----------:|------------------:|-------------------:|
| count | 531       |               531 |          531       |
| mean  |   1.30508 |                 0 |            4.66478 |
| std   |   3.23033 |                 0 |           25.3202  |
| min   |   0       |                 0 |            0       |
| 25%   |   0       |                 0 |            0       |
| 50%   |   0       |                 0 |            0       |
| 75%   |   0       |                 0 |            0       |
| max   |  10       |                 0 |          345       |

 
<p align = "center">  
Tabel 11. Describe dari <i>anime list</i> dengan <i>watching status</i> 0
</p>

Berdasarkan dari tabel diatas, ada 531 data yang memiliki watching_status dengan nilai 0. Kemudian meskipun data di kolom watching_status bernilai 0, tetapi nilai di kolom rating dan watched_episodes bisa lebih dari 0. Untuk memastikan, maka penulis mengambil sampel data dimana kolom rating dan watched_episodes bukan 0 dan hasilnya sebagai berikut.

|         |   rating |   watching_status |   watched_episodes |
|--------:|---------:|------------------:|-------------------:|
| 2970880 |        0 |                 0 |                  5 |
| 2970881 |        0 |                 0 |                  6 |
| 2970882 |        7 |                 0 |                  2 |
| 2970886 |       10 |                 0 |                 12 |
| 2970889 |       10 |                 0 |                 13 |

<p align = "center">  
Tabel 12. Sampel dari data <i>anime list</i> dengan <i>watching status</i> 0 dan kolom <i> rating</i> dan <i> watched_episodes</i> lebih dari 0
</p>

Berdasarkan tabel 11 ini, ada kemungkinan kolom rating ataupun watched_episoded bernilai lebih dari 0. Sebenarnya secara bawaan fitur daftar _anime_ di  _MyAnimeList_ memungkinkan seorang pengguna untuk menambahkan suatu _anime_ tanpa memberikan rating, ataupun watched_episodes seperti di gambar berikut.

![Anime list MAL](https://media.discordapp.net/attachments/1121095008926302358/1126473127652769822/image.png)

<p align = "center">  
Gambar 6. Tampilan halaman daftar <i>anime</i> di <i>MyAnimeList</i> 
</p>

Seperti yang terlihat di gambar 6, terdapat sebuah _anime_ di dalam daftar tersebut dimana nilai _score_ dan _progress_ adalah 0 ataupun diganti dengan **"-"**, namun _anime_ tersebut berada di status **Currently Watching** sehingga seharusnya _watching_status_ bukan 0. Dan ketika pengguna ingin menambahkan sebuah _anime_, maka pada _form_ tambah ke daftar, untuk status tonton akan secara otomatis di atur ke _watching_ seperti gambar 7 berikut.

<p align="center">
<img src="https://media.discordapp.net/attachments/1121095008926302358/1126471511528722544/Screenshot_from_2023-07-05_23-03-19.png">
</p>

<p align = "center">  
Gambar 7. Tampilan <i>form</i> tambah daftar di <i>MyAnimeList</i> 
</p>

Sehingga kesimpulan penulis, kemungkinan penyebab data **watching_status** bernilai 0 disebabkan akibat kesalahan dalam pemrosesan data _scrapping_. Dan dikarenakan data tersebut hanya terdapat **531 data** dibandingkan data keseluruhan preferensi pengguna di daftar _anime_ sebesar **109.224.747 data**, maka penulis memutuskan untuk menghapus seluruh data dengan **watching_status** bernilai 0. Sehingga data di _anime list_ menjadi **109.224.216 data**.

Setelah mengatasi permasalah **watching_status** tersebut, langkah selanjutnya adalah melakukan _replace_ kode status tersebut dengan data _description_ dari variabel **watch status**, sehingga didapatkan grafik distribusi sebagai berikut.

![Grafik status tonton](https://cdn.discordapp.com/attachments/1121095008926302358/1126360684582678538/watching_status.png)

<p align = "center">  
Gambar 8. Grafik jumlah <i>anime</i> berdasarkan <i>watching status</i> 
</p>

Berdasarkan grafik diatas, ada sebanyak **68.089.751 judul** yang ditamatkan oleh pengguna, **27.938.700 judul** yang sedang direncanakan ditonton, **5.228.658 judul** yang sedang ditonton, **4.266.591 judul** yang di-_drop_ atau ditinggalkan oleh pengguna, dan **3.700.516 judul** yang sedang di-_hold_ oleh pengguna. Status _hold_ biasanya digunakan jika pengguna atau penonton ingin menonton _anime_ tersebut secara _batch_ dan bukan _simmulcast_ ataupun alasan lainnya seperti beberapa episode kedepan lebih ke episode _filler_ yang tidak mempengaruhi alur cerita utamanya.

## Data Preparation

### Hapus _anime_ yang memiliki genre tertentu

Langkah pertama yang dilakukan adalah melakukan pembersihan pada data _anime_ dengan genre tertentu, seperti genre yang mengandung unsur seksual.

#### Filter kolom di Data _anime_

Setelah melakukan filterisasi genre, langkah berikutnya adalah mengambil beberapa kolom tertentu untuk data _anime_. Kolom yang diambil adalah **MAL_ID, Name, Score, Genres, Type,** dan **Members**.

#### Gabungkan data _anime_ dengan kolom sinopsis

Setelah mengambil beberapa kolom yang dibutuhkan, langkah selanjutnya adalah menggabungkan data _anime_ dengan data sinopsis. Pada data sinopsis terdapat beberapa kolom yang akan diambil, yaitu **MAL_ID** dan **synopsis**, Setelah digabungkan, maka data _anime_ akan memiliki kolom sebagai berikut.

|    |   MAL_ID | Name                            |   Score | Genres                                              | Type   |   Members | sypnopsis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|---:|---------:|:--------------------------------|--------:|:----------------------------------------------------|:-------|----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  0 |        1 | Cowboy Bebop                    |    8.78 | Action, Adventure, Comedy, Drama, Sci-Fi, Space     | TV     |   1251960 | In the year 2071, humanity has colonized several of the planets and moons of the solar system leaving the now uninhabitable surface of planet Earth behind. The Inter Solar System Police attempts to keep peace in the galaxy, aided in part by outlaw bounty hunters, referred to as "Cowboys." The ragtag team aboard the spaceship Bebop are two such individuals. Mellow and carefree Spike Spiegel is balanced by his boisterous, pragmatic partner Jet Black as the pair makes a living chasing bounties and collecting rewards. Thrown off course by the addition of new members that they meet in their travels—Ein, a genetically engineered, highly intelligent Welsh Corgi; femme fatale Faye Valentine, an enigmatic trickster with memory loss; and the strange computer whiz kid Edward Wong—the crew embarks on thrilling adventures that unravel each member's dark and mysterious past little by little. Well-balanced with high density action and light-hearted comedy, Cowboy Bebop is a space Western classic and an homage to the smooth and improvised music it is named after. |
|  1 |        5 | Cowboy Bebop: Tengoku no Tobira |    8.39 | Action, Drama, Mystery, Sci-Fi, Space               | Movie  |    273145 | other day, another bounty—such is the life of the often unlucky crew of the Bebop. However, this routine is interrupted when Faye, who is chasing a fairly worthless target on Mars, witnesses an oil tanker suddenly explode, causing mass hysteria. As casualties mount due to a strange disease spreading through the smoke from the blast, a whopping three hundred million woolong price is placed on the head of the supposed perpetrator. With lives at stake and a solution to their money problems in sight, the Bebop crew springs into action. Spike, Jet, Faye, and Edward, followed closely by Ein, split up to pursue different leads across Alba City. Through their individual investigations, they discover a cover-up scheme involving a pharmaceutical company, revealing a plot that reaches much further than the ragtag team of bounty hunters could have realized.                                                                                                                                                                                                               |
|  2 |        6 | Trigun                          |    8.24 | Action, Sci-Fi, Adventure, Comedy, Drama, Shounen   | TV     |    558913 | Vash the Stampede is the man with a $$60,000,000,000 bounty on his head. The reason: he's a merciless villain who lays waste to all those that oppose him and flattens entire cities for fun, garnering him the title "The Humanoid Typhoon." He leaves a trail of death and destruction wherever he goes, and anyone can count themselves dead if they so much as make eye contact—or so the rumors say. In actuality, Vash is a huge softie who claims to have never taken a life and avoids violence at all costs. With his crazy doughnut obsession and buffoonish attitude in tow, Vash traverses the wasteland of the planet Gunsmoke, all the while followed by two insurance agents, Meryl Stryfe and Milly Thompson, who attempt to minimize his impact on the public. But soon, their misadventures evolve into life-or-death situations as a group of legendary assassins are summoned to bring about suffering to the trio. Vash's agonizing past will be unraveled and his morality and principles pushed to the breaking point.                                                           |
|  3 |        7 | Witch Hunter Robin              |    7.27 | Action, Mystery, Police, Supernatural, Drama, Magic | TV     |     94683 | ches are individuals with special powers like ESP, telekinesis, mind control, etc. Robin, a 15-year-old craft user, arrives from Italy to Japan to work for an organization named STN Japan Division (STN-J) as a replacement for one of STN-J's witch hunters who was recently killed. Unlike other divisions of STN, STN-J tries to capture the witches alive in order to learn why and how they became witches in the first place. (Source: ANN)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|  4 |        8 | Bouken Ou Beet                  |    6.98 | Adventure, Fantasy, Shounen, Supernatural           | TV     |     13224 | It is the dark century and the people are suffering under the rule of the devil, Vandel, who is able to manipulate monsters. The Vandel Busters are a group of people who hunt these devils, and among them, the Zenon Squad is known to be the strongest busters on the continent. A young boy, Beet, dreams of joining the Zenon Squad. However, one day, as a result of Beet's fault, the Zenon squad was defeated by the devil, Beltose. The five dying busters sacrificed their life power into their five weapons, Saiga. After giving their weapons to Beet, they passed away. Years have passed since then and the young Vandel Buster, Beet, begins his adventure to carry out the Zenon Squad's will to put an end to the dark century.

<p align = "center">  
Tabel 13. Sampel dari data <i>anime</i> setelah digabungkan
</p>

### Data Preprocessing untuk Content Based Filtering

Setelah melakukan filterisasi genre, kolom dan menggabungkan kolom sinopsis, langkah berikutnya adalah melakukan _preprocessing_ untuk data yang akan digunakan untuk pelatihan model. Dikarenakan ada 2 pendekatan, maka tiap _processing_ akan dipisah berdasarkan pendekatannya, Untuk model dengan pendekatan _Content Based Filtering_ data yang akan digunakan adalah data dari variabel _anime_ dan hanya perlu satu tahapan saja sebagai berikut.

#### Filter Daftar _Anime_ Berdasarkan Jumlah Member

Agar hasil dari prediksi berbasis _Content Based Filtering_ lebih baik, maka _anime_ yang akan diberikan harusnya _anime_ yang memiliki jumlah member yang cukup banyak. Untuk tahap ini, penulis akan melakukan filter data _anime_ dengan jumlah member **>= 34658**. Nilai tersebut didapatkan berdasarkan hasil _Exploratory Data Analysts_ pada kolom _Members_ sehingga total _anime_ yang terdapat pada daftar menjadi **2.362** judul dengan sampel sebagai berikut.

| | MAL_ID | Name | Score | Genres | Type | Members | sypnopsis | 
|---|---------|--------------------------------|--------|----------------------------------------------------|-------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 0 | 1 | Cowboy Bebop | 8.78 | Action, Adventure, Comedy, Drama, Sci-Fi, Space | TV | 1251960 | In the year 2071, humanity has colonized several of the planets and moons of the solar system leaving the now uninhabitable surface of planet Earth behind. The Inter Solar System Police attempts to keep peace in the galaxy, aided in part by outlaw bounty hunters, referred to as "Cowboys." The ragtag team aboard the spaceship Bebop are two such individuals. Mellow and carefree Spike Spiegel is balanced by his boisterous, pragmatic partner Jet Black as the pair makes a living chasing bounties and collecting rewards. Thrown off course by the addition of new members that they meet in their travels—Ein, a genetically engineered, highly intelligent Welsh Corgi; femme fatale Faye Valentine, an enigmatic trickster with memory loss; and the strange computer whiz kid Edward Wong—the crew embarks on thrilling adventures that unravel each member's dark and mysterious past little by little. Well-balanced with high density action and light-hearted comedy, Cowboy Bebop is a space Western classic and an homage to the smooth and improvised music it is named after. | 
| 1 | 5 | Cowboy Bebop: Tengoku no Tobira | 8.39 | Action, Drama, Mystery, Sci-Fi, Space | Movie | 273145 | other day, another bounty—such is the life of the often unlucky crew of the Bebop. However, this routine is interrupted when Faye, who is chasing a fairly worthless target on Mars, witnesses an oil tanker suddenly explode, causing mass hysteria. As casualties mount due to a strange disease spreading through the smoke from the blast, a whopping three hundred million woolong price is placed on the head of the supposed perpetrator. With lives at stake and a solution to their money problems in sight, the Bebop crew springs into action. Spike, Jet, Faye, and Edward, followed closely by Ein, split up to pursue different leads across Alba City. Through their individual investigations, they discover a cover-up scheme involving a pharmaceutical company, revealing a plot that reaches much further than the ragtag team of bounty hunters could have realized. | 
| 2 | 6 | Trigun | 8.24 | Action, Sci-Fi, Adventure, Comedy, Drama, Shounen | TV | 558913 | Vash the Stampede is the man with a $$60,000,000,000 bounty on his head. The reason: he's a merciless villain who lays waste to all those that oppose him and flattens entire cities for fun, garnering him the title "The Humanoid Typhoon." He leaves a trail of death and destruction wherever he goes, and anyone can count themselves dead if they so much as make eye contact—or so the rumors say. In actuality, Vash is a huge softie who claims to have never taken a life and avoids violence at all costs. With his crazy doughnut obsession and buffoonish attitude in tow, Vash traverses the wasteland of the planet Gunsmoke, all the while followed by two insurance agents, Meryl Stryfe and Milly Thompson, who attempt to minimize his impact on the public. But soon, their misadventures evolve into life-or-death situations as a group of legendary assassins are summoned to bring about suffering to the trio. Vash's agonizing past will be unraveled and his morality and principles pushed to the breaking point. | 
| 3 | 7 | Witch Hunter Robin | 7.27 | Action, Mystery, Police, Supernatural, Drama, Magic | TV | 94683 | ches are individuals with special powers like ESP, telekinesis, mind control, etc. Robin, a 15-year-old craft user, arrives from Italy to Japan to work for an organization named STN Japan Division (STN-J) as a replacement for one of STN-J's witch hunters who was recently killed. Unlike other divisions of STN, STN-J tries to capture the witches alive in order to learn why and how they became witches in the first place. (Source: ANN) | 
| 5 | 15 | Eyeshield 21 | 7.95 | Action, Sports, Comedy, Shounen | TV | 148259 | Sena is like any other shy kid starting high school; he's just trying to survive. Constantly bullied, he's accustomed to running away. Surviving high school is about to become a lot more difficult after Hiruma, captain of the school's American football team, witnesses Sena's incredible agility and speed during an escape from some bullies. Hiruma schemes to make Sena the running back of his school team, The Devil Bats, hoping that it will turn around the squad's fortunes from being the laughingstock of Japan's high school leagues, to title contender. To protect his precious star player from rivaling recruiters, he enlists Sena as "team secretary," giving him a visored helmet and the nickname "Eyeshield 21" to hide his identity. The Devilbats will look to make their way to the Christmas Bowl, an annual tournament attended by the best football teams in Japan, with "Eyeshield 21" leading the way. Will they be able to win the Christmas Bowl? Will Sena be able to transform from a timid, undersized freshman to an all-star player? Put on your pads and helmet to find out! |

<p align = "center">  
Tabel 13. Sampel dari data <i>anime</i> setelah di filter berdasarkan jumlah member
</p>

### Data Preprocessing untuk Collaborative Based Filtering

Untuk _preprocessing_ data dengan pendekatan _Collaborative Based Filtering_, data yang akan digunakan adalah data dari variabel _anime list_ yang akan digabungkan dengan data dari variabel _anime_. Hal ini disebabkan pada pendekatan ini, data yang akan dijadikan patokan adalah id pengguna, id _anime_ dan _rating_ yang diberikan oleh pengguna tersebut.

Dikarenakan itu, ada 8 tahapan yang akan dilakukan, yaitu

1. Filter _ranking_ pengguna dengan status tonton selesai atau berhenti menonton
2. Encode fitur _user_id_ dan _anime_id_
3. Konversi fitur _rating_
4. Ambil jumlah data pengguna, anime, serta nilai _rating_ minimum dan maksimum
5. _Train-Test Split_

#### Filter _ranking_ pengguna dengan status tonton selesai atau berhenti menonton

Langkah pertama adalah mengambil data dimana status tonton _anime_ tersebut telah selesai atau berhenti. Alasan penulis melakukan filterisasi adalah untuk memastikan pengguna akan mendapatkan rekomendasi yang terbaik. _Rating_ dari pengguna yang telah menyelesaikan dan berhenti merupakan _rating_ yang secara umum bersifat final dimana _rating_ dari pengguna yang menamatkan adalah rating untuk keseluruhan _anime_ tersebut. Sedangkan _rating_ ketika pengguna berhenti menonton bisa dikatakan final dikarena pengguna berhenti menonton suatu _anime_ dikarenakan beberapa hal dan hasil penilaiannya bisa digunakan untuk menghindarkan rekomendasi judul _anime_ ke pengguna yang memiliki kemiripan dengan pengguna yang pernah berhenti menonton judul anime tersebut.

#### _Encode_ fitur _user_id_ dan _anime_id_

Setelah melakukan filter, langkah berikutnya adalah melakukan _encode_ fitur _user_id_ dan _anime_id_. _Encode_ digunakan agar data tersebut dapat masuk dan diproses oleh model. _Encode_ akan memiliki dua format, yaitu **_id_ to _encoded_** dan **_encoded_ to _id_**.

Setelah dilakukan _encode_, hasil _encode_ **_id_ to _encoded_** dilakukan _mapping_ dan simpan ke variabel **anime list** dengan nama kolom _user_ dan _anime_. Sehingga data variabel **anime list** akan menjadi sebagai berikut.

|    |   user_id |   anime_id |   rating | watching_status   |   watched_episodes |   user |   anime |
|---|----------|-----------|---------|------------------|-------------------|-------|--------|
|  0 |         0 |         68 |        6 | Completed         |                 23 |       0 |       0 |
|  1 |         4 |         68 |        7 | Completed         |                 23 |       1 |       0 |
|  2 |        16 |         68 |        7 | Completed         |                 23 |       2 |       0 |
|  3 |        34 |         68 |       10 | Completed         |                 23  |     3 |       0 |
|  4 |        51 |         68 |        7 | Completed         |                 23  |    4 |       0 |


<p align = "center">  
Tabel 14. Sampel dari data <i>anime list</i> setelah hasil <i>encode</i> disimpan
</p>

#### Konversi fitur _rating_

Setelah melakukan _encode_, langkah berikutnya adalah melakukan konversi dari nilai _rating_ dari **string** menjadi **float64**. Sehingga hasil `info()` dari variabel _anime list_ menjadi sebagai berikut.

|# |  Column|Dtype  |
|---|  ------ |-----  |
| 0  | user_id           |int64  
| 1  | anime_id          |int64  
| 2  | rating            |float64
| 3  | watching_status   |object 
| 4  | watched_episodes  |int64  
| 5  | user              |int64  
| 6  | anime             |int64

<p align = "center">  
Tabel 15. Informasi kolom dan tipe data di variabel <i>anime list</i> setelah hasil konversi
</p>

#### Ambil Total Pengguna, Anime, dan Nilai Rating Minimum dan Maksimum

Langkah berikutnya adalah menghitung total pengguna, judul _anime_ dan nilai _rating_ minimum dan maksimum. Total pengguna dan judul _anime_ akan digunakan untuk mengatur ukuran dari _embedding_ pada model, kemudian nilai minimum dan maksimum _rating_ digunakan untuk normalisasi nilai _rating_ pada tahapan berikutnya.

Hasil dari tahapan ini, dapat disimpulkan bahwa total pengguna adalah **320.950** pengguna dengan total judul _anime_ sebanyak **17183** judul, kemudian _rating_ minimum sebesar 0 dan maksimum sebesar 10.

#### Train-Test Split

Langkah terakhir adalah membagi data tersebut menjadi data latih dan data uji. Untuk rasio pembagian adalah **80:20** dimana 80% adalah data latih dan 20% merupakan data uji.

Langkah pertama adalah melakukan pengacakan data. Hal ini digunakan agar data yang akan digunakan untuk latih dan uji bervariasi sehingga sampel 5 data pertama pada variabel _anime list_ menjadi sebagai berikut.

|          |   user_id |   anime_id |   rating | watching_status   |   watched_episodes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |   user |   anime |
|---------:|----------:|-----------:|---------:|:------------------|----------------:|:-------------------------------------------------|--------|
| 10696538 |     87835 |      20787 |        7 | Completed         |                 13                                                                        |  53270 |     182 |
| 37217644 |    152696 |      17831 |        7 | Completed         |                 12                                                                                                                                                                                                                                                                                                                                                                                                                                 |  13803 |    1281 |
| 36378880 |    259498 |        125 |        4 | Completed         |                 13                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | 187765 |    1220 |
| 45193320 |    188114 |      36029 |        6 | Completed         |                 23                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | 141958 |    1935 |
|  5680741 |    306841 |      39587 |        8 | Completed         |                 13 | 200855 |      98 |


<p align = "center">  
Tabel 16. Sampel di variabel <i>anime list</i> setelah diacak
</p>

Setelah diacak, lakukan pembagian dengan mengambil data dari fitur _user_, _anime_ dan _rating_, kemudian untuk fitur _rating_ akan di normalisasi dengan rumus sebagai berikut.

$$Rating_{norm} = \dfrac{rating - min(rating)}{max(rating) - min(rating)}$$

## Modelling

Pada proyek ini, akan diterapkan 2 tipe model, yaitu _Content Based Filtering_ dan _Collaborative Based Filtering_.

### Content Based Filtering

_Content-Based Filtering_ adalah metode dalam sistem rekomendasi yang menggunakan informasi konten atau fitur dari item (produk, film, lagu, dll.) dan preferensi pengguna untuk memberikan rekomendasi yang sesuai. Pendekatan ini mencocokkan preferensi pengguna dengan fitur-fitur item yang relevan.

Kelebihan dari _Content Based Filtering_ adalah

1.  Tidak memerlukan data pengguna lain atau kolaboratif.
2.  Dapat memberikan rekomendasi personal yang disesuaikan dengan preferensi pengguna.
3.  Dapat memanfaatkan fitur-fitur detail dari item untuk memberikan rekomendasi yang lebih spesifik.
4.  Mampu menangani keadaan baru, di mana item baru dapat direkomendasikan berdasarkan fitur-fitur yang relevan.

Namun terdapat beberapa kelemahannya, yaitu

1.  Rentan terhadap _overfitting_, di mana rekomendasi dapat menjadi terlalu spesifik dan kurang variasi.
2.  Terbatas pada informasi konten yang tersedia untuk menggambarkan item.
3.  Tidak dapat menangkap preferensi pengguna yang kompleks atau berubah seiring waktu.
4.  Tidak mampu merekomendasikan item baru yang tidak ada dalam data pelatihan.

Pada metode ini, model yang dikembangkan akan menggunakan fitur genre dimana hasilnya akan merekomendasikan _anime_ berdasarkan kemiripan genre. Akan ada 2 teknik perhitungan _similarity_ yang akan digunakan, yaitu _**Cosine Similarity**_ dan _**euclidean Distance**_.

#### TF-IDF Vectorizer

_Term Frequency-Inverse Document Frequency (TF-IDF) Vectorizer_ adalah sebuah metode yang digunakan untuk mengubah teks menjadi representasi vektor numerik. Metode ini digunakan dalam pemrosesan bahasa alami dan analisis teks untuk mengekstrak fitur-fitur penting dari teks.

Pada dasarnya, _TF-IDF Vectorizer_ mengukur pentingnya suatu kata dalam suatu dokumen berdasarkan frekuensi kemunculan kata dokumen tersebut (TF) dan keberulangan kata di seluruh dokumen dalam korpus (IDF). 

Rumus umum untuk menghitung nilai TF-IDF adalah sebagai berikut:

$$TF-IDF(d, t) = TF(d, t) * IDF(t)$$

Di mana:

-   TF(d, t) adalah frekuensi kemunculan kata (term) t dalam dokumen d. Frekuensi ini dapat dihitung dengan berbagai metode, misalnya menggunakan skema biner (jika kata ada dalam dokumen, nilai TF = 1) atau menggunakan frekuensi relatif (jumlah kemunculan kata dibagi dengan total kata dalam dokumen).
-   IDF(t) adalah inverse document frequency (kebalikan frekuensi dokumen) dari kata t. IDF mengukur sejauh mana kata t umum atau langka di seluruh dokumen dalam korpus. IDF dihitung sebagai logaritma dari jumlah total dokumen dalam korpus dibagi dengan jumlah dokumen yang mengandung kata t.

Untuk rumus TF adalah sebagai berikut

$$TF(d, t) = \dfrac{f_d(t)}{maxf_d(w)}$$

Dimana:

- $f_d(t)$ merupakan frekuensi kemunculan kata $t$ dalam dokumen $d$
- $maxf_d(w)$ merupakan jumlah kata dalam dokumen $d$

Sedangkan urum IDF adalah

$$IDF(t) = log(\dfrac{N}{1+ df})$$

Dimana:

- $N$ Panjang dokumen
- $df$ Jumlah dokumen yang mengandung kata $t$

Pada bagian ini, _TF-IDF_ akan diterapkan untuk kolom genre. Langkah yang dilakukan untuk menerapkan Pada tahapan ini, _tokenizer_ yang akan digunakan adalah dengan _split_ pada data kolom tersebut. Hal ini digunakan agar data genre akan diproses dalam keadaan utuh, seperti pada suatu _anime_ dengan Genre _"Action, Sci-Fi, Drama"_, maka setelah dilakukan _vectonizer_ menjadi `['action', 'sci-fi', 'drama']`. Setelah itu lakukan perhitungan _IDF_ pada data genre. Kemudian jika di-_mapping_, maka hasilnya akan sebagai berikut.

```
array(['action', 'adventure', 'cars', 'comedy', 'dementia', 'demons', 'drama', 'fantasy', 
'game', 'harem', 'historical', 'horror', 'josei', 'kids', 'magic', 'martial arts', 'mecha', 
'military', 'music', 'mystery', 'parody', 'police', 'psychological', 'romance', 'samurai', 
'school', 'sci-fi', 'seinen', 'shoujo', 'shounen', 'slice of life', 'space', 'sports', 
'super power', 'supernatural', 'thriller', 'vampire'], dtype=object)
```

Setelah itu, lakukan proses _fit_ dan transformasikan ke dalam bentuk matriks. Sehingga hasil ukuran matriks yang terbentuk adalah **2362 x 37** dengan 10 sampel hasil nya adalah sebagai berikut.

| Name | mystery | psychological | fantasy | parody | horror | demons | shounen | romance | magic | historical | harem | thriller | shoujo | drama | military | martial arts | sci-fi | dementia | slice of life | school | space | music |
|:-------------------------------------------|----------:|----------------:|----------:|---------:|---------:|---------:|----------:|----------:|--------:|-------------:|---------:|-----------:|---------:|---------:|-----------:|---------------:|---------:|-----------:|----------------:|---------:|---------:|--------:|
| Non Non Biyori Movie: Vacation | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.591009 | 0 | 0 | 0 |
| Kizumonogatari II: Nekketsu-hen | 0.484082 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Mobile Suit Gundam SEED Destiny | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.289756 | 0 | 0 | 0 | 0 | 0 | 0.267906 | 0.446671 | 0 | 0.316291 | 0 | 0 | 0 | 0.550729 | 0 |
| Hoshi wo Ou Kodomo | 0 | 0 | 0.5445 | 0 | 0 | 0 | 0 | 0.588908 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Soredemo Machi wa Mawatteiru | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.591009 | 0 | 0 | 0 |
| Non Non Biyori: Okinawa e Ikukoto ni Natta | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.517628 | 0.482604 | 0 | 0 |
| Nana Maru San Batsu | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.424736 | 0 | 0 |
| Nisekoi: | 0 | 0 | 0 | 0 | 0 | 0 | 0.372698 | 0.386251 | 0 | 0 | 0.686092 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.402636 | 0 | 0 |
| Mushishi: Hihamukage | 0.402827 | 0 | 0.292893 | 0 | 0 | 0 | 0 | 0 | 0 | 0.488331 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.354184 | 0 | 0 | 0 |
| Bakuman. 3rd Season | 0 | 0 | 0 | 0 | 0 | 0 | 0.529891 | 0.54916 | 0 | 0 | 0 | 0 | 0 | 0.50775 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

<p align = "center">  
Tabel 17. Sampel hasil <i>TF-IDF</i> 
</p>

#### Cosine Similarity

_Cosine Similarity_ adalah sebuah metode yang digunakan untuk mengukur kemiripan antara dua vektor dalam ruang berdimensi banyak. Metode ini sering digunakan dalam pemrosesan bahasa alami, analisis teks, dan pengelompokan data.

Dalam _cosine similarity_, kemiripan antara dua vektor diukur berdasarkan sudut antara vektor-vektor tersebut. Nilai _cosine similarity_ berkisar antara -1 hingga 1, di mana nilai 1 menunjukkan kedua vektor memiliki arah yang sama atau sangat mirip, nilai 0 menunjukkan tidak ada kemiripan, dan nilai -1 menunjukkan arah yang berlawanan atau sangat berbeda.

Rumus untuk _Cosine Similarity_ adalah

$$Cosine Similarity_{(A,B)} = \dfrac{(A.B)}{(||A|| * ||B||)}$$

Di mana:

-   A dan B adalah dua vektor yang akan dibandingkan.
-   A . B adalah hasil perkalian dot (inner product) antara vektor A dan B.
-   ||A|| dan ||B|| adalah panjang (magnitude) dari vektor A dan B.


 <p align="center">
 <img src="https://images.deepai.org/glossary-terms/cosine-similarity-1007790.jpg" alt="Cosine Similarity Concept">
 Gambar 9. Grafik jarak antar 2 vektor di <i>Cosine Similarity</i> 
 </p>

Untuk penerapan pada proyek ini, dapat menggunakan fungsi `cosine_similarity` dari _library sklearn_. Pada tahapan ini, kita akan menghitung _cosine similarity_ pada data hasil _tf-idf_ sebelumnya. Sehingga hasil dari proses ini dapat dilihat di tabel sampel berikut ini.

| Name | Innocence | Ore wo Suki nano wa Omae dake ka yo | Arakawa Under the Bridge x Bridge | Ixion Saga DT | Takanashi Rikka Kai: Chuunibyou demo Koi ga Shitai! Movie | 
|:------------------------------------------------------|------------:|--------------------------------------:|------------------------------------:|----------------:|------------------------------------------------------------:| 
| Kizumonogatari I: Tekketsu-hen | 0 | 0 | 0 | 0 | 0 | | Hakushaku to Yousei | 0 | 0.135105 | 0.177902 | 0.197938 | 0.149377 | 
| D.N.Angel | 0 | 0.378417 | 0.291357 | 0.487065 | 0.418392 | 
| Gate: Jieitai Kanochi nite, Kaku Tatakaeri 2nd Season | 0.314457 | 0 | 0 | 0.465354 | 0 | 
| Inu x Boku SS Special | 0 | 0.139507 | 0.183698 | 0.239084 | 0.154244 | 
| Oshiete! Galko-chan | 0 | 0.39743 | 0.171562 | 0.223289 | 0.779198 | 
| Koro-sensei Quest! | 0 | 0.122095 | 0.160772 | 0.209245 | 0.134993 | 
| Soredemo Sekai wa Utsukushii | 0 | 0.1806 | 0.237808 | 0.264591 | 0.199678 | 
| Minami-ke Tadaima | 0 | 0.39743 | 0.171562 | 0.223289 | 0.779198 | 
| One Punch Man 2nd Season | 0.120169 | 0.0764204 | 0.100628 | 0.274376 | 0.0844932 |

<p align = "center">  
Tabel 18. Sampel hasil perhitungan jarak menggunakan <i>Cosine Similarity</i> 
</p>

#### euclidean Distance

_Euclidean Distance_ adalah sebuah metode yang digunakan untuk mengukur jarak antara dua titik dalam ruang berdimensi banyak. Metode ini sering digunakan dalam analisis data, pengelompokan data, dan pengenalan pola.

Dalam _Euclidean Distance_, jarak antara dua titik dihitung sebagai panjang garis lurus yang menghubungkan kedua titik tersebut. Jarak ini dihitung berdasarkan perbedaan koordinat antara dua titik pada setiap dimensi. Semakin besar nilainya, maka semakin jauh perbedaannya.

Rumusnya adalah sebagai berikut

$$Euclidean Distance_{(A,B)} = \sqrt{(x2 - x1)^2 + (y2 - y1)^2}$$

Di mana:

-   A dan B adalah dua titik yang akan diukur jaraknya.
-   (x1, y1) dan (x2, y2) adalah koordinat dari titik A dan B pada setiap dimensi.

 <p align="center">
 <img src="https://www.researchgate.net/profile/Young-Sun-Lee-2/publication/263889770/figure/fig1/AS:890653479284740@1589359745492/An-example-of-Euclidean-distance-between-two-objects-on-variables-X-and-Y.png" alt="euclidean Distance">
 Gambar 10. Grafik jarak antara 2 vektor di <i>euclidean Distance</i>  dimana konsep pengukurannya sama dengan perhitungan sisi miring Pythagoras
 </p>

Untuk penerapan pada proyek ini, dapat menggunakan fungsi `euclidean_distance` dari _library sklearn_. Pada tahapan ini, kita akan menghitung _euclidean distance_ pada data hasil _tf-idf_ sebelumnya. Sehingga hasil dari proses ini dapat dilihat di tabel sampel berikut ini.

| Name | High Score Girl: Extra Stage | Basilisk: Kouga Ninpou Chou | Toaru Kagaku no Railgun: Motto Marutto Railgun | Digimon Adventure tri. 3: Kokuhaku | School Rumble | 
|:-------------------------------|-------------------------------:|------------------------------:|-------------------------------------------------:|-------------------------------------:|----------------:| 
| Noragami OVA | 1.34527 | 1.10114 | 1.13214 | 0.8834 | 1.11117 | | Digimon Savers | 1.34603 | 1.20249 | 1.13556 | 0.79917 | 1.11487 | 
| Otome Youkai Zakuro | 1.17976 | 1.09781 | 1.41421 | 1.41421 | 1.29728 | 
| Zan Sayonara Zetsubou Sensei | 1.22597 | 1.41421 | 1.17682 | 1.31955 | 0.925836 | 
| Tantei Opera Milky Holmes | 1.34504 | 1.41421 | 1.13112 | 1.30262 | 1.31206 | 
| Lupin III: Cagliostro no Shiro | 1.13179 | 1.26036 | 1.17568 | 0.975199 | 1.32711 | 
| Hyouka | 1.26583 | 1.41421 | 1.41421 | 1.41421 | 1.19152 | 
| Tamako Love Story | 1.15423 | 1.28003 | 1.06149 | 1.27773 | 1.01274 | 
| Koi Kaze | 1.11147 | 1.3318 | 1.41421 | 1.27633 | 1.26545 | 
| Dragon Ball Kai (2014) | 1.36885 | 1.23037 | 1.23424 | 1.09116 | 1.22152 |

<p align = "center">  
Tabel 19. Sampel hasil perhitungan jarak menggunakan <i>euclidean Distance</i> 
</p>

#### Hasil Rekomendasi

Setelah menerapkan kedua metode pengukuran kemiripan diatas, langkah terakhir adalah membuat sebuah fungsi untuk menghasilkan hasil prediksi menggunakan _dataframe_ hasil implementasi tersebut. Fungsi tersebut memiliki 1 parameter wajib dan 4 parameter opsional dengan sebagai berikut

- **title** - Judul anime yang menjadi patokan untuk direkomendasikan (Wajib)
- **similarity_data** - _dataframe_ dari hasil perhitungan _similarity_. Secara bawaan, _dataframe cosine similarity_  yang digunakan
- **similar_type** - Tipe _similarity_ yang digunakan. Secara bawaan "cosine" yang digunakan
- **items** - _dataframe anime_ yang akan digunakan untuk mengambil informasi dari hasil rekomendasi. Secara bawaan, akan menggunakan _dataframe_ yang digunakan ketika sebelum dilakukan proses _TF-IDF_.
- k - Jumlah rekomendasi yang akan dihasilkan

Cara kerja algoritma ini adalah sebagai berikut

1. Mengambil indeks dengan menggunakan _argpartition_ untuk melakukan pemartisian secara tidak langsung sepanjang sumbu yang diberikan. Ada perbedaan antara _similarity_type_ "cosinus" dengan :euclidean". Pada "cosinus", _range_ partisi dimulai dari indeks paling akhir hingga _n-k_, contoh jika ada larik seperti berikut.

	`[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]`

	Larik tersebut memiliki panjang data sebesar 15. Jika k adalah 5, maka larik yang terbentuk adalah

	`[ 1,  0,  2,  3,  4,  5,  6,  8,  7,  9, 10, 11, 12]` 

	Sedangkan untuk "euclidean", _range_ partisi dimulai dari 0 hingga _k+2_

2. Ambil data dengan similarity terbesar berdasarkan larik indeks
3. _Drop_ judul _anime_ yang dijadikan patokan rekomendasi, sehingga tidak muncul dalam daftar
4. Tampilkan daftar rekomendasi

Pada contoh ini, saya akan memasukkan title salah satu _anime_ yang berjudul **"Clannad: After Story"** dengan informasi _anime_ tersebut sebagai berikut.

|       |   MAL_ID | Name                        |   Score | Genres                                              | Type   |
|------:|---------:|:----------------------------|--------:|:----------------------------------------------------|:-------|
|  2839 |     4181 | Clannad: After Story        |    8.96 | Slice of Life, Comedy, Supernatural, Drama, Romance | TV     |

<p align = "center">  
Tabel 20. Judul <i>anime</i> yang akan dijadikan salah satu contoh
</p>

Kemudian hasil dari daftar 10 _anime_ yang direkomendasi berdasarkan metode **_Cosine Similarity_** adalah sebagai berikut

|    | Name                          |   MAL_ID |   Score | Genres                                                      | Type    |    score |
|---:|:------------------------------|---------:|--------:|:------------------------------------------------------------|:--------|---------:|
|  0 | Kanon                         |      144 |    7.11 | Drama, Romance, Slice of Life, Supernatural                 | TV      | 1        |
|  1 | Sola                          |     1965 |    7.22 | Drama, Romance, Slice of Life, Supernatural                 | TV      | 0.941605 |
|  2 | Kanon (2006)                  |     1530 |    8.01 | Slice of Life, Supernatural, Drama, Romance                 | TV      | 0.941605 |
|  3 | Air                           |      101 |    7.32 | Slice of Life, Supernatural, Drama, Romance                 | TV      | 0.941605 |
|  4 | Sewayaki Kitsune no Senko-san |    38759 |    7.36 | Slice of Life, Comedy, Supernatural, Romance                | TV      | 0.941605 |
|  5 | Little Busters!: EX           |    20517 |    7.74 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | Special | 0.903943 |
|  6 | Kokoro Connect                |    11887 |    7.82 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | TV      | 0.900766 |
|  7 | Little Busters!: Refrain      |    18195 |    8.23 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | TV      | 0.900766 |
|  8 | Clannad                       |     2167 |    8.07 | Comedy, Drama, Romance, School, Slice of Life, Supernatural | TV      | 0.900766 |
|  9 | Kokoro Connect: Michi Random  |    16001 |    8.01 | Comedy, Drama, Romance, School, Slice of Life, Supernatural | Special | 0.900766 |

<p align = "center">  
Tabel 21.  Hasil 10 <i>anime</i> yang direkomendasikan menggunakan pendekatan <i>cosine similarity</i>
</p>

Sedangkan untuk hasil dari daftar 10 _anime_ yang direkomendasi berdasarkan metode **_euclidean Distance_** adalah sebagai berikut

|    | Name                          |   MAL_ID |   Score | Genres                                                      | Type    |    score |
|---:|:------------------------------|---------:|--------:|:------------------------------------------------------------|:--------|---------:|
|  0 | Air                           |      101 |    7.32 | Slice of Life, Supernatural, Drama, Romance                 | TV      | 0        |
|  1 | Kanon                         |      144 |    7.11 | Drama, Romance, Slice of Life, Supernatural                 | TV      | 0.341746 |
|  2 | Kanon (2006)                  |     1530 |    8.01 | Slice of Life, Supernatural, Drama, Romance                 | TV      | 0.341746 |
|  3 | Sola                          |     1965 |    7.22 | Drama, Romance, Slice of Life, Supernatural                 | TV      | 0.341746 |
|  4 | Sewayaki Kitsune no Senko-san |    38759 |    7.36 | Slice of Life, Comedy, Supernatural, Romance                | TV      | 0.341746 |
|  5 | Clannad                       |     2167 |    8.07 | Comedy, Drama, Romance, School, Slice of Life, Supernatural | TV      | 0.438307 |
|  6 | Kokoro Connect                |    11887 |    7.82 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | TV      | 0.445498 |
|  7 | Kokoro Connect: Michi Random  |    16001 |    8.01 | Comedy, Drama, Romance, School, Slice of Life, Supernatural | Special | 0.445498 |
|  8 | Little Busters!: Refrain      |    18195 |    8.23 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | TV      | 0.445498 |
|  9 | Little Busters!: EX           |    20517 |    7.74 | Slice of Life, Comedy, Supernatural, Drama, Romance, School | Special | 0.445498 |

<p align = "center">  
Tabel 22.  Hasil 10 <i>anime</i> yang direkomendasikan menggunakan pendekatan <i>euclidean distance</i>
</p>

### Collaborative Based Filtering

_Collaborative Based Filtering_ adalah metode dalam sistem rekomendasi yang mengandalkan informasi dari pengguna lain untuk memberikan rekomendasi. Pendekatan ini mencocokkan preferensi pengguna dengan preferensi pengguna lain yang memiliki profil atau perilaku serupa.

Kelebihan dari metode ini adalah

1.  Mampu menangani kompleksitas preferensi pengguna yang tidak dapat dilihat dari informasi konten item.
2.  Dapat merekomendasikan item baru yang tidak ada dalam data pelatihan berdasarkan perilaku pengguna lain.
3.  Tidak terbatas pada fitur-fitur item, sehingga dapat merekomendasikan item yang berbeda tetapi relevan.

Namun terdapat beberapa kekurangan, yaitu

1.  Bergantung pada ketersediaan data pengguna yang cukup untuk membuat rekomendasi yang akurat.
2.  Membutuhkan pemrosesan yang lebih intensif dan kompleks, terutama dalam skala besar.
3.  Rentan terhadap _cold start_ di mana rekomendasi sulit untuk pengguna baru yang memiliki sedikit atau tanpa data perilaku.

#### Membangun Model
Untuk metode ini, algoritma model yang akan digunakan adalah algoritma _**RecommenderNet**_. Model ini memiliki arsitektur sebagai berikut.

<p align="center">
	<img src="https://cdn.discordapp.com/attachments/1121095008926302358/1127162714159063040/image.png" alt="RecommenderNet Architectur">
</p>
<p align="center">
Gambar 11. Arsitektur dari <i>RecommenderNet</i>
</p>

Berdasarkan gambar diatas, _RecommenderNet_ menggunakan 4 buah node _embeddings_. _Embedding_ adalah sebuah _hidden layers_ di sebuah _neural network_. Tujuan dari _embedding_ adalah melakukan _mapping_ dari data dengan dimensi tinggi ke dimensi yang lebih rendah, sehingga model dapat lebih mudah mempelajari hubungan antara _input_ dan proses data lebih efisien.

<p align="center">
	<img src="https://www.baeldung.com/wp-content/uploads/sites/4/2023/01/embedding_layer.png" alt="RecommenderNet Architectur">
</p>
<p align="center">
Gambar 12. Gambaran dari <i>Embedding Layers</i>
</p>

_Embedding layer_ pada model ini ada 2 tipe, yaitu _embedding_ untuk fitur dan _bias layer_ dimana _embedding_ fitur akan memiliki parameter _regularizer l2_ dengan nilai **0.000001** dan ukurannya adalah **total fitur x 50**.

Sedangkan bias akan memiliki ukuran **total fitur x 1**.

Hasil dari _embedding_ fitur _user_ dan _anime_ kemudian dilakukan operasi perkalian matriks menggunakan `tensordot`. Kemudian hasil perkalian tersebut baru dijumlahkan dengan _bias_ dari _user_ dan _anime_. Setelah itu dimasukkan ke fungsi aktivasi _**sigmoid**_.

#### Compile Model dan Buat Callbacks

Setelah membangun model, model kemudian dilakukan kompilasi. Pada bagian ini, juga akan ditentukan _loss function, optimizer, dan metrics_. Untuk **_loss function_** dan **_metrics_** akan menggunakan _**BinaryCrossentropy**_ dan _**RootMeanSquare Error**_. Sedangkan untuk optimizer, penulis akan mencoba menggunakan 2 metode, yaitu **_Adam lr.0.001_** dan **RMSprop lr.0.0001**. 

Kemudian dibuat dua _callback_ yaitu _EarlyStopping_ yang bertujuan untuk menghentikan proses latih jika nilai metrik tertentu tidak mengalami perubahan ke yang lebih baik. Selain itu teknik ini bisa digunakan untuk menyimpan model dengan hasil terbaik, sehingga ketika pelatihan selesai, model yang dijalankan di memori adalah model dengan _weight_ dan kualitas terbaiknya. Pada _EarlyStopping_ ini, nilai _patience_ adalah **3** yang menunjukkan jika 3 _epoch_ berikutnya tidak ada peningkatan kualitas, maka proses latih dihentikan. Kemudian parameter _restore_best_weight_ menjadi **True** dan _monitor_ diatur menjadi **_"val_root_mean_squared_error"_**, sehingga hasil _RMSE_ validasi yang akan dijadikan patokan.

Selain itu juga diterapkan _callback ModelCheckpoint_. Tujuan dari _callback_ ini adalah agar setiap _epochs_ yang memberikan hasil terbaik, model tersebut langsung disimpan. Model dapat disimpan dalam format **h5, hdf, ** dan **ckpt**.

#### Training

Setelah itu, maka dijalankan proses pelatihan dengan jumlah _batch_ sebesar **8192** dengan jumlah _epochs_ sebesar **100** dan _validation batch_ adalah **32**. Lama proses pelatihan sangat bervariasi. Untuk model dengan **_optimizer Adam_**, proses pelatihan cukup singkat dengan jumlah _epoch_ adalah **4 _epoch_**, sedangkan untuk **_optimizer RMSprop**_ sebesar **57 _epoch_**.

Setelah dilakukan perbandingan, maka model dengan _optimizer RMSprop_ memberikan hasil yang lebih baik dibandingkan menggunakan _Adam_ dimana penjelasan lebih detail akan dibahas di bagian **_Evaluation_**.

#### Hasil Rekomendasi

Setelah melakukan pelatihan, langkah terakhir adalah membuat sebuah fungsi untuk menghasilkan hasil rekomendasi ke pengguna. Langkah yang perlu dilakukan adalah sebagai berikut

1. Masukkan ID pengguna. Pada bagian ini, penulis akan memilih secara acak pengguna yang akan diberikan rekomendasi
2. Ambil data _anime_ yang pernah ditonton pengguna
3. Berdasarkan data _anime_ yang pernah ditonton, ambil data _anime_ yang belum pernah di tonton
4. Ambil _encoded anime_ dari daftar _anime_ yang belom pernah ditonton
5. Ambil _encoded_ pengguna yang akan diberikan rekomendasi
6. Buat sebuah data awal yang akan digunkan model untuk memprediksi berdasarkan _encode user_ sekarang dengan _encode anime_ yang belum pernah ditonton
7. Jalankan prediksi model berdasarkan data tersebut
8. Ambil hasil dengan rating tertinggi kemudian ambil id _anime_ tersebut
9. Tampilkan hasil rekomendasi _anime_

Pada contoh ini, sistem rekomendasi akan memberikan rekomendasi _anime_ untuk pengguna dengan id  **256400** dimana 10 _anime_ yang paling tinggi _rating_ yang ia berikan adalah sebagai berikut

|      |   MAL_ID | Name                                |   Score | Genres                                                                       | Type   |
|-----:|---------:|:------------------------------------|--------:|:-----------------------------------------------------------------------------|:-------|
|  142 |      164 | Mononoke Hime                       |    8.72 | Action, Adventure, Fantasy                                                   | Movie  |
|  428 |      457 | Mushishi                            |    8.69 | Adventure, Slice of Life, Mystery, Historical, Supernatural, Fantasy, Seinen | TV     |
| 1388 |     1530 | Kanon (2006)                        |    8.01 | Slice of Life, Supernatural, Drama, Romance                                  | TV     |
| 2061 |     2251 | Baccano!                            |    8.42 | Action, Comedy, Historical, Mystery, Supernatural                            | TV     |
| 3954 |     5081 | Bakemonogatari                      |    8.36 | Romance, Supernatural, Mystery, Vampire                                      | TV     |
| 4661 |     6594 | Katanagatari                        |    8.36 | Action, Adventure, Historical, Martial Arts, Romance                         | TV     |
| 7577 |    17074 | Monogatari Series: Second Season    |    8.78 | Mystery, Comedy, Supernatural, Romance, Vampire                              | TV     |
| 8559 |    21939 | Mushishi Zoku Shou                  |    8.72 | Adventure, Slice of Life, Mystery, Historical, Supernatural, Fantasy, Seinen | TV     |
| 9182 |    24701 | Mushishi Zoku Shou 2nd Season       |    8.76 | Adventure, Fantasy, Historical, Mystery, Seinen, Slice of Life, Supernatural | TV     |
| 9908 |    28957 | Mushishi Zoku Shou: Suzu no Shizuku |    8.63 | Adventure, Fantasy, Historical, Mystery, Seinen, Slice of Life, Supernatural | Movie  |

<p align = "center">  
Tabel 22.  Hasil 10 <i>anime</i> dari pengguna 256400 dengan <i>rating</i> tertinggi
</p>

Dan setelah dilakukan prediksi, maka 10 _anime_ yang direkomendasikan untuk pengguna **256400** adalah sebagai berikut

|       |   MAL_ID | Name                                                    |   Score | Genres                                                       | Type   |
|------:|---------:|:--------------------------------------------------------|--------:|:-------------------------------------------------------------|:-------|
|   741 |      820 | Ginga Eiyuu Densetsu                                    |    9.07 | Military, Sci-Fi, Space, Drama                               | OVA    |
|  2668 |     2921 | Ashita no Joe 2                                         |    8.67 | Action, Drama, Shounen, Slice of Life, Sports                | TV     |
|  5683 |     9253 | Steins;Gate                                             |    9.11 | Thriller, Sci-Fi                                             | TV     |
|  9886 |    28851 | Koe no Katachi                                          |    9    | Drama, School, Shounen                                       | Movie  |
|  9913 |    28977 | Gintama°                                                |    9.1  | Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen | TV     |
| 11308 |    32281 | Kimi no Na wa.                                          |    8.96 | Romance, Supernatural, School, Drama                         | Movie  |
| 11684 |    33050 | Fate/stay night Movie: Heaven's Feel - III. Spring Song |    8.79 | Action, Supernatural, Magic, Fantasy                         | Movie  |
| 11708 |    33095 | Shouwa Genroku Rakugo Shinjuu: Sukeroku Futatabi-hen    |    8.79 | Drama, Historical, Josei                                     | TV     |
| 12898 |    35180 | 3-gatsu no Lion 2nd Season                              |    9    | Drama, Game, Seinen, Slice of Life                           | TV     |
| 12933 |    35247 | Owarimonogatari 2nd Season                              |    8.93 | Mystery, Comedy, Supernatural, Vampire                       | TV     |

<p align = "center">  
Tabel 22.  Hasil rekomendasi 10 <i>anime</i> untuk pengguna 256400 
</p>

## Evaluation

Pada proyek ini, ada dua perhitungan metrik yang digunakan berdasarkan metode pendekatan yang digunakan, yaitu _Precision_ untuk pendekatan _Content Based Filtering_ dan _Root Mean Square Error_ untuk _Collaborative Based Filtering_.

### Content Based Filtetring

Pada pendekatan ini, metrik yang digunakan adalah _precision_. Sebelum masuk ke penjelasan mengenai _precission_, maka kita harus mengetahui mengenai _confusion matrix_.

_Confusion Matrix_ adalah suatu metode pengukuran performa yang sering digunakan dalam tipe _Supervised Machine Learning_. _Confusion Matrix_ merepresentasikan prediksi dan kondisi sebenarnya(aktual) dari data yang dihasilkan oleh model. Berdasarkan _Confusion Matrix_, kita bisa menentukan _Accuracy, Precission, Recall_ dan _Specificity_.

<p align="center">
	<img src="https://miro.medium.com/v2/resize:fit:1400/1*fxiTNIgOyvAombPJx5KGeA.png" alt="Confusion Matrix">
</p>
<p align="center">
Gambar 13. <i>Confusion Matrix</i>
</p>

Agar dapat lebih memahami _confusion matrix_ lebih baik, perhatikan tabel hasil prediksi klasifikasi foto kucing dan anjing berikut.

| No. Foto | Aktual | Prediksi |
|:----------:|------|----------|
| 1         | Kucing | Kucing  |
| 2         | Anjing | Kucing  |
| 3         | Anjing | Anjing  |
| 4         | Kucing | Anjing  |
| 5         | Kucing | Kucing  |

<p align="center">
Tabel 24. Contoh hasil prediksi dan aktual dari model klasifikasi foto kucing dan anjing
</p>

Jika asumsi foto dengan nama kelas "kucing" merupakan kelas positif dan "anjing" merupakan kelas negatif. Maka akan ada 4 kemungkinan berdasarkan tabel tersebut, terdapat 4 kasus yang terjadi, yaitu

- **True Positive (TP)** : Kasus dimana model memprediksi foto tersebut kucing (positif) dan hasil aktualnya adalah kucing (positif). Pada tabel 24, **Foto 1 dan 5** merupakan **True Positive**, sehingga TP nya adalah **2**.
- **True Negative (TN)** : Kasus dimana model memprediksi foto tersebut anjing (negatif) dan hasil aktualnya adalah anjing (negatif). Pada tabel 24, **Foto 3** merupakan **True Negative**, sehingga TN nya adalah **1**.
- **False Positive (FP)** : Kasus dimana model memprediksi foto tersebut kucing, namun hasil aktualnya adalah anjing. Pada tabel 24, **Foto 2** merupakan **False Positive (FP)**, sehingga FP nya adalah **1**.
- **False Negative (FN)** : Kasus dimana model memprediksi foto tersebut anjing, namun hasil aktualnya adalah kucing. PAda tabel 24, **Foto 4** merupakan **False Negative (FN)**, sehingga FN nya adalah **1**.

Sehingga jika diterapkan pada grafik _confusion matrix_ akan menjadi sebagai berikut.

<p align="center">
	<img src="https://cdn.discordapp.com/attachments/1121095008926302358/1127295277649367160/image.png">
</p>
<p align="center">
Gambar 14. <i>Confusion Matrix</i> berdasarkan hasil dari tabel 24
</p>

Dari _confusion matrix_ ini dapat ditentukan nilai _Accuracy, Precission, Recall_ dan _Specificity_. Karena pendekatan model ini menggunakan _Precission_, maka yang akan dijelaskan disini adalah _pression_.

_Precission_ adalah salah satu metrik evaluasi yang umum digunakan untuk mengukur sejauh mana model klasifikasi benar dalam mengidentifikasi secara akurat. _Precission_ memberikan gambaran tentang seberapa baik model dalam menghindari memberikan hasil _false positive_. _Precission_ yang tinggi menunjukkan bahwa model memiliki sedikit jumlah kesalahan dalam mengklasifikasikan data dengan kelas negatif menjadi positif.

Rumus dalam perhitungan _precission_ matiks adalah sebagai berikut.

$$Precission = \dfrac{TP}{TP + FP}$$

Sebagai contoh, berdasarkan _confusion matrix_ pada gambar 14, nilai **TP** adalah 2 dan nilai **FP** adalah 1, maka hasil perhitungannya adalah sebagai berikut

$$Precission = \dfrac{2}{2 + 1}$$

$$Precission = \dfrac{2}{3}$$

$$Precission = 0.667$$ 

Pada proyek ini, penulis akan melakukan percobaan untuk mendapatkan rekomendasi _anime_ dimana ada **3 judul _anime_** yang akan dijadikan bahan percobaan. Untuk nilai **TP** dapat diberikan jika genre tersebut memiliki relevansi dengan genre dari _anime_ yang jadi patokan. Suatu judul dinyatakan **relevan** jika memenuhi **minimal 2 Genre** yang ada pada _anime_ patokannya.

|       |   MAL_ID | Name                        |   Score | Genres                                              | Type   |
|------:|---------:|:----------------------------|--------:|:----------------------------------------------------|:-------|
|  2839 |     4181 | Clannad: After Story        |    8.96 | Slice of Life, Comedy, Supernatural, Drama, Romance | TV     |
|  6192 |    17549 | Non Non Biyori              |    7.95 | Comedy, School, Seinen, Slice of Life               | TV     |
|  5283 |    11757 | Sword Art Online            |    7.25 | Action, Game, Adventure, Romance, Fantasy           | TV     |

<p align="center">
Tabel 25. Judul <i>anime</i> yang akan dijadikan patokan untuk mendapatkan daftar rekomendasi <i>anime</i>
</p>

Selain itu penulis akan membandingkan hasil rekomendasi yang menggunakan _cosine similarity_ dan _euclidean distance_ dimana hasil nya untuk _anime_ pertama adalah sebagai berikut.

<table>
<thead>
  <tr>
    <th colspan="3">Cosine Similarity</th>
    <th></th>
    <th colspan="4">Euclidean Distance </th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Kanon</td>
    <td>Drama, Romance, Slice of Life, Supernatural</td>
    <td>1</td>
    <td>1</td>
    <td>Air</td>
    <td>Slice of Life, Supernatural, Drama, Romance</td>
    <td>0</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Sola</td>
    <td>Drama, Romance, Slice of Life, Supernatural</td>
    <td>0.941605</td>
    <td>2</td>
    <td>Kanon</td>
    <td>Drama, Romance, Slice of Life, Supernatural</td>
    <td>0.341746</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Kanon (2006)</td>
    <td>Slice of Life, Supernatural, Drama, Romance</td>
    <td>0.941605</td>
    <td>3</td>
    <td>Kanon (2006)</td>
    <td>Slice of Life, Supernatural, Drama, Romance</td>
    <td>0.341746</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Air</td>
    <td>Slice of Life, Supernatural, Drama, Romance</td>
    <td>0.941605</td>
    <td>4</td>
    <td>Sola</td>
    <td>Drama, Romance, Slice of Life, Supernatural</td>
    <td>0.341746</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Sewayaki Kitsune no Senko-san</td>
    <td>Slice of Life, Comedy, Supernatural, Romance</td>
    <td>0.941605</td>
    <td>5</td>
    <td>Sewayaki Kitsune no Senko-san</td>
    <td>Slice of Life, Comedy, Supernatural, Romance</td>
    <td>0.341746</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Little Busters!: EX</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.903943</td>
    <td>6</td>
    <td>Clannad</td>
    <td>Comedy, Drama, Romance, School, Slice of Life, Supernatural</td>
    <td>0.438307</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Kokoro Connect</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.900766</td>
    <td>7</td>
    <td>Kokoro Connect</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.445498</td>
  </tr>
  <tr>
    <td>8</td>
    <td>Little Busters!: Refrain</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.900766</td>
    <td>8</td>
    <td>Kokoro Connect: Michi Random</td>
    <td>Comedy, Drama, Romance, School, Slice of Life, Supernatural</td>
    <td>0.445498</td>
  </tr>
  <tr>
    <td>9</td>
    <td>Clannad</td>
    <td>Comedy, Drama, Romance, School, Slice of Life, Supernatural</td>
    <td>0.900766</td>
    <td>9</td>
    <td>Little Busters!: Refrain</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.445498</td>
  </tr>
  <tr>
    <td>10</td>
    <td>Kokoro Connect: Michi Random</td>
    <td>Comedy, Drama, Romance, School, Slice of Life, Supernatural</td>
    <td>0.900766</td>
    <td>10</td>
    <td>Little Busters!: EX</td>
    <td>Slice of Life, Comedy, Supernatural, Drama, Romance, School</td>
    <td>0.445498</td>
  </tr>
</tbody>
</table>


<p align="center">
Tabel 26. Hasil perbandingan daftar rekomendasi <i>anime</i> menggunakan<i>Cosine Similarity</i> dengan <i>euclidean DIstance</i> dengan judul <i>anime</i> patokan <b>Clannad: After Story</b>
</p>

Berdasarkan hasil dari tabel diatas, keseluruhan _anime_ memiliki kesamaan berdasarkan genre, meskipun semua _anime_ yang ada pada daftar tersebut tidak memiliki genre yang persis sama, contohnya pada 4 _anime_ pertama tidak memiliki genre **comedy**, sedangkan pada anime nomor 5 baik di _cosine similarity_ dan _euclidean distance_ memiliki genre **comedy** namun tidak memiliki genre **Drama**. Dan dikarena genre pada daftar _anime_ tersebut memenuhi setidaknya 2 genre pada _anime_ patokannya, maka  nilai presisi dari rekomendasi pada tabel 26 adalah **100%**. 

Perbedaan antara hasil dari _cosine similarity_ dengan _euclidean distance_ terlihat pada urutan daftar _anime_ nya. Secara kebetulan 4 _anime_ pertama dari hasil rekomendasi menggunakan _euclidean distance_  memiliki kesamaan secara cerita dan pihak produksi _anime_ tersebut. 

Setelah itu berikut ini hasil dari rekomendasi _anime_ dengan judul _anime_ patokannya adalah **Non Non Biyori**.

<table>
<thead>
  <tr>
    <th colspan="3">Cosine Similarity</th>
    <th></th>
    <th colspan="4">Euclidean Distance </th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Hello!! Kiniro Mosaic</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>1</td>
    <td>1</td>
    <td>Hidamari Sketch</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>0</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Himouto! Umaru-chan R</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>2</td>
    <td>A-Channel</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>0</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Non Non Biyori Repeat</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>3</td>
    <td>Recorder to Randoseru Do♪</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>0</td>
  </tr>
  <tr>
    <td>4</td>
    <td>A-Channel</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>4</td>
    <td>Yuyushiki</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>0</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Sakamoto Desu ga?</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>1</td>
    <td>5</td>
    <td>Kiniro Mosaic</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>0</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Hidamari Sketch</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>6</td>
    <td>Non Non Biyori: Okinawa e Ikukoto ni Natta</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>0</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Himouto! Umaru-chan</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>7</td>
    <td>Hello!! Kiniro Mosaic</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>0</td>
  </tr>
  <tr>
    <td>8</td>
    <td>Non Non Biyori: Okinawa e Ikukoto ni Natta</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>1</td>
    <td>8</td>
    <td>Non Non Biyori Repeat</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>0</td>
  </tr>
  <tr>
    <td>9</td>
    <td>Himouto! Umaru-chan OVA</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>1</td>
    <td>9</td>
    <td>Himouto! Umaru-chan</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>0</td>
  </tr>
  <tr>
    <td>10</td>
    <td>Recorder to Randoseru Do♪</td>
    <td>Comedy, School, Seinen, Slice of Life</td>
    <td>1</td>
    <td>10</td>
    <td>Himouto! Umaru-chan OVA</td>
    <td>Slice of Life, Comedy, School, Seinen</td>
    <td>0</td>
  </tr>
</tbody>
</table>


<p align="center">
Tabel 27. Hasil perbandingan daftar rekomendasi <i>anime</i> menggunakan<i>Cosine Similarity</i> dengan <i>euclidean DIstance</i> dengan judul <i>anime</i> patokan <b>Non Non Biyori</b>
</p>

Berdasarkan hasil dari tabel 27 berikut, seluruh _anime_ yang dijadikan rekomendasi memiliki genre yang sama persis dengan _anime_ yang dijadikan patokan. Hal ini bisa dilihat melalui nilai skor dengan nilai _similarity_ sama persis, yaitu 1 untuk _cosine similarity_ dan 0 untuk _euclidean distance_. Sehingga hasil prediksi di tabel 27 memiliki **presisi** sebesar **100%**.

Setelah itu berikut ini hasil dari rekomendasi _anime_ dengan judul _anime_ patokannya adalah **Sword Art Online**.

<table>
<thead>
  <tr>
    <th colspan="3">Cosine Similarity</th>
    <th></th>
    <th colspan="4">Euclidean Distance </th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
    <td>No</td>
    <td>Title</td>
    <td>Genres</td>
    <td>Score</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Sword Art Online II</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>1</td>
    <td>Sword Art Online: Extra Edition</td>
    <td>Action, Adventure, Fantasy, Game, Romance</td>
    <td>0</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Sword Art Online: Alicization</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>2</td>
    <td>Sword Art Online II</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Sword Art Online: Progressive Movie - Hoshi Naki Yoru no Aria</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>3</td>
    <td>Sword Art Online Movie: Ordinal Scale</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Sword Art Online: Extra Edition</td>
    <td>Action, Adventure, Fantasy, Game, Romance</td>
    <td>1</td>
    <td>4</td>
    <td>Sword Art Online: Alicization</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Sword Art Online Movie: Ordinal Scale</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>5</td>
    <td>Sword Art Online: Alicization - War of Underworld</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Sword Art Online: Alicization - War of Underworld</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>6</td>
    <td>Sword Art Online: Alicization - War of Underworld Reflection</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Sword Art Online: Alicization - War of Underworld Reflection</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>7</td>
    <td>Sword Art Online: Alicization - War of Underworld 2nd Season</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>8</td>
    <td>Sword Art Online: Alicization - War of Underworld 2nd Season</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>1</td>
    <td>8</td>
    <td>Sword Art Online: Progressive Movie - Hoshi Naki Yoru no Aria</td>
    <td>Action, Game, Adventure, Romance, Fantasy</td>
    <td>0</td>
  </tr>
  <tr>
    <td>9</td>
    <td>Sword Art Online II: Debriefing</td>
    <td>Action, Adventure, Fantasy, Game</td>
    <td>1</td>
    <td>9</td>
    <td>Sword Art Online II: Debriefing</td>
    <td>Action, Adventure, Fantasy, Game</td>
    <td>0</td>
  </tr>
  <tr>
    <td>10</td>
    <td>.hack//Quantum</td>
    <td>Action, Adventure, Fantasy, Game, Sci-Fi</td>
    <td>0.921154</td>
    <td>10</td>
    <td>.hack//Quantum</td>
    <td>Action, Adventure, Fantasy, Game, Sci-Fi</td>
    <td>0.397105</td>
  </tr>
</tbody>
</table>


<p align="center">
Tabel 28. Hasil perbandingan daftar rekomendasi <i>anime</i> menggunakan<i>Cosine Similarity</i> dengan <i>euclidean DIstance</i> dengan judul <i>anime</i> patokan <b>Sword Art Online</b>
</p>

Berdasarkan hasil dari tabel 28 berikut, hampir _anime_ yang dijadikan rekomendasi merupakan _anime_ dengan _franchise_ yang sama, yaitu _Sword Art Online_ dengan genre yang hampir sama persis dimana ada dua _anime_ yang tidak memiliki genre **Romance** dan satu _anime_ yang justru memiliki genre **Sci-fi**. Meskipun begitu untuk _anime_ terakhir yang memiliki genre **Sci-fi** masih memiliki konsep yang serupa dengan _Sword Art Online_. Sehingga untuk nilai presisi untuk tabel 28 adalah **100%**.

### Collaborative Based Filtetring

Pada pendekatan ini, metrik yang digunakan adalah _Root Mean Square Error (RMSE)_.  _RMSE_ adalah metrik evaluasi yang umum digunakan untuk mengukur sejauh mana prediksi model mendekati nilai sebenarnya. _RMSE_ pada dasarnya merupakan akar kuadrat dari _Mean Square Error (MSE)_. 

Rumus dari _RMSE_ adalah sebagai berikut.

$$RMSE  = \sqrt{\sum_{i = 1}^{n}\dfrac{(\hat y _i- y_i)}{n}}$$

Dimana:

- $n$ : Total data yang diamati / diprediksi
- $\hat y_i$ : Data hasil prediksi
- $y_i$ : Data yang sebenarnya (aktual)

Pada proyek ini, model yang digunakan adalah _**RecommenderNet**_ dengan _optimizer_ yang berbeda, yaitu _**Adam**_ dan _**RMSprop**_ dengan hasil seperti terlihat pada gambar berikut.
 
 <p align="center">
	<img src="https://cdn.discordapp.com/attachments/1121095008926302358/1127500834465394708/model_1_2.png">
</p>
<p align="center">
Gambar 14. Hasil model dengan <i>Optimizer Adams</i> dan <i>RMSprop</i>
</p>

Pada gambar diatas, model dengan _optimizer adam_ memiliki nilai **RMSE** yang tinggi, yaitu **0.4659** untuk latih dan **0.5084** untuk validasi di _epoch_ pertama, dan di _epoch_ berikutnya, nilai **RMSE** terus meningkat.

Sedangkan dengan _optimizer RMSprop_, nilai **RMSE** terus bergerak turun dari **0.3165** untuk latih dan **0.3075** untuk validasi hingga hingga mendapatkan hasil akhir yaitu **0.2248** untuk latih dan **0.2257** untuk validasi. Sehingga model ini menjadi model yang lebih optimal.

## Kesimpulan

Berdasarkan proyek ini dapat disimpulkan sebagai berikut

1. _Anime_ dengan genre _Action_ merupakan _anime_ yang paling populer dan paling banyak ditamatin pentonton
2. Meskipun begitu, _anime_ yang masuk daftar _anime_ populer dan paling banyak ditamatkan juga termasuk _anime_ yang paling banyak di-_drop_ oleh penonton
3. _Anime_ paling banyak rilis di musim Semi dan musim Gugur
4. Mayoritas skor _anime_ berada di _range_ 5.5 hingga 8 dengan rata-rata 6.51
5. _Comedy_ merupakan genre anime yang paling banyak diproduksi, selain genre _action_ dan _fantacy_
6. Mayoritas _anime_ diproduksi dalam format _TV, OVA,_ dan _Movie_
7. Mayoritas pengguna _MyAnimeList_ yang menambahkan _anime_ nya ke dalam daftar _anime_ telah menamatkan judul _anime_ tersebut
8. Berdasarkan hasil dari sistem rekomendasi dengan metode _Content-Based Filtering_, model dengan metode perhitungan _Cosine Similarity_ dan _euclidean Distance_ memberikan hasil yang sama nilai presisi sebesar 100%. Namun pembeda antara kedua metode tersebut adalah posisi dari daftar _anime_ yang direkomendasikan.
9. Berdasarkan hasil dari sistem rekomendasi dengan metode _Collaborative Filtering_, model dengan _optimizer RMSprop_ memberikan hasil yang lebih bak dibandingkan dengan _Adam_ dengan nilai _RMSE_ sebesar 0.2257

## References

​​Girsang, A. S., Al Faruq, B., Herlianto, H. R., & Simbolon, S. (2020). Collaborative  Recommendation System in Users  of Anime Films. Journal  of  Physics: Conference  Series, 1566(1). [https://doi.org/10.1088/1742-6596/1566/1/012057](https://doi.org/10.1088/1742-6596/1566/1/012057)

​Jayaperwira, I., Toto Wibowo, A., & Nurjanah, D. (2023). Anime Rekomendasi Menggunakan Collaborative  Filtering. E-Proceeding  of Engineering, 10(3), 3431–3440.

​Reynaldi, & Istiono, W. (2023). Content-based  Filtering  and Web Scraping in Website  for  Recommended Anime. Asian Journal  of  Research in Computer  Science, 15(2), 32–42. [https://doi.org/10.9734/ajrcos/2023/v15i2318](https://doi.org/10.9734/ajrcos/2023/v15i2318) 


