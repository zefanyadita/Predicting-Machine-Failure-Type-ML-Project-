# Predictive Failure Machine System - Machine Learning Project Report

## Domain Proyek

Perkembangan industri modern, khususnya yang berkaitan dengan konsep Industri 4.0, memerlukan interaksi mesin manufaktur, sensor, dan perangkat lunak khusus untuk menjamin efisiensi, produktivitas, dan keandalan proses produksi yang lebih baik [[1](https://www.researchgate.net/publication/337895714_Development_of_tools_utilization_monitoring_system_on_labor-intensive_manufacturing_industries)][[2](https://www.mdpi.com/2076-3417/11/12/5725)][[3](https://www.mdpi.com/1424-8220/20/23/6783)]. Salah satu aspek penting dalam menjamin kelangsungan proses produksi adalah dengan prediksi kerusakan pada alat yang digunakan. Seiring dengan otomatisasi dan digitalisasi, revolusi industri 4.0 memperkenalkan konsep pemeliharaan prediktif. Pemeliharaan Prediktif atau *Predictive Maintenance System* (PM) adalah metode untuk memantau status atau kerusakan pada mesin untuk mencegah kegagalan yang mahal terjadi dan untuk melakukan pemeliharaan ketika benar-benar diperlukan [[4](https://www.mdpi.com/1424-8220/23/23/9346#B1-sensors-23-09346)][[5](https://www.sciencedirect.com/science/article/pii/S240589631931122X)]. Estimasi yang tepat memungkinkan perusahaan untuk mengurangi biaya yang terkait sebagai akibat kerusakan pada masing-masing alat atau mesin [[6](https://www.mdpi.com/2076-3417/13/8/4971)].

Pemeliharaan Prediktif menggabungkan kemampuan pengumpulan data dengan kapasitas untuk melakukan analisis yang efektif dan terintegrasi (*Machine Learning*) [[7](https://ieeexplore.ieee.org/document/8449150)]. Teknik pembelajaran mesin (ML) muncul sebagai alat yang menjanjikan dalam aplikasi PM untuk memprediksi kegagalan peralatan guna meminimalkan waktu henti dan mendapatkan keuntungan bagi perusahaan. Secara khusus, metode regresi sering digunakan untuk memprediksi kerusakan peralatan karena kemampuannya dalam memodelkan hubungan antara variabel yang berbeda [[8](https://www.sciencedirect.com/science/article/abs/pii/S0141029620340633)].

## Business Understanding
Pengembangan model *Predictive Failure Machine System* memiliki potensi yang signifikan sebagai alat bantu dalam pengambilan keputusan khususnya pada bidang industri dan manufaktur.

*Predictive Failure Machine System* adalah sistem yang memiliki potensi besar dalam meningkatkan efisiensi operasional, mengurangi downtime produksi, meningkatkan keselamatan dan kesehatan pekerja, serta meningkatkan kualitas produk dan membantu perusahaan untuk tetap kompetitif di pasar yang semakin kompetitif dan dinamis.

### Problem Statements
- Berdasarkan eksplorasi *dataset*, fitur apa saja yang mempengaruhi dalam menentukan kerusakan mesin?
- Bagaimana mengolah *dataset* agar dapat dibuat model prediksi kerusakan mesin?
- Bagaimana cara meningkatkan nilai perfoma model prediksi kerusakan mesin?

### Goals
- Mengeksplorasi semua fitur yang tersedia pada *dataset* untuk melihat korelasi dan faktor apa saja yang paling berpengaruh sampai paling kurang berpengaruh terhadap kerusakan mesin.
- Melakukan proses *data wragling* dan *data preparation* terhadap *dataset* untuk membuat prediksi kerusakan mesin.
- Melakukan beberapa variasi model untuk mendapatkan model yang paling baik dari beberapa model yang telah dibuat untuk prediksi kerusakan mesin.

### Solution statements
- Untuk eksplorasi fitur dilakukan Analisis Univariat, Analisis Bivariat dan Analisis Multivariat. Analisis Univariat dilakukan untuk mengeksploasi data numerik dan data kategorik. Analisis Bivariat dilakukan untuk melihat hubungan antar 2 fitur. Analisis Multivariat dilakukan untuk melihat hubungan antar fitur. Teknik yang digunakan adalah penggunaan catplot, pairplot, serta heatmap untuk melihat *Correlation Matrix* dari fitur yang dimiliki.
- Dilakukan proses *Data Wragling* yang meliputi *Data Gathering*, *Data Assessing*, dan *Data Cleaning* untuk mendapatkan model prediksi.
- Untuk mengetahui perfoma model dilakukan pengecekan performa dengan metrik evaluasi.

## Data Understanding
Data yang digunakan dalam pembuatan model merupakan data sekunder. Data diambil dari Kaggle dengan nama dataset yaitu *Machine Predictive Maintenance Classification*. 

URL: https://www.kaggle.com/datasets/shivamb/machine-predictive-maintenance-classification

Berikut merupakan detail dari *dataset* yang digunakan untuk pembuatan model:
- Dataset berupa CSV
- Dataset terdiri dari 10000 records dengan 10 buah fitur yang diukur.
- Dataset terdiri dari 3 data kategori, dan 7 data numerik.

### Variabel-variabel *dataset*
- UID: Nilai unik yang menunjukkan bahwa setiap data berhubungan dengan peristiwa tertentu dalam proses manufaktur (nilai 1 - 10.000).
- Product ID: Nomor seri khusus dari Type. Hal ini mengindikasikan jenis atau variasi produk yang berbeda yang diproduksi oleh mesin.
- Type: Varian Kualitas Produk, teridir dari 3 kategori, Low (L) (50% dari seluruh produk), Medium (M) (30%), dan High (H) (20%).
- Air Temperature [K]: Suhu Udara yang dihasilkan menggunakan proses random walk kemudian dinormalisasi ke standar deviasi 2 K sekitar 300 K.
- Process Temperature [K]: Suhu Proses pada mesin yang dihasilkan menggunakan proses random walk dan dinormalisasi.
- Rotational Speed [rpm]: Kecepatan rotasi mesin, yang dihitung berdasarkan daya 2860 W dan termasuk kebisingan yang terdistribusi secara normal.
- Torque [Nm]: Torsi yang diterapkan pada mesin, biasanya terdistribusi sekitar 40 Nm dengan min T = 10 Nm dan tidak ada nilai negatif.
- Tool Wear [min]: Keausan alat berhubungan dengan varian kualitas mesin (H/M/L). Hal ini menunjukkan bahwa alat digunakan bersama dengan mesin selama proses manufaktur.
- Target: Mesin gagal atau tidak yang dinilai dengan 0 atau 1.
- Failure Type: Menyatakan jenis kegagalan mesin. Terdapat 5 jenis kegagalan, yaitu *Tool Wear Failure* (TWF), *Heat Dissipation Failure* (HDF), *Power Failure* (PWF), *Overstrain Failure* (OSF), *Random Failures* (RNF).

### Data Analysis (EDA)
Untuk memahami data lebih lanjut, dilakukan Analisis Univariat, Analisis Bivariate dan Analisis Multivariat, serta Visualisasi Data melalui EDA. EDA/*Exploratory Data Analysis* adalah proses analisis data yang digunakan untuk menjelajahi, memahami, dan meringkas karakteristik dasar dari dataset secara visual dan deskriptif. Tujuan utama dari EDA adalah untuk memahami struktur dataset, menemukan pola atau tren yang menarik, serta mempersiapkan data untuk tahap analisis yang lebih lanjut.


Analisis Univariat

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel. Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu *dataset*. Berikut adalah visualisasi EDA dari Analisis Univariate dari data kategori dan numerik:

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/c2280e4e-456f-48ab-ab45-94a5ac16f109)

Gambar 3.1 Analisis Univariat *Type* (Data Kategori)

Berdasarkan Gambar 3.1, diketahui bahwa terdapat 3 variansi kualitas mesin, yaitu Low (L), Medium (M), dan High (H). *Dataset* di dominansi oleh Tipe mesin 'L' yang berjulah 6000 buah, Tipe 'M' berjumlah 2997 buah, dan Tipe 'H' berjumlah 1003 buah.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/117491cb-6618-47c9-8cf2-000ca6abd98c)

Gambar 3.2 Analisis Univariat *Failure Type* (Data Kategori)

Berdasarkan Gambar 3.2, diketahui bahwa distribusi data kategori 'Failure Type' memiliki perbandingan jumlah yang tidak sama. Data di dominansi oleh data kategori 'No Failure' dengan nilai 9652. Sementara itu, data paling sedikit adalah kategori 'Random Failures' dengan nilai 18.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/74ea97eb-ef04-4bfd-9502-d78be24484b1)

Gambar 3.3 Analisis Univariat (Data Numerik)

Berdasarkan Gambar 3.3, Diketahui karakteristik dari data numerik adalah sebagai berikut:
- Terdapat 600 mesin yang memiliki suhu udara (Air Tmeperature [K]) antara 297K hingga 303K. Sementara sisanya memiliki suhu udara yang lebih rendah selama bekerja.
- Terdapat  lebih dari 800 mesin yang mencapai suhu proses (Process Tmeperature [K]) antara 310K hingga 311K. Juga mesin lain yang suhunya berada di antara 308K hingga 312K selama pemrosesan.
- Terdapat  600 mesin yang mencapai putaran rotasi (Rotation Speed [rpm]) 1500 rpm, 500 mesin mencapai kecepatan rotasi 1400 hingga 1500 rpm, dan hanya ada sedikit mesin yang mencapai kecepatan rotasi maksimum 2000 rpm, mungkin kurang dari 100 mesin.
- Terdapat  500 mesin yang mencapai torsi (Torque [Nm])antara 35Nm hingga 45Nm.
- Terdapat  mesin yang mungkin menghadapi kegagalan karena keausan pahat(Tool Wear [min]) (min) hingga 220 keausan pahat min.


Anaisis Bivariat

Analisis Bivariat adalah analisis statistik yang dilakukan untuk memahami hubungan antara dua variabel dalam sebuah *dataset*. Ini melibatkan hubungan atau ketergantungan antara dua variabel secara bersama-sama. Berikut adalah visualisasi EDA dari Analisis Bivariat:

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/ec915b5a-1ca7-40a8-81fb-7a0980332844)

Gambar 3.4 Analisis Bivariate antara kategori 'Target' dengan Fitur *dataset*

Berdasarkan Gambar 3.4, Hubungan antara setiap fitur dengan kategori 'Type' di dominansi oleh data dengan nilai Target 0, hal ini berbanding lurus dengan lebih banyaknya data dengan jenis kegagalan 'No Failure' dibanding dengan jenis kegagalan lainnya.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/e462cff7-2b2c-4d88-aeb9-32c94d0dc5e0)

Gambar 3.5 Analisis Bivariate antara Data Numerik dengan *Failure Type*

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/8be596c8-a4a5-48c0-9aca-d35a95decadf)

Gambar 3.6 Analisis Bivariate antara Data Numerik dengan 'Failure Type'

Berdasarkan Gambar 3.5 tampak persebaran data 'Failure Type' yang relatif terhadap data numerik. Berikut adalah karakteristik hubungan kedua kategori tersebut:
- Rata-rata jenis kegagalan pada fitur 'Air Temperature [K]' dan 'Process Temperature [K]' cenderung sama yaitu berkisar pada nilai 300K.
- Pada fitur 'Rotational Speed [rpm]' sebaran nilainya terhadap jenis kegagalan bervariasi, 'No Failure', 'Tool Wear Failure', dan 'Random Failures' berada pada nilai 1500 rpm. Sementara 'Power Failure' berada pada kisaran nilai >1500 rpm.
- Pada fitur 'Torque [Nm]', rata-rata dari jenis kegagalan cenderung bervariasi. Rentangnya berada antara 30 hingga 60.
- Berdasarkan Gambar 3.6, Diketahui bahwa rata-rata jenis kegagalan yang terjadi akibat pada fitur 'Tool Wear [min]' juga bervariasi, dimana nilai rata-rata tertinggi adalah pada jenis kegagalan 'Tool Wear Failure' >200 min.
- Sehingga, dapat disimpulkan bahwa fitur kategori 'Failure Type' memiliki pengaruh terhadap fitur numerik. Dimana jenis kegagalan yang terjadi berhubungan dengan jenis parameter atau fitur penyebabnya.

Berikut adalah Tabel Analisis Bivariate antara fitur 'Type' dengan 'Failure Type':
| Type/Failure Type | Heat Dissipation Failure | No Failure | Overstrain Failure | Power Failure | Random Failures | Tool Wear Failure |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| H | 8 | 979 | 1 | 5 | 4 | 6 |
| L | 74 | 5757 | 73 | 59 | 12 | 25 |
| 8 | 30 | 2916 | 4 | 31 | 2 | 14 |

Tabel 3.1 Analisis Bivariate fitur 'Type' dengan 'Failure Type'
Tabel diatas adalah Tabel yang menjelaskan hubungan dari banykanya nilai antara  variasi tipe mesin dengan jenis kegagalan yang terjadi. Sama seperti Gambar 4.1, Kegagalan mesin pada setiap jenis kegagalan di dominansi oleh mesin tipe 'L'.


Analisis Multivariat

Analisis Multivariat merupakan jenis analisis data yang terdapat dalam lebih dari dua variabel. Jenis visualisasi ini digunakan untuk merepresentasikan hubungan dan pola yang terdapat dalam multidimensional data. Berikut adalah visualisasi EDA dari Analisis Multivariate:
![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/cbe85e8f-514a-4e5c-b974-191538953ca0)

Gambar 3.7 Analisis Multivariat

Pada Gambar 3.7, dengan menggunakan fungsi pairplot dari library seaborn, tampak terlihat relasi pasangan dalam dataset. Dari gambar, terlihat plot relasi masing-masing fitur numerik pada dataset. Pada pola sebaran data grafik pairplot, terlihat bahwa fitur numerik 'Rotational Speed [rpm]' memiliki korelasi dengan fitur 'Torque [Nm]' serta korelasi antara fitur 'Air Temperature [K]' dengan fitur 'Process Temperature [K]'. Sementara itu, tampak sebaran pair plot antara data numerik dengan fitur 'Target'.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/288cb974-c1a8-4604-b4ba-17b0a4dd87f4)

Gambar 3.8 Correlation Matrix Numeric Fiture

Gambar 3.8 merupakan Matrix Korelasi untuk Fitur Numerik. Matrix ini menunjukkan hubungan antar fitur dalam nilai korelasi. Koefisien korelasi berkisar antara -1 dan +1. Ia mengukur kekuatan hubungan antara dua variabel serta arahnya (positif atau negatif). Mengenai kekuatan hubungan antar variabel, semakin dekat nilainya ke 1 atau -1, korelasinya semakin kuat. Sedangkan, semakin dekat nilainya ke 0, korelasinya semakin lemah.

Jika diamati, fitur 'Target' memiliki skor korelasi yang cukup untuk menunjukkan adanya hubungan korelasi dengan fitur numerik. Semenara itu, fitur UID memiliki korelasi yang negatif. Sehingga, fitur 'UID' dan 'Product ID' dieliminasi atau drop.

## Data Preparation
Pada proses *Data Preparation* dilakukan kegiatan seperti *Data Gathering*, *Data Assessing*, dan *Data Cleaning*. Pada proses *Data Gathering*, data diimpor sedemikian rupa agar bisa dibaca dengan baik menggunakan *dataframe* Pandas. Untuk proses *Data Assessing*, berikut adalah beberapa pengecekan yang dilakukan:
- *Duplicate* data (data yang serupa dengan data lainnya)
- *Missing value* (data atau informasi yang "hilang" atau tidak tersedia)
- *Outlier* (data yang menyimpang dari rata-rata sekumpulan data yang ada)

Pada proses *Data Cleaning*, secara garis besar, terdapat tiga metode yang dapat digunakan antara lain seperti berikut:
- *Dropping* (metode yang dilakukan dengan cara menghapus sejumlah baris data)
- *Imputation* (metode yang dilakukan dengan cara mengganti nilai yang "hilang" atau tidak tersedia dengan nilai tertentu yang bisa berupa median atau mean dari data)
- *Interpolation* (metode menghasilkan titik-titik data baru dalam suatu jangkauan dari suatu data)
Pada kasus proyek ini, tidak ditemukan *Duplicate Data* dan *Missing Value*.

### Outliers

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/ab740a5b-56f8-40d8-91a8-73e862e37d3a)

Gambar 4.1
Berdasarkan boxplot, ditemui adanya kemungkinan outlier. Namun, tidak dilakukan penanganan terhadap outlier tersebut. Hal ini dikarenakan dapat menghilangkan informasi yang diperlukan.

### Anomalie Target
Dilakukan pengamatan terhadap distribusi target untuk menemukan ketidakseimbangan dan memperbaikinya sebelum membagi dataset. Anomali pertama yang ditemukan adalah adanya jenis kegagalan 'Random Failures' yang memiliki target 0.
```
Failure_machine = machine[['Target','Failure Type']][machine['Target'] == 0]
Failure_machine.value_counts()
```
| Target | Failure Type | Count |
| :---: | :---: | :---: |
| 0 | No Failure | 9643 |
| 0 | Random Failures | 18 |

Anomali jenis kegagalan mesin 'Random Failure' hanya terjadi pada 18 pengamatan dan bersifat acak dan tidak dapat diprediksi. Sehingga untuk menangani hal tersebut, data jenis kegagalan mesin 'Random Failure' akan dihapus. Anomali kedua adalah terdapat 9 data dengan Target ‘1’ namun memiliki label ‘No Failure’.
```
Failure_machine_Type = machine[['Target','Failure Type']][machine['Failure Type'] == 'No Failure']
Failure_machine_Type.value_counts()
```
| Target | Failure Type | Count |
| :---: | :---: | :---: |
| 0 | No Failure | 9643 |
| 1 | No Failure | 9 |

Data pada keadaan anomali tersebut merupakan data yang ambigu dikarenakan Kita tidak dapat mengetahui apakah benar-benar terjadi kegagalan atau tidak. Sehingga, untuk menangani hal tersebut 9 data ini dihapus.

### Encoding
Encoding data adalah proses mengonversi variabel kategoris menjadi bentuk numerik sehingga dapat dimengerti oleh algoritma machine learning atau model statistik. Dalam hal ini, kita melakukan encoding pada 2 fitur, yaitu fitur 'Type' dan 'Failure Type'. Berikut adalah hasil encoding pada fitur 'Type':
| Type | Encoded | Count |
| :---: | :---: | :---: |
| L | 0 | 5984 |
| M | 1 | 2991 |
| H | 2 | 998 |

Berikut adalah hasil encoding pada fitur 'Failure Type':
| Failure Type | Encoded | Count |
| :---: | :---: | :---: |
| Heat Dissipation Failure | 0 | 112 |
| No Failure | 1 | 9643 |
| Overstrain Failure | 2 | 78 |
| Power Failure | 3 | 95 |
| Tool Wear Failure | 4 | 45 |

### Reduction with PCA
```
pca = PCA(n_components=2, random_state=123)
```
Reduksi dimensi dengan PCA (Principal Component Analysis) adalah teknik yang digunakan untuk mengurangi jumlah fitur (variabel) dalam dataset, tetapi tetap mempertahankan sebanyak mungkin informasi yang mungkin. Berdasarkan analisis multivariat yang dilakukan, diketahui bahwa terdapat korelasi antara 'Rotational Speed [rpm]' dengan fitur 'Torque [Nm]' serta korelasi antara fitur 'Air Temperature [K]' dengan fitur 'Process Temperature [K]'. Sehingga, dilakukan reduksi PCA pada fitur-fitur tersebut. 

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/de90ce60-390e-49a4-9cde-1d510c29d9fd)

Gambar 4.2 Visualisasi Hubungan antar Fitur 'Air Temperature [K]' dan 'Process Temperature [K]'sebelum Reduksi PCA

Hasil dari Reduksi PCA adalah 94.4% informasi pada kedua fitur 'Air temperature [K]' dan 'Process temperature [K]' terdapat pada PC1. Sedangkan sisanya, sebesar 5.6% terdapat pada PC2.
Berdasarkan hasil reduksi fitur (dimensi), dipertahankan PC1 (komponen). PC1 ini akan direpresentasikan sebagai fitur 'Temperature' menggantikan kedua fitur lainnya ('Air temperature [K]' dan 'Process temperature [K]'). 

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/83a9167a-f683-4dc8-ab4d-d4cd1e4000dc)

Gambar 4.3 Visualisasi Hubungan antar Fitur 'Rotational Speed [rpm]' dan 'Torque [Nm]'sebelum Reduksi PCA

Hasil dari Reduksi PCA adalah 99.9% informasi pada kedua fitur 'Rotational speed [rpm]' dan 'Torque [Nm]' terdapat pada PC1. Sedangkan sisanya, sebesar 0.1% terdapat pada PC2.
Berdasarkan hasil reduksi fitur (dimensi), dipertahankan PC1 (komponen). PC1 ini akan direpresentasikan sebagai fitur 'Machine Power' menggantikan kedua fitur lainnya ('Rotational speed [rpm]' dan 'Torque [Nm]').


Setelah data dibersihkan, dataset dibagi menjadi data train dan data test untuk proses Modeling, dimana rasio pembagian data yang dipilih adalah 80:20 mengingat data test untuk rasio tersebut sudah terbilang cukup. Namun, diketahui bahwa jumlah kategori pada fitur 'Failure Type' tidak seimbang. Sehingga untuk menangani hal tersebut, dilakukan Oversampling dengan SMOTE.

### Over Sampling With SMOTE
Oversampling dengan SMOTE (Synthetic Minority Over-sampling Technique) adalah teknik yang digunakan untuk menangani ketidakseimbangan kelas dalam dataset dengan meningkatkan jumlah sampel dalam kelas minoritas. Oversampling dengan SMOTE dilakukan agar sample data antar kategori dapat seimbang ketika dilakukan trainining model. 
```
smt = SMOTETomek(sampling_strategy ='auto',random_state=123)
```
Berikut adalah grafik pembagian sample data train:

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/d7c782f6-7cd6-46d9-be78-f98218a2c97c)

Gambar 4.4 Grafik pembagian sample data train

| Failure Type | Encoded | Dist |
| :---: | :---: | :---: |
| Heat Dissipation Failure | 0 | 7677 |
| No Failure | 1 | 7602 |
| Overstrain Failure | 2 | 7703 |
| Power Failure | 3 | 7623 |
| Tool Wear Failure | 4 | 7701 |


Berikut adalah detail dari dataset:
- Total sampel di dalam dataset train: 38306
- Total sampel di dalam dataset test: 1995

## Modeling
Model yang digunakan untuk memprediksi kegagalan mesin adalah model regresi. Dalam bentuk yang sederhana, regresi terdiri dari intersep dan slope yang dituliskan dalam rumusan berikut:

$$ y = a + bX $$

dimana: 
- y adalah variabel kriterium (variabel terikat yang digunakan untuk memprediksi)
- a adalah intersep (variabel konstan yang memiliki arti sebagai titik perpotongan suatu garis dengan sumbu Y),
- b adalah slope (nilai koefisien yang menyatakan ukuran kemiringan suatu garis), dan
- X adalah variabel prediktor (variabel yang digunakan untuk memprediksi atau menjelaskan variabel lain dalam suatu model)

Secara khusus, metode regresi sering digunakan untuk memprediksi atau meramalkan pengaruh variabel prediktor terhadap variabel kriterium atau membuktikan ada atau tidaknya hubungan fungsional antara variabel bebas (X) dengan variabel terikat (y). Berikut adalah kelebihan dan kekurangan dari model regresi:
Kelebihan regresi:
- Kemudahan untuk digunakan
- Kekuatan Prediktor dalam mengidentifikasi sekuat apa pengaruh yang diberikan oleh variabel prediktor (variabel independen) terhadap variabel lainnya (variabel dependen).
- Dapat memprediksi nilai/tren di masa yang mendatang

Kelemahan dari model regresi adalah karena hasil ramalan dari analisis regresi merupakan nilai estimasi sehingga kemungkinan untuk tidak sesuai dengan data aktual tetaplah ada. Pada proyek *Predictive Machine Failure System*, digunakan 4 macam algoritma regresi, yaitu:
- Linear Regression
- Ridge Regression
- Random Forest Regresor
- Random Forest Regresor - Tunning GridSearchCV

Berikut adalah penjelasan tiap algoritma regresi:
- Regresi linear adalah teknik analisis data yang memprediksi nilai data yang tidak diketahui dengan menggunakan nilai data lain yang terkait dan diketahui dimana secara matematis dimodelkan sebagai persamaan linier
- Regresi ridge merupakan metode estimasi koefisien regresi yang diperoleh melalui penambahan konstanta bias c.
- Random forest adalah suatu algoritma yang digunakan pada klasifikasi data dalam jumlah yang besar dimana teknik klasifikasi *random forest* dilakukan melalui penggabungan pohon dengan melakukan training pada sampel data yang dimiliki.
- Random Forest Regresor dengan Tunning GridSearchCV digunakan untuk meningkatkan model. Paramater yang di-tuning antara lain n_estimators', 'max_depth', 'min_samples_split', dan 'min_samples_leaf. Untuk memudahkan proses *tuning* digunakan GridSearchCV. GridSearchCV itu sendiri merupakan bagian dari modul scikit-learn yang dapat digunakan untuk mendapatkan nilai *hyperparameter* secara otomatis. Grid Search adalah metode yang digunakan untuk mencari parameter yang paling tepat untuk meningkatkan performa model dengan mencoba seluruh kombinasi *hyperparameter* yang diberikan. Berikut adalah nilai parameter *tuning*
  ```
  params = {'n_estimators' : [50,80,100],
          'max_depth' : [3,5,10],
           'min_samples_split':[2,3,4],
            'min_samples_leaf': [2,3,4]}
  ```

  Berdasarkan hasil pengujian, terpilih grid.best_params_ yaitu
  ```
  {'max_depth': 10,
  'min_samples_leaf': 2,
  'min_samples_split': 2,
  'n_estimators': 100}
  ```

  Parameter dengan nilai ini kemudian dibuat sebagai model 4.

Hasil dari pemodelan dengan 4 macam algoritma regresi tersebut kemudian dibandingkan untuk mendapatkan model terbaik.

## Evaluation
Adapun metrik yang sebagai alat ukur perfoma model yang dibuat antara lain **MSE · MAE · R<sup>2</sup>**. 

Berikut merupakan rumus dari masing-masing metrik yang digunakan:

$$ MAE = (1/n) Σ |y<sub>i</sub> - ŷ<sub>i</sub>| $$

$$ MSE = (1/n) Σ (y<sub>i</sub> - ŷ<sub>i</sub>)<sup>2</sup> $$

$$ R<sup>2</sup> = 1 - (MSE / Var(y)) $$

y<sub>i</sub> mewakili nilai yang diamati,
ŷ<sub>i</sub> mewakili nilai prediksi,
n adalah jumlah titik data,
Var(y) mewakili varians dari nilai yang diamati.

Berikut merupakan penjelasan kegunaan dari masing-masing metrik yang digunakan:
- MAE menghitung rata-rata dari selisih absolut antara nilai prediksi dan nilai aktual. Semakin kecil nilai MAE, semakin baik kualitas model tersebut.
- MSE menghitung rata-rata dari selisih kuadrat antara nilai prediksi dan nilai aktual. Semakin kecil nilai MSE, semakin baik kualitas model tersebut.
- R<sup>2</sup> digunakan untuk menilai seberapa besar pengaruh variabel independen tertentu terhadap variabel dependen.

Berikut adalah tabel yang menyajikan perbandingan 4 buah model:

|     |Model 1|Model 2|Model 3|Model 4|
|---|---|---|---|---|
|R<sup>2</sup>|-142571.22047889986|-142562.82814195784|-7.092059116469194|-9.23334987107827|
|MSE|117.51993191251806|117.51647302909402|0.8853675447084435|0.9956414891470533|
|MAE|83.15954515654357|83.15714189178568|0.6505664160401003|0.7491044047744142|

Tabel 5.1 Perbandingan Performa MAE, MSE, dan R<sup>2</sup> Model

Berdasarkan Tabel 5.1, secara umum Model 3 (RF1) dan Model 4 (RF2) menampilkan hasil performa yang lebih baik dimana masing-masing memiliki nilai R^2 yaitu sebesar -7.092059116469194 dan -9.23334987107827.

Perbandingan Model 1, 2, 3, dan 4 bisa dilihat pada Gambar 5.5 berikut.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/a3d059c1-400a-4501-b08a-ecad3680d111)


Gambar 5.5 Perbandingan Model berdasarkan Nilai Error

Berdasarkan Gambar 5.5, dapat terlihat bahwa nilai error train dan test dari Model 3 (RF1) dan Model 4 (RF2) jauh lebih baik dibandingkan model lainnya. Juga dilakukan perbandingan nilai y_true terhadap nilai prediksi harga rumah dari 4 buah model yang dibuat. Tabel 5.2 berikut merupakan hasil dari evaluasi model yang telah dibuat.

Tabel 5.2 Perbandingan Model

|     |y_true|prediksi_LR|prediksi_RR|prediksi_RF1|prediksi_RF2|
|:---:|:---:|:---:|:---:|:---:|:---:|
|4979|1|0.0|0.0|1.0|1.0|

Berdasarkan hasil evaluasi, terlihat bahwa prediksi harga rumah dengan *Random Forest* (RF), baik RF1 (tanpa tuning) ataupun RF2 (dengan tuning) memberikan hasil yang paling mendekati y_true, dimana nilai y_true yaitu 1 dan nilai RF1 dan RF2 masing-masing yaitu 1.0 dan 1.0. Dengan demikian bisa disimpulkan bahwa model yang telah dikembangkan dapat memprediksi harga rumah dengan baik dengan menggunakan *Random Forest Regressor*.

## Referensi:
[1] Harja, H.B. et al. (2019) ‘Development of tools utilization monitoring system on labor-intensive manufacturing industries’, AIP Conference Proceedings [Preprint]. doi:10.1063/1.5138309.

[2] Jamwal, A. et al. (2021) ‘Industry 4.0 technologies for manufacturing sustainability: A systematic review and Future Research Directions’, Applied Sciences, 11(12), p. 5725. doi:10.3390/app11125725. 

[3] Kalsoom, T. et al. (2020) ‘Advances in sensor technologies in the era of Smart Factory and industry 4.0’, Sensors, 20(23), p. 6783. doi:10.3390/s20236783. 

[4] Paszkiewicz, A. et al. (2023) ‘Estimation of tool life in the milling process—testing regression models’, Sensors, 23(23), p. 9346. doi:10.3390/s23239346. 

[5] Traini, E. et al. (2019) ‘Machine learning framework for predictive maintenance in milling’, IFAC-PapersOnLine, 52(13), pp. 177–182. doi:10.1016/j.ifacol.2019.11.172. 

[6] Rojek, I. et al. (2023) ‘An artificial intelligence approach for improving maintenance to supervise machine failures and support their repair’, Applied Sciences, 13(8), p. 4971. doi:10.3390/app13084971. 

[7] Paolanti, M. et al. (2018) ‘Machine Learning Approach for predictive maintenance in industry 4.0’, 2018 14th IEEE/ASME International Conference on Mechatronic and Embedded Systems and Applications (MESA) [Preprint]. doi:10.1109/mesa.2018.8449150. 

[8] Soo Lon Wah, W., Chen, Y.-T. and Owen, J.S. (2021) ‘A regression-based damage detection method for structures subjected to changing environmental and operational conditions’, Engineering Structures, 228, p. 111462. doi:10.1016/j.engstruct.2020.111462. 

