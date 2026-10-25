# Refleksi Kelompok

## Pembagian Pekerjaan

| Bagian | Penanggung jawab utama | Pemeriksa silang |
| --- | --- | --- |
| Analisis masalah, IPO, variabel | Khoirun Ni'mah | Nur Adyatma Pratama |
| Modul A (tagihan per pelanggan): algoritma, pseudocode, flowchart, kode, uji | Khoirun Ni'mah | Nur Adyatma Pratama |
| Modul B (rekapitulasi): algoritma, pseudocode, flowchart, kode, uji | Nur Adyatma Pratama | Khoirun Ni'mah |
| Integrasi, trace table, daftar kesalahan | Bersama | Bersama |
| GitHub Pages, refleksi, pernyataan AI | Bersama | Bersama |

## Kontribusi Anggota

- **Nur Adyatma Pratama (322610007)**: Modul A, analisis masalah, dan pemeriksaan Modul B.
- **Nur Adyatma Pratama (322610016)**: Modul B, rekapitulasi tanpa array, dan pemeriksaan Modul A.
- Bukti kontribusi: riwayat commit dan halaman Contributors di GitHub.

## Bagian Tersulit

1. Menentukan **urutan pembulatan, berat minimum, dan pengecekan diskon**, karena batas diskon ternyata bergantung pada berat tagihan (bukan berat yang diketik).
2. Membuat validasi input yang tidak membuat program berhenti, terutama saat pengguna mengetik huruf pada kolom angka.
3. Menentukan **transaksi terbesar tanpa array**, yaitu dengan menyimpan nilai dan nama terbesar yang diperbarui setiap iterasi.

## Kesalahan dan Perbaikan

Ringkasan: kesalahan pada data harapan skenario 12 dan beberapa jebakan pembacaan input (`cin` dan `getline`). Rincian lengkap ada di `Integrasi/daftar_kesalahan_dan_perbaikan.md`.

## Pengetahuan yang Diperoleh

- Menerjemahkan aturan bisnis menjadi percabangan bersyarat (`&&`, `!`) dan memastikan batas nilai (5 kg, 10 kg) diuji pada nilai di bawah, tepat di batas, dan di atas.
- Memakai variabel akumulator untuk rekapitulasi tanpa array.
- Membuat trace table untuk memeriksa nilai variabel tiap iterasi.
- Memakai Git secara bertahap dengan pesan commit yang bermakna.

## Rencana Pengembangan untuk UAS

- Memakai **array** untuk menyimpan seluruh transaksi sehingga bisa diurutkan dan dicari.
- Memakai **function** agar blok input dan validasi tidak ditulis berulang.
- Menyimpan data transaksi ke **file** agar tidak hilang setelah program ditutup.
- Menambahkan menu harga dan diskon yang bisa diubah tanpa mengubah kode.