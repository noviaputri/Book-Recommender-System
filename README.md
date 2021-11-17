# Book Recommender System

## Project Overview
<p align=justify>Pada proyek ini mengambil permasalahan tentang sistem rekomendasi. Sistem rekomendasi merupakan suatu aplikasi untuk menyediakan dan merekomendasikan suatu item dalam membuat suatu keputusan yang diinginkan oleh pengguna (Ungkawa, et al., 2013). Topik yang diambil yaitu sistem rekomendasi pada buku. Pada dasarnya di suatu perpustakaan atau tempat jual buku memang disediakan fitur pencarian buku, tetapi fitur tersebut mungkin hanya sebatas mencari berdasarkan judul, pengarang, atau tahun terbit. Dengan begitu akan memunculkan banyak buku berdasarkan pencarian tersebut, sehingga membuat pengguna/pencari bingung serta membutuhkan waktu yang lama dalam menentukan pilihan buku apa yang sesuai dengan kebutuhannya. Untuk itulah dibuat sistem rekomendasi buku untuk menyediakan pilihan buku berdasarkan keinginan atau kebutuhan pengguna. Sistem rekomendasi ini akan lebih mengefektifkan proses pencarian buku serta efisien dari segi waktu karena nantinya buku yang akan direkomendasikan tidak sebanyak dengan fitur pencarian biasa sehingga dapat lebih menghemat waktu dalam proses pemilihannya.

