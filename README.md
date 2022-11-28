# EcommerceChurnPrediction

Capstone Project Ketiga yang diberikan oleh Purwadhika.

Pada 20 tahun terakhir, perdagangan dalam bentuk e-commerce berkembang dengan pesat sehingga banyak e-commerce bermunculan. E-commerce mulai berlomba-lomba untuk memberikan fitur dan inovasi yang menarik untuk menarik pelanggan. Persaingan yang ketat terjadi di mana pelanggan dapat berhenti dari satu platform e-commerce ke platform lain dengan mudah. Customer churn adalah peristiwa ketika pelanggan perusahaan berhenti berlanggaanan/tidak membeli dari perusahaan lagi setelah jangka waktu tertentu.

Customer churn merupakan permasalahan yang sangat penting karena sebagai sumber pendapatan utama perusahaan, pelanggan adalah salah satu aset terpenting dalam perusahaan. Jika tingkat churn tinggi, maka pendapatan keseluruhan perusahaan akan berpengaruh.

Selain itu, secara umum, menurut European Business Review, biaya untuk mencari pelanggan baru 5-6x lebih mahal dibandingkan mempertahankan pelanggan lama. Maka dari itu, Customer Retention (kemampuan sebuah perusahaan mempertahankan customer) sangat penting. Apalagi, sedikit peningkatan pada nilai customer retention bisa menaikkan penjualan dan keuntungan secara dramatis. Maka dari itu, untuk memaksimalisasi keuntungan, perusahaan perlu meningkatkan customer retention.

Untuk memaksimalisasi keuntungan, perusahaan ingin menaikkan customer retention dengan cara melakukan churn analysis dari data yang sudah tersedia. Perusahaan ingin (1) mampu memprediksi konsumer mana yang berpotensi akan churn, (2) mengetahui variabel/fitur penting apa saja yang mempengaruhi perilaku churn pelanggan. Hal ini dilakukan agar perusahaan dapat melakukan perencanaan marketing khusus bagi pelanggan-pelanggan yang berpotensi untuk churn.

Menganalisis data untuk menemukan pola dari ciri-ciri pelanggan yang churn. Setelah itu, data scientist dapat membuat model klasifikasi yang dapat memprediksi apakah seorang pelanggan akan churn atau tidak.

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

Supaya perusahaan dapat fokus pada FN tanpa mengabaikan FP sepenuhnya, Metriks Evaluasi utama yang akan digunakan adalah f beta score. Dengan F beta score, data scientist dapat mengatur proporsi FN dan FP. Selain itu, f-beta score juga digunakan karena cocok untuk melihat evaluasi dari dataset yang imbalance.

Sesuai dengan referensi sebelumnya, digunakan *rule-of-thumb* bahwa untuk mengakuisi pelanggan baru 5x lebih mahal dibandingkan dengan mempertahankan pelanggan lama sehingga setiap 1 FN akan menyebabkan kerugian 5x lebih banyak daripada 1 FP. Maka dari itu, weighted average yang digunakan pada fbeta score adalah beta=5
