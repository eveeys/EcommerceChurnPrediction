## Business Context
Pada 20 tahun terakhir, perdagangan dalam bentuk e-commerce berkembang dengan pesat sehingga banyak e-commerce bermunculan. E-commerce mulai berlomba-lomba untuk memberikan fitur dan inovasi untuk menarik pelanggan. Persaingan yang ketat terjadi di mana pelanggan dapat berhenti dari satu platform e-commerce ke platform lain dengan mudah. **Customer churn** adalah peristiwa ketika **pelanggan perusahaan berhenti berlanggaanan/tidak membeli** dari perusahaan lagi setelah jangka waktu tertentu.

## Problem Statement
Customer churn merupakan permasalahan yang sangat penting karena sebagai sumber pendapatan utama perusahaan, pelanggan adalah salah satu aset terpenting dalam perusahaan. Jika tingkat churn tinggi, maka pendapatan keseluruhan perusahaan akan berpengaruh.

Selain itu, secara umum, menurut European Business Review, biaya untuk mencari pelanggan baru 5-6x lebih mahal dibandingkan mempertahankan pelanggan lama. Maka dari itu, Customer Retention (kemampuan sebuah perusahaan mempertahankan customer) sangat penting. Apalagi, sedikit peningkatan pada nilai customer retention bisa menaikkan penjualan dan keuntungan secara dramatis. Maka dari itu, untuk memaksimalisasi keuntungan, perusahaan perlu meningkatkan customer retention.

## Goals
Untuk memaksimalisasi keuntungan, perusahaan ingin menaikkan customer retention dengan cara melakukan churn analysis dari data yang sudah tersedia. Perusahaan ingin (1) mampu memprediksi konsumer mana yang berpotensi akan churn, (2) mengetahui variabel/fitur penting apa saja yang mempengaruhi perilaku churn pelanggan. Hal ini dilakukan agar perusahaan dapat melakukan perencanaan marketing khusus bagi pelanggan-pelanggan yang berpotensi untuk churn.

## Analytic Approach
Data scientist akan menganalisis data untuk menemukan pola dari ciri-ciri pelanggan yang churn. Setelah itu, data scientist dapat membuat model klasifikasi yang dapat memprediksi apakah seorang pelanggan akan churn atau tidak.

## Metric Evaluation
Hasil prediksi churn oleh model yang akan dibuat memiliki definisi:  
0 : Negative --> diprediksi masih akan menjadi pelanggan/ tidak akan churn  
1 : Positive --> diprediksi akan berhenti menjadi pelanggan/ churn

Type 1 Error : **False Positive**  
Pelanggan diprediksi oleh model akan berhenti berbelanja di e-commerce, tetapi ternyata masih menjadi pelanggan.  
Konsekuensi: **pemborosan biaya** retensi, waktu, dan sumber daya (marketing, promo, dll untuk mengembalikan pelanggan).

Type 2 Error : **False Negative**  
Pelanggan diprediksi oleh model masih tetap akan berbelanja di e-commerce, tetapi ternyata berhenti belanja/churn.  
Konsekuensi: **kehilangan pelanggan** sehingga perusahaan akan kehilangan (1) sales & profit dari pelanggan, (2) mengeluarkan biaya untuk mengakuisisi pelanggan baru (yang jauh lebih mahal daripada biaya untuk mempertahankan pelanggan lama)

Lewat konsekuensi-konsekuensi di atas: Dikarenakan biaya untuk mengakuisisi pelanggan baru jauh lebih mahal dibandingkan menaikkan retensi, maka perusahaan akan fokus untuk meminimalisir FN agar perusahaan tidak kehilangan pelanggan.

Supaya perusahaan dapat fokus pada FN tanpa mengabaikan FP sepenuhnya, Metriks Evaluasi utama yang akan digunakan adalah **f beta score**. Dengan F beta score, data scientist dapat mengatur proporsi FN dan FP. Selain itu, f-beta score juga digunakan karena cocok untuk melihat evaluasi dari dataset yang imbalance.

Sesuai dengan referensi sebelumnya, digunakan *rule-of-thumb* bahwa untuk mengakuisi pelanggan baru 5x lebih mahal dibandingkan dengan mempertahankan pelanggan lama sehingga setiap 1 FN akan menyebabkan kerugian 5x lebih banyak daripada 1 FP. Maka dari itu, weighted average yang digunakan pada fbeta score adalah beta=5

