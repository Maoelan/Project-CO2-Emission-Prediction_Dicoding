# Laporan Proyek Machine Learning - Maulana Muhammad

## Lingkungan - CO2 Emission

CO2/Carbon *emissions* atau emisi karbon merupakan proses karbon dioksida ke atmosfer yang terjadi secara alami maupun dipicu aktivitas manusia, seperti deforestasi, konsumsi listrik, hingga kegiatan industri manufaktur. Jenis senyawa ini adalah salah satu hasil dari pembakaran yang perlu dibuang. Gas buang berupa karbondioksida ini merupakan emisi yang kebanyakan saat ini dihasilkan kendaraan yang perlu diujikan dalam proses uji emisi. Emisi C02 ini sangat berpengaruh terhadap percepatan pemanasan global.

- Mengapa dan bagaimana masalah ini harus diselesaikan?
  
  Dari pelepas senyawa karbon CO2 ke lapisan atmosfer bumi akan memberikan dampat pada lingkungan, kesehatan, dan ekonomi. Yang cukup terlihat sekarang yaitu pada   lingkungan seperti ada peningkatan suhu bumi pertahun yang berakibat salju dikutub dan cangkupan glesternya akan berkurang dan menyebabkan peningkatan permukaan air laut sehingga masalah ini harus diselesaikan untuk mencegah hal tersebut terjadi dalam jangka dekat.

## Business Understanding

CO2 *Emission* atau emisi karbon merupakan proses pelepasan karbon ke atmosfer. Jenis senyawa karbon merupakan hasil pembakaran yang perlu dibuang. Pada saat ini kebanyak penghasil emisi karbon merupakan kendaraan sehari-hari yang menghasilkan karbon dari pembakaran bahan bakar yang dilepaskan begitu saja ke atmosfer bumi. Bayangkan berapa banyak karbon yang dilepaskan dalam sehari oleh kendaraan. Kendaraan roda 4 menghasilkan rata-rata 200g/km karbon CO2. Itu dalam hitungan km, bagaimana dengan penggunaan kendaraan roda 4 dalam sehari? ditambah seluruh penduduk bumi sekarang tidak terlepas dari kendaraan. Oleh karena itu dibuatlah sistem untuk memprediksi penghasilan karbon CO2 untuk mengukur berapa banyak kendaraan roda 4 mengeluarkan karbon dalam hitungan g/km.

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Dari banyaknya fitur, fitur apa yang memiliki pengaruh pada penghasilan CO2 *emission*?
- Berapa banyak CO2 *emission* yang dihasilkan pada fitur yang berpengaruh dengan CO2 *emission*?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang berkorelasi dengan CO2 *emission*.
- Membuat model machine learning yang dapat memprediksi CO2 *emission*.

    ### Solution statements
    - Menggunakan 5 algoritma berbeda untuk menentukan hasil prediki terbaik yaitu Linear Regressor, Decision Tree Regressor, K-Nearest Neighbor, Random Forest Regressor, dan Ada Boosting.
    - Melakukan improvement pada ke 4 baseline yaitu Decison Tree Regressor, K-Nearest Neighbor, Random Forest Regressor, dan Ada Boosting menggunakan hyperparameter tunning. 

