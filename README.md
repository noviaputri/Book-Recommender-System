# Book Recommender System

## Domain Proyek
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
	<p align=justify>Content based filtering adalah sistem rekomendasi yang akan merekomendasikan buku yang mirip dengan buku yang dibaca oleh pembaca di masa lalu. Contoh dari sistem rekomendasi ini yaitu jika pembaca menyukai buku Dilan 1990 karya Pidi Baiq maka sistem akan merekomendasikan buku karya Pidi Baiq lainnya atau buku dengan genre yang sama dengan Dilan 1990. Sistem rekomendasi ini akan semakin akurat, jika data yang diberikan semakin banyak.</p>
  
- Collaborative Based Filtering
	<p align=justify>Collaborative filtering adalah sistem rekomendasi yang didasarkan oleh pendapat komunitas pengguna. Sehingga sistem ini tidak seperti content based filtering yang berdasarkan informasi dari buku, tetapi dilihat dari informasi pengguna lainnya. Collaborative filtering dibagi menjadi dua bagian yaitu : </p>
  
  - Memory Based (metode berbasis memori)
    1. User Based
        <p align=justify>Sistem rekomendasi ini merekomendasikan item berdasarkan kesamaan pengguna. Contohnya jika Sinta dan Rara memberikan rating yang tinggi terhadap buku bergenre fiksi, lalu Sinta menyukai buku The Lord of the Rings maka kemungkinan besar Rara juga akan menyukai buku tersebut.</p>
    2. Item Based
        <p align=justify>Sistem rekomendasi ini merekomendasikan item berdasarkan kesamaan antar item. Contohnya jika Sinta dan Rara menyukai buku The Lord of the Rings dan House of Glass, lalu Tita ternyata menyukai buku House of Glass maka sistem akan merekomendasikan buku The Lord of the Rings kepada Tita karena dianggap mirip dengan buku yang Tita sukai.</p>
      
  - Model Based (metode berbasis model machine learning)
  
    <p align=justify>Model based melibatkan machine learning dalam menganalisa data dan pembuatan rekomendasi. Metode ini bekerja dengan mengekstrak kumpulan data lalu membuat model probabilitas untuk menghasilkan rekomendasi. Dengan metode ini, kita dapat membuat rekomendasi untuk pengguna baru karena pengguna baru tidak akan mengubah model yang sudah ada. Metode model based ini dibagi 2 yaitu matrix factorization dan deep learning.</p>

## Data Understanding
<p align=justify>Dataset yang diambil berasal dari Kaggle. Dataset tersebut berisi data-data tentang buku. Dataset ini dibagi menjadi 3 file csv yang berbeda yaitu books.csv, ratings.csv, dan users.csv. Secara rinci, data-data pada book dataset adalah sebagai berikut:</p>

1. File books.csv

    Pada data buku ini disediakan berbagai informasi seperti berikut :
    - ISBN yang berisi kode ISBN atau ID dari suatu buku.
    - Title yang berisi judul buku.
    - Author yang berisi penulis atau pengarang buku.
    - Tahun publikasi yang berisi pada tahun berapa buku tersebut diterbitkan.
    - Publisher yang berisi informasi mengenai tempat yang mempublish buku tersebut.
    - Image-URL-S yang berisi link gambar berukuran kecil dari buku tersebut.
    - Image-URL-M yang berisi link gambar berukuran sedang dari buku tersebut.
    - Image-URL-L yang berisi link gambar berukuran besar dari buku tersebut.
    
2. File ratings.csv 

    Pada data rating ini disediakan berbagai informasi seperti berikut :
    - UserID yang berisi ID user yang memberikan rating pada buku.
    - ISBN yang berisi ISBN dari buku yang diberikan rating.
    - Book-Rating yang berisi nilai rating yang diberikan oleh pengguna pada buku tersebut.
    
3. File users.csv

    Pada data user ini disediakan berbagai informasi seperti berikut :
    - UserID yang berisi ID dari user.
    - Location yang berisi informasi lokasi dari user.
    - Age yang berisi informasi umur dari user.
	
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

## Modeling
<p align=justify>Untuk menyelesaikan permasalahan yang sudah dijelaskan di atas, pada proyek ini menggunakan 2 jenis metode untuk membuat sistem rekomendasi yaitu Content Based Filtering dan Collaborative Based Filtering. Kedua metode tersebut sama sama akan menghasilkan rekomendasi buku, hanya saja pada content based filtering akan merekomendasikan buku sesuai dengan kesamaan konten pada buku sedangkan pada collaborative based filtering akan merekomendasikan buku berdasarkan data komunitas pengguna. Hasil rekomendasi buku berdasarkan kedua metode tersebut dapat dilihat pada gambar berikut:</p>

- Pada metode Content Based Filtering

  Hasil pencarian rekomendasi buku dengan judul "Horrible Harry and the Green Slime" dan author "Suzy Kline"
  
  [![Content.png](https://i.postimg.cc/85LfZXwK/Content.png)](https://postimg.cc/phXdTZwz)
  
- Pada metode Collaborative Based Filtering

  Hasil pencarian rekomendasi buku dengan user id "243930"
  
  [![colab.png](https://i.postimg.cc/zfZgT1Fb/colab.png)](https://postimg.cc/759hydcw)

## Evaluation
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
    metrics=[tf.keras.metrics.RootMeanSquaredError()]
)
```

***Referensi***
- Dokumentasi RMSE : https://towardsdatascience.com/evaluating-recommender-systems-root-means-squared-error-or-mean-absolute-error-1744abc2beac dan https://www.statisticshowto.com/probability-and-statistics/regression-analysis/rmse-root-mean-square-error/
- Content and Collaborative FIltering : https://www.dicoding.com/academies/319/tutorials/19657

