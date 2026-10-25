# Proses Integrasi Modul A dan Modul B

## Strategi

Modul A (tagihan per pelanggan, Khoirun Ni'mah) dan Modul B (rekapitulasi, Nur Adyatma Pratama) dibuat sebagai program mandiri dengan blok input, validasi, dan perhitungan yang sama. Integrasi dilakukan dengan menyatukan keduanya dalam **satu perulangan `do ... while`**:

1. Blok input, validasi, dan proses diambil dari Modul A (identik di kedua modul).
2. Blok **output rincian tagihan** milik Modul A dipertahankan.
3. Blok **akumulasi rekap** milik Modul B ditempatkan tepat setelah rincian tagihan, di dalam perulangan yang sama.
4. Laporan rekapitulasi Modul B ditempatkan **setelah** perulangan berakhir.

## Urutan Eksekusi dalam Satu Iterasi

| Urutan | Aktivitas                                               |   Asal    |
| :----: | ------------------------------------------------------- | :-------: |
|   1    | Input dan validasi 5 data                               | A (dan B) |
|   2    | Hitung berat tagihan, tarif, diskon, biaya antar, total | A (dan B) |
|   3    | Tampilkan rincian tagihan                               |     A     |
|   4    | Akumulasi variabel rekap                                |     B     |
|   5    | Tanya lanjut atau berhenti                              | A (dan B) |

## Hal yang Disesuaikan Saat Integrasi

- Variabel `nomorPelanggan` dipakai bersama: sebagai nomor urut di Modul A dan sebagai "total pelanggan" di rekap Modul B (satu variabel, bukan dua penghitung terpisah).
- Variabel proses (`totalBayar`, `nominalDiskon`, `biayaAntar`, `beratTagihan`) dipakai oleh kedua blok, sehingga rekap selalu konsisten dengan rincian yang ditampilkan.
- Pesan "data dicatat" milik Modul B diganti rincian tagihan lengkap milik Modul A.

## Verifikasi Hasil Integrasi

Kedua program mandiri dan program terintegrasi diuji dengan **12 skenario yang sama**, dan hasilnya sama: total tagihan di Modul A sama dengan total pendapatan di Modul B untuk satu pelanggan. Untuk sesi 4 pelanggan, rekap Modul B dan program terintegrasi identik (lihat `hasil_eksekusi_dan_pengujian.md`).
