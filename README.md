# 🍎 Klasifikasi Penyakit Daun Apel Menggunakan ResNet50

## 👥 Kelompok 4

| Nama                      | NIM          |
| ------------------------- | ------------ |
| **Rizqita Martha Amalia** | 240441100027 |
| **Reva Pramaulidia**      | 240441100131 |
| **Hilyatul Abidah**       | 240441100132 |

---

## 📌 Deskripsi Proyek

Proyek ini merupakan implementasi **Deep Learning untuk klasifikasi citra daun apel** menggunakan metode **Transfer Learning** dengan arsitektur **ResNet50**.

Model digunakan untuk mengklasifikasikan citra daun apel ke dalam **4 kategori**, yaitu:

1. 🍎 **APPLE ROT LEAVES**
2. 🌿 **HEALTHY LEAVES**
3. 🍂 **LEAF BLOTCH**
4. 🍃 **SCAB LEAVES**

Dataset yang digunakan terdiri dari **419 citra daun apel** yang kemudian diproses melalui tahap preprocessing, pembagian dataset, training model, dan evaluasi.

---

## 🎯 Tujuan

Tujuan dari proyek ini adalah:

* Membangun model Deep Learning untuk melakukan klasifikasi penyakit pada daun apel.
* Menerapkan **Transfer Learning menggunakan ResNet50**.
* Membandingkan beberapa strategi training untuk mengetahui pengaruh **data augmentation** dan **fine-tuning** terhadap performa model.
* Mengevaluasi performa model menggunakan beberapa metrik evaluasi.

---

## 📊 Dataset

Dataset yang digunakan adalah **APPLE_DISEASE_DATASET**.
https://www.kaggle.com/datasets/hsmcaju/d-kap?utm_source=&select=APPLE_DISEASE_DATASET

### Jumlah Data

| Kelas            | Jumlah Citra |
| ---------------- | -----------: |
| APPLE ROT LEAVES |          103 |
| HEALTHY LEAVES   |           46 |
| LEAF BLOTCH      |          111 |
| SCAB LEAVES      |          159 |
| **Total**        |      **419** |

Dataset terdiri dari 4 kelas dengan karakteristik visual yang berbeda.

---

## 🔄 Preprocessing Data

Sebelum digunakan untuk proses training, citra melalui beberapa tahap preprocessing.

### Tahapan preprocessing:

1. Membaca dataset berdasarkan kategori kelas.
2. Membagi dataset menjadi:

   * **Training: 333 citra**
   * **Validation: 40 citra**
   * **Testing: 46 citra**
3. Mengubah ukuran citra menjadi **224 × 224 piksel**.
4. Mengubah citra menjadi tensor.
5. Melakukan normalisasi menggunakan parameter yang sesuai dengan **ImageNet**.
6. Pada skenario tertentu, diterapkan **Data Augmentation** pada data training.

---

## 🧠 Model yang Digunakan

Model yang digunakan adalah:

### ResNet50

ResNet50 merupakan arsitektur Convolutional Neural Network (CNN) yang digunakan dalam pendekatan **Transfer Learning**.

Model menggunakan bobot **pre-trained ImageNet**, kemudian bagian klasifikasi disesuaikan dengan jumlah kelas pada dataset.

### Konfigurasi Utama

| Parameter     | Nilai            |
| ------------- | ---------------- |
| Model         | ResNet50         |
| Pre-trained   | ImageNet         |
| Jumlah kelas  | 4                |
| Input image   | 224 × 224        |
| Loss Function | CrossEntropyLoss |
| Optimizer     | Adam             |
| Learning Rate | 0.001            |
| Epoch         | 10               |

---

## 🧪 Skenario Eksperimen

Dalam proyek ini digunakan **3 skenario eksperimen**.

### 🔹 Skenario 1 — Transfer Learning

Pada skenario pertama:

* Menggunakan ResNet50 pre-trained.
* Seluruh backbone ResNet50 dibekukan.
* Hanya **Fully Connected (FC) Layer** yang dilatih.
* Tidak menggunakan data augmentation.

Tujuannya adalah melihat performa dasar dari pendekatan transfer learning.

---

### 🔹 Skenario 2 — Transfer Learning + Data Augmentation

Pada skenario kedua:

* Menggunakan ResNet50 pre-trained.
* Backbone tetap dibekukan.
* FC layer dilatih.
* Data training diberikan **data augmentation**.

Tujuannya adalah melihat apakah penambahan variasi pada data training dapat membantu model melakukan generalisasi dengan lebih baik.

---

### 🔹 Skenario 3 — Fine-Tuning + Data Augmentation

Pada skenario ketiga:

* Menggunakan ResNet50 pre-trained.
* Sebagian besar backbone tetap dibekukan.
* Bagian **`layer4`** dan FC layer dibuat trainable.
* Data augmentation tetap digunakan.

Fine-tuning dilakukan agar model dapat menyesuaikan fitur yang telah dipelajari dari ImageNet dengan karakteristik citra daun apel.

---

## 📈 Hasil Training

### Skenario 1

Pada epoch ke-10 diperoleh:

