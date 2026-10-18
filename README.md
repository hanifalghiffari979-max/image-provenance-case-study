# Image Provenance Case Study

> Case study tracing the origin and integrity of a public JPEG using EXIF/MakerNotes analysis, with tiered conclusions (proven / hypothesis / unknown) and a documented self-correction log.

**Author:** Mohammad Hanif Alghifari
**Language:** English · [Bahasa Indonesia di bawah](#bahasa-indonesia)

---

## Overview

This project examines a single publicly hosted JPEG (`Mostrando_los_productos_de_la_milpa.jpg`, hosted on Wikimedia Commons) and asks two questions:

1. **Is the file internally consistent and free of editing traces?**
2. **Can its origin (who, where, when) be established from the evidence available?**

The goal is not only the findings but the method: every claim is classified as **proven**, **hypothesis**, or **unknown**, and mistakes found during the analysis are kept visible in a corrections log instead of being deleted.

## Key Findings

| Area | Result |
|---|---|
| Device consistency | Metadata matches a Sony DSLR-A350 with a Minolta/Sony AF DT 18-70mm F3.5-5.6 (D) lens; all cross-checks pass (focal length, resolution, light value, dimensions) |
| Editing traces | None found in the metadata (not proof the file is unaltered, since metadata can be stripped or forged) |
| Capture date | 12 Oct 2013, 18:38:39 per camera clock; no time zone, no GPS, **not independently verified** |
| Photographer | **Not identified** |
| Flickr ↔ Commons link | **Not verified**; the photo does not appear in the provided Flickr screenshots |

## Method

- Metadata reading (EXIF, MakerNotes) from an ExifTools.com report
- Cross-tag consistency tests
- Cross-checking against the Wikimedia Commons file page and a related Flickr profile
- Manual astronomical plausibility test of the timestamp (including 2013 Mexican daylight saving time)
- Tiered conclusions and an explicit corrections log

## Corrections Log (highlights)

The first draft overstated several conclusions. They were corrected in the report (Section 11), for example:

- A sunset-based contradiction was withdrawn because it used a 2026 sunset table for a 2013 event.
- "Flickr account created in 2020 could not be the photographer" was replaced with a weaker, correct statement: the account only sets the earliest upload date.
- "Proven unedited" became "no trace of editing in the metadata".
- Autofocus sensor deviations were withdrawn as a "device fingerprint" because they depend on the scene, not on calibration.

## Repository Structure

```
image-provenance-case-study/
├── README.md
├── report/
│   ├── Laporan_Analisis_Metadata_Milpa.pdf        # Indonesian
│   └── Report_Metadata_Provenance_Analysis_EN.pdf # English
├── evidence/                                       # screenshots, ExifTools.com report
└── LICENSE
```

## Reproducing the Analysis

```bash
exiftool -a -G1 -u file.jpg                              # all blocks incl. MakerNotes
sha256sum file.jpg; sha1sum file.jpg; md5sum file.jpg    # hashes
exiftool -AFStatus* file.jpg                             # AF sensor status
exiftool -b -ThumbnailImage file.jpg > thumb.jpg
exiftool -b -PreviewImage file.jpg > preview.jpg
exiftool -b -TiffMeteringImage file.jpg > metering.tif
```

## Scope and Ethics

The analysis concerns the **file**, not a person. The photo contains a recognizable face, and the subject's identity was **deliberately not investigated**. The Commons caption is a description, not an identity.

## Attribution

The analyzed photo is hosted on Wikimedia Commons. Please check the license and author credit on its [Commons file page](https://commons.wikimedia.org/wiki/File:Mostrando_los_productos_de_la_milpa.jpg) and follow its terms when reusing the image. The photographer is not identified in the evidence reviewed here.

## Limitations

- Based on a PDF metadata report and screenshots, not direct local inspection of the original file
- Embedded thumbnail/preview images were only compared visually, not at pixel level
- Sunset times are a manual estimate and should be checked with an ephemeris calculator

## Next Steps

- Extract and pixel-compare the embedded thumbnail, preview, and metering images
- Compare the SHA-1 with the value on the Commons file page
- Check the Commons Source field, file history, and upload log
- Reverse image search for appearances before 2020

---

# Bahasa Indonesia

## Studi Kasus Provenansi Gambar

> Studi kasus penelusuran asal-usul dan integritas sebuah JPEG publik melalui analisis EXIF/MakerNotes, dengan kesimpulan berjenjang (terbukti / hipotesis / tidak diketahui) dan catatan koreksi diri yang terdokumentasi.

**Penyusun:** Mohammad Hanif Alghifari

### Gambaran Umum

Proyek ini memeriksa satu JPEG yang tersedia publik (`Mostrando_los_productos_de_la_milpa.jpg`, di Wikimedia Commons) dengan dua pertanyaan:

1. **Apakah berkas konsisten secara internal dan bebas jejak penyuntingan?**
2. **Apakah asal-usulnya (siapa, di mana, kapan) dapat dipastikan dari bukti yang ada?**

Tujuannya bukan hanya temuan, tetapi juga metode: setiap klaim digolongkan sebagai **terbukti**, **hipotesis**, atau **tidak diketahui**, dan kesalahan yang ditemukan selama analisis tetap ditampilkan dalam catatan koreksi, bukan dihapus.

### Temuan Utama

| Aspek | Hasil |
|---|---|
| Konsistensi perangkat | Metadata cocok dengan Sony DSLR-A350 dan lensa Minolta/Sony AF DT 18-70mm F3.5-5.6 (D); semua uji silang lolos |
| Jejak penyuntingan | Tidak ditemukan di metadata (bukan bukti berkas tidak diubah, karena metadata bisa dihapus atau dipalsukan) |
| Tanggal pemotretan | 12 Okt 2013, 18:38:39 menurut jam kamera; tanpa zona waktu dan GPS, **belum terverifikasi independen** |
| Fotografer | **Tidak teridentifikasi** |
| Hubungan Flickr ↔ Commons | **Belum terverifikasi**; foto tidak terlihat pada tangkapan layar Flickr |

### Metode

- Pembacaan metadata (EXIF, MakerNotes) dari laporan ExifTools.com
- Uji konsistensi antar-tag
- Pembandingan dengan halaman berkas Wikimedia Commons dan profil Flickr terkait
- Uji kewajaran waktu secara astronomis (manual), termasuk waktu musim panas Meksiko 2013
- Kesimpulan berjenjang dan catatan koreksi yang eksplisit

### Catatan Koreksi (ringkas)

Draf awal sempat terlalu kuat dalam beberapa kesimpulan. Semuanya dikoreksi di laporan (Bagian 11), misalnya:

- Kontradiksi berbasis matahari terbenam dibatalkan karena memakai tabel 2026 untuk peristiwa 2013.
- "Akun Flickr 2020 mustahil memotret" diganti menjadi pernyataan yang benar: akun hanya menetapkan batas paling awal unggahan.
- "Terbukti tidak disunting" menjadi "tidak ada jejak penyuntingan di metadata".
- Deviasi sensor autofokus dibatalkan sebagai "sidik jari perangkat" karena bergantung pada adegan, bukan kalibrasi.

### Struktur Repositori

Lihat bagian *Repository Structure* di atas. Laporan tersedia dalam dua bahasa di folder `report/`.

### Cakupan dan Etika

Analisis ini tentang **berkas**, bukan orang. Foto memuat wajah yang dapat dikenali, dan identitas subjek **sengaja tidak ditelusuri**. Keterangan di Commons adalah deskripsi, bukan identitas.

### Atribusi

Foto yang dianalisis berada di Wikimedia Commons. Periksa lisensi dan kredit penulis pada [halaman berkasnya](https://commons.wikimedia.org/wiki/File:Mostrando_los_productos_de_la_milpa.jpg) dan patuhi ketentuannya bila memakai ulang gambar. Fotografer tidak teridentifikasi dalam bukti yang ditinjau.

### Batasan

- Berbasis laporan metadata PDF dan tangkapan layar, bukan pemeriksaan lokal terhadap berkas asli
- Gambar thumbnail/preview tersemat hanya dibandingkan secara visual, bukan tingkat piksel
- Waktu matahari terbenam adalah estimasi manual dan perlu dicek dengan kalkulator efemeris
