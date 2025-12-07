🚀 Prediksi Kebutuhan Satuan Pendidikan - Kabupaten Bone
Proyek ini menyajikan implementasi pipeline Machine Learning Klasifikasi end-to-end yang bertujuan untuk memprediksi Kategori Prioritas Kebutuhan Satuan Pendidikan pada tingkat kecamatan di Kabupaten Bone, berdasarkan distribusi jumlah sekolah per jenjang.

🎯 Tujuan Utama
Tujuan utama dari proyek ini adalah untuk menyediakan alat bantu keputusan yang reliable bagi pihak berwenang di Kabupaten Bone dalam menentukan alokasi sumber daya atau upaya peningkatan kualitas pendidikan pada kecamatan yang memiliki kebutuhan paling tinggi (Prioritas Tinggi).

1. Persiapan dan Pembentukan Variabel Target

Proses dimulai dengan penyiapan data, diawali dengan konversi kolom-kolom hitungan sekolah per jenjang (fitur kuantitatif) ke tipe data numerik (`float64`). Selanjutnya, variabel target (`Prioritas_Label`) dibentuk menggunakan diskritisasi kuantil (q=3) berdasarkan total jumlah sekolah. Kecamatan dengan jumlah sekolah sedikit dikategorikan sebagai **Prioritas Tinggi**, sedangkan kecamatan dengan jumlah sekolah banyak dikategorikan sebagai **Prioritas Rendah**. Data kemudian di-*encode* menjadi numerik dan dibagi secara **stratifikasi** menjadi **Data Latih** (23 sampel) dan **Data Uji** (6 sampel), memastikan distribusi kelas yang seimbang di kedua set.

2. Seleksi Model dan Validasi Silang

Setelah data siap, dilakukan proses seleksi model dengan menguji lima algoritma klasifikasi berbeda, masing-masing terintegrasi dalam **`Pipeline`** bersama dengan *feature scaling*. Pengujian dilakukan melalui **5-fold Cross-Validation** dengan metrik utama **F1-macro**, yang ideal untuk mengukur kinerja seimbang pada klasifikasi multi-kelas. Dari hasil pengujian, **Random Forest Classifier** terpilih sebagai model terbaik dengan skor F1-macro tertinggi ($\approx 0.8489$).

 3. Evaluasi Kinerja Kritis

Model terbaik kemudian dilatih ulang dan dievaluasi pada Data Uji yang belum pernah dilihat. Hasil evaluasi menunjukkan akurasi keseluruhan sebesar **$83.33\%$**. Namun, analisis *Classification Report* mengungkapkan adanya **kelemahan kritis** pada kategori **'Prioritas Sedang'**, ditandai dengan nilai **Recall hanya $0.50$**. Maksud dari temuan ini adalah bahwa model sering gagal mengidentifikasi separuh dari kasus 'Prioritas Sedang' yang sebenarnya, menggarisbawahi kebutuhan mendesak untuk tahap pengoptimalan (*refinement*) model lebih lanjut.

 4. Penerapan Model (*Deployment*) Interaktif

Sebagai langkah akhir, model yang sudah divalidasi dikemas menjadi alat yang dapat digunakan secara praktis. Hal ini dicapai dengan membuat fungsi prediksi (`predict_priority`) dan mengintegrasikannya ke dalam antarmuka web interaktif menggunakan pustaka **Gradio**. Antarmuka ini memungkinkan pengguna memasukkan jumlah satuan pendidikan per jenjang dan menerima hasil prediksi **Kategori Prioritas (Tinggi/Sedang/Rendah)** secara instan, mengubah model Machine Learning menjadi alat bantu pengambilan keputusan yang siap diimplementasikan.