| Metrik              |      Nilai |
| ------------------- | ---------: |
| Train Loss          |     0.6285 |
| Validation Loss     |     0.9500 |
| Train Accuracy      | **81.08%** |
| Validation Accuracy | **65.00%** |

---

### Skenario 2

Pada epoch ke-10 diperoleh:

| Metrik              |      Nilai |
| ------------------- | ---------: |
| Train Loss          |     0.7998 |
| Validation Loss     |     0.9703 |
| Train Accuracy      | **72.07%** |
| Validation Accuracy | **60.00%** |

---

### Skenario 3

Skenario ketiga menggunakan pendekatan **fine-tuning pada `layer4` dan FC layer serta data augmentation**.

Nilai evaluasi akhir Skenario 3 mengikuti hasil output evaluasi pada notebook.

> **Catatan:** nilai Accuracy, Precision, Recall, dan F1-Score Skenario 3 perlu diambil dari output evaluasi final notebook apabila sudah dijalankan.

---

## 📏 Evaluasi Model

Model dievaluasi menggunakan beberapa metrik:

### Accuracy

Mengukur persentase prediksi model yang sesuai dengan label sebenarnya.

### Precision

Mengukur ketepatan model ketika memberikan prediksi terhadap suatu kelas.

### Recall

Mengukur kemampuan model dalam menemukan data yang termasuk ke dalam suatu kelas.

### F1-Score

Merupakan nilai yang menggabungkan Precision dan Recall.

### Confusion Matrix

Confusion Matrix digunakan untuk melihat distribusi prediksi model pada masing-masing kelas, termasuk prediksi yang benar maupun salah.

---

## 🔬 Alur Penelitian

```text
Dataset Apple Disease
        │
        ▼
   Preprocessing
        │
        ▼
  Pembagian Dataset
        │
   ┌────┼────┐
   ▼    ▼    ▼
 Train  Val  Test
   │
   ▼
ResNet50 Pre-trained
   │
   ├───────────────┐
   ▼               ▼
Skenario 1     Skenario 2
Transfer       Transfer Learning
Learning       + Augmentation
   │               │
   └───────┬───────┘
           ▼
      Skenario 3
 Fine-Tuning + Augmentation
           │
           ▼
       Evaluasi Model
           │
           ▼
 Accuracy, Precision,
 Recall, F1-Score &
 Confusion Matrix
```

---

## 🛠️ Teknologi yang Digunakan

Proyek ini menggunakan beberapa teknologi dan library berikut:

* **Python**
* **Google Colab**
* **PyTorch**
* **Torchvision**
* **ResNet50**
* **NumPy**
* **Matplotlib**
* **Scikit-learn**
* **PIL (Python Imaging Library)**

---

## 📁 Struktur Repository

Struktur repository dapat disusun seperti berikut:

```text
📦 apple-disease-classification
│
├── 📂 dataset/
│   └── APPLE_DISEASE_DATASET/
│
├── 📂 notebook/
│   └── dataset_apel.ipynb
│
├── 📂 results/
│   ├── training_curve/
│   ├── confusion_matrix/
│   └── evaluation/
│
├── 📄 README.md
└── 📄 requirements.txt
```

> Dataset dapat diletakkan secara terpisah apabila ukurannya terlalu besar untuk disimpan langsung di repository GitHub.

---

## 🚀 Cara Menjalankan Project

### 1. Clone Repository

```bash
git clone https://github.com/username/apple-disease-classification.git
```

### 2. Masuk ke Folder Project

```bash
cd apple-disease-classification
```

### 3. Install Library

```bash
pip install torch torchvision numpy matplotlib scikit-learn pillow
```

Atau jika tersedia file `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 4. Jalankan Notebook

Buka:

```text
notebook/dataset_apel.ipynb
```

Notebook dapat dijalankan menggunakan **Google Colab** atau **Jupyter Notebook**.

### 5. Siapkan Dataset

Pastikan dataset memiliki struktur folder berdasarkan kelas:

```text
APPLE_DISEASE_DATASET/
│
├── APPLE ROT LEAVES/
├── HEALTHY LEAVES/
├── LEAF BLOTCH/
└── SCAB LEAVES/
```

### 6. Jalankan Sel Notebook

Jalankan cell secara berurutan mulai dari proses pembacaan dataset, preprocessing, training, hingga evaluasi.

---

## 📌 Kesimpulan

Proyek ini menerapkan **Transfer Learning menggunakan ResNet50** untuk melakukan klasifikasi citra penyakit daun apel.

Eksperimen dilakukan melalui tiga pendekatan, yaitu:

* Transfer Learning tanpa augmentasi.
* Transfer Learning dengan data augmentation.
* Fine-Tuning dengan data augmentation.

Hasil eksperimen menunjukkan bahwa strategi training yang berbeda dapat menghasilkan performa model yang berbeda. Oleh karena itu, perbandingan beberapa skenario digunakan untuk melihat pengaruh augmentasi dan fine-tuning terhadap proses klasifikasi.

---


## 📚 Catatan

Repository ini dibuat sebagai bagian dari tugas kelompok pada mata kuliah yang berkaitan dengan **Data Science / Deep Learning**.

**Kelompok 4 — Klasifikasi Penyakit Daun Apel 🍎**
