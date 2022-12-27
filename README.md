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
- Mengubah userID menjadi list tanpa nilai yang sama.
- Melakukan *encoding* userID.
- Melakukan proses *encoding* angka ke ke userID.
- Mengubah movieID menjadi list tanpa nilai yang sama.
- Melakukan proses *encoding* movieID.
- Melakukan proses *encoding* angka ke placeID.
- Mapping userID ke *dataframe* *user*
- Mapping placeID ke *dataframe* *movie*
- Cek beberapa hal dalam data seperti jumlah *user*, jumlah film, dan mengubah nilai *rating* menjadi *float*.
- Mengacak data agar distribusinya menjadi *random*.

## *Modelling*
Model dibuat menggunakan *Collaborative Filtering* dengan *library* TensorFlow dan Keras. Model menghitung skor kecocokan antara pengguna dan film dengan teknik *embedding*. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi *sigmoid*. Sistem merekomendasikan sejumlah film berdasarkan *rating* yang telah diberikan sebelumnya. Dari data *rating* pengguna, akan dilakukan identifikasi film yang mirip dan belum pernah ditonton oleh pengguna untuk direkomendasikan. 

### Rangkuman Model
![image](https://user-images.githubusercontent.com/73519055/209692272-1bbbe9fa-b3a4-4d2b-bb0a-48fa41a02791.png)

### Parameter model :
- Model : *RecommenderNet*
- *Loss* : *Binary Cross-Entropy*
- *Metrics* : *Root Mean Squared Error*
- *Optimizer* : Adam (*Adaptive Moment Estimation*) 
- *Learning rate* : 0.001
- *Epoch* : 20
- *Batch size* : 8
- *Verbose* : 1

## *Evaluation*
*Metric* evaluasi yang digunakan adalah *Root Mean Squared Error* (RMSE). RMSE merupakan besarnya tingkat kesalahan hasil prediksi, dimana semakin kecil (mendekati 0) nilai maka hasil prediksi akan semakin akurat. RMSE mengukur tingkat akurasi hasil perkiraan suatu model. RMSE dihitung dengan mengkuadratkan *error* (prediksi “ observasi) dibagi dengan jumlah data (= rata-rata), lalu diakarkan.

### *Training Visualization*
![output plot training](https://user-images.githubusercontent.com/73519055/209693012-a605aa93-9239-4f52-aff5-8ce202dfe962.png)

Hasil yang didapat dari visualisasi training adalah loss: 0.5900, val_loss: 0.6091, root_mean_squared_error: 0.1804, dan val_root_mean_squared_error: 0.2003.

### Hasil Evaluasi
Dilakukan evaluasi pada model menggunakan data *validation* dengan menggunakan fungsi model.evaluate. Hasil penerapan dengan *metric* evaluasi yang digunakan pada gambar visualisasi *training* adalah loss: 0.6227 dan root_mean_squared_error: 0.2132. Dilihat dari nilai RMSE model sudah dapat dibilang baik karena memiliki nilai yang cukup kecil.