## Data Understanding
Dataset : [CO2 Emission by Vehicles](https://www.kaggle.com/datasets/debajyotipodder/co2-emission-by-vehicles).

### Variabel-variabel pada CO2 *Emission by Vehicles* dataset adalah sebagai berikut:
*   Make : Perusahaan yang membuat kendaraan
*   Model : Model dari kendaraan
*   Vehicle Class : Kelas dari kendaraan berdasarkan utilitas, kapasitas dan berat 
*   Engine Size (L) : Ukuran dari mesin dalam satuan liter (L)
*   Cylinders : Jumlah silinder kendaraan (ruang naiknya piston)
*   Transmission : Tipe transmisi dengan jumlah gigi kendaraan
    *   A = Otomatis
    *   AM = Manual Otomatis
    *   AS = Otomatis dengan pilihan shift
    *   AV = Variabel kontinu
    *   M = Manual
    *   X = Angka dari gigi
*   Fuel Type : Tipe bahan bakar
    *   X = Bensin Reguler
    *   Z = Bensin Premium
    *   D = Disel
    *   E = Ethanol (E85)
    *   N = Gas Natural
*   Fuel Consumption City (L/100 km) : Jumlah konsumsi bahan bakar dijalanan kota dalam satuan (L/100 km)
*   Fuel Consumption City (L/100 km) : Jumlah konsumsi bahan bakar dijalanan raya dalam satuan (L/100 km)
*   Fuel Consumption Comb (L/100 km) : Jumlah konsumsi bahan bakar (55% kota. 45% jalan raya) dalam satuan (L/100 km)
*   CO2 Emissions(g/km) : Emisi knalpot karbon dioksida dalam gram/kilometer (g/km) dari gabungan berkendara pada jalanan kota dan jalan raya

### Exploratory Data Analysis
- Mengecek banyak fitur categorical dan numerik, diperoleh informasi dimana terdapat 5 fitur yang bertipe categorical dan 7 fitur yang bertipe numerik.
- Menghapus data yang dianggap tidak terlalu penting, terdiri dari 3 data categorical yaitu Make, Model dan Vehicle Class.
- Mengecek missing value dan data yang dianggap memiliki kejanggalan, pada data terlihat apabila data memiliki kejanggalan pada kuartil ketiga dengan nilai maksimum dan diduga kalau data ini merupakan outlier.
- Melakukan visualisasi data dengan boxplot pada tipa numerik untuk mengecek apakah data tersebut merupakan outlier atau tidak dan didapatkan hasil kalau data tersebut merupakan data outlier.
- Menghapus data outlier menggunakan IQR method.
- Melakukan teknik EDA menggunakan unvariate analysis dengan memvisualisasikan data untuk memahami satu persatu data pada fitur yang tersedia pada dataset.
- Melakukan teknik EDA menggunakan multivariate analysis dengan memvisualisasikan data untuk memahami hubungan antar dua fitur atau lebih.
- Mengecek korelasi antar data yang tediri menggunakan pairplot dan skor korelasi menggunakan corr().

## Data Preparation
Teknik Data preparation yang dilakukan terdiri dari:
 - Label encoding
 - OneHot encoding
 - Reduksi dimensi dengan PCA
 - Train-test-split data

**Proses Data Preparation** 
- Mengubah fitur categorical menjadi data numerik, pertama adalah fitur Transmission kalan diubah menggunakan LabelEncoder.
- Fitur fuel type diubah menggunakan OneHotEncoder.
- Mengecek korelasi antara ketiga fitur yaitu Fuel Consumption City (L/100 km), Fuel Consumption Hwy (L/100 km), Fuel Consumption Comb (L/100 km) untuk menentukan apakah fitur ini dapat dilakukan reduksi dimensi dengan PCA.
- Setelah diketahui ketiga fitur tersebut berkorelasi dilakukan reduksi dimensi dengan PCA, membuat fitur baru yaitu Fuel Consumption untuk menggantikan ketiga fitur tersebut.
- Kemudian melakukan train-test-split, data train dan test dibagi menjadi rasio 80:20.

**Mengapa perlu dilakukan data prepration?** 
- Perlu dilakukan proses encoding pada data categorical adalah agar data dapat diproses oleh model, karena model lebih dapat memproses data bertipe numerik.
- Diperlukannya reduksi dimensi adalah agar menyederhanakan model dan mencegah terjadinya overfitting
- Perlu dilakukan train-test-split agar hasil prediksi dapat lebih akurat pada data baru

## Modeling
Model machine learning yang digunakan untuk masalah ini terdiri dari 5 model yaitu:
- LinearRegression : tidak memiliki parameter
- DecisionTreeRegressor dengan parameter sebagai berikut:
    * max_depth = 10 : kedalaman pohon
    * random_state = 20 : digunakan untuk random generator
- K-Nearest Neighbor dengan parameter sebagai berikut:
    * n_neighbors = 7 : jumlah tetangga yang digunakan untuk mengukur jarak
- RandomForestRegressor dengan parameter sebagai berikut:
    * n_estimators = 50 : jumlah tree pada forest
    * max_depth = 15 : kedalaman pohon
    * random_state = 55 : digunakan untuk random generator
    * n_jobs = -1 : jumlah job yang digunakan secara pararel
- Adaptive Boosting dengan parameter sebagai berikut:
    * learning_rate = 0.9 : bobot pada regressor pada masing-masing iterasi
    * random_state = 50 : digunakan untuk random generator
    * n_estimators = 10 : jumlah base estimator yang ingin digunakan dalam data

**Kelebihan dan kekurangan algoritma yang digunakan**
- LinearRegression:
    * Kelebihan : Mengetahui hubungan antar variabel independen dan dependen.
    * Kekurangan : Pada dunia nyata tidak banyak masalah yang menunjukkan hubungan yang jelas antar variabel independen dan dependen.
- DecisionTreeRegressor:
    * Kelebihan : Mudah dalam pembuatan dan dimasukkan dalam rangkaian pohon keputusan.
    * Kekurangan : Tidak baik digunakan pada kasus-kasus kompleks karena akan membuat gambaran tree membingungkan.
- K-Nearest Neighbor:
    * Kelebihan : Mudah diterapkan pada proses regresi, dan model mudah beradaptasi.
    * Kekurangan : Apabila dataset berukuran besar maka akan tidak berfungsi dengan baik.
- RandomForestRegressor:
    * Kelebihan : Dapat mengatasi noise dan missing value dan dapat mengatasi data dalam jumlah yang terbilang besar.
    * Kekurangan : Interpretasi yang sulit dan membutuhkan hyperparameter tunning model yang tepat agar tepat untuk data.
- RandomForestRegressor:
    * Kelebihan : Dapat mengatasi noise dan missing value dan dapat mengatasi data dalam jumlah yang terbilang besar.
    * Kekurangan : Interpretasi yang sulit dan membutuhkan hyperparameter tunning model yang tepat agar tepat untuk data.
- Adaptive Boosting:
    * Kelebihan : Hasil dari pemodelan dapat lebih akurat karena mengkombinasikan beberapa model.
    * Kekurangan : Dapat mengurangi kemampuan interpretasi model karena meningkatnya kompleksitas model.

**Mengapa menggunakan model tersebut?**
- LinearRegression karena dapat melakukan generalisasi pada pola data, dan melakukan perhitungan pararel sehinggan proses training lebih cepat.
- DecisionTreeRegressor karena mampu memproses pengambilan keputusan yang kompleks menjadi lebih simpel dan mudan diinterpretasikan.
- K-Nearest Neighbor karena titik data akan diklasifikasikan berdasarkan kesamaan antar kelompok data yang berdekatan.
- RandomForestRegressor karena terbuat dari beberapa decision tree yang digabungkan sehingga mendapatkan hasil prediksi yang lebih stabil.
- Adaptive Boosting karena memilai prediksi model dan meningkatkan bobot sample dengan kesalahan yang dibuat pada model sebelumnya.

## Evaluation
- Metrik evaluasi yang digunakan disini adalah Mean Squared Error. Mean Squared Error disini dapat dikatakan adalah sebuah metrik yang mengukur seberapa besar error pada nilai aktual dan nilai hasil prediksi.
- Hasil yang diperoleh dari metrik ini apabila diurutkan dari error terkecil sampai terbesar adalah sebagai berikut:
    - RandomForestRegressor | train 0.002074 | test 0.009687
    - DecisionTreeRegressor | train 0.004165 | test 0.010623
    - K-Nearest Neighbor    | train 0.007251 | test 0.011366
    - LinearRegressor       | train 0.013481 | test 0.014259
    - Adaptive Boosting     | train 0.080138 | test 0.078409
  Dapat disimpulkan dari hasil diatas RandomForestRegressor merupakan paling akurat memprediksi data dengan selisih   
  error terkecil dibandingkan dengan model lainnya dan Adaptive Boosting memiliki error yang paling tinggi diantara 
  kelima model yang digunakan

**Formula Mean Squared Error dan cara Mean Squared Error bekerja** 

formula Mean Squared Error : (1/n) * Σ(actual – forecast)2

**Bagaimana cara Mean Squared Error bekerja?**

Cara kerjanya adalah dengan melakukan pengurangan nilai data aktual dengan nilai prediksi dan hasilnya akan dikuadratkan dan dijumlahkan secara keseluruhan kemudian dibagi dengan banyak data yang ada.

REFERENSI :
  [Irreversible climate change due to carbon dioxide emissions](https://www.pnas.org/doi/full/10.1073/pnas.0812721106) 

  [Climate Change: Atmospheric Carbon Dioxide](https://www.climate.gov/news-features/understanding-climate/climate-change-atmospheric-carbon-dioxide) 

  [CO2, the greenhouse effect and global warming: from the pioneering work of Arrhenius and Callendar to today’s Earth System Models](https://reader.elsevier.com/reader/sd/pii/S0160932716300308?token=926B8C03B6AF557DFA13E43DFAE380301F452C9AE0BD0ACA7B7345D65C02F0CE8AAC54E8BBC1904F448064BE28D0BBFD&originRegion=eu-west-1&originCreation=20230327151603) 
