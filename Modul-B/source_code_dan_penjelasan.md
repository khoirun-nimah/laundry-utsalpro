# Source Code dan Penjelasan: Modul B (Rekapitulasi Harian)

File: `modul_b.cpp` (C++, konsol, tanpa array dan tanpa library selain `iostream` dan `string`).

```cpp
// Modul B - Rekapitulasi Pendapatan Laundry Harian
// SSI1144 Algoritma dan Pengantar Pemrograman - Studi Kasus 02 (C++ konsol)
#include <iostream>
#include <string>
using namespace std;

int main() {
    // ===== KONSTANTA (ketentuan studi kasus laundry) =====
    const int TARIF_REGULER = 7000;      // Rp per kg
    const int TARIF_EXPRESS = 11000;     // Rp per kg
    const int BIAYA_ANTAR = 8000;        // Rp, tidak termasuk komponen diskon
    const int BERAT_MINIMUM = 2;         // kg, berat tagihan minimum
    const int BERAT_MAKSIMUM = 100;      // kg, batas kapasitas per transaksi (asumsi desain)
    const int BATAS_ANGGOTA = 5;         // kg minimum diskon anggota
    const int BATAS_NONANGGOTA = 10;     // kg minimum diskon nonanggota
    const int DISKON_ANGGOTA = 5;        // persen
    const int DISKON_NONANGGOTA = 3;     // persen

    // ===== VARIABEL INPUT =====
    string namaPelanggan, jawaban;
    double beratInput;
    int jenisLayanan;
    bool anggota, layananAntar;

    // ===== VARIABEL PROSES =====
    int beratTagihan, tarif, biayaLayanan, persenDiskon, nominalDiskon, biayaAntar, totalBayar;
    string namaLayanan;
    int nomorPelanggan = 0;
    bool lanjut;

    // ===== VARIABEL REKAPITULASI (akumulator, tanpa array) =====
    int jumlahReguler = 0, jumlahExpress = 0, jumlahAnggota = 0;
    int totalBerat = 0, totalDiskon = 0, totalAntar = 0, totalPendapatan = 0;
    int transaksiTerbesar = 0;
    string namaTransaksiTerbesar = "-";

    cout << "==================================================\n";
    cout << "   SISTEM BIAYA LAUNDRY - MODUL B (REKAPITULASI)\n";
    cout << "==================================================\n";

    do {
        nomorPelanggan++;
        cout << "\n--- Pelanggan ke-" << nomorPelanggan << " ---\n";

        // ----- INPUT DAN VALIDASI -----
        while (true) {
            cout << "Nama pelanggan                       : ";
            if (!getline(cin, namaPelanggan)) return 0;
            if (namaPelanggan.find_first_not_of(" \t") != string::npos) break;
            cout << "  [!] Nama tidak boleh kosong.\n";
        }
        while (true) {
            cout << "Berat cucian (kg)                    : ";
            if (cin >> beratInput && cin.peek() == '\n') {
                cin.ignore(10000, '\n');
                if (beratInput <= 0) cout << "  [!] Berat harus lebih dari 0 kg.\n";
                else if (beratInput > BERAT_MAKSIMUM) cout << "  [!] Berat melebihi kapasitas maksimum 100 kg.\n";
                else break;
            } else {
                if (cin.eof()) return 0;
                cout << "  [!] Berat harus berupa angka.\n";
                cin.clear();
                cin.ignore(10000, '\n');
            }
        }
        while (true) {
            cout << "Jenis layanan (1=Reguler, 2=Express) : ";
            if (cin >> jenisLayanan && cin.peek() == '\n') {
                cin.ignore(10000, '\n');
                if (jenisLayanan == 1 || jenisLayanan == 2) break;
                cout << "  [!] Pilihan harus 1 atau 2.\n";
            } else {
                if (cin.eof()) return 0;
                cout << "  [!] Pilihan harus berupa angka 1 atau 2.\n";
                cin.clear();
                cin.ignore(10000, '\n');
            }
        }
        while (true) {
            cout << "Anggota? (y/t)                       : ";
            if (!getline(cin, jawaban)) return 0;
            if (jawaban == "y" || jawaban == "Y") { anggota = true; break; }
            if (jawaban == "t" || jawaban == "T") { anggota = false; break; }
            cout << "  [!] Jawab dengan y atau t.\n";
        }
        while (true) {
            cout << "Layanan antar? (y/t)                 : ";
            if (!getline(cin, jawaban)) return 0;
            if (jawaban == "y" || jawaban == "Y") { layananAntar = true; break; }
            if (jawaban == "t" || jawaban == "T") { layananAntar = false; break; }
            cout << "  [!] Jawab dengan y atau t.\n";
        }

        // ----- PROSES -----
        beratTagihan = (int)beratInput;
        if (beratInput > beratTagihan) beratTagihan++;            // pembulatan ke atas
        if (beratTagihan < BERAT_MINIMUM) beratTagihan = BERAT_MINIMUM;

        if (jenisLayanan == 1) { namaLayanan = "Reguler"; tarif = TARIF_REGULER; }
        else                   { namaLayanan = "Express"; tarif = TARIF_EXPRESS; }
        biayaLayanan = beratTagihan * tarif;

        persenDiskon = 0;
        if (anggota && beratTagihan >= BATAS_ANGGOTA) persenDiskon = DISKON_ANGGOTA;
        else if (!anggota && beratTagihan >= BATAS_NONANGGOTA) persenDiskon = DISKON_NONANGGOTA;
        nominalDiskon = biayaLayanan * persenDiskon / 100;

        if (layananAntar) biayaAntar = BIAYA_ANTAR; else biayaAntar = 0;   // antar tidak didiskon
        totalBayar = biayaLayanan - nominalDiskon + biayaAntar;

        cout << ">> Data pelanggan dicatat. Total tagihan: Rp" << totalBayar << "\n";

        // ----- AKUMULASI REKAPITULASI -----
        if (jenisLayanan == 1) jumlahReguler++; else jumlahExpress++;
        if (anggota) jumlahAnggota++;
        totalBerat += beratTagihan;
        totalDiskon += nominalDiskon;
        totalAntar += biayaAntar;
        totalPendapatan += totalBayar;
        if (totalBayar > transaksiTerbesar) {
            transaksiTerbesar = totalBayar;
            namaTransaksiTerbesar = namaPelanggan;
        }

        // ----- PILIHAN ULANG / AKHIRI -----
        while (true) {
            cout << "\nProses pelanggan lain? (y/t)         : ";
            if (!getline(cin, jawaban)) return 0;
            if (jawaban == "y" || jawaban == "Y") { lanjut = true; break; }
            if (jawaban == "t" || jawaban == "T") { lanjut = false; break; }
            cout << "  [!] Jawab dengan y atau t.\n";
        }
    } while (lanjut);

    // ===== LAPORAN REKAPITULASI HARIAN =====
    cout << "\n==================================================\n";
    cout << "          REKAPITULASI LAUNDRY HARIAN\n";
    cout << "==================================================\n";
    cout << "Total pelanggan            : " << nomorPelanggan << "\n";
    cout << "Pelanggan Reguler          : " << jumlahReguler << "\n";
    cout << "Pelanggan Express          : " << jumlahExpress << "\n";
    cout << "Pelanggan Anggota          : " << jumlahAnggota << "\n";
    cout << "Total berat cucian         : " << totalBerat << " kg\n";
    cout << "Total diskon               : Rp" << totalDiskon << "\n";
    cout << "Total biaya antar          : Rp" << totalAntar << "\n";
    cout << "Total pendapatan           : Rp" << totalPendapatan << "\n";
    cout << "Transaksi terbesar         : Rp" << transaksiTerbesar << " (" << namaTransaksiTerbesar << ")\n";
    cout << "==================================================\n";
    cout << "Rekapitulasi selesai.\n";
    return 0;
}
```

