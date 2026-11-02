# FIRE-MAR

**Penyaringan evakuasi kapal dan akses SAR untuk kapal Ro-Pax domestik.**
Website ini menerapkan paper *FIRE-MAR: A Route-Specific Framework for Prioritizing Evacuation Redesign and Rescue Preparedness on Indonesian Domestic Ro-Pax Ferries* (Tim Doa Ibu, Teknik Perkapalan ITS, SMC 2026).

> FIRE-MAR adalah alat penyaringan, bukan alat persetujuan. Hasilnya perlu diperiksa oleh orang yang kompeten, dicocokkan dengan ukuran di kapal, dan dikonfirmasi oleh Badan Klasifikasi atau Direktorat Jenderal Perhubungan Laut sebelum dipakai untuk keputusan.

## Yang dihitung

| Bagian | Isi | Sumber |
|---|---|---|
| Evakuasi kapal | 1,25 (R + T) + ⅔ (E + L) ≤ 60 menit; skenario A (arahan kru), B (tangga terdekat), sekunder (setiap tangga diuji hilang) | IMO MSC.1/Circ.1533, metode sederhana |
| Akses SAR rute | notifikasi + persiapan + 60 × jarak ÷ kecepatan ≤ 175 menit | Peraturan Basarnas No. 6/2022 (25 + 150 menit) + waktu notifikasi |
| Pemeriksaan aturan | 16 pemeriksaan: kinerja dan kemacetan Circ.1533, dua jalan keluar, lebar tangga/pintu/lorong, pegangan, arah, tinggi dan sudut, bordes, pintu keluar, tangga tertutup, ruang di bawah geladak sekat, penanda rendah, pintu tanpa kunci, pembuka cepat, muster station | SOLAS II-2/13.3.2, FSS Code bab 13 (MSC.410(97)), SOLAS III/11.2 |
| Uji skenario | lokasi api (tangga/pintu tertandai hilang), tambahan orang, laporan terlambat, unit SAR melambat | metode yang sama, kasus sekunder γ = 1,3 |

Status setiap pemeriksaan: Memenuhi, Tidak memenuhi, Perlu konfirmasi, Perlu data, Tidak berlaku. Data yang belum ada tidak ditebak. Aturan klas BKI dan standar NCVS (KM 65/2009) tidak diperiksa; daftar lengkap hal yang tidak diperiksa ada di halaman Pemeriksaan aturan dan di laporan PDF.

## Cara memakai

1. **Data kapal**: zona, tangga, pintu dan lorong, jalur zona ke tangga.
2. **Rute dan SAR**: jarak terjauh dari pos SAR dan tiga skenario waktu.
3. **Ringkasan**, **Evakuasi kapal**, **Akses SAR**: kategori, angka utama, rekomendasi, jejak hitung.
4. **Pemeriksaan aturan**: lengkapi ukuran tambahan dan pernyataan penilai.
5. **Laporan**: identitas, alasan dan catatan, lalu PDF. Status *Siap diperiksa* hanya keluar bila enam syarat kelengkapan terpenuhi; selain itu bertanda *Draf*.

Semua hitungan berjalan di perangkat pengguna; data kapal tidak dikirim ke server mana pun.

## Pengujian

| Uji | Perintah |
|---|---|
| Mesin hitung: semua angka paper, contoh resmi FSS Code gambar 2, aturan, uji skenario, migrasi versi 1, 400 kapal acak dibandingkan model Python independen | `node tests/run.js` |
| Browser: PDF, Excel pulang-pergi, kode verifikasi | `python3 build.py && python3 tests/files_test.py dist/site /tmp/out id` |
| Tangkapan layar desktop, ponsel, gelap, Inggris | `python3 tests/screenshots.py dist/site /tmp/out light,dark,en,phone` |

Hasil terakhir: 6.942 pemeriksaan mesin lulus.

## Memasang di GitHub Pages

1. Buat repositori, misalnya `fire-mar`, lalu unggah seluruh isi folder `dist/site/`.
2. **Settings → Pages** → *Deploy from a branch* → `main`, folder `/ (root)` → **Save**.
3. Website tersedia di `https://<nama-akun>.github.io/fire-mar/` dan tetap jalan tanpa sinyal setelah kunjungan pertama.

## Struktur

```
src/engine.js      mesin hitung (fungsi murni)
src/i18n.js        teks Indonesia dan Inggris
src/report.js      laporan PDF, Excel, kode verifikasi
src/app/*.js       tampilan: inti, grafik, halaman data, hasil, analisis, kerangka
src/styles.css     desain
scripts/build_fonts.py  membuat subset huruf
tests/             uji mesin, uji silang Python, uji browser
build.py           menyusun dist/artifact dan dist/site
```

## Lisensi

Kode: MIT. Huruf: SIL Open Font License 1.1 (lihat `fonts/LICENSE-OFL.txt`).
