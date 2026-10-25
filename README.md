# Proyek UTS Algoritma dan Pengantar Pemrograman (SSI1144)
**Program Studi Sistem Informasi, Fakultas Teknologi dan Desain, Universitas Ma Chung**

## Identitas Proyek

- **Mata kuliah:** Algoritma dan Pengantar Pemrograman (SSI1144)
- **Studi kasus 02:** Sistem Perhitungan Biaya Laundry
- **Bahasa:** C++ (konsol)
- **Repository:** https://github.com/GANTI-USERNAME/laundry_alpro
- **GitHub Pages:** https://GANTI-USERNAME.github.io/laundry_alpro/

| No | Nama | NIM | Tanggung jawab utama |
|:-:|---|:-:|---|
| 1 | Nur Adyatma Pratama | 322610016 | Modul A (proses utama) |
| 2 | Khoirun Ni'mah | 322610007 | Modul B (rekapitulasi) |

## Deskripsi

Program menghitung tagihan laundry per pelanggan dan merekap pendapatan harian.

| Ketentuan | Nilai |
|---|---|
| Tarif | Reguler Rp7.000/kg, Express Rp11.000/kg |
| Berat | Dibulatkan ke atas; kurang dari 2 kg dihitung 2 kg |
| Diskon | Anggota >= 5 kg: 5%. Nonanggota >= 10 kg: 3% |
| Layanan antar | Rp8.000, tidak didiskon |

Rekapitulasi: jumlah pelanggan reguler dan express, jumlah anggota, total berat, total diskon, total biaya antar, total pendapatan, dan transaksi terbesar.

## Struktur Direktori

```text
laundry_alpro/
├── README.md
├── beranda.md
├── index.html                      # halaman GitHub Pages
├── .gitignore
├── Analisis-Masalah/analisis_masalah.md
├── Modul-A/                        # Nur Adyatma Pratama
│   ├── algoritma_deskriptif.md  pseudocode.md  flowchart.md
│   ├── modul_a.cpp
│   ├── source_code_dan_penjelasan.md  hasil_eksekusi_dan_pengujian.md
│   └── gambar/
├── Modul-B/                        # Khoirun Ni'mah
│   └── (isi sama, dengan modul_b.cpp)
├── Integrasi/
│   ├── program_terintegrasi.cpp
│   ├── proses_integrasi.md  pseudocode.md  flowchart.md
│   ├── source_code_dan_penjelasan.md  hasil_eksekusi_dan_pengujian.md
│   ├── daftar_kesalahan_dan_perbaikan.md
│   └── gambar/
└── Refleksi/
    ├── refleksi.md
    └── pernyataan_penggunaan_ai.md
```

## Cara Menjalankan

Butuh compiler C++ (g++/MinGW/Clang).

```bash
git clone https://github.com/GANTI-USERNAME/laundry_alpro.git
cd laundry_alpro/Integrasi
g++ program_terintegrasi.cpp -o program_terintegrasi
./program_terintegrasi          # Windows: program_terintegrasi.exe
```

Modul mandiri: `cd Modul-A && g++ modul_a.cpp -o modul_a` atau `cd Modul-B && g++ modul_b.cpp -o modul_b`.

## Contoh Input dan Output

Input: `Sari`, `4.2`, `1`, `y`, `y`, lalu `t` untuk berhenti.

```text
>>> RINCIAN TAGIHAN <<<
Pelanggan          : Sari (Anggota)
Layanan            : Reguler @ Rp7000/kg
Berat input        : 4.2 kg
Berat tagihan      : 5 kg
Biaya layanan      : Rp35000
Diskon             : Rp1750 (5%)
Biaya antar        : Rp8000
TOTAL BAYAR        : Rp41250
```

## Validasi Input

Program menolak nama kosong, berat bukan angka / nol / negatif / lebih dari 100 kg, jenis layanan selain 1 atau 2, dan jawaban selain y atau t. Setiap penolakan memunculkan pesan dan meminta input ulang tanpa menghentikan program.

## Hasil Pengujian

12 skenario diuji pada Modul A, Modul B, dan program terintegrasi: **semuanya berhasil**. Detail ada di `hasil_eksekusi_dan_pengujian.md` pada tiap folder.