## Informasi Atribut  
`Tenure` Lama pelanggan menjadi pelanggan (dalam satuan bulan)  
`WarehouseToHome` Jarak antara gudang dengan alamat pelanggan  
`NumberofDeviceRegistered` Jumlah gawai/perangkat yang terdaftar dengan akun pelanggan  
`PreferedOrderCat` Preferensi kategori pelanggan  
`SatisficationScore` Nilai satisfikasi/kepuasan pelanggan (dalam skala 1-5)  
`MaritalStatus` Status pernikahan pelanggan
`NumberofAddress`  Jumlah alamat yang ditambahkan pelanggan  
`Complain` Status komplain (1 - Pernah komplain, 0 - Tidak pernah komplain)  
`DaySinceLastOrder` Jumlah hari semenjak terakhir kali pelanggan memesan  
`CashbackAmount` Jumlah uang cashback yang didapatkan pelanggan  
`Churn` Status Churn, Pelanggan berhenti/pindah ke ecommerce lainnya (1 - Churn, 0 - Tidak Churn)

## Model Building & Evaluation
Setelah melakukan beberapa model building dan evaluasi (dapat dilihat di file Capstone1.ipynb), kami menyimpulkan akan menggunakan model **XGboost** dengan teknik **RandomOverSampling**.

