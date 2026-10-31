# EDA dan Enumerasi Gigi Susu Berbasis FDI

**Aprilia Dwi Cristyana — 1226800011**

## Tentang pengumpulan ini

Repositori ini mendokumentasikan pekerjaan UTS Sains Data secara lengkap, mulai dari EDA awal, penanganan temuan EDA, pengujian hipotesis, analisis ketahanan, sampai pelatihan dan evaluasi model deteksi serta enumerasi gigi susu. **Notebook yang disertakan sudah dijalankan dan disimpan beserta output-nya.** Folder hasil, laporan PDF, serta dokumen Word juga disertakan sebagai bukti pelaksanaan analisis.

**Pembaca tidak perlu menjalankan ulang notebook untuk menilai hasil pengumpulan ini.** Tabel, grafik, log keputusan, hasil koreksi, hasil pengujian, dan evaluasi model dapat diperiksa langsung dari notebook serta folder hasil yang tersedia. Petunjuk eksekusi ulang disediakan sebagai pilihan bagi pembaca yang ingin mereproduksi analisis atau mencoba eksperimen berikutnya.

### Cara membaca hasil tanpa menjalankan ulang

1. Baca `1226800011_Aprilia_Dwi_Cristyana_UjianEDA.pdf` untuk mengikuti tujuan, temuan, penanganan, serta interpretasi hasil.  
2. Buka notebook **00** untuk memeriksa bukti EDA sebelum penanganan UTS dan masalah awal yang ditemukan.  
3. Buka notebook **01** untuk melihat penerapan koreksi anotasi, audit split, hasil empat hipotesis, tiga analisis ketahanan, dan praktik perubahan parameter IQR pada cell terakhir.  
4. Buka notebook **02** untuk melihat hasil training baseline YOLO11n dan model usulan YOLO11m, termasuk metrik test, kurva training, dan confusion matrix.  
5. Buka notebook **04** untuk melihat perbandingan YOLO11n tanpa preprocessing dan augmentasi dengan baseline HE dan brightness, pada patience 15 yang sama.  
6. Cocokkan output notebook dengan tabel, manifest, log koreksi, dan berkas evaluasi di folder hasil. Tidak perlu menekan **Run all** apabila hanya ingin membaca hasil yang sudah tersedia.

### Status pelaksanaan

| Tahap | Bukti yang disertakan | Status |
| :---- | :---- | :---- |
| EDA awal | Output notebook 00 dan folder `hasil_EDA_awal_sebelum_UTS/` | Sudah dijalankan |
| Penanganan dan audit data | Output notebook 01, log koreksi, manifest split, dan dataset terkoreksi | Sudah dijalankan |
| Hipotesis dan ketahanan | Tabel empat hipotesis dan tiga analisis ketahanan di `hasil_analisis/tabel/` | Sudah dijalankan |
| Praktik perubahan IQR | Output cell terakhir notebook 01 dan CSV praktik IQR | Sudah dijalankan |
| Baseline dan model usulan | Output notebook 02 serta hasil run `20261031_124203` | Sudah dijalankan |
| Perbandingan sebelum dan sesudah pengolahan | Output notebook 04 serta hasil run `20261031_173820` | Sudah dijalankan |

## Struktur paket pengumpulan

Nama folder dan berkas dipertahankan agar notebook, hasil run, dan panduan saling sesuai.

```
1226800011_Aprilia_UjianEDA_Revisi/
├── README
├── 00_Salinan_EDA_sebelum_UTS.ipynb
├── 01_EDA_Penanganan_Hasil_Akhir.ipynb
├── 02_Baseline_YOLO11n_Usulan_YOLO11m_Colab.ipynb
├── 04_Perbandingan_YOLO11n_Asli_vs_Baseline_Patience15.ipynb
├── 1226800011_Aprilia_Dwi_Cristyana_UjianEDA.pdf
├── enumerasi_gigi_susu_252_label_asli.zip
├── DENTAL DATASET PARAMITA 2016-2018/
├── Data terpilih dari Dental Paramita 11-12/
├── Dataset PARAMITA 2026/
├── Childrens dental caries segmentation dataset_KAGEL/
├── hasil_EDA_awal_sebelum_UTS/
├── hasil_analisis/
│   ├── tabel/
│   ├── grafik/
│   ├── review/
│   ├── overlay_koreksi/
│   ├── dataset_terkoreksi/
│   └── pemodelan/
│       └── 20261031_124203/
└── hasil_perbandingan_dua_YOLO11n/
    └── 20261031_173820/
```

