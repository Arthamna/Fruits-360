# Fruits-360 — Klasifikasi Buah

Final Project Machine Learning. Proyek ini melatih dan membandingkan dua model untuk mengklasifikasikan gambar buah dari dataset [Fruits-360](https://www.kaggle.com/datasets/moltean/fruits) (260 kelas, gambar 100×100), lalu menyediakan antarmuka Gradio untuk prediksi interaktif.

## Model

| Model | Deskripsi |
|-------|-----------|
| **CustomCNN** | CNN sederhana dilatih dari nol (3 blok Conv → GlobalAveragePooling → Dense). |
| **MobileNetV2** | Transfer learning dari bobot ImageNet, base dibekukan, hanya head yang dilatih. |

Kedua model menyertakan layer preprocessing (`Rescaling`) di dalamnya, sehingga gambar input cukup dalam rentang 0–255 tanpa rescaling manual.

## Struktur Proyek

```
.
├── fruits-360-build-model.ipynb   # Latih, evaluasi, dan bandingkan kedua model
├── gradio.ipynb                   # Antarmuka prediksi interaktif
├── Fruits360-CustomCNN.keras      # Model CustomCNN terlatih
├── Fruits360-MobileNetV2.keras    # Model MobileNetV2 terlatih
└── README.md
```

## Persyaratan

- Python 3.12
- TensorFlow / Keras, scikit-learn, matplotlib, numpy, gradio

```bash
pip install tensorflow scikit-learn matplotlib numpy gradio
```

## Penggunaan

### 1. Melatih & mengevaluasi model

Buka `fruits-360-build-model.ipynb`. Notebook ini:

- Memuat dataset dan membagi data Training menjadi train/validation (80/20).
- Melatih CustomCNN dan MobileNetV2, dengan augmentasi dan EarlyStopping.
- Menampilkan grafik loss & accuracy per epoch.
- Mengevaluasi pada data Test: accuracy, loss, precision, recall, F1-score, dan classification report per kelas.

Sesuaikan `train_path` dan `test_path` di sel pertama dengan lokasi dataset di komputermu.

### 2. Menjalankan antarmuka prediksi

Buka `gradio.ipynb`, sesuaikan `TEST_PATH` (untuk membaca nama kelas) lalu jalankan semua sel. Unggah gambar buah, pilih model (CustomCNN atau MobileNetV2), dan lihat 5 prediksi teratas beserta probabilitasnya.

## Catatan

- Dataset Fruits-360 difoto pada kondisi terkontrol (latar bersih, objek di tengah). Model cenderung sangat akurat pada data Test, tetapi performa pada gambar dunia nyata bisa lebih rendah karena perbedaan distribusi.
- `IMG_SIZE` saat prediksi harus sama dengan ukuran saat training (100×100).