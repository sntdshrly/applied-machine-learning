# Klasifikasi Rambu Lalu Lintas - Husnan

## Domain Proyek

Beberapa penerapan computer vision yang paling penting untuk self-driving cars adalah kemampuan mendeteksi, mengklasifikasikan, dan melokalisasi berbagai jenis objek. Objek-objek ini bisa berupa kendaraan lain, pejalan kaki, rambu lalu lintas, atau hal aneh lain yang mungkin kita lihat saat mengemudi.
Pada kesempatan kali ini, saya membuat model machine learning terkait dengan penerapan computer vision pada self-driving cars. Saya membuat model klasifikasi gambar dengan data berupa rambu-rambu lalu lintas.

## Business Understanding

### Problem Statements
- Bagaimana self-driving cars memahami peringatan, larangan, perintah, atau petunjuk pada jalan?

### Goals
- Membuat model klasifikasi gambar dengan data berupa rambu-rambu lalu lintas.

## Data Understanding
[German Traffic Sign Dataset](https://www.kaggle.com/datasets/saadhaxxan/germantrafficsigns) merupakan benchmark dataset untuk klasifikasi gambar multi kelas. Terdapat satu rambu lalu lintas pada masing-masing gambar, sehingga dataset ini disebut juga sebagai single-image atau gambar tunggal.

### Variabel-variabel pada German Traffic Sign Dataset adalah sebagai berikut:
|Kelas |Label                                        |Kelas   |Label                                         | 
|------|---------------------------------------------|--------|----------------------------------------------|
|0   	 |Speed limit (20km/h)   	                     |22   	  |Bumpy road   	                               |
|1   	 |Speed limit (30km/h)   	                     |23   	  |Slippery road   	                             |
|2   	 |Speed limit (50km/h)   	                     |24   	  |Road narrows on the right   	                 |
|3   	 |Speed limit (60km/h)   	                     |25   	  |Road work   	                                 |
|4   	 |Speed limit (70km/h)   	                     |26   	  |Traffic signals   	                           |
|5   	 |Speed limit (80km/h)   	                     |27   	  |Pedestrians   	                               |
|6   	 |End of speed limit (80km/h)                  |28   	  |Children crossing   	                         |
|7   	 |Speed limit (100km/h)   	                   |29   	  |Bicycles crossing   	                         |
|8   	 |Speed limit (120km/h)   	                   |30   	  |Beware of ice/snow   	                       |
|9   	 |No passing   	                               |31   	  |Wild animals crossing   	                     |
|10    |No passing for vehicles over 3.5 metric tons |32   	  |End of all speed and passing limits   	       |
|11    |Right-of-way at the next intersection   	   |33   	  |Turn right ahead   	                         |
|12    |Priority road   	                           |34   	  |Turn left ahead   	                           |
|13    |Yield   	                                   |35   	  |Ahead only   	                               |
|14    |Stop   	                                     |36   	  |Go straight or right   	                     |
|15    |No vehicles   	                             |37   	  |Go straight or left   	                       |
|16    |Vehicles over 3.5 metric tons prohibited   	 |38   	  |Keep right   	                               |
|17    |No entry   	                                 |39   	  |Keep left   	                                 |
|18    |General caution   	                         |40   	  |Roundabout mandatory   	                     |
|19    |Dangerous curve to the left   	             |41   	  |End of no passing   	                         |
|20    |Dangerous curve to the right   	             |42   	  |End of no passing by vehicles over 3.5 metric |
|21    |Double curve   	                             |   	    |   	                                         |


## Data Preparation
Pada tahap ini kita akan mengonversi label pada data training dan validasi dengan teknik one hot encoding. Tujuannya agar label, yang sebelumnya merupakan tipe data string menjadi fitur kategorik. Kita akan menggunakan fungsi `to_categorical` dari library tensorflow.

## Modeling
- Implementasi callback pada model. 
- Set training berhenti saat akurasi model mencapai 96%. 
- Set parameter layer pertama sebagai berikut:
  - Ukuran filter untuk proses konvolusi=32
  - Ukuran kernel=(5,5)
  - Fungsi aktivasi RELU
  - Pooling yang kita gunakan adalah Maxpool dengan ukuran 2,2
  - Dropout rate sebesar 0.25
- Selanjutnya, untuk layer kedua, gunakan arsitektur sebagai berikut:
  - Ukuran filter untuk proses konvolusi=64
  - Ukuran kernel=(3,3)
  - Fungsi aktivasi RELU
  - Pooling yang kita gunakan adalah Maxpool dengan ukuran 2,2
  - Dropout rate sebesar 0.25
- Fully connected layer beserta Output dari model summary.
- Melakukan kompilasi model dan memanggil fungsi fit untuk memulai training
- Melakukan plotting untuk mendapatkan grafik akurasi dan loss

## Evaluation
- Metrik evaluasi yang digunakan adalah sebagai berikut:
  - `accuracy_score` untuk menghitung akurasi subset pada klasifikasi banyak kelas.
  - `classification_report` untuk memperoleh metrik klasifikasi lain seperti precision, recall, dan f1-score.