![image](https://github.com/eveeys/EcommerceChurnPrediction/assets/113023460/b03bfba9-a972-4d32-ab51-79b587e90906)

![image](https://github.com/eveeys/EcommerceChurnPrediction/assets/113023460/0af79aa6-c33e-4aa1-9a0e-c613a9ed0c25)

Berdasarkan hasil pada model pada classification report: 

Dapat disimpulkan bahwa model dapat mengidentifikasi 97% pelanggan yang tidak akan churn dan juga berhasil mengidentifikasi 83% pelanggan yang akan churn. (berdasarkan recall)

Model ini memiliki ketepatan prediksi 83% di mana ada kemungkinan 17% dari pelanggan yang diprediksi churn ini ternyata tidak churn. (berdasarkan precision)

Untuk mengevaluasi model yang sudah ditetapkan (XGBoost Classifier), skenario bisnis akan dibuat seperti ini:

Diasumsikan bahwa biaya untuk mencari pelanggan baru 5x lebih mahal dibandingkan biaya untuk menarik pelanggan lama (retensi) sehingga:
* True Negative (TN) membutuhkan **0 * cost** karena merupakan pelanggan yang tidak churn dan diprediksi tidak churn
* False Negative (FN) membutuhkan cost tertinggi karena hasil FN merupakan pelanggan yang tidak terdeteksi akan churn sehingga harus membayar biaya mengakuisisi pelanggan. Diasumsikan membutuhkan **5 * cost**
* True Positive (TP) & False Positive (FP) merupakan pelanggan yang diprediksikan churn sehingga harus membayar biaya retensi sebanyak **1 * cost**

sehingga rumus untuk menghitung cost:
\begin{align}
Cost (c) = 5 * (c) * FN + 1 * (c) * (TP+FP) + 0 * (c) * TN 
\end{align}

Hasil :  
1. Skenario tidak memakai model & berasumsi semua pelanggan tidak churn  
Pada realitanya terdapat 137 pelanggan yang churn sehingga dibutuhkan biaya **5 * 137 (c) = 685 (c)**
2. Skenario tidak memakai model & fokus retensi kepada semua pelanggan  
Perusahaan membutuhkan **1 * 682 (c) = 682 (c)**
3. Skenario memakai model data scientist dan melakukan marketing sesuai kebutuhan  
Dengan menggunakan model XGBoost di atas maka butuh biaya : **5 * 17 (c) + 1 * (99+38) (c) + 0 * 528 (c) = 222 (c)**

![image](https://github.com/eveeys/EcommerceChurnPrediction/assets/113023460/e301e3f1-e780-4ead-b47f-f72146a74968)

Lewat analisis di atas, dapat disimpulkan bahwa dengan menggunakan XGBoost yang sudah di tuned, biaya yang bisa direduksi 67.5% daripada menggunakan tanpa model ataupun fokus retensi kepada semua pelanggan.

Ini berarti perusahaan dapat **menghemat sekitar 67.5% dari total biaya**.

Jika diasumsikan biaya untuk mengembalikan pelanggan lama USD 10, maka biaya yang dibutuhkan untuk:
* No Model: USD 6850
* Fokus retensi kepada semua pelanggan: USD 6820
* Menggunakan Model XGBoost yang Dituning: USD 2220

Ini berarti perusahaan dapat **menghemat sekitar USD 4600**.


## Feature Importance

![image](https://github.com/eveeys/EcommerceChurnPrediction/assets/113023460/423a48d1-84a2-4128-ae7f-38be1d2db9ad)

Dari plot SHAP di atas, dapat dilihat bahwa 5 fitur terpenting (secara berurutan dari yang paling penting) adalah: `Tenure`, `Complain`, `CashbackAmount`, `NumberOfAddress`, dan `DaySinceLastOrder`, di mana:
* Potensi churn semakin meningkat pada pelanggan yang baru berlangganan (nilai tenure kecil)
* Potensi churn semakin meningkat ketika pelanggan komplain
* Potensi churn semakin meningkat ketika jumlah cashback yang diterima pelanggan semakin sedikit
* Potensi churn semakin meningkat ketika semakin banyak jumlah alamat pelanggan yang terdaftar
* Potensi churn semakin meningkat pada pelanggan yang baru berbelanja

Selain itu:
* Potensi churn semakin meningkat pada pelanggan yang single
* Potensi churn semakin meningkat ketika jarak antara alamat pelanggan dan gudang semakin jauh
* Potensi churn semakin meningkat ketika tingkat satisfaction score semakin tinggi
* Potensi churn semakin meningkat ketika kategori yang dibeli bukan Laptop & Accessory, sedangkan potensi churn semakin meningkat ketika kategori yang dibeli adalah mobile phone

## Konklusi
1. Model dapat mengidentifikasi 97% pelanggan yang tidak akan churn dan juga **berhasil mengidentifikasi 83% pelanggan yang akan churn**. (berdasarkan recall)
2. Model ini memiliki **ketepatan prediksi 83%** di mana ada kemungkinan 17% dari pelanggan yang diprediksi churn ini ternyata tidak churn. (berdasarkan precision)
3. Model dapat **menghemat sekitar 67.5% dari total biaya** dengan asumsi biaya akuisisi pelanggan baru 5x lebih mahal dari biaya mengembalikan pelanggan lama
4. Limitasi dari model sebatas oleh value dari data yang sudah tersedia sebelumnya
5. Lima fitur terpenting (secara berurutan) berdasarkan model prediksi yang dibuat, dan shap plot merupakan `Tenure`, `Complain`, `CashbackAmount`, `NumberOfAddress`, dan `DaySinceLastOrder`

## Rekomendasi
Rekomendasi berdasarkan hasil analisis & pemodelan di atas adalah:
1. Untuk membuat model yang telah dibuat data scientist lebih baik, dapat:
    * Menambahkan data karena isi data sangat kecil, terutama untuk kelas 1 (churn)
    * Mencoba model hanya menggunakan fitur-fitur terpenting
    * Menambahkan fitur-fitur baru yang dapat berguna untuk churn prediction. Contoh berdasarkan artikel oleh Sid Dhuri:
        * Customer charateristic (Industry, Size, Revenue)
        * Product Charateristics (Type, Offline/Online)
        * Transaction HIstory (Recency, Frequency, Monetary Value, Length of Relationship)
        * Customer Engangement (CSAT, NPS)
        * User Experience (Hours Spent, Number of Visit, Ease of Use)
        * Faktor Eksternal (R&D Spent  Budget, Economic Indicators)
    * Mencoba algoritma Machine Learning, khususnya dengan metode gradient boosting, seperti AdaBoosting, LightGBM
    * Mencoba kembali hyperparameter tuning dengan parameter-parameter yang berbeda
    * Menganalisis data yang memiliki prediksi False Positive (FP) dan False Negative (FN) untuk mengetahui karakteristik dari data-data tersebut 
2. Membuat analisis lebih lanjut terhadap fitur-fitur berdasarkan plot shap & EDA yang sudah dilakukan untuk menemukan penyebab hubungan kausalitas/korelasi untuk mengurangi kemungkinan pelanggan churn. Hal-hal yang bisa dianalisis, salah satunya:
    * Apakah ada masalah pengiriman barang? (Karena pelanggan yang memiliki banyak alamat dan memiliki alamat yang jauh dari gudang cenderung untuk churn)
    * Apakah ada perubahan kebijakan dari perusahaan yang baru-baru ini diputuskan mempengaruhi tingkat churn? (pelanggan baru dan pelanggan yang baru membeli cenderung untuk churn)
    * Analisis komplain seperti apa yang dilakukan oleh pelanggan?
