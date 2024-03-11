# Predictive Failure Machine System - Machine Learning Project Report

## Domain Proyek

Perkembangan industri modern, khususnya yang berkaitan dengan konsep Industri 4.0, memerlukan interaksi mesin manufaktur, sensor, dan perangkat lunak khusus untuk menjamin efisiensi, produktivitas, dan keandalan proses produksi yang lebih baik [[1](https://www.researchgate.net/publication/337895714_Development_of_tools_utilization_monitoring_system_on_labor-intensive_manufacturing_industries)] [[2](https://www.mdpi.com/2076-3417/11/12/5725)] [[3](https://www.mdpi.com/1424-8220/20/23/6783)]. Salah satu aspek penting dalam menjamin kelangsungan proses produksi adalah dengan prediksi kerusakan pada alat yang digunakan. Seiring dengan otomatisasi dan digitalisasi, revolusi industri 4.0 memperkenalkan konsep pemeliharaan prediktif. Pemeliharaan Prediktif (PM) atau *Predictive Maintenance System* adalah metode untuk memantau status atau kerusakan pada mesin untuk mencegah kegagalan yang mahal terjadi dan untuk melakukan pemeliharaan ketika benar-benar diperlukan [[4](https://www.mdpi.com/1424-8220/23/23/9346#B1-sensors-23-09346)] [[5](https://www.sciencedirect.com/science/article/pii/S240589631931122X)]. Estimasi yang tepat memungkinkan untuk mengurangi biaya yang terkait sebagai akibat kerusakan pada masing-masing alat atau mesin [[6](https://www.mdpi.com/2076-3417/13/8/4971)].

Pemeliharaan Prediktif menggabungkan kemampuan pengumpulan data dengan kapasitas untuk melakukan analisis yang efektif dan terintegrasi (*Machine Learning*) [[7](https://ieeexplore.ieee.org/document/8449150)]. Prediksi kegagalan mesin menggunakan Machine Learning dapat meningkatkan ketergantungan operasional, sehingga memungkinkan pemeliharaan proaktif dan meminimalkan waktu henti. 
Secara khusus, metode regresi sering digunakan untuk memprediksi kerusakan peralatan karena kemampuannya dalam memodelkan hubungan antara variabel yang berbeda [[8](https://www.sciencedirect.com/science/article/abs/pii/S0141029620340633)].

## Business Understanding

Pengembangan model *Predictive Failure Machine System* memiliki potensi yang signifikan sebagai alat bantu dalam pengambilan keputusan khususnya pada bidang industri dan manufaktur.

*Predictive Failure Machine System* adalah sistem yang memiliki potensi besar dalam meningkatkan efisiensi operasional, mengurangi downtime produksi, meningkatkan keselamatan dan kesehatan pekerja, serta meningkatkan kualitas produk dan membantu perusahaan untuk tetap kompetitif di pasar yang semakin kompetitif dan dinamis.

### Problem Statements
- Berdasarkan eksplorasi *dataset*, fitur apa saja yang mempengaruhi dalam menentukan kerusakan mesin?
- Bagaimana mengolah *dataset* agar dapat dibuat model prediksi kerusakan mesin?
- Bagaimanna cara meningkatkan nilai perfoma model prediksi kerusakan mesin?

### Goals
- Mengeksplorasi semua fitur yang tersedia pada *dataset* untuk melihat korelasi dan faktor apa saja yang paling berpengaruh sampai paling kurang berpengaruh terhadap kerusakan mesin
- Melakukan proses *data wragling* dan *data preparation* terhadap *dataset* untuk membuat prediksi kerusakan mesin
- Melakukan beberapa variasi model untuk mendapatkan model yang paling baik dari beberapa model yang telah dibuat untuk prediksi kerusakan mesin


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

### Variabel-variabel pada *dataset* adalah sebagai berikut:
- UID
  Pengidentifikasi unik yang menunjukkan bahwa setiap titik data berhubungan dengan peristiwa atau pengamatan tertentu dalam proses manufaktur (nilai 1 - 10.000).
- Product ID
  Nomor seri khusus dari Type. Hal ini dapat mengindikasikan jenis atau variasi produk yang berbeda yang diproduksi oleh mesin.
- Type
  Varian Kualitas Produk, teridir dari 3 kategori, Low (L) (50% dari seluruh produk), Medium (M) (30%), dan High (H) (20%) 
- Air Temperature [K]
  Suhu Udara yang dihasilkan menggunakan proses random walk kemudian dinormalisasi ke standar deviasi 2 K sekitar 300 K
- Process Temperature [K]
  Suhu Proses pada mesin yang dihasilkan menggunakan proses random walk dan dinormalisasi.
- Rotational Speed [rpm]
  Kecepatan rotasi mesin, yang dihitung berdasarkan daya 2860 W dan termasuk kebisingan yang terdistribusi secara normal. 
- Torque [Nm]
  Torsi yang diterapkan pada mesin, biasanya terdistribusi sekitar 40 Nm dengan Ïƒ = 10 Nm dan tidak ada nilai negatif.
- Tool Wear [min]
  Keausan alat berhubungan dengan varian kualitas mesin (H/M/L). Hal ini menunjukkan bahwa alat digunakan bersama dengan mesin selama proses manufaktur.
- Target
  Mesin gagal atau tidak yang dinilai dengan 0 atau 1.
- Failure Type
  Jenis kegagalan mesin. Jika setidaknya satu dari jenis kegagalan di berikut benar, mesin diberikan label 'kegagalan mesin' dan diatur ke 1. 
  - Tool Wear Failure (TWF)
  - Heat Dissipation Failure (HDF)
  - Power Failure (PWF)
  - Overstrain Failure (OSF)
  - Random Failures (RNF)

## Data Preparation
Pada proses *Data Preparation* dilakukan kegiatan seperti *Data Gathering*, *Data Assessing*, dan *Data Cleaning*. Pada proses *Data Gathering*, data diimpor sedemikian rupa agar bisa dibaca dengan baik menggunakan *dataframe* Pandas. Untuk proses *Data Assessing*, berikut adalah beberapa pengecekan yang dilakukan:
- *Duplicate* data (data yang serupa dengan data lainnya)
- *Missing value* (data atau informasi yang "hilang" atau tidak tersedia)
- *Mislabelled* data (klasifikasi/label data yang tidak sesuai dengan kelas atau kelompok sebenarnya)
- *Outlier* (data yang menyimpang dari rata-rata sekumpulan data yang ada)

Pada proses *Data Cleaning*, secara garis besar, terdapat tiga metode yang dapat digunakan antara lain seperti berikut:
- *Dropping* (metode yang dilakukan dengan cara menghapus sejumlah baris data)
- *Imputation* (metode yang dilakukan dengan cara mengganti nilai yang "hilang" atau tidak tersedia dengan nilai tertentu yang bisa berupa median atau mean dari data)
- *Interpolation* (metode menghasilkan titik-titik data baru dalam suatu jangkauan dari suatu data)
  
Pada kasus proyek ini, tidak ditemukan *Duplicate Data* dan *Missing Value*. Namun, ditemukan *Mislabelled data*. Sementara itu, pada proyek ini tidak dilakukan penanganan terhadap *outliers*, hal ini dikarenakan penanganan terhadap outliers dapat menghilangkan variable *Failure Type*.

### Mislabelled Data
Terdapat 18 data dengan Target ‘0’ namun memiliki label *‘Random Failure’* serta terdapat 9 data dengan Target ‘1’ namun memiliki label *‘No Failure’*. Metode yang digunakan untuk mengatasi hal ini adalah dengan melakukan pengakategorian antara ‘Target’ dan *Failure Type’*. 

```
machine.loc[machine['Failure Type'] == 'Random Failures', 'Target'] = 1
machine.loc[machine['Failure Type'] == 'No Failure', 'Target'] = 0
```

## DATA ANALYSIS (EDA)
Untuk memahami data lebih lanjut, dilakukan Analisis Univariat, Analisis Bivariate dan Analisis Multivariat, serta Visualisasi Data melalui EDA. EDA/Exploratory Data Analysis adalah proses analisis data yang digunakan untuk menjelajahi, memahami, dan meringkas karakteristik dasar dari dataset secara visual dan deskriptif. Tujuan utama dari EDA adalah untuk memahami struktur dataset, menemukan pola atau tren yang menarik, mengidentifikasi outlier atau anomali, serta mempersiapkan data untuk tahap analisis yang lebih lanjut.

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel. Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu *dataset*. Berikut adalah visualisasi EDA dari Analisis Univariate dari data kategori dan numerik:
![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/be01e8ff-c380-4a05-b828-46eaa673a47e)

Gambar 4.1 Analisis Univariat *Type*(Data Kategori)

Berdasarkan Gambar 4.1., diketahui bahwa terdapat 3 variansi kualitas mobil, yaitu Low (L), Medium (M), dan High (H). *Dataset* di dominansi oleh Tipe 'L' yang berjulah 6000 mesin, Tipe 'M' berjumlah 2997 mesin, dan Tipe 'H' berjumlah 1003 mesin.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/64971f85-2da3-4b4b-8365-607111495ec6)

Gambar 4.2. Analisis Univariat *Failure Type* (Data Kategori)

Berdasarkan Gambar 4.2., dapat dilihat bahwa distribusi data kategori 'Failure Type' memiliki perbandingan jumlah yang tidak sama. Data di dominansi oleh data 'No Failure' dengan nilai 9652. Sementara itu, data paling sedikit adalah 'Random Failures' dengan nilai 18.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/e1b7208c-75f7-41d6-9cd4-25b5e77d87f9)

Gambar 4.3 Analisis Univariat (Data Numerik)

Berdasarkan Gambar 4.3., Diketahui karakteristik dari data numerik adalah sebagai berikut:
- Terdapat 600 mesin yang memiliki suhu udara antara 297K hingga 303K. Sementara sisanya memiliki suhu udara yang lebih rendah selama bekerja.
- Terdapat  lebih dari 800 mesin yang mencapai suhu proses antara 310K hingga 311K. Juga mesin lain yang suhunya berada di antara 308K hingga 312K selama pemrosesan.
- Terdapat  600 mesin yang mencapai putaran rotasi 1500 rpm, 500 mesin mencapai kecepatan rotasi 1400 hingga 1500 rpm, dan hanya ada sedikit mesin yang mencapai kecepatan rotasi maksimum 2000 rpm, mungkin kurang dari 100 mesin.
- Terdapat  500 mesin yang mencapai torsi antara 35Nm hingga 45Nm.
- Terdapat  mesin yang mungkin menghadapi kegagalan karena keausan pahat (min) hingga 220 keausan pahat min.


Analisis Bivariat adalah analisis statistik yang dilakukan untuk memahami hubungan antara dua variabel dalam sebuah *dataset*. Ini melibatkan memeriksa hubungan atau ketergantungan antara dua variabel secara bersama-sama. Berikut adalah visualisasi EDA dari Analisis Bivariate:
![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/9a73cf86-583b-4265-9864-1b4c35530048)
Gambar 4.4 Analisis Bivariate antara 'Target' dengan Fitur *dataset*

Berdasarkan Gambar 4.4., Hubungan antara setiap fitur dengan kategori 'Type' di dominannsi oleh data dengan nilai 'Type' 1, hal ini sejalan dengan lebih banyaknya data kategori 'No Failure' dibanding dengan tipe kegagalan lainnya.

![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/7fa058b6-79ab-443f-b9cb-813b4365c290)
Gambar 4.5 Analisis Bivariate antara Data Numerik dengan *Failure Type*
![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/a4c93b8e-e2bd-4a08-8aee-a24ee0c5b6bc)
Gambar 4.6 Analisis Bivariate antara Data Numerik dengan *Failure Type*

Berdasarkan Gambar 4.5., Diketahui bahwa kegagalan yang terjadi akibat parameter *Air Temperature [K]* dan *Process Temperature [K]* pada setiap jenis kegagalan cenderung sama yaitu pada nilai 300K. Pada parameter *Rotational Speed [rpm]* sebaran nilainya bervariasi, 'No Failure', 'Tool Wear Failure', dan 'Random Failures' berada di sekitar nilai 1500 rpm. sementara 'Power Failure' dengan nilai >1500 rpm. Pada parameter *Torque [Nm], nilai dari jenis kegagalan 'Overstrain Failure' >40 Nm. Berdasarkan Gambar 4.6., Diketahui bahwa kegagalan yang terjadi akibat parameter *Tool Wear [min]* juga bervariasi, dimana nilai dari jenis kegagalan 'Tool Wear Failure' >200 min.

Tabel diatas adalah Tabel yang menjelaskan hubungan dari banykanya nilai antara  variasi tipe mesin dengan jenis kegagalan yang terjadi. Sama seperti Gambar 4.1., Kegagalan mesin pada setiap jenis kegagalan di dominansi oleh mesin tipe 'L'.

Analisis Multivariat merupakan jenis analisis data yang terdapat dalam lebih dari dua variabel. Jenis visualisasi ini digunakan untuk merepresentasikan hubungan dan pola yang terdapat dalam multidimensional data. Berikut adalah visualisasi EDA dari Analisis Multivariate:
![image](https://github.com/zefanyadita/Predictive-Failure-Machine-System-Machine-Learning-Project-/assets/147527401/cb036de3-e3e1-4021-b359-f536a610a32e)
Gambar 4.7 Analisis Multivariat

Pada Gambar 2b, dengan menggunakan fungsi pairplot dari library seaborn, tampak terlihat relasi pasangan dalam dataset. Dari gambar, terlihat plot relasi masing-masing fitur numerik pada dataset. Pada pola sebaran data grafik pairplot, terlihat bahwa 'median_income' memiliki korelasi dengan fitur 'median_house_value'. Sedangkan kedua fitur lainnya terlihat memiliki korelasi yang lemah karena sebarannya tidak membentuk pola

Terakhir, Gambar 2c merupakan Correlation Matrix menunjukkan hubungan antar fitur dalam nilai korelasi. Jika diamati, fitur 'median_income' memiliki skor korelasi yang cukup besar (0.63) dengan fitur target 'median_house_value'. Artinya, fitur 'median_house_value' berkorelasi cukup tinggi dengan keempat fitur tersebut. Sementara itu, fitur lainnya memiliki korelasi negatif sehingga fitur tersebut dapat dieliminasi.

Fitur UID serta Product ID memiliki korelasi negatif sehingga, fitur tersebut dapat di-drop.

## Modeling
Seperti yang dijelaskan di awal, model yang dipilih adalah model regresi karena merupakan salah satu algoritma yang paling umum digunakan dalam pembuatan model prediksi. Dalam bentuk yang sederhana, regresi terdiri dari intersep dan slope yang dituliskan dalam rumusan berikut

$$ y = a + bX $$

dimana: 
- y adalah variabel kriterium (variabel terikat yang digunakan untuk memprediksi)
- a adalah intersep (variabel konstan yang memiliki arti sebagai titik perpotongan suatu garis dengan sumbu Y),
- b adalah slope (nilai koefisien yang menyatakan ukuran kemiringan suatu garis), dan
- X adalah variabel prediktor (variabel yang digunakan untuk memprediksi atau menjelaskan variabel lain dalam suatu model)

Secara umum, regresi ini itu sendiri digunakan untuk meramalkan pengaruh variabel prediktor terhadap variabel kriterium atau membuktikan ada atau tidaknya hubungan fungsional antara variabel bebas (X) dengan variabel terikat (y).

Namun begitu terdapat kelebihan dan kekurangan dari model regresi, yaitu:

Kelebihan regresi:
- Kemudahan untuk digunakan
- Kekuatan Prediktor dalam mengidentifikasi sekuat apa pengaruh yang diberikan oleh variabel prediktor (variabel independen) terhadap variabel lainnya (variabel dependen).
- Dapat memprediksi nilai/tren di masa yang mendatang

Kelemahan dari model regresi adalah karena hasil ramalan dari analisis regresi merupakan nilai estimasi sehingga kemungkinan untuk tidak sesuai dengan data aktual tetaplah ada.

Pada proyek yang dikerjakan, algoritma regresi yang coba dibandingkan adalah regresi linear, regresi ridge, *random forest regressor*, dan *random forest regressor* dengan hyperparamter tuning. Regresi linear adalah teknik analisis data yang memprediksi nilai data yang tidak diketahui dengan menggunakan nilai data lain yang terkait dan diketahui dimana secara matematis dimodelkan sebagai persamaan linier, regresi ridge merupakan metode estimasi koefisien regresi yang diperoleh melalui penambahan konstanta bias c, dan random forest adalah suatu algoritma yang digunakan pada klasifikasi data dalam jumlah yang besar dimana teknik klasifikasi *random forest* dilakukan melalui penggabungan pohon dengan melakukan training pada sampel data yang dimiliki.

Untuk meningkatkan model, dilakukan *hyperparamter tuning*. Adapun paramater yang di-tuning antara lain n_estimators', 'max_depth', 'min_samples_split', dan 'min_samples_leaf. Untuk memudahkan proses *tuning* digunakan GridSearchCV. GridSearchCV itu sendiri merupakan bagian dari modul scikit-learn yang dapat digunakan untuk mendapatkan nilai *hyperparameter* secara otomatis. Grid Search adalah metode yang digunakan untuk mencari parameter yang paling tepat untuk meningkatkan performa model dengan mencoba seluruh kombinasi *hyperparameter* yang diberikan.

Berikut adalah nilai parameter *tuning*
```
params = {'n_estimators' : [50,80,100],
          'max_depth' : [3,5,10],
           'min_samples_split':[2,3,4],
            'min_samples_leaf': [2,3,4]}
```
Berdasarkan hasil pengujian, terpilih grid.best_params_ yaitu 
```
{'max_depth': 10,
 'min_samples_leaf': 4,
 'min_samples_split': 2,
 'n_estimators': 100}
```
Parameter dengan nilai inilah yang kemudian dibuat sebagai model.

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
- R<sup>2</sup> digunakan untuk menilai seberapa besar pengaruh variabel independen tertentu terhadap variabel dependen

Tabel 1 berikut merupakan perbandingan 4 buah model yang coba dibandingkan

|     |Model 1|Model 2|Model 3|Model 4|
|---|---|---|---|---|
|R<sup>2</sup>|-7504.309425109431|-7498.0783949337365.146779279|-1.880080745581838|2.432728538383974|
|MSE|8166746.146779279|8163355.360001828|159980.5138016423|174656.3925179131|
|MAE|6509173.648630178|6506404.9997212|133115.5655366269|154364.3230594773|

Tabel 1. Perbandingan Performa MAE, MSE, dan R<sup>2</sup> Model

Berdasarkan Tabel 1, secara umum Model 3 (RF1) dan Model 4 (RF2) menampilkan hasil performa yang lebih baik dimana masing-masing memiliki nilai R^2 yaitu sebesar -1.880080745581838 dan -2.432728538383974.

Secara lebih jauh perbandingan Model 1, 2, 3, dan 4 bisa dilihat pada Gambar 4 berikut.

![download (1)](https://github.com/ahmadsuaif/Proyek-Pertama-Predictive-Analytics/assets/66425290/a46a2fa1-d5c5-4371-a18f-409a84bb42da)

Gambar 4. Perbandingan Model berdasarkan Nilai Error (dalam 1e6)

Berdasarkan Gambar 4 dapat terlihat bahwa nilai error train dan test dari Model 3 (RF1) dan Model 4 (RF2) jauh lebih baik dibandingkan model lainnya.

Selain itu dilakukan perbandingan nilai y_true terhadap nilai prediksi harga rumah dari 4 buah model yang dibuat. Tabel 2 berikut merupakan hasil dari evaluasi model yang telah dibuat.

|     |y_true|prediksi_LR|prediksi_RR|prediksi_RF1|prediksi_RF2|
|---|---|---|---|---|---|
|15732|341700|218287.6|218309.3|347466.0|315645.2|

Tabel 2. Perbandingan Model


Berdasarkan hasil evaluasi, terlihat bahwa prediksi harga rumah dengan *Random Forest* (RF), baik RF1 (tanpa tuning) ataupun RF2 (dengan tuning) memberikan hasil yang paling mendekati y_true, dimana nilai y_true yaitu 341700 dan nilai RF1 dan RF2 masing-masing yaitu 347466.0 dan 315645.2. Dengan demikian bisa disimpulkan bahwa model yang telah dikembangkan dapat memprediksi harga rumah dengan baik dengan menggunakan *Random Forest Regressor*.

## Referensi:
[1] Hassan, Mohammad Mujaheed & Ahmad, Nobaya & Hariza, Ahmad & Hashim, Ahmad. (2021). Factors Influencing Housing Purchase Decision. 11. 429-443. 10.6007/IJARBSS/v11-i7/10295.

[2] Ariyawansa, Ranthilaka. (2009). Housing Market: A Review of Purchase Decision of Potential Buyers.

[3] Jiang, Jiaxin & Zhang, Jin. (2021). Analysis of County Consumers’ Housing Purchase Intention and Influencing Factors. 

[4] Heymann, Sommervoll. (2019). House prices and relative location

[5] Jayasekare, Ajith & Herath, Shanaka & Wickramasuriya, Rohan & Perez, Pascal. (2019). The price of a view: Estimating the impact of view on house prices. Pacific Rim Property Research Journal. 25. 1-18. 10.1080/14445921.2019.1626543. 

[6] Agarwal, Umang & Gupta, Smriti & Goyal, Madhav. (2022). House Price Prediction using Linear Regression. 10.13140/RG.2.2.11175.62887. 

[7] Li, Xinshu. (2022). Prediction and Analysis of Housing Price Based on the Generalized Linear Regression Model. Computational Intelligence and Neuroscience. 2022. 1-9. 10.1155/2022/3590224. 

[8] Zietz, Joachim & Zietz, Emily & Sirmans, G.. (2008). Determinants of House Prices: A Quantile Regression Approach. The Journal of Real Estate Finance and Economics. 37. 317-333. 10.1007/s11146-007-9053-7. 