Link jurnal terkait : 
[Referensi 1](https://iopscience.iop.org/article/10.1088/1742-6596/1477/3/032024/meta "Referensi 1") dan [Referensi 2](http://e-journal.uajy.ac.id/8852/4/3TF06448.pdf "Referensi 2")
  
## Business Understanding
### Problem Statements
- Bagaimana cara membuat sistem rekomendasi buku berdasarkan data yang sudah ada?
- Fitur apa yang paling mempengaruhi dari sistem rekomendasi buku?
### Goals
- Mampu membuat sistem rekomendasi buku yang efisien dan akurat.
- Dapat mengetahui fitur-fitur apa saja yang sangat mempengaruhi sistem rekomendasi buku.
### Solution statements
<p align=justify>Berdasarkan permasalahan yang ada di atas, maka solusi yang akan ditawarkan yaitu membuat sistem rekomendasi buku dengan efisien dan akurat menggunakan 2 metode yaitu :</p>

- Content Based Filtering
	<p align=justify>Content based filtering adalah sistem rekomendasi yang nantinya akan merekomendasikan buku yang mirip dengan buku yang dibaca oleh pembaca di masa lalu. Contoh dari sistem rekomendasi ini yaitu jika pembaca menyukai buku Dilan 1990 karya Pidi Baiq maka sistem akan merekomendasikan buku karya Pidi Baiq lainnya. Sistem rekomendasi ini akan semakin akurat, jika data yang diberikan semakin banyak. Pada metode ini nantinya menggunakan TF-IDF Vectorizer untuk menemukan representasi fitur penting dari setiap author buku dan menggunakan cosine similarity untuk menghitung derajat kesamaan (similarity degree) antar buku.</p>
  
- Collaborative Based Filtering
	<p align=justify>Collaborative filtering adalah sistem rekomendasi yang didasarkan oleh pendapat komunitas pengguna. Sehingga sistem ini tidak seperti content based filtering yang berdasarkan informasi dari buku saja, tetapi dilihat dari informasi pengguna lainnya. Metode ini nantinya menghasilkan rekomendasi sejumlah buku yang sesuai dengan preferensi pengguna berdasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna, selanjutnya akan mengidentifikasi buku-buku yang mirip dan belum pernah dibaca oleh pengguna untuk direkomendasikan.

## Data Understanding
<p align=justify>Dataset yang diambil berasal dari Kaggle. Dataset tersebut dikumpulkan oleh Cai-Nicolas Ziegler dalam 4 minggu (August/September 2004) dari Book-Crossing community atas izin dari Ron Hornbaker (CTO dari Humankind Systems). Dataset ini dibagi menjadi 3 file csv yang berbeda yaitu books.csv, ratings.csv, dan users.csv. Secara rinci, data-data pada book dataset tersebut adalah sebagai berikut:</p>

1. File books.csv

    Pada data buku ini terdapat 271360 baris data yang masing-masing memiliki informasi seperti berikut :
    - ISBN yang berisi kode ISBN atau ID dari suatu buku.
    - Title yang berisi judul buku.
    - Author yang berisi penulis atau pengarang buku.
    - Tahun publikasi yang berisi pada tahun berapa buku tersebut diterbitkan.
    - Publisher yang berisi informasi mengenai tempat yang mempublish buku tersebut.
    - Image-URL-S yang berisi link gambar berukuran kecil dari buku tersebut.
    - Image-URL-M yang berisi link gambar berukuran sedang dari buku tersebut.
    - Image-URL-L yang berisi link gambar berukuran besar dari buku tersebut.
    
    Informasi selengkapnya mengenai data buku dapat dilihat pada gambar berikut :
    
    [![bookinfo.png](https://i.postimg.cc/B6mDPScT/bookinfo.png)](https://postimg.cc/5YFjZMry)
    
2. File ratings.csv 

    Pada data rating ini terdapat 1149780 baris data yang masing-masing memiliki informasi seperti berikut :
    - UserID yang berisi ID user yang memberikan rating pada buku.
    - ISBN yang berisi ISBN dari buku yang diberikan rating.
    - Book-Rating yang berisi nilai rating yang diberikan oleh pengguna pada buku tersebut.
    
    Informasi selengkapnya mengenai data rating dapat dilihat pada gambar berikut :
    
    [![ratinginfo.png](https://i.postimg.cc/zGYLBHYm/ratinginfo.png)](https://postimg.cc/fJ5WqLb5)
    
3. File users.csv

    Pada data user ini terdapat 278858 baris data yang masing-masing memiliki informasi seperti berikut :
    - UserID yang berisi ID dari user.
    - Location yang berisi informasi lokasi dari user.
    - Age yang berisi informasi umur dari user.
    
    Informasi selengkapnya mengenai data user dapat dilihat pada gambar berikut :
    
    [![userinfo.png](https://i.postimg.cc/2SY4tK6B/userinfo.png)](https://postimg.cc/mtdzzV7b)

Untuk menelaah lebih lanjut informasi dari data-data tersebut, maka dibuatlah visualisasi data sebagai berikut :

- Membuat histogram pada data umur untuk melihat persebaran umur user

	[![histo1.png](https://i.postimg.cc/L8C9jdKk/histo1.png)](https://postimg.cc/RWtxzD0q)
	
	<p align=justify>Pada histogram di atas dapat diketahui bahwa terdapat beberapa user yang memiliki data umur 0 tahun atau lebih dari 100 tahun. Dan rata-rata umur user paling banyak terdapat pada rentang 0-50 tahun. Untuk mengatasi hal tersebut maka selanjutnya data akan dilakukan proses cleaning yang akan dilakukan pada tahap data preparation.</p>
	
- Membuat pairplot untuk melihat hubungan antar fitur numerik pada data ratings

	[![rating1.png](https://i.postimg.cc/wv5ncJRK/rating1.png)](https://postimg.cc/LYXymJVv)
	
	<p align=justify>Pada pairplot di atas dapat diketahui bahwa nilai rating yang diberikan oleh user bermacam macam, mulai dari 0 hingga 10 semuanya terdapat di dalam data rating. Lalu dapat diketahui juga bahwa rating yang paling banyak diberikan adalah rating 0.</p>
	
- Membuat pairplot untuk melihat hubungan antar fitur numerik pada data users

	[![user.png](https://i.postimg.cc/y6PwDmzc/user.png)](https://postimg.cc/yWDf5Sx8)
	
	<p align=justify>Pada pairplot di atas dapat diketahui bahwa umur user memang sangat bervariasi tetapi yang paling banyak terletak pada rentang 0-100 tahun. Walaupun begitu ternyata juga ada user dengan umur 100 tahun ke atas.</p>
	
[Link download dataset](https://www.kaggle.com/arashnic/book-recommendation-dataset?select=Books.csv "Dataset Kaggle")

## Data Preparation
Pada tahap data preparation ini dibagi menjadi 3 tahap pengerjaan yaitu :
- Mengatasi kerancuan pada data
   
  <p align=justify>Proses ini dilakukan untuk mengatasi data yang tidak tepat posisinya atau nilainya. Kerancuan pertama terdapat pada kolom tahun publikasi. Dapat dilihat pada gambar di bawah ini adalah nilai unik pada tahun publikasi. Pada gambar tersebut terdapat tahun publikasi yang berisi 'DK Publishing Inc' dan 'Gallimard' yang mana jika dilihat sepertinya adalah publisher, sehingga dapat diartikan bahwa bisa saja data tersebut terdapat kesalahan dalam meletekkan nilai pada kolomnya.</p>
   
  [![tahun1.png](https://i.postimg.cc/R0cwDYb6/tahun1.png)](https://postimg.cc/sBgBBTzs)
  
  Selanjutnya maka dilihat secara spesifik pada baris data yang salah tersebut.
  
  [![tahun2.png](https://i.postimg.cc/nLR9gtGL/tahun2.png)](https://postimg.cc/06SNKF3g)
  [![tahun3.png](https://i.postimg.cc/L4ZgCwYH/tahun3.png)](https://postimg.cc/14sz4WrT)
  
  <p align=justify>Dapat dilihat pada gambar di atas bahwa memang terjadi kesalahan dalam meletakkan nilai dari beberapa kolom, sehingga hal yang perlu dilakukan adalah meletakkan ulang nilai pada kolom-kolom tersebut sesuai dengan tempatnya dengan contoh program sebagai berikut :</p>
  
  ```python
     all_data.loc[all_data.ISBN == '078946697X','Book-Title'] = "DK Readers: Creating the X-Men, How It All Began (Level 4: Proficient Readers)"
     all_data.loc[all_data.ISBN == '078946697X','Book-Author'] = "Michael Teitelbaum"
     all_data.loc[all_data.ISBN == '078946697X','Year-Of-Publication'] = 2000
     all_data.loc[all_data.ISBN == '078946697X','Publisher'] = "DK Publishing Inc"
  ```
  
  <p align=justify>Kerancuan selanjutnya terdapat pula pada tahun publikasi yaitu nilai tahunnya, dimana terdapat beberapa data yang memiliki tahun publikasi 0 atau lebih dari 2004. Karena dapat dilihat pada sumber data terdapat informasi bahwa dataset tersebut dibuat pada tahun 2004 sehingga kecil sekali kemungkinan bahwa tahun publikasi buku akan lebih dari tahun 2004. Jadi hal yang akan dilakukan yaitu menghapus data dengan tahun publikasi 0 atau lebih dari 2004 dengan kode program sebagai berikut :</p>
  
  ```python
  # mengubah tahun yang lebih dari 2004 dan sama dengan 0 menjadi nan
  all_data.loc[(all_data['Year-Of-Publication'] > 2004) | (all_data['Year-Of-Publication'] == 0), 'Year-Of-Publication'] = np.nan
  all_data = all_data.dropna()
  ```
 
- Mengatasi missing value

  Pada data dicek jumlah missing value untuk melihat apakah data tersebut terdapat missing value atau tidak. Hasil pengecekan dapat dilihat pada gambar di bawah ini :
  
  [![missing.png](https://i.postimg.cc/JhWp0ZfX/missing.png)](https://postimg.cc/sMwY0QDf)
  
  <p align=justify>Pada gambar tersebut dapat dilihat bahwa missing value yang paling banyak terdapat pada kategori umur, lalu untuk menelaah lebih lanjut dilihat lagi nilai unik pada kolom umur dengan hasil sebagai berikut :</p>
  
  [![umur.png](https://i.postimg.cc/Nfd4YZ4W/umur.png)](https://postimg.cc/9rqTY8sp)
  
  <p align=justify>Pada gambar diatas dapat dilihat bahwa umur user sangat bervariasi sekali bahkan selain memiliki nilai null ternyata jugga terdapat beberapa umur yang jika dipikir secara logika tidak masuk akal yaitu ada umur 0 dan juga bahkan banyak yang diatas 100. Untuk mengatasi hal tersebut maka pada kategori umur diganti nilai umur yang lebih dari 80 tahun atau kurang dari 5 tahun dengan nilai null, lalu nilai null diganti dengan nilai rata-rata umur dengan kode program sebagai berikut :</p>
  
  ```python
    # merubah umur lebih dari 80 tahun atau kurang dari 5 tahun menjadi nan
    all_data.loc[(all_data.Age > 80) | (all_data.Age < 5), 'Age'] = np.nan
    # mengganti nan dengan nilai mean
    all_data['Age'] = all_data['Age'].fillna(all_data['Age'].mean())
  ```
  
  Selanjutnya untuk nilai missing value yang lainnya akan di drop saja dengan kode program sebagai berikut :
  
  ```python
    all_data = all_data.dropna()
  ```

- Mengubah tipe data yang tidak sesuai

	<p align=justify>Dapat dilihat pada nilai unik kolom tahun publikasi dan umur terdapat tipe data yang berbeda yaitu object, float, dan integer. Padahal pada kolom tersebut seharusnya memiliki tipe data integer saja. Maka dari itu tipe data pada kolom tersebut harus diubah agar seluruh data pada kolom tersebut memiliki tipe data yang sama yaitu integer. Perubahan tipe data dilakukan dengan code program sebagai berikut :</p>
  
  ```python
    # mengubah tipe data yang tidak sesuai 
    all_data['Year-Of-Publication'] = all_data['Year-Of-Publication'].astype(int)
    all_data['Age'] = all_data['Age'].astype(int)
  ```

- Normalisasi nilai rating
	<p align=justify>Teknik ini dilakukan agar nilai pada variabel rating tidak memiliki rentang nilai yang terlalu jauh. Hal ini membantu untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Data dengan skala relatif sama atau mendekati distribusi normal akan lebih mudah serta memiliki performa yang lebih baik untuk dimodelkan. Teknik normalisasi data yang digunakan adalah min max scaler yang bekerja dengan cara mengurangi nilai fitur dengan nilai minimum fitur tersebut, kemudian dibagi dengan rentang nilai fitur tersebut atau nilai maksimum dikurangi nilai minimum dari fitur. Normalisasi nilai rating dilakukan dengan code program sebagai berikut :</p>
	
  ```python
     y = df['Book-Rating'].apply(lambda x: (x - min_rating) / (max_rating - min_rating)).values
  ```

- Train test split
	<p align=justify>Proses selanjutnya pada data preparation yaitu train test split. Proses ini dilakukan dengan tujuan membagi data latih dan data uji sesuai dengan porsi yang diinginkan. Hal ini dilakukan agar nantinya tidak mengotori data uji dengan informasi yang kita dapat dari data latih karena data uji akan berperan sebagai data baru. Pada proyek ini train test split dibagi dengan rasio 80:20, dimana 80% dari keseluruhan data berperan sebagai data latih dan 20% sisanya berperan sebagai data uji.</p>

## Modeling and Result
<p align=justify>Untuk menyelesaikan permasalahan yang sudah dijelaskan di atas, pada proyek ini menggunakan 2 jenis metode untuk membuat sistem rekomendasi yaitu Content Based Filtering dan Collaborative Based Filtering. Kedua metode tersebut sama sama akan menghasilkan rekomendasi buku, hanya saja pada content based filtering akan merekomendasikan buku sesuai dengan kesamaan konten pada buku sedangkan pada collaborative based filtering akan merekomendasikan buku berdasarkan data komunitas pengguna. Hasil rekomendasi buku berdasarkan kedua metode tersebut dapat dilihat pada gambar berikut:</p>

- Pada metode Content Based Filtering

  <p align=justify>Pada metode ini dilakukan pemodelan dengan membuat satu fungsi yang berisi 4 parameter yaitu nama_book, similarity_data, items, dan k. Parameter nama_book bertipe data string yang akan diisikan dengan judul buku, lalu parameter similarity_data yang berisi kesamaan antara buku satu dengan yang lainnya berdasarkan judul buku. Parameter items berisi judul buku dan author yang digunakan untuk mendefinisikan kemiripan, lalu yang terakhir parameter k yang bertipe data integer untuk mendefinisikan banyaknya jumlah buku yang akan direkomendasikan. Hasil pencarian rekomendasi buku dengan judul "Horrible Harry and the Green Slime" dan author "Suzy Kline" : </p>
  
  [![Content.png](https://i.postimg.cc/85LfZXwK/Content.png)](https://postimg.cc/phXdTZwz)
  
- Pada metode Collaborative Based Filtering

  <p align=justify>Pada metode ini dilakukan pemodelan dengan membuat satu fungsi yang berisi 3 parameter yaitu num_users (jumlah user), num_book (jumlah buku), dan embedding_size. Proses compile menggunakan binary crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. Hasil pencarian rekomendasi buku dengan user id "243930" :</p>
  
  [![colab.png](https://i.postimg.cc/zfZgT1Fb/colab.png)](https://postimg.cc/759hydcw)

<p align=justify>Baik content based filtering maupun collaborative filtering tentunya memiliki kekurangan dan kelebihan masing-masing. Salah satu kekurangan yang terdapat pada content based filtering yaitu hanya dapat digunakan untuk fitur yang sesuai serta barang yang di spesialisasi secara berlebihan. Sedangkan kekurangan yang terdapat pada collaborative filtering yaitu akan menghasilkan data yang kurang akurat ketika penilaian pada satu data terlalu sedikit dan akan menjadi salah persepsi.</p>

## Evaluation

- Content Based Filtering
	<p align=justify>Untuk mengukur kinerja metode content based filtering dilakukan dengan menghitung presisi secara manual yaitu dengan membagi jumlah buku relevan yang direkomendasikan dengan jumlah rekomendasi keseluruhan.
	
- Collaborative Based Filtering
	<p align=justify>Untuk mengukur kinerja metode collaborative based filtering, maka digunakanlah metrik evaluasi yaitu Root Mean Squared Error (MSE). Metrik ini adalah standar deviasi dari residual (kesalahan prediksi). Residual adalah ukuran seberapa jauh dari titik data garis regresi dan RMSE adalah ukuran seberapa menyebar residu ini. Hal ini dapat memberi tahu kita seberapa terkonsentrasi data di sekitar garis yang paling cocok. Metrik ini juga biasanya digunakan untuk mengevaluasi kinerja sistem rekomendasi. Salah satu kecenderungan Root Mean Squared Error adalah cenderung menghukum kesalahan besar secara tidak proporsional karena residual (kesalahan) dikuadratkan. Ini berarti RMSE lebih rentan terpengaruh oleh outlier atau prediksi buruk. Namun, jika istilah kesalahan mengikuti distribusi normal, T. Chai dan R. R. Draxler menunjukkan bahwa menggunakan RSME memungkinkan untuk merekonstruksi kumpulan kesalahan, dengan data yang cukup. Selain itu, RSME tidak menggunakan Nilai Absolut, yang jauh lebih nyaman secara matematis saat menghitung jarak, gradien, atau metrik lainnya. Itu sebabnya sebagian besar fungsi biaya dalam Machine Learning lebih memilih menggunakan sum of squared errors atau Root Mean Squared Error. Rumus dari RMSE dapatdilihat pada gambar berikut :</p>

	[![rmse.png](https://i.postimg.cc/6q0kfwZ9/rmse.png)](https://postimg.cc/JHsYRfKg)

	Keterangan:
	<br>f = forecasts (nilai yang diharapkan atau hasil yang tidak diketahui)
	<br>o = observed values (hasil yang diketahui)

	Cara mengimplementasikan RMSE pada program yaitu menggunakan kode program sebagai berikut :

	```python
	model.compile(
    		loss = tf.keras.losses.BinaryCrossentropy(),
    		optimizer = keras.optimizers.Adam(learning_rate=0.001),
    		metrics=[tf.keras.metrics.RootMeanSquaredError()])
	```

	Hasil evaluasi pada sistem rekomendasi buku dengan metode collaborative based filtering dapat dilihat pada grafik berikut :

	[![metrics.png](https://i.postimg.cc/wTTNcpR3/metrics.png)](https://postimg.cc/WtCtTxnP)

	<p align=justify>Pada grafik tersebut dapat diketahui bahwa proses training model cukup smooth dan model ditraining sebanyak 100 epochs. Dari proses tersebut, diperoleh nilai error akhir sebesar sekitar 0.02 dan error pada data validasi sebesar 0.36. Nilai tersebut dapat dikatakan cukup bagus untuk sistem rekomendasi.</p>

***Referensi***
- Dokumentasi RMSE : 
   1. [Towardsdatascience](https://towardsdatascience.com/evaluating-recommender-systems-root-means-squared-error-or-mean-absolute-error-1744abc2beac) 
   2. [Statisticshowto](https://www.statisticshowto.com/probability-and-statistics/regression-analysis/rmse-root-mean-square-error/)
- Content and Collaborative FIltering : 
   1. [Dicoding Academy](https://www.dicoding.com/academies/319/tutorials/19657) 
   2. [Jurnal Unikom](https://elib.unikom.ac.id/files/disk1/747/jbptunikompp-gdl-rendinusap-37304-7-unikom_r-i.pdf)

