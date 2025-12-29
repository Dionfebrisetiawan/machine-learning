# machine-learning

# Laporan Proyek Machine Learning - Dion Febri Setiawan

## Project Overview
  Meningkatnya jumlah koleksi buku pada platform digital menyebabkan pengguna mengalami kesulitan dalam menemukan buku yang sesuai dengan minat dan preferensinya. Kondisi ini dikenal sebagai information overload, di mana banyaknya pilihan justru menurunkan efektivitas pencarian dan pengalaman pengguna. Oleh karena itu, diperlukan sebuah sistem yang mampu menyajikan rekomendasi buku secara personal dan relevan.

  Proyek ini bertujuan untuk membangun sistem rekomendasi buku yang dapat menghasilkan top-N recommendation bagi pengguna berdasarkan data interaksi historis dan informasi konten buku. Sistem rekomendasi diharapkan dapat membantu pengguna menemukan buku yang sesuai dengan preferensinya serta meningkatkan keterlibatan (engagement) pengguna pada platform.

  Pendekatan yang digunakan dalam proyek ini adalah Content-Based Filtering dan Collaborative Filtering. Content-Based Filtering memanfaatkan karakteristik buku untuk merekomendasikan item yang serupa dengan preferensi pengguna, sedangkan Collaborative Filtering memanfaatkan pola interaksi pengguna lain yang memiliki kesamaan preferensi. Kombinasi kedua pendekatan ini dipilih karena telah terbukti efektif dalam meningkatkan kualitas rekomendasi pada berbagai penelitian sebelumnya.

  Dengan membangun sistem rekomendasi ini, proyek diharapkan mampu memberikan solusi terhadap permasalahan information overload serta menjadi implementasi nyata penerapan sistem rekomendasi dalam domain literasi digital.

## Business Understanding
Meningkatnya jumlah koleksi buku pada platform digital membuat pengguna kesulitan menemukan buku yang sesuai dengan minat dan preferensinya. Proses pencarian manual atau berbasis popularitas saja sering kali tidak mampu memberikan rekomendasi yang relevan secara personal. Akibatnya, pengguna berpotensi melewatkan buku yang sebenarnya sesuai dengan kebutuhannya, sementara platform kehilangan peluang untuk meningkatkan keterlibatan dan kepuasan pengguna.

Selain itu, perbedaan preferensi antar pengguna menyebabkan pendekatan rekomendasi yang bersifat umum menjadi kurang efektif. Oleh karena itu, diperlukan sebuah sistem yang mampu memahami karakteristik buku serta pola interaksi pengguna untuk menghasilkan rekomendasi yang lebih tepat sasaran.

### Problem Statements
- Bagaimana cara mempermudah pengguna menemukan buku yang relevan dengan minat dan preferensinya di tengah banyaknya koleksi buku yang tersedia pada platform digital?

- Bagaimana membangun sistem rekomendasi buku yang mampu memberikan rekomendasi secara personal dan tidak hanya bergantung pada popularitas buku?

- Bagaimana memanfaatkan data interaksi historis pengguna dan informasi konten buku untuk menghasilkan rekomendasi buku yang relevan dan akurat?

### Goals
- Mengembangkan sistem rekomendasi buku yang mampu menghasilkan top-N recommendation untuk membantu pengguna menemukan buku yang relevan dengan minat dan preferensinya secara lebih efektif.
- Membangun sistem rekomendasi buku yang bersifat personal dengan memanfaatkan preferensi dan pola interaksi pengguna, sehingga rekomendasi yang diberikan tidak hanya berdasarkan tingkat popularitas buku.
- Mengimplementasikan pendekatan Content-Based Filtering dan Collaborative Filtering dengan memanfaatkan data interaksi historis pengguna dan informasi konten buku guna menghasilkan rekomendasi yang lebih akurat dan relevan.

**Rubrik/Kriteria Tambahan (Opsional)**:
  ### Solution statements
  - Content-Based Filtering : Pendekatan ini merekomendasikan buku berdasarkan kemiripan karakteristik konten buku dengan preferensi pengguna, sehingga pengguna mendapatkan rekomendasi yang sesuai dengan minat bacaan mereka.
- Collaborative Filtering : Pendekatan ini merekomendasikan buku berdasarkan pola interaksi pengguna lain yang memiliki preferensi serupa, dengan memanfaatkan data interaksi historis pengguna dan buku.

### 1. **Sumber Data**

Data Understanding

Dataset yang digunakan dalam proyek ini adalah dataset buku (Books.csv) yang berisi informasi deskriptif mengenai buku beserta statistik penilaian pengguna. Dataset ini digunakan sebagai dasar untuk membangun sistem rekomendasi buku dengan pendekatan Content-Based Filtering dan Collaborative Filtering.

Dataset terdiri dari ribuan entri buku, di mana setiap baris merepresentasikan satu buku unik. Secara umum, kondisi data cukup baik, namun terdapat beberapa tantangan umum seperti ketidakseimbangan jumlah rating antar buku dan kemungkinan nilai kosong pada beberapa kolom. Dataset ini tidak memiliki label klasifikasi, melainkan data preferensi pengguna yang dimanfaatkan untuk menghasilkan rekomendasi.

