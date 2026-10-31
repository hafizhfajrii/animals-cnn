# Animals-10 Image Classification

Klasifikasi gambar 10 jenis hewan menggunakan CNN (TensorFlow/Keras), dengan model akhir diekspor ke format **SavedModel**, **TF-Lite**, dan **TFJS**.

## Dataset
- **Sumber**: [Animals-10 (Kaggle)](https://www.kaggle.com/datasets/alessiocorrado99/animals10)
- **Jumlah**: 26.179 gambar, 10 kelas (butterfly, cat, chicken, cow, dog, elephant, horse, sheep, spider, squirrel)
- **Resolusi**: tidak seragam (diubah ke 150x150 saat dimuat)
- **Pembagian**: Train 80% (20.938) / Validation 10% (2.614) / Test 10% (2.627)

## Model
- `Sequential` dengan layer `Conv2D`, `MaxPooling2D`, dan `GlobalAveragePooling2D`
- Transfer learning menggunakan MobileNetV2 (pretrained ImageNet) sebagai ekstraktor fitur
- Augmentasi (flip, rotasi, zoom, kontras) hanya diterapkan pada data training
- Callback: `EarlyStopping`, `ReduceLROnPlateau`, dan callback kustom berhenti di akurasi >= 95%

## Hasil
| Data       | Akurasi |
|------------|---------|
| Train      | 96,57%  |
| Validation | 94,22%  |
| Test       | 94,21%  |

## Struktur Folder
```
submission
├── tfjs_model
│   ├── group1-shardXofY.bin
│   └── model.json
├── tflite
│   ├── model.tflite
│   └── label.txt
├── saved_model
│   ├── saved_model.pb
│   └── variables
├── notebook.ipynb
├── notebook.py
├── README.md
└── requirements.txt
```

## Cara Menjalankan
1. Buka `notebook.ipynb` di Google Colab (disarankan GPU T4).
2. Jalankan semua cell secara berurutan. Dataset diunduh otomatis lewat `kagglehub`.
3. Untuk menginstal dependensi lokal: `pip install -r requirements.txt`

> Catatan: konversi TFJS dijalankan di environment terpisah (Python 3.11, TensorFlow 2.15.1, tensorflowjs 4.22.0) karena tidak kompatibel dengan TensorFlow versi terbaru.