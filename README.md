# 🌍 Predict CO2 Emissions in Rwanda 

## 📌 Project Overview
[cite_start]Proyek ini bertujuan untuk mengembangkan model *machine learning* yang mampu memprediksi tingkat emisi CO2 mingguan di berbagai lokasi di Rwanda[cite: 104, 105]. [cite_start]Hasil prediksi ini dirancang untuk mengeksplorasi berbagai skenario polutan, sehingga dapat membantu pembuat kebijakan dalam memahami konsekuensi lingkungan dan merencanakan program pengurangan emisi, seperti pengembangan energi terbarukan[cite: 106, 107, 702, 706, 709, 711].

* [cite_start]**Peran Saya:** Project Leader & Data Analyst (Tim PyBoys)[cite: 43, 44, 46, 47].
* [cite_start]**Dataset:** Data kompetisi Kaggle yang terdiri dari pengamatan emisi mingguan di 497 lokasi unik di Rwanda (Data latih: 2019-2021, Data uji: 2022)[cite: 124, 133, 138, 140].

## 🔬 Methodology & Workflow

### 1. Exploratory Data Analysis (EDA)
Melalui analisis data eksploratif, ditemukan beberapa *insight* krusial:
* [cite_start]**Tren Siklis:** Emisi CO2 memiliki pola siklis di mana tingkat emisi cenderung naik selama 8-10 minggu, kemudian turun selama 8-10 minggu, dan berulang[cite: 422].
* [cite_start]**Anomali Pandemi:** Terdapat anomali tren pada tahun 2020 akibat kebijakan *lockdown* pandemi COVID-19, yang menyebabkan polanya berbeda dari tahun 2019 dan 2021[cite: 423].
* [cite_start]**Distribusi Target:** Terdapat *outliers* yang signifikan pada variabel target emisi[cite: 256].
* [cite_start]**Missing Values:** Fitur `UvAerosolLayerHeight` memiliki data kosong ekstrem (lebih dari 90%)[cite: 241].

### 2. Data Preparation & Engineering
Untuk menangani kompleksitas data, beberapa teknik pra-pemrosesan diterapkan:
* [cite_start]**Penanganan Missing Values:** Menghapus kolom dengan data kosong >60%, menggunakan algoritma *KNN Imputer* untuk kolom dengan kekosongan 10-60%, dan *Mean Imputation* untuk kekosongan <10%[cite: 440, 443, 449].
* [cite_start]**Modifikasi Anomali 2020:** Melakukan normalisasi data emisi tahun 2020 dengan mengalikannya menggunakan rasio rata-rata mingguan dari tahun 2019 dan 2021[cite: 461].
* [cite_start]**Feature Engineering:** Menerapkan teknik *sin-cos encoding* (penskalaan sinus dan kosinus) pada fitur koordinat (lintang/bujur) serta fitur waktu (bulan dan minggu) untuk menangkap pola siklis secara matematis[cite: 490, 492].

### 3. Modelling & Evaluation
[cite_start]Dua algoritma ansambel berbasis *tree*, yaitu XGBoost dan Random Forest, dievaluasi[cite: 546, 561, 564]. [cite_start]Kedua model ini dipilih karena ketahanannya terhadap *overfitting* dan efektivitasnya pada masalah regresi[cite: 570, 572].

[cite_start]Setelah melakukan *Hyperparameter Tuning* menggunakan `RandomizedSearchCV`[cite: 581], model **Random Forest** terpilih sebagai model terbaik dengan konfigurasi akhir dan metrik performa sebagai berikut:
* [cite_start]**n_estimators:** 100 [cite: 596]
* **min_sample_split:** 4 [cite: 594]
* [cite_start]**min_sample_leaf:** 3 [cite: 593]
* [cite_start]**RMSE:** 16.71 [cite: 598]
* **R-squared:** 0.987 [cite: 599]

Visualisasi sebaran prediksi menunjukkan bahwa titik data hasil prediksi tersebar sangat dekat dengan garis prediksi aktual sempurna, membuktikan keakuratan model[cite: 624, 625, 628].

*(Tambahkan gambar screenshot grafik Prediksi vs Aktual di sini)*
`![Evaluation](assets/evaluation.png)`

## 🚀 Deployment (Streamlit Web App)
Logika prediksi dari model yang telah dilatih kemudian diintegrasikan ke dalam antarmuka aplikasi web interaktif menggunakan antarmuka **Streamlit**. Aplikasi ini memuat fitur deskripsi data, analitik, dan panel *Predict Emission* berbasis koordinat peta[cite: 671, 672, 673, 680, 681].

[cite_start]🔗 **Coba Aplikasi Web secara langsung:** [PyBoys CO2 Emission Prediction](https://pyboys-project.streamlit.app/) [cite: 668, 677, 680]

*(Tambahkan gambar screenshot web aplikasi Anda di sini)*
`![Web Preview](assets/web_preview.png)`

---
*Catatan: Repositori ini dikhususkan untuk menampilkan antarmuka deployment dan arsitektur web (Front-End/App). Kode pelatihan model Machine Learning inti bersifat privat.*