Kaggle : https://www.google.com/url?q=https%3A%2F%2Fwww.kaggle.com%2Fdatasets%2Farashnic%2Fbook-recommendation-dataset

### Variabel pada Books dataset adalah sebagai berikut :
- ISBN : Merupakan kode identifikasi unik untuk setiap buku (International Standard Book Number).

- Book-Title : Merupakan judul buku.

- Book-Author : Merupakan nama penulis buku.

- Year-Of-Publication : Merupakan tahun terbit buku.

- Publisher : Merupakan nama penerbit buku.

- Image-URL-S : Merupakan tautan gambar sampul buku berukuran kecil (small).

- Image-URL-M : Merupakan tautan gambar sampul buku berukuran sedang (medium).

- Image-URL-L : Merupakan tautan gambar sampul buku berukuran besar (large).

### 2. **Struktur Data**

Dataset ini berisi data pribadi peserta asuransi beserta dengan biaya tagihan asuransinya. Berdasarkan pengamatan dataset tersebut memiliki 271360 baris dan 8 kolom data.


**Rubrik/Kriteria Tambahan (Opsional)**:

A. Konversi dan pembersihan tahun publikasi

Kolom Year-Of-Publication dikonversi ke format numerik, kemudian nilai yang tidak valid atau berada di luar rentang wajar dihapus dari dataset.

B. Penanganan nilai kosong (missing values)

Baris data yang memiliki nilai kosong pada kolom penting seperti Book-Title, Book-Author, dan Publisher dihapus untuk menjaga konsistensi data.

C. Penghapusan fitur yang tidak relevan

Kolom Image-URL-S, Image-URL-M, dan Image-URL-L dihapus karena tidak digunakan dalam proses pemodelan sistem rekomendasi.

D. Seleksi fitur utama

Fitur ISBN, Book-Title, Book-Author, Publisher, dan Year-Of-Publication dipilih sebagai representasi utama buku untuk tahap pemodelan.

## Modeling
Pada tahap ini, sistem rekomendasi dibangun untuk menghasilkan rekomendasi buku yang relevan bagi pengguna. Dua pendekatan digunakan, yaitu Content-Based Filtering dan Collaborative Filtering, guna membandingkan performa dan karakteristik masing-masing metode.

### Pemilihan modal

1. Content-Based Filtering

Pendekatan Content-Based Filtering merekomendasikan buku berdasarkan kemiripan karakteristik konten buku. Fitur yang digunakan meliputi judul buku, penulis, penerbit, dan tahun publikasi. Kemiripan antar buku dihitung menggunakan Cosine Similarity, sehingga sistem dapat merekomendasikan buku dengan konten yang paling mirip dengan buku referensi.

Kelebihan:

- Tidak bergantung pada data pengguna lain

- Mampu memberikan rekomendasi untuk pengguna baru (cold-start user)

- Rekomendasi bersifat personal dan konsisten dengan minat pengguna

Kekurangan:

- Rekomendasi cenderung terbatas pada buku dengan karakteristik yang mirip

- Kurang mampu memberikan rekomendasi yang beragam


2. Collaborative Filtering

Pendekatan Collaborative Filtering merekomendasikan buku berdasarkan pola interaksi antar pengguna. Sistem memanfaatkan kesamaan preferensi pengguna untuk merekomendasikan buku yang disukai oleh pengguna lain dengan pola serupa.

Kelebihan:

- Mampu menangkap preferensi kolektif pengguna

- Rekomendasi lebih variatif dan tidak terbatas pada kemiripan konten

Kekurangan:

- Membutuhkan data interaksi pengguna dalam jumlah cukup

- Rentan terhadap masalah cold-start pada pengguna baru atau buku baru.

## Evaluation

Hasil proses TF-IDF menghasilkan matriks dengan dimensi (266.716 × 115.578), yang menunjukkan bahwa terdapat 266.716 buku dan 115.578 jumlah fitur kata unik yang terbentuk setelah proses TF-IDF. Matriks ini bersifat sparse dan mencerminkan tingginya keragaman konten buku dalam dataset. Representasi ini menjadi dasar dalam penghitungan kemiripan antar buku menggunakan metode Cosine Similarity pada tahap berikutnya.
Berdasarkan hasil evaluasi, sistem rekomendasi mampu menghasilkan daftar Top-N buku dengan tingkat kemiripan konten yang tinggi terhadap buku acuan. Buku-buku yang direkomendasikan menunjukkan kesamaan pada atribut utama, seperti penulis, tema, dan penerbit.

Nilai Cosine Similarity yang tinggi pada buku-buku teratas mengindikasikan bahwa matriks TF-IDF berhasil merepresentasikan karakteristik konten buku secara efektif. Sementara itu, hasil Precision@N menunjukkan bahwa sebagian besar rekomendasi yang diberikan dapat dianggap relevan, sehingga sistem memiliki tingkat presisi yang baik dalam menyajikan rekomendasi.
