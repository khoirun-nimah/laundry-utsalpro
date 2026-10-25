# Analisis Masalah: Studi Kasus 02, Sistem Perhitungan Biaya Laundry

## Latar Belakang dan Rumusan Masalah

Usaha laundry menghitung tagihan pelanggan berdasarkan berat cucian, jenis layanan, status keanggotaan, dan layanan antar. Aturan pembulatan berat, berat minimum, diskon bersyarat, dan biaya antar yang tidak terdiskon membuat perhitungan manual mudah salah, terutama saat pelanggan banyak. Rekapitulasi pendapatan harian juga memerlukan penjumlahan banyak data.

Rumusan masalah:
1. Bagaimana menghitung tagihan satu pelanggan sesuai aturan tarif, pembulatan, diskon, dan biaya antar?
2. Bagaimana memproses banyak pelanggan berulang dan merekap hasilnya tanpa menyimpan seluruh data dalam array?
3. Bagaimana memastikan program tetap berjalan ketika input tidak valid?

## Tujuan dan Pengguna Program

- **Tujuan:** menghasilkan rincian tagihan yang akurat dan transparan, serta rekapitulasi harian.
- **Pengguna:** kasir atau pemilik usaha laundry yang menjalankan program di terminal.

## Ketentuan dan Batasan

- Tarif: Reguler Rp7.000/kg, Express Rp11.000/kg.
- Berat dibulatkan ke atas; berat kurang dari 2 kg tetap dihitung 2 kg.
- Diskon: anggota dengan berat minimal 5 kg mendapat 5%; nonanggota dengan berat minimal 10 kg mendapat 3%.
- Layanan antar Rp8.000 dan tidak termasuk komponen yang didiskon.
- Program berjalan di konsol, memakai C++, tanpa array, tanpa function/class, tanpa library eksternal.
- Program memproses lebih dari satu pelanggan lewat perulangan dan menyediakan pilihan lanjut atau berhenti.
- Input tidak valid ditolak dan program meminta input ulang.

## Asumsi Desain

Ketentuan tidak menjelaskan beberapa hal, sehingga kelompok menetapkan asumsi berikut dan menyatakannya secara eksplisit:

1. Ambang diskon (5 kg dan 10 kg) dibandingkan dengan **berat tagihan** (setelah pembulatan dan berat minimum). Contoh: 4,2 kg ditagih 5 kg sehingga anggota mendapat diskon.
2. Diskon dihitung dari **biaya layanan** saja.
3. Berat maksimum per transaksi adalah **100 kg** (kapasitas), agar ada batas atas untuk validasi dan pengujian.
4. "Total berat cucian" pada rekap memakai **berat tagihan**.
5. Semua nilai uang berupa bilangan bulat; diskon selalu bulat karena tarif kelipatan Rp1.000.
6. Jika dua transaksi sama besar, transaksi terbesar adalah yang **pertama** dimasukkan.

## Input-Process-Output

| Input | Proses | Output |
|---|---|---|
| Nama pelanggan | Validasi tidak kosong | Rincian tagihan per pelanggan: nama, layanan, tarif, berat input, berat tagihan, biaya layanan, diskon (nominal dan persen), biaya antar, total bayar |
| Berat cucian (kg) | Validasi angka, > 0, <= 100; bulatkan ke atas; minimum 2 kg | |
| Jenis layanan (1/2) | Validasi 1 atau 2; tentukan tarif | |
| Status anggota (y/t) | Validasi y/t; tentukan persen diskon (5%, 3%, atau 0%) | |
| Layanan antar (y/t) | Validasi y/t; tentukan biaya antar | |
| Pilihan lanjut (y/t) | Perulangan pelanggan; akumulasi: jumlah per jenis, anggota, berat, diskon, antar, pendapatan, transaksi terbesar | Rekapitulasi harian setelah perulangan berakhir |

## Variabel dan Tipe Data

| Variabel | Tipe | Nilai awal | Kegunaan |
|---|---|---|---|
| `namaPelanggan` | string | - | Nama pelanggan |
| `jawaban` | string | - | Menampung jawaban y/t |
| `beratInput` | double | - | Berat cucian yang diketik (boleh pecahan) |
| `jenisLayanan` | int | - | 1 = Reguler, 2 = Express |
| `anggota` | bool | - | Status keanggotaan |
| `layananAntar` | bool | - | Status layanan antar |
| `beratTagihan` | int | - | Berat setelah pembulatan dan minimum |
| `tarif` | int | - | Tarif per kg sesuai layanan |
| `namaLayanan` | string | - | Teks "Reguler" atau "Express" |
| `biayaLayanan` | int | - | `beratTagihan x tarif` |
| `persenDiskon` | int | 0 | 0, 3, atau 5 |
| `nominalDiskon` | int | - | Nilai diskon dalam rupiah |
| `biayaAntar` | int | - | 0 atau 8000 |
| `totalBayar` | int | - | Tagihan akhir pelanggan |
| `nomorPelanggan` | int | 0 | Penghitung pelanggan (sekaligus total pelanggan) |
| `lanjut` | bool | - | Kondisi perulangan |
| `jumlahReguler`, `jumlahExpress`, `jumlahAnggota` | int | 0 | Akumulator jumlah pelanggan |
| `totalBerat`, `totalDiskon`, `totalAntar`, `totalPendapatan` | int | 0 | Akumulator total |
| `transaksiTerbesar` | int | 0 | Nilai tagihan terbesar |
| `namaTransaksiTerbesar` | string | "-" | Nama pemilik tagihan terbesar |
| Konstanta: `TARIF_REGULER`, `TARIF_EXPRESS`, `BIAYA_ANTAR`, `BERAT_MINIMUM`, `BERAT_MAKSIMUM`, `BATAS_ANGGOTA`, `BATAS_NONANGGOTA`, `DISKON_ANGGOTA`, `DISKON_NONANGGOTA` | const int | 7000, 11000, 8000, 2, 100, 5, 10, 5, 3 | Menyimpan ketentuan agar mudah diubah |

## Operator yang Digunakan

- Aritmetika: `*`, `/`, `+`, `-`, `++`, `+=`
- Perbandingan: `<`, `<=`, `>`, `>=`, `==`
- Logika: `&&`, `||`, `!`