## Penjelasan Bagian Penting

| Bagian kode                                                                      | Fungsi                                                                                                                            |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Konstanta (`const int ...`)                                                      | Menyimpan tarif, batas, dan persen diskon di satu tempat. Jika ketentuan berubah (misalnya tarif express), cukup ubah satu baris. |
| Perulangan `do ... while (lanjut)`                                               | Memproses pelanggan berulang sampai pengguna menjawab `t`.                                                                        |
| Perulangan `while (true)` pada input                                             | Mengulang pertanyaan sampai data valid, sehingga program tidak berhenti saat input salah.                                         |
| `cin >> x && cin.peek() == '\n'`                                                 | Memastikan baris input hanya berisi angka. Input seperti `abc` atau `3abc` ditolak.                                               |
| `beratTagihan = (int)beratInput; if (beratInput > beratTagihan) beratTagihan++;` | Pembulatan ke atas tanpa library tambahan. Contoh: 4,2 menjadi 5; 5,0 tetap 5.                                                    |
| `if (beratTagihan < BERAT_MINIMUM)`                                              | Berat di bawah 2 kg tetap ditagih 2 kg.                                                                                           |
| `if (anggota && beratTagihan >= 5) ... else if (!anggota && beratTagihan >= 10)` | Menentukan diskon 5% atau 3% atau 0%. Operator logika `&&` dan `!` dipakai di sini.                                               |
| `totalBayar = biayaLayanan - nominalDiskon + biayaAntar`                         | Diskon hanya mengurangi biaya layanan. Biaya antar ditambahkan setelahnya sehingga tidak terdiskon.                               |

### Rekapitulasi tanpa array

Semua data rekap disimpan sebagai variabel akumulator (`jumlahReguler`, `totalBerat`, `totalDiskon`, `totalAntar`, `totalPendapatan`, dan seterusnya) yang bertambah setiap iterasi. **Transaksi terbesar** ditentukan dengan membandingkan `totalBayar` pelanggan saat ini dengan `transaksiTerbesar`; jika lebih besar, nilai dan nama pelanggan disimpan. Jika ada dua transaksi sama besar, yang pertama dipertahankan karena memakai tanda `>` (bukan `>=`).

## Cara Kompilasi dan Menjalankan

```bash
cd Modul-B
g++ modul_b.cpp -o modul_b
./modul_b      # Windows: modul_b.exe
```
