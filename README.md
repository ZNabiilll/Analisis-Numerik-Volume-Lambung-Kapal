# Analisis-Numerik-Volume-Lambung-Kapal

## Deskripsi Tugas

Gambar perahu katamaran diberi grid putus-putus. Dari gambar tersebut dihitung volume **kedua lambung** dengan ketentuan:

- Satu *dash-kosong* bernilai 5 + 5 cm = 10 cm.
- Lantai kapal dianggap datar (tanpa keel), sehingga penampang lambung dari tampak depan berbentuk persegi panjang.
- Volume *reserve buoyancy* tidak dihitung.

## Pendekatan Pengerjaan

### 1. Mengiris lambung menjadi penampang

Lambung diiris tegak lurus sumbu panjang kapal, seperti mengiris roti tawar. Karena lantai datar, setiap irisan berbentuk persegi panjang, sehingga luas penampangnya:

```
A(s) = lebar(s) × tinggi(s)
```

- `lebar(s)` dibaca dari gambar tampak atas.
- `tinggi(s)` dibaca dari gambar tampak samping.

### 2. Membaca data dari gambar

Pada sejumlah stasiun yang berjarak sama sepanjang kapal, lebar dan tinggi lambung dibaca secara visual dalam satuan kotak grid, lalu dikonversi ke meter menggunakan skala dari soal (1 dash-kosong = 10 cm). Lambung atas dan lambung bawah dibaca terpisah untuk lebarnya.

### 3. Mengintegralkan luas penampang

Volume adalah integral luas penampang sepanjang kapal:

```
V = ∫ A(s) ds
```

Karena `A(s)` hanya diketahui di titik-titik pengukuran, integral dihitung secara numerik dengan dua metode:

| Metode | Peran | Rumus |
|---|---|---|
| Simpson 1/3 komposit | Metode utama | `V ≈ (h/3) [A0 + 4(A1 + A3 + ...) + 2(A2 + A4 + ...) + An]` |
| Trapesium komposit | Pembanding | `V ≈ (h/2) [A0 + 2(A1 + A2 + ... + An-1) + An]` |

Simpson 1/3 mensyaratkan jumlah interval genap, sehingga jumlah stasiun dipilih ganjil.

### 4. Memeriksa hasil

- Hasil Simpson dibandingkan dengan trapesium. Jika keduanya berdekatan, hasil hitungan konsisten.
- Dilakukan uji sensitivitas: pembacaan lebar dan tinggi digeser sedikit untuk melihat seberapa besar pengaruh galat pembacaan visual terhadap volume.
- Hasil divisualisasikan dalam grafik profil lebar, tinggi, dan luas penampang sepanjang kapal.

## Isi Repository

| File | Keterangan |
|---|---|
| `volume_lambung_katamaran.ipynb` | Notebook berisi soal, landasan teori, data pengukuran, kode Python, visualisasi, dan kesimpulan |
| `README.md` | Deskripsi proyek ini |

## Cara Menjalankan

1. Pastikan Python 3 dan Jupyter sudah terpasang.
2. Pasang pustaka yang dibutuhkan:

   ```bash
   pip install numpy matplotlib jupyter
   ```

3. Buka notebook, lalu jalankan semua sel dari atas ke bawah:

   ```bash
   jupyter notebook volume_lambung_katamaran.ipynb
   ```

Semua data pengukuran sudah ada langsung di dalam notebook, jadi tidak diperlukan file tambahan. Hasil perhitungan dapat dilihat pada keluaran notebook.

## Sumber Gambar

Gambar perahu berasal dari publikasi *Desain dan Konstruksi Perahu Katamaran Fiberglass untuk Wisata Pancing*:
https://www.researchgate.net/publication/342077926_Desain_dan_Konstruksi_Perahu_Katamaran_Fiberglass_untuk_Wisata_Pancing
