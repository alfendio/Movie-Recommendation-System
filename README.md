# Laporan Proyek *Machine Learning* 2 - Alfendio Alif Faudisyah

## *Project Domain*
Pada era modern ini film menjadi salah satu media hiburan yang populer di masyarakat. Produksi film yang semakin meningkat dan menghasilkan semakin banyak film yang rilis. Banyaknya film yang ada membuat masyarakat kesulitan untuk menentukan film mana yang ingin ditonton. Oleh karena itu dibuatlah sistem yang dapat memberikan rekomendasi film sesuai preferensi pengguna, sehingga pengguna dapat lebih mudah mendapatkan pilihan film-film yang mungkin disukainya.

## *Business Understanding*
### *Problem Statements*
- Bagaimana cara membuat sistem yang dapat memberikan rekomendasi film dengan peringkat tinggi dari pengguna?  
- Bagaimana cara membuat sistem yang dapat memberikan rekomendasi 10 film untuk pengguna?

### *Goals*
- Membuat sistem yang dapat merekomendasikan film dengan peringkat tinggi dari pengguna.
- Membuat sistem yang dapat merekomendasikan 10 film untuk pengguna.

## *Data Understanding*
Dataset didapatkan dari [*Small MovieLens* Dataset](http://files.grouplens.org/datasets/movielens/ml-latest-small.zip).

### Nama Dataset
- *Small MovieLens* Dataset

### Jumlah Dataset
Dataset *ratings* berisi 100836 baris dan 4 kolom.

### Variabel-variabel pada *ratings* dataset:
- userId : ID dari pengguna
- movieId : ID dari film
- rating : Peringkat film yang diberikan oleh pengguna
- timestamp  : *Time stamp* pada film

## *Data Preparation*
- Mengubah userID menjadi list tanpa nilai yang sama dengan menggunakan fungsi unique().tolist()
- Melakukan *encoding* userID dengan menggunakan fungsi enumerate()
- Melakukan proses *encoding* angka ke ke userID dengan menggunakan fungsi enumerate()
- Mengubah movieID menjadi list tanpa nilai yang sama dengan menggunakan fungsi unique().tolist()
- Melakukan proses *encoding* movieID dengan menggunakan fungsi enumerate()
- Melakukan proses *encoding* angka ke movieID dengan menggunakan fungsi enumerate()
- Mapping userID ke *dataframe* *user* dengan menggunakan fungsi map()
- Mapping movieID ke *dataframe* *movie* dengan menggunakan fungsi map()
- Cek data jumlah *user* dengan menggunakan fungsi len()
- Cek data jumlah film dengan menggunakan fungsi len()
- Mengubah nilai *rating* menjadi *float* dengan menggunakan fungsi astype()
- Mengacak distribusi data dengan menggunakan fungsi sample()
- Membagi dataset untuk *training* 90% dan *validation* 10%

## *Modeling and Results*
Model dibuat menggunakan *Collaborative Filtering* dengan *library* TensorFlow dan Keras. Sistem merekomendasikan sejumlah film berdasarkan *rating* yang telah diberikan sebelumnya. Dari data *rating* pengguna, akan dilakukan identifikasi film yang mirip dan belum pernah ditonton oleh pengguna untuk direkomendasikan. 
Model menggunakan 4 lapisan *layer* *embedding* dengan total *params* 527.034. Teknik *embedding* menghitung skor kecocokan antara pengguna dan film. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi *sigmoid*.

### Model *summary*
![image](https://user-images.githubusercontent.com/73519055/209692272-1bbbe9fa-b3a4-4d2b-bb0a-48fa41a02791.png)

### Parameter model :
- Model : *RecommenderNet*

RecommenderNet dari Keras digunakan untuk membuat model rekomendasi.

- *Loss* : *Binary Cross-Entropy*

*Binary Cross-Entropy* adalah rata-rata negatif dari log probabilitas prediksi yang dikoreksi.

- *Metrics* : *Root Mean Squared Error*

RMSE merupakan besarnya tingkat kesalahan hasil prediksi.

- *Optimizer* : Adam (*Adaptive Moment Estimation*).

 Adam (Adaptive Moment Estimation) adalah metode learning rate adaptif yang menghitung learning rate individu untuk parameter yang berbeda.

- *Learning rate* : 0.001

- *Epoch* : 20

- *Batch size* : 8

- *Verbose* : 1

### *Recommendation results*
#### *Movies with high ratings from user* (*user*: 66)
1. *Sixth Sense*, *The* (1999) : *Drama|Horror|Mystery*
2. *Memento* (2000) : Mystery|Thriller
3. *Punch-Drunk Love* (2002) : *Comedy|Drama|Romance*
4. Gallipoli (1981) : *Drama|War*
5. *Matchstick Men* (2003) : *Comedy|Crime|Drama*

#### *Top* 10 *movie recommendations* (*user*: 66)
1. *Women, The* (1939) : *Comedy*
2. *Sleepers* (1996) : *Thriller*
3. Aladdin *and the King of Thieves* (1996) : *Animation|Children|Comedy|Fantasy|Musical|Romance*
4. *Old Man and the Sea, The* (1958) : *Adventure|Drama*
5. *Nightmare on Elm Street* 2: *Freddy's Revenge, A* (1985) : *Horror*
6. Popeye (1980) : *Adventure|Comedy|Musical*
7. *Red Violin, The (Violon rouge, Le)* (1998) : *Drama|Mystery*
8. AVP: *Alien vs. Predator* (2004) : *Action|Horror|Sci-Fi|Thriller*
9. *Land of the Dead* (2005) : *Action|Horror|Thriller*
10. *Legionnaire* (1998) : *Action|Adventure|Drama|War*


## *Evaluation*
*Metric* evaluasi yang digunakan adalah *Root Mean Squared Error* (RMSE). RMSE merupakan besarnya tingkat kesalahan hasil prediksi, dimana semakin kecil (mendekati 0) nilai maka hasil prediksi akan semakin akurat. RMSE mengukur tingkat akurasi hasil perkiraan suatu model. RMSE dihitung dengan mengkuadratkan *error* (prediksi “ observasi) dibagi dengan jumlah data (= rata-rata), lalu diakarkan.

### *Training Visualization*
![output plot training](https://user-images.githubusercontent.com/73519055/209693012-a605aa93-9239-4f52-aff5-8ce202dfe962.png)

Hasil yang didapat dari visualisasi training adalah loss: 0.5900, val_loss: 0.6091, root_mean_squared_error: 0.1804, dan val_root_mean_squared_error: 0.2003.

### *Evaluation results*
Dilakukan evaluasi pada model menggunakan data *validation* dengan menggunakan fungsi model.evaluate. Hasil penerapan dengan *metric* evaluasi yang digunakan pada gambar visualisasi *training* adalah loss: 0.6227 dan root_mean_squared_error: 0.2132. Dilihat dari nilai RMSE model sudah dapat dibilang baik karena memiliki nilai yang cukup kecil.