Pada GitHub, gunakan nama **`README.md`** di direktori utama agar panduan ini muncul saat repositori dibuka. `README` merupakan salinan panduan untuk folder pengumpulan di Drive. File sumber, dataset, dan keluaran dijelaskan pada bagian berikutnya.

Penelitian ini bertujuan mendeteksi lokasi gigi susu pada radiograf panoramik dan memberikan nomor FDI pada setiap gigi yang tampak. Target terdiri atas 20 kelas, yaitu 51–55, 61–65, 71–75, dan 81–85. Cakupan penelitian adalah anak usia 1–12 tahun. Umur bukan input atau target prediksi model. Data tanpa umur tepat tetap dianalisis berdasarkan keberadaan gigi susu dan anotasi FDI, tanpa mengisi umur secara perkiraan.

Folder proyek di Drive: [1226800011\_Aprilia\_UjianEDA\_Revisi](https://drive.google.com/drive/folders/1ixSBScRA9kuaY-9KscP21o4kEbd7nrfu).

## 1\. File, fungsi, dan lokasi hasil

Seluruh lokasi hasil berikut dihitung dari folder proyek `MyDrive/1226800011_Aprilia_UjianEDA_Revisi`.

1. [**00\_Salinan\_EDA\_sebelum\_UTS.ipynb**](https://drive.google.com/file/d/1bhKlhwu8BVLGOeMo_MG9jYEMO_fP_m3q/view) digunakan untuk EDA awal sebelum penanganan UTS. Notebook membaca label asli untuk memperlihatkan distribusi kelas, statistik citra, metadata usia, outlier, FDI berulang, dan kandidat kemiripan. Terdapat pula demonstrasi preprocessing dan augmentasi. Hasilnya disimpan di `hasil_EDA_awal_sebelum_UTS/`, dengan subfolder EDA sebelum label serta hasil EDA berlabel. Dataset ekspor pada tahap ini masih menggunakan versi anotasi awal.  
2. [**01\_EDA\_Penanganan\_Hasil\_Akhir.ipynb**](https://drive.google.com/file/d/1-fH5M78xBwmJn5MpH2snnd9r04WgM9Q3/view) digunakan untuk membaca ulang data sumber, menerapkan koreksi FDI, memverifikasi split dan duplikat citra, menganalisis outlier, menguji empat hipotesis, serta menjalankan tiga analisis ketahanan. Cell terakhir memuat praktik perubahan parameter IQR dari 1,5 menjadi 3,0. Hasil utama disimpan di `hasil_analisis/`.  
3. [**02\_Baseline\_YOLO11n\_Usulan\_YOLO11m\_Colab.ipynb**](https://drive.google.com/file/d/1XUdEoii_qYjcqrYjdRp_vDgulhx8_HS3/view) melatih dan mengevaluasi baseline YOLO11n serta model usulan YOLO11m pada dataset terkoreksi yang sama. Kedua model memakai HE dan augmentasi brightness train. Hasil disimpan di `hasil_analisis/pemodelan/<waktu_run>/`. Run yang dilaporkan adalah `20261031_124203`.  
4. [**04\_Perbandingan\_YOLO11n\_Asli\_vs\_Baseline\_Patience15.ipynb**](https://drive.google.com/file/d/1MVQrbQqmkusO8Ne4rqLUZI6qMJc4FOy8/view) melatih YOLO11n pada citra asli bersih tanpa HE dan augmentasi, kemudian membandingkannya dengan baseline YOLO11n pada nomor 3\. Patience keduanya sama, yaitu 15\. Hasil disimpan di `hasil_perbandingan_dua_YOLO11n/<waktu_run>/`. Run citra asli yang dilaporkan adalah `20261031_173820`.  
5. **`1226800011_Aprilia_Dwi_Cristyana_UjianEDA.pdf`** merupakan laporan PDF final dengan hasil Colab.  
6. `README` berisi penjelasan berkas, sumber data, keputusan, hasil angka, dan urutan eksekusi. Keduanya memuat panduan yang sama dalam paket lokal.  
7. **`enumerasi_gigi_susu_252_label_asli.zip`** berisi 252 citra asli, pasangan label YOLO awal, dan `data.yaml`. Notebook mengekstraknya otomatis ke penyimpanan lokal runtime. ZIP ini adalah input, bukan dataset terkoreksi.

### Keluaran penting dalam `hasil_analisis/`

| Folder atau file | Isi dan kegunaan |
| :---- | :---- |
| `tabel/` | Statistik awal dan akhir, log koreksi, audit FDI berulang, empat hipotesis, sensitivitas, dan praktik IQR. |
| `grafik/` | Visualisasi distribusi FDI, kualitas citra, skema FDI, dan before–after. |
| `overlay_koreksi/` | Perbandingan citra beranotasi sebelum dan sesudah koreksi. |
| `review/` | Bukti audit dan daftar pemeriksaan citra. |
| `dataset_terkoreksi/` | Dataset siap model, berisi `train/`, `valid/`, `test/`, `data.yaml`, dan `manifest.csv`. |
| `RUN_COMPLETE.json` | Penanda bahwa persiapan data selesai dan hash manifest tercatat. |
| `pemodelan/20261031_124203/perbandingan_test.csv` | Hasil test YOLO11n dan YOLO11m yang digunakan dalam laporan. |
| `tabel/praktik_parameter_IQR_1_5_vs_3.csv` | Hasil praktik perubahan koefisien IQR di cell terakhir notebook 01\. |

### Keluaran notebook 04

- `perbandingan_dua_kondisi.csv` menyimpan perbandingan metrik lengkap.  
- `tabel_singkat_untuk_laporan.csv` menyimpan tabel ringkas untuk laporan.  
- `ringkasan_untuk_laporan.txt` memuat tabel serta selisih mAP50.  
- `asli_bersih_patience15/weights/best.pt` menyimpan bobot terbaik citra asli berdasarkan validation.  
- `asli_bersih_patience15/evaluasi/` menyimpan metrik test, evaluasi per FDI, prediksi per citra, dan confusion matrix.

## 2\. Keputusan review terakhir

- **Seluruh 252 citra dipertahankan.** Tidak ada citra yang dikeluarkan setelah konfirmasi koreksi terakhir.  
- **Sebanyak 37 nomor kelas diubah pada 25 citra.** Perubahan mengikuti review mamual dengan merujuk nomor baris label asli.  
- **Satu box dihapus**, yaitu IMG0043 baris \#13 yang sebelumnya berlabel FDI 55\. Dengan demikian, jumlah anotasi berkurang dari 3.343 menjadi 3.342.  
- **IMG0014:** baris \#6 diubah menjadi FDI 73\.  
- **IMG0121:** baris \#13 menjadi 62, \#14 menjadi 63, \#15 menjadi 64, dan \#16 menjadi 65\.  
- **IMG0172:** baris \#14 menjadi 74 dan \#15 menjadi 75\.  
- **IMG0224:** baris \#6 menjadi 65\.  
- **FDI berulang setelah koreksi berjumlah nol** berdasarkan audit pasangan citra dan kelas FDI. Log lengkap tersedia di `hasil_analisis/tabel/log_koreksi_FDI.csv`.  
- **Outlier tetap dipertahankan** karena dinilai mewakili kondisi nyata citra dan gigi susu. Nilai IQR dipakai untuk penandaan dan analisis sensitivitas, bukan penghapusan otomatis.  
- **Sebanyak 28 pasangan yang ditandai mirip oleh dHash telah direview.** Semuanya merupakan gambar berbeda dan dipertahankan. Pemeriksaan hash piksel tidak menemukan duplikat citra lintas split. Audit ini berfokus pada kebocoran citra.  
- **Umur yang tidak tersedia tidak diimputasi.** Data diberi keterangan tidak ada informasi umur. Umur yang diketahui dari nama file digunakan untuk deskripsi dan analisis bagian data yang memiliki informasi tersebut.  
- **Label dan citra mentah disimpan sebagai sumber.** Dataset hasil koreksi diekspor terpisah sehingga perubahan dapat ditelusuri kembali.

## 3\. Hasil angka yang digunakan

- **Dataset awal:** 252 citra dan 3.343 anotasi dalam 20 kelas FDI.  
- **Dataset sesudah koreksi:** 252 citra dan 3.342 anotasi, tanpa FDI berulang pada audit.  
- **Komposisi sumber:** 121 citra Paramita 2016–2018, 48 citra Paramita 2026, dan 83 citra Kaggle.  
- **Train sebelum augmentasi:** 175 citra dan 2.306 anotasi.  
- **Validation:** 50 citra dan 709 anotasi.  
- **Test:** 27 citra dan 327 anotasi.  
- **Train sesudah augmentasi:** 525 file dan 6.918 anotasi. Setiap citra train memiliki tiga versi total, yaitu HE dasar, brightness −15%, dan brightness \+15%.  
- **Total hasil pengolahan:** 602 file dan 7.954 anotasi, termasuk turunan augmentasi train. Jumlah citra sumber tetap 252\.  
- **Umur tepat diketahui pada 120 citra** dengan rentang 4–12 tahun. Sebanyak 132 citra tidak mencantumkan umur tepat. Rentang umur koleksi Paramita 2026 dicatat pada tingkat sumber, bukan diisikan sebagai umur pasti setiap file.  
- **Praktik IQR pada train:** k=1,5 menandai 12 citra, sedangkan k=3,0 menandai 3 citra. Median kenaikan kontras dan sharpness tetap positif pada kedua pengaturan. Dataset utama tidak berubah.  
- **Empat hipotesis EDA** dan **tiga analisis ketahanan** telah dijalankan. Unit analisis statistik adalah kelompok citra asal, bukan file augmentasi sebagai pengamatan tambahan.

### Hasil test model yang sudah dijalankan

| Kondisi | Patience | Epoch aktual | mAP50 | mAP50–95 | F1 micro | Kappa |
| :---- | ----: | ----: | ----: | ----: | ----: | ----: |
| YOLO11n citra asli bersih tanpa HE dan augmentasi | 15 | 38 | 75,01% | 39,72% | 74,62% | 0,6555 |
| Baseline YOLO11n dengan HE dan brightness | 15 | 59 | 78,89% | 42,71% | 76,05% | 0,6801 |
| Usulan YOLO11m dengan HE dan brightness | 15 | 69 | 90,34% | 53,81% | 86,99% | 0,7977 |

Pada perbandingan dua kondisi nano, paket pengolahan meningkatkan mAP50 sebesar **3,88 poin persen**, mAP50–95 sebesar **2,99 poin persen**, dan F1 micro sebesar **1,43 poin persen**. Pengaruh HE dan brightness tidak dipisahkan. Selisih ini merupakan hasil satu run pada split yang sama dan belum menunjukkan kestabilan antar-seed. Augmentasi menambah jumlah langkah training per epoch sehingga hasil dibaca sebagai perbandingan pipeline pada anggaran epoch yang sama.

## 4\. Sumber dataset dan isi folder

Data lokal berasal dari koleksi laboratorium Paramita yang bekerja sama dengan RSGM UNAIR. Data tersebut dilengkapi dengan dataset publik Kaggle.

1. **`DENTAL DATASET PARAMITA 2016-2018`** berisi koleksi radiograf campuran anak dan dewasa. Catatan awal mencantumkan 2.039 citra. Seleksi sesuai informasi usia yang tersedia dan penilaian citra menghasilkan 171 kandidat, kemudian 121 citra digunakan pada dataset final.  
2. **`Data terpilih dari Dental Paramita 11-12`** berisi 171 kandidat dari koleksi Paramita 2016–2018. Sebanyak 121 kandidat masuk dataset final dan 50 kandidat tidak terpilih. Folder ini dipakai untuk merekonstruksi alur seleksi awal.  
3. **`Dataset PARAMITA 2026`** berisi 69 citra koleksi 2026 dengan rentang usia sumber 11–12 tahun. Sebanyak 48 citra dipakai pada dataset final dengan awalan nama `sulung`. Umur tepat tidak tercantum pada setiap nama file.  
4. **`Childrens dental caries segmentation dataset_KAGEL`** berisi 100 radiograf publik Kaggle yang diperiksa sebagai kandidat. Sebanyak 83 citra dipakai pada dataset final dengan awalan nama `cate`.&nbsp;  
5. **`enumerasi_gigi_susu_252_label_asli.zip`** berisi folder `enumerasi gigi susu6-252-.v1i.yolov11`. Di dalamnya tersedia `train/images` berisi 252 radiograf, `train/labels` berisi pasangan label awal, serta `data.yaml` yang memetakan class\_id YOLO ke nomor FDI. Seluruh citra ekspor awal berada di folder train sebelum split penelitian diterapkan.

## 5\. Opsional Menyiapkan Drive dan menjalankan ulang Colab

Langkah berikut hanya diperlukan untuk reproduksi atau eksperimen baru. Output run yang digunakan pada laporan sudah tersedia. Menjalankan ulang training dapat menggunakan kuota GPU dan menghasilkan timestamp baru.

1. Buka folder proyek menggunakan akun yang akan digunakan menjalankan Colab.  
2. Jika folder berada di **Dibagikan kepada saya**, tambahkan **pintasan ke Drive Saya** pada tingkat utama. Pertahankan nama `1226800011_Aprilia_UjianEDA_Revisi`. Pastikan akun memiliki akses Editor agar hasil dapat disimpan. Link drive : [https\://drive.google.com/drive/folders/1ixSBScRA9kuaY-9KscP21o4kEbd7nrfu?usp=sharing](https://drive.google.com/drive/folders/1ixSBScRA9kuaY-9KscP21o4kEbd7nrfu?usp=sharing)&nbsp;  
3. Pastikan empat folder sumber dan ZIP dataset berlabel berada dalam folder proyek. Dataset tidak perlu diunggah ulang ketika berganti akun, selama pintasan dan akses tersedia.  
4. Buka **notebook 00** untuk melihat EDA awal. Pilih **Run all**, kemudian izinkan mount Drive. Notebook ini tidak memerlukan GPU untuk analisis citra.  
5. Buka **notebook 01**, lalu pilih **Run all**. Notebook menerapkan keputusan koreksi dan mengekspor dataset bersih. Tunggu sampai pesan selesai dan `RUN_COMPLETE.json` terbentuk.  
6. Jalankan **cell terakhir notebook 01** untuk praktik perubahan parameter IQR. Hasilnya disimpan di subfolder `tabel/` tanpa menghapus outlier dari dataset utama.  
7. Buka **notebook 02**, pilih **Runtime → Change runtime type → T4 GPU**, lalu **Run all**. Notebook membaca dataset bersih, menyalinnya ke penyimpanan lokal runtime, melatih model nano dan medium, memilih confidence dari validation, lalu mengevaluasi test.  
8. Buka **notebook 04**, pilih **GPU T4**, lalu **Run all**. Notebook ini memerlukan hasil baseline notebook 02 pada run `20261031_124203`. Model citra asli dilatih ulang dengan patience 15, sedangkan baseline dibaca dari hasil yang sudah selesai.  
9. Jangan mengubah seed, batch, input size, atau split pada satu kondisi saja ketika ingin membandingkan hasil. Maksimal epoch adalah 80 dan patience 15 pada seluruh model final yang dilaporkan.  
10. Setelah run selesai, simpan notebook dengan **Ctrl+S** agar output tabel dan pesan training tersimpan bersama notebook.  
11. Periksa folder hasil dan catat timestamp run. Tabel perbandingan di README dan laporan menggunakan run yang disebut pada bagian 1\. Run baru dapat membentuk folder timestamp lain.

## 6\. Konfigurasi dan batas interpretasi

- Model menggunakan bobot YOLO11 pralatih. Baseline dan pembanding citra asli memakai nano, sedangkan model usulan memakai medium.  
- Input model adalah 640 piksel dengan resize/letterbox bawaan YOLO. Batch 8, AdamW, learning rate awal 0,001, seed 42, maksimal 80 epoch, dan patience 15\.  
- Early stopping serta pemilihan checkpoint terbaik menggunakan validation, bukan test. Oleh sebab itu, epoch aktual dapat kurang dari 80\.  
- Train baseline mendapat auto-orient, HE, dan tiga versi brightness total. Validation dan test baseline hanya dipreproses tanpa augmentasi.  
- Citra asli pada notebook 04 tidak mendapat HE, brightness, atau auto-orient. Grayscale dan penyimpanan PNG dilakukan untuk menyiapkan format input yang konsisten. Koordinat label dikembalikan ke posisi piksel asli jika metadata orientasi memerlukannya.  
- Augmentasi bawaan tambahan seperti flip, mosaic, mixup, dan HSV dinonaktifkan. Nomor FDI memiliki makna posisi anatomis sehingga transformasi sisi tidak diterapkan sembarangan.  
- Empat skenario ablasi ber-patience 20 merupakan eksperimen terdahulu dan bukan perbandingan akhir yang digunakan dalam laporan ini. Gunakan notebook 04 versi patience 15\.

## 7\. Definisi evaluasi

| Istilah atau metrik | Definisi dan penggunaan |
| :---- | :---- |
| IoU pencocokan | Luas irisan box dibagi luas gabungannya. Prediksi dan gigi acuan dipasangkan satu-ke-satu pada IoU ≥ 0,5. |
| TP | Prediksi yang berhasil dipasangkan dan nomor FDI-nya benar. |
| FP | Prediksi berlebih atau prediksi dengan kelas FDI yang salah pada perhitungan per kelas. |
| FN | Gigi acuan yang tidak terdeteksi dengan nomor FDI yang benar. |
| Precision | TP / (TP \+ FP). Mengukur proporsi prediksi yang benar. |
| Recall | TP / (TP \+ FN). Mengukur proporsi gigi acuan yang berhasil dikenali. |
| F1 micro | 2TP / (2TP \+ FP \+ FN), dihitung dari total seluruh kelas. |
| F1 macro | Rata-rata F1 per kelas yang memiliki gigi acuan pada data evaluasi. |
| mAP@0,5 | Rata-rata average precision kelas pada IoU 0,5, dihitung sepanjang kurva precision–recall oleh Ultralytics. |
| mAP@0,5:0,95 | Rata-rata AP pada ambang IoU 0,5 hingga 0,95 dengan interval 0,05. Metrik ini menilai ketepatan lokalisasi lebih ketat. |
| Confusion matrix | Baris menunjukkan FDI acuan dan kolom menunjukkan prediksi, dengan kategori tambahan untuk objek tidak terdeteksi atau background. |
| Kappa unit gigi acuan | Kesepakatan nomor FDI setelah memperhitungkan kesepakatan karena peluang. Setiap gigi acuan menjadi satu unit dan gigi terlewat diberi kategori tidak terdeteksi. |
| Confidence | Ambang skor prediksi yang dipilih dari validation berdasarkan F1 micro. Ambang dikunci sebelum evaluasi test. |
| NMS IoU | Ambang 0,7 untuk menekan prediksi yang saling tumpang tindih. Ini berbeda dari IoU 0,5 untuk pencocokan evaluasi. |

Pencocokan lokasi tidak mensyaratkan kelas yang sama agar kesalahan nomor FDI tetap terlihat pada confusion matrix. Prediksi yang salah nomor dapat menjadi FP untuk kelas prediksi sekaligus FN untuk kelas acuan. Prediksi berlebih dicatat dalam precision dan F1. Pada Kappa, unit penilaian adalah gigi acuan sehingga prediksi berlebih dilaporkan terpisah sebagai FP.

Precision, recall, dan F1 pada tabel akhir dihitung oleh evaluator notebook pada confidence pilihan validation. Ringkasan bawaan Ultralytics dapat menampilkan precision dan recall pada titik kurva yang berbeda. Oleh karena itu, angka tersebut tidak dicampur. mAP berasal dari evaluasi Ultralytics sepanjang kurva, sedangkan F1 micro memakai ambang yang telah dikunci. Kappa dibaca bersama FP dan FN agar penilaian kesepakatan tidak menggantikan penilaian deteksi.

## 8\. Opsional Menjalankan ulang di komputer lokal

1. Siapkan Python, Jupyter, dan ruang penyimpanan untuk citra asli serta ekspor PNG. Untuk training model, gunakan komputer dengan NVIDIA GPU, driver, dan PyTorch CUDA yang sesuai. Notebook pemodelan tidak melanjutkan training pada CPU secara otomatis.

2. Unduh notebook 00, 01, 02, 04, empat folder sumber, serta ZIP dataset asli. Susun semuanya dalam folder lokal bernama `1226800011_Aprilia_UjianEDA_Revisi`. Contoh folder induk adalah `D:\EDA_Colab`, sehingga folder proyek berada di `D:\EDA_Colab\1226800011_Aprilia_UjianEDA_Revisi`.

3. Jika notebook 04 akan memakai baseline yang sudah selesai, unduh juga `hasil_analisis/pemodelan/20261031_124203/` beserta `baseline_metadata.json` dan `perbandingan_test.csv`. Alternatifnya, jalankan notebook 02 terlebih dahulu dan sesuaikan `BASELINE_RUN` ke timestamp hasil lokal tersebut.

4. Pasang dependensi notebook melalui terminal:

   ```powershell

   python -m pip install jupyter nbconvert ipykernel numpy pandas matplotlib pillow scipy pyyaml opencv-python-headless scikit-learn tzdata

   ```

5. Atur lokasi lokal melalui PowerShell sebelum membuka Jupyter:

   ```powershell

   $env:FDI_MYDRIVE = 'D:\EDA_Colab'

   $env:FDI_SCRATCH = 'D:\EDA_Colab\runtime'

   python -m jupyter lab

   ```

6. Buka notebook dari folder proyek dan jalankan berurutan sesuai bagian 5\. Variabel `FDI_MYDRIVE` menggantikan lokasi MyDrive pada pemeriksaan lokal, sedangkan `FDI_SCRATCH` menggantikan penyimpanan sementara `/content`.

7. Untuk eksekusi otomatis notebook 01 dari terminal, gunakan:

   ```powershell

   python -m jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=-1 'D:\EDA_Colab\1226800011_Aprilia_UjianEDA_Revisi\01_EDA_Penanganan_Hasil_Akhir.ipynb'

   ```

8. Untuk notebook model, pastikan `torch.cuda.is_available()` bernilai `True`. Gunakan notebook 02 dan 04 yang sama agar konfigurasi serta evaluator konsisten dengan Colab. Instalasi PyTorch GPU mengikuti kecocokan CUDA komputer yang digunakan.

9. Setelah selesai, periksa folder hasil dalam proyek lokal. File `.py` tersedia untuk audit dan pengembangan, tetapi jalur utama reproduksi adalah notebook mandiri. File inti `.py` versi awal dapat bergantung pada susunan hasil EDA historis sehingga tidak menggantikan langkah notebook tanpa penyesuaian path.

## Catatan PENTING

1. Angka dalam laporan akhir menggunakan run yang tercatat pada README ini. Jika training diulang, simpan run baru terpisah dan perbarui tabel laporan sesuai output aktual.
2. Folder hasil run masih dalam bentuk zip, kerena memiliki kebutuhan penyimpanan yang besar (jika ingin melihat data dialam folder tersebut silahkan di download kemudian di ekstraksi)

### Kelengkapan yang disertakan

- **Dokumen:** laporan PDF, dokumen Word yang dapat diedit, dan README.  
- **Kode yang sudah dijalankan:** empat notebook utama dengan output cell yang tersimpan.  
- **Data sumber:** empat folder radiograf dan kandidat seleksi, serta ZIP citra dan label YOLO awal.  
- **Bukti sebelum penanganan:** seluruh hasil EDA awal pada folder `hasil_EDA_awal_sebelum_UTS/`.  
- **Bukti setelah penanganan:** dataset terkoreksi, tabel, grafik, overlay, log keputusan, dan manifest pada `hasil_analisis/`.  
- **Bukti pemodelan:** folder training, checkpoint model yang tersedia, tabel test, evaluasi per FDI, dan confusion matrix dari notebook 02\.  
- **Bukti perbandingan pengolahan:** folder `hasil_perbandingan_dua_YOLO11n/20261031_173820/` dengan hasil citra asli dan pembanding baseline.

&nbsp;
