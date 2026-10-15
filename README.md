# Pemodelan pada Pertumbuhan Ekonomi Per Sektor Lapangan Usaha dengan Data Google Trends

## Identitas

- **Nama:**  Aulia Zulfa Kurniawan
- **NIM:** 222212525
- **Program Studi:** DIV Komputasi Statistik
- **Institusi:** Politeknik Statistika STIS
- **Topik penelitian:** Pemodelan pada Pertumbuhan Ekonomi Per Sektor Lapangan Usaha dengan Data Google Trends.


## Deskripsi Proyek

Repositori ini berisi kode pemodelan dan aplikasi dashboard *Monthly Tracker* untuk menghasilkan estimasi pertumbuhan PDB (*year-on-year*/y-o-y) pada 17 sektor ekonomi. Prediktor yang digunakan dalam kode meliputi indikator Google Trends serta variabel statistik resmi, yaitu inflasi, JISDOR, impor, dan ekspor.

Kode pemodelan membandingkan beberapa skenario prediktor (S1–S7) dan melakukan pemodelan SVR dengan pencarian hiperparameter menggunakan `GridSearchCV` serta `TimeSeriesSplit`. Dashboard Streamlit menggunakan model yang telah disimpan untuk memproses data input bulanan dan menampilkan hasil tracker.

## Struktur File

Struktur yang disarankan untuk repositori GitHub:

```text
.
├── README.md
├── kode pemodelan.py
├── kode artefak.py
├── data/
│   └── data_pertumbuhan.xlsx
├── model/
│   └── model_terbaik.joblib
└── df_tracker_final.xlsx
```

Keterangan file yang tersedia saat ini:

| File | Fungsi |
|---|---|
| `kode pemodelan.py` | Kode analisis dan pemodelan: membaca data, memisahkan prediktor dan target 17 sektor, menyiapkan skenario fitur, melakukan pemodelan SVR, serta analisis/visualisasi hasil. |
| `kode artefak.py` | Aplikasi dashboard berbasis Streamlit yang menyediakan halaman Beranda, Visualisasi, dan Monthly Tracker. |
| `.data fix pertumbuhan.xlsx` | Data kerja pemodelan. Kode membaca sheet bernama `yoy`. |
| `model_terbaik(2).joblib` | Berkas model tersimpan. Untuk digunakan langsung oleh aplikasi, sesuaikan namanya menjadi `model_terbaik.joblib` atau ubah konfigurasi `MODEL_PATH` pada kode aplikasi. |
| `df_tracker_final.xlsx` | Berkas data tracker yang dibaca oleh halaman Visualisasi. Berkas ini belum termasuk dalam file yang disediakan saat README dibuat. |

> **Catatan:** Struktur di atas adalah susunan yang disarankan, bukan klaim bahwa semua folder tersebut sudah ada. Jika memakai folder `data/` atau `model/`, perbarui path pada kedua kode agar sesuai dengan struktur repositori.

## Sektor PDB

Kode menggunakan 17 kode sektor berikut:

| Kode | Sektor |
|---|---|
| A | Pertanian, Kehutanan, dan Perikanan |
| B | Pertambangan dan Penggalian |
| C | Industri Pengolahan |
| D | Pengadaan Listrik dan Gas |
| E | Pengadaan Air, Pengelolaan Sampah, Limbah dan Daur Ulang |
| F | Konstruksi |
| G | Perdagangan Besar dan Eceran |
| H | Transportasi dan Pergudangan |
| I | Penyediaan Akomodasi dan Makan Minum |
| J | Informasi dan Komunikasi |
| K | Jasa Keuangan dan Asuransi |
| L | Real Estat |
| MN | Jasa Perusahaan |
| O | Administrasi Pemerintahan |
| P | Jasa Pendidikan |
| Q | Jasa Kesehatan dan Kegiatan Sosial |
| RSTU | Jasa Lainnya |

## Kebutuhan Pustaka

Pustaka yang diimpor dalam kode mencakup:

- `pandas`
- `numpy`
- `scikit-learn`
- `openpyxl`
- `joblib`
- `matplotlib`
- `plotly`
- `streamlit`
- `scipy`
- `boruta` (digunakan pada bagian seleksi fitur dalam kode pemodelan)

Instalasi awal dapat dilakukan dengan:

```bash
pip install pandas numpy scikit-learn openpyxl joblib matplotlib plotly streamlit scipy boruta
```

Versi pustaka yang kompatibel dapat berbeda tergantung lingkungan eksekusi. Untuk reproduksibilitas, disarankan mencatat versi pustaka yang benar-benar digunakan dalam berkas `requirements.txt`.

## Menjalankan Dashboard

1. Pastikan berkas model tersedia dan path pada `kode artefak.py` sudah sesuai.
2. Pastikan `df_tracker_final.xlsx` tersedia jika halaman **Visualisasi** ingin digunakan. Berkas ini dibaca saat aplikasi dimulai.
3. Pasang pustaka yang diperlukan.
4. Jalankan perintah berikut dari direktori proyek:

   ```bash
   streamlit run "kode artefak.py"
   ```

5. Pada halaman **Monthly Tracker**, unduh template Excel dari aplikasi, isi data sesuai nama kolom dan format pengolahan yang diminta, lalu unggah kembali untuk menghasilkan prediksi.

### Format input Monthly Tracker

Template yang dibuat aplikasi memuat kolom `Periode`, empat variabel statistik resmi (`inflasi`, `jisdor`, `import`, `export`), dan topik Google Trends yang didefinisikan dalam kode aplikasi. Nilai input harus mengikuti format pengolahan yang dijelaskan pada aplikasi, bukan langsung menggunakan nilai mentah. Periksa kembali petunjuk di dashboard sebelum melakukan prediksi.

## Catatan Penting Sebelum Mengunggah ke GitHub

- **Periksa izin publikasi data.** Pastikan file Excel, hasil tracker, dan model boleh dibagikan. Jika tidak, keluarkan file tersebut dari repositori dan sediakan petunjuk untuk memperoleh atau menyiapkannya.
- **Hindari file berukuran besar atau sensitif.** Gunakan `.gitignore` untuk mengecualikan data/model yang tidak boleh dipublikasikan.
- **Samakan nama dan lokasi file.** Aplikasi saat ini mencari `model_terbaik.joblib` dan `df_tracker_final.xlsx` pada direktori yang sama dengan file aplikasi. Jika lokasi file diubah, perbarui path dalam kode.
- **Periksa jumlah fitur Google Trends.** Daftar fitur pada aplikasi memiliki pemeriksaan jumlah fitur. Pastikan daftar kolom di data input cocok dengan fitur yang dibutuhkan model tersimpan.
- **Model tersimpan harus cocok dengan kode dan pustaka.** Berkas `.joblib` dapat bergantung pada versi scikit-learn dan struktur objek yang digunakan saat pelatihan. Gunakan lingkungan yang sesuai dengan proses pelatihan.
- **Jangan menganggap hasil sebagai data PDB resmi.** Keluaran dashboard adalah estimasi *nowcasting* dari model penelitian.

## Lisensi dan Sitasi

Tambahkan informasi lisensi apabila repositori akan dibagikan secara publik. Jika kode atau metode mengadaptasi penelitian/pustaka pihak lain, cantumkan referensi yang relevan pada bagian ini.
