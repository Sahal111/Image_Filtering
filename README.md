<div align="center">

# Operasi Dasar Citra Digital
### Gaussian Blur & Median Filter

Membandingkan dua teknik *image filtering* untuk mengurangi salt-and-pepper noise pada citra digital.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-cv2-5C3EE8?logo=opencv&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

</div>

---

## Tentang Proyek

Proyek tugas mata kuliah **Pengolahan Citra Digital**. Citra sering terganggu noise akibat sensor, pencahayaan, atau transmisi data. Notebook ini menambahkan *salt-and-pepper noise* pada citra, menyaringnya dengan **Gaussian Blur** dan **Median Filter**, lalu membandingkan hasilnya secara visual dan dengan metrik MSE/PSNR.

Metode *Image Colorization* tidak digunakan.

## Fitur Utama

- Membaca gambar sendiri, dengan pemeriksaan jika gagal dibaca (gambar contoh dipakai bila file tidak ada)
- Konversi RGB ke grayscale
- Penambahan salt-and-pepper noise dengan tingkat noise dan seed yang dapat diatur
- Gaussian Blur dan Median Filter dengan OpenCV
- Visualisasi perbandingan empat citra dalam satu figure
- Evaluasi MSE dan PSNR terhadap citra grayscale asli yang bersih
- Eksperimen kernel 3×3, 5×5, dan 7×7

## Preview Hasil

![Perbandingan hasil](docs/hasil_perbandingan.png)

*Gambar diambil dari output notebook dengan gambar contoh bawaan, noise 5%, kernel 5×5. Urutan: asli, ber-noise, Gaussian Blur, Median Filter.*

## Teknologi

| Library | Fungsi |
|---|---|
| `opencv-python` | Membaca gambar, grayscale, Gaussian Blur, Median Filter |
| `numpy` | Operasi array piksel, pembuatan noise, hitung MSE/PSNR |
| `matplotlib` | Menampilkan gambar dan grafik |
| `pandas` | Tabel hasil evaluasi |
| Jupyter Notebook | Lingkungan menjalankan dan mendokumentasikan kode |

## Struktur Repository

```text
.
├── Operasi_Dasar_Citra_Digital_Gaussian_Median.ipynb   # notebook utama
├── docs/
│   └── hasil_perbandingan.png                          # gambar preview
├── build_nb.py                                         # skrip pembuat notebook (versi awal)
├── build_nb2.py                                        # skrip pembuat notebook (versi ringkas)
└── README.md
```

## Instalasi dan Menjalankan

**Jupyter Notebook (lokal)**

```bash
git clone https://github.com/<username>/<nama-repository>.git
cd <nama-repository>

python -m venv venv                  # opsional
source venv/bin/activate             # Windows: venv\Scripts\activate

pip install opencv-python numpy matplotlib pandas notebook
jupyter notebook Operasi_Dasar_Citra_Digital_Gaussian_Median.ipynb
```

Lalu pilih **Run → Run All Cells**.

**Google Colab**

Upload file `.ipynb` ke [Google Colab](https://colab.research.google.com/), lalu pilih **Runtime → Run all**. Library yang dibutuhkan sudah tersedia di Colab.

**Memakai gambar sendiri**

Letakkan file JPG/PNG di folder yang sama dengan notebook, lalu ubah variabel di cell pemuatan gambar:

```python
NAMA_FILE_GAMBAR = "gambar_input.jpg"
```

Parameter lain yang dapat diubah: `TINGKAT_NOISE`, `SEED_ACAK`, `UKURAN_KERNEL`.

## Metode Pengolahan Citra

| | Gaussian Blur | Median Filter |
|---|---|---|
| Jenis | Linear | Non-linear |
| Cara kerja | Rata-rata berbobot; piksel dekat pusat kernel berbobot lebih besar | Nilai di jendela diurutkan, nilai tengah dipakai |
| Terhadap noise ekstrem (0/255) | Diredam dan menyebar ke tetangga | Terbuang karena berada di ujung urutan |
| Fungsi OpenCV | `cv2.GaussianBlur` | `cv2.medianBlur` |

Kernel harus berukuran ganjil. Kernel lebih besar menghaluskan lebih kuat, tetapi detail halus lebih mudah hilang.

## Evaluasi

Kedua hasil dibandingkan dengan citra grayscale asli yang bersih.

- **MSE**: rata-rata kuadrat selisih nilai piksel. Makin kecil, makin mirip.
- **PSNR**: `10·log10(255² / MSE)` dalam dB. Makin besar, makin mirip.

Kedua metrik hanya mengukur selisih angka piksel dan tidak selalu sejalan dengan kesan visual.

## Hasil dan Kesimpulan

Semua angka dihitung langsung oleh notebook. Cuplikan dari satu kali eksekusi dengan **gambar contoh bawaan, noise 5%, seed 42**:

| Citra | MSE | PSNR (dB) |
|---|---|---|
| Ber-noise (tanpa filter) | 1022,68 | 18,03 |
| Gaussian Blur 5×5 | 264,47 | 23,91 |
| Median Filter 5×5 | 166,86 | 25,91 |

Pada gambar dan pengaturan tersebut, Median Filter memberi PSNR lebih tinggi di kernel 3×3, 5×5, dan 7×7. Hasil ini belum tentu berlaku untuk gambar, tingkat noise, atau seed lain. Jalankan ulang notebook dengan data Anda sendiri untuk menarik kesimpulan.

## Pengembangan Selanjutnya

- Menguji jenis noise lain, misalnya Gaussian noise
- Menguji lebih banyak ukuran kernel dan tingkat noise
- Memakai beberapa gambar dengan tekstur berbeda
- Menambahkan metrik SSIM
- Membandingkan dengan filter lain, misalnya bilateral filter

## Referensi

- [OpenCV: Smoothing Images](https://docs.opencv.org/4.x/d4/d13/tutorial_py_filtering.html)
- [OpenCV: Image Filtering](https://docs.opencv.org/4.x/d4/d86/group__imgproc__filter.html)
- [NumPy Documentation](https://numpy.org/doc/stable/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [Jupyter Notebook Documentation](https://jupyter-notebook.readthedocs.io/)

---

<div align="center">

Dibuat sebagai tugas mata kuliah Pengolahan Citra Digital.

| | |
|---|---|
| Nama | [Isi Nama] |
| NIM | [Isi NIM] |
| Program Studi | [Isi Program Studi] |
| Dosen | [Isi Nama Dosen] |
| Tahun Akademik | [Isi Tahun Akademik] |

</div>
