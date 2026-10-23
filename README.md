# Online Command Teltonika

Cari perintah GPS tracker Teltonika cukup dengan satu kata kunci. Ketik "suhu", "apn", atau nomor ID, lalu langsung dapat perintah SMS/GPRS, `readio`, `getparam`, atau `setparam` yang siap disalin dan dikirim ke perangkat.

**Buka web:** https://igaababil.github.io/online-command-teltonika/

Dibuat oleh **Iga Ababil**.

---

## Kenapa web ini dibuat

Saat instalasi atau pengecekan unit di lapangan, teknisi sering harus membuka wiki Teltonika, mencari tabel yang panjang, lalu mencocokkan ID secara manual. Web ini merangkum semua itu dalam satu kolom pencarian yang bisa dipakai dari ponsel.

## Fitur

- **Pencarian satu kata.** Bisa memakai bahasa Indonesia (suhu, aki, pintu, sinyal), nama sensor atau parameter (Dallas Temperature, APN), maupun nomor ID (72, 2001).
- **Perintah SMS/GPRS umum.** 68 perintah seperti `getgps`, `ggps`, `getver`, `cpureset`, `setdigout`, `flush`, `odoset`, serta perintah Bluetooth, OBD, dan CAN adapter. Perintah yang butuh argumen punya formulir isian yang membentuk perintahnya otomatis, dan perintah berisiko diberi peringatan.
- **Perintah berbasis ID.**
  - `readio <ID>` untuk membaca nilai I/O element.
  - `getparam <ID>` untuk membaca konfigurasi.
  - `setparam <ID>:<nilai>` untuk mengubah konfigurasi.
- **Pembentuk perintah SET.** Isi nilai atau pilih dari daftar, perintah terbentuk otomatis. Nilai dicek terhadap rentang yang diizinkan sebelum disalin.
- **Konversi nilai readio.** Masukkan angka mentah, web menghitung pengali dan satuannya. Contoh: `285` pada Dallas Temperature menjadi `28.5 °C`.
- **Kode error sensor.** Nilai seperti `3000` langsung dikenali sebagai "sensor tidak terhubung", bukan dibaca sebagai suhu.
- **Pengaturan event I/O dan geofence.** Priority, operand, high/low level, dan notifikasi SMS untuk setiap I/O, OBD, flag CAN, serta 50 zona geofence.
- **Format SMS.** Satu centang untuk menambahkan dua spasi di depan perintah (format SMS tanpa login dan password).
- **Tautan berbagi.** Kata kunci ikut tersimpan di alamat web, misalnya `.../#temp1`, sehingga hasil pencarian bisa dikirim ke rekan kerja.
- **Ringan dan tanpa server.** Seluruh web ada dalam satu file `index.html`, bisa dibuka di ponsel, dan mendukung mode gelap.

## Cara pakai

| Yang dicari | Ketik | Hasil teratas |
|---|---|---|
| Cek lokasi | `lokasi` | `getgps` |
| Nyalakan relay | `relay` | `setdigout <DOUT1><DOUT2>` |
| Restart perangkat | `restart` | `cpureset` |
| Baca suhu sensor 1 | `temp1` | `readio 72` |
| Atur APN | `set apn` | `setparam 2001:<nilai>` |
| Alarm suhu | `set temp` | `setparam 50310` s/d `50313` |
| Sensor BBM UL202 | `ul202` | `readio 327` |
| Interval kirim data | `interval` | `getparam 10000`, `10005`, dan seterusnya |

Kata **set**, **atur**, atau **ubah** memfilter hasil ke parameter yang bisa diubah. Kata **baca** atau **readio** memfilter ke I/O yang hanya bisa dibaca.

### Mengirim lewat SMS

```
<login> <password> readio 72
```

Jika login dan password SMS di perangkat kosong, awali perintah dengan dua spasi:

```
  readio 72
```

Semua perintah peka huruf besar/kecil. SMS ke perangkat yang sedang Deep Sleep baru diterima setelah perangkat bangun, sedangkan perintah GPRS (yang memakai protokol Codec 12) tidak akan diterima.

Login dan password SMS diatur di parameter `3003` dan `3004`. Sangat disarankan untuk mengisinya agar perangkat tidak bisa dikendalikan oleh nomor sembarang.

## Sumber data

Data diambil dari Teltonika Wiki untuk FMB130 (firmware FMB.Ver.03.29.00 ke atas):

- *FMB130 Teltonika Data Sending Parameters ID* untuk daftar I/O element.
- *FMB130 Parameter list* untuk daftar parameter konfigurasi.
- *FMB130 SMS/GPRS Commands* untuk daftar perintah umum.

Sebagian besar ID juga berlaku untuk seri FMB lain, tetapi beberapa model punya I/O atau parameter yang berbeda. Selalu cocokkan dengan dokumentasi model perangkat yang dipakai.

**Catatan:** di tabel wiki ada dua kemungkinan salah ketik, yaitu ID event GNSS PDOP (tertulis 5061–5065, polanya 50061–50065) dan Event only GNSS Status (tertulis dobel di 50053). Web ini mengikuti polanya dan memberi tanda peringatan. Cek dengan `getparam` sebelum memakai `setparam` pada ID tersebut.

## Peringatan

Perintah `setparam` langsung mengubah konfigurasi perangkat, termasuk server tujuan dan output (misalnya relay putus mesin). Periksa ulang ID dan nilai sebelum mengirim. Pembuat web tidak bertanggung jawab atas kesalahan konfigurasi akibat penggunaan alat ini.

Web ini adalah proyek independen dan tidak berafiliasi dengan Teltonika.

## Memperbarui web

1. Siapkan file `index.html` versi terbaru.
2. Di repository ini, klik **Add file** lalu **Upload files**.
3. Unggah file dengan nama yang sama (`index.html`), lalu klik **Commit changes**.
4. Tunggu 1–2 menit sampai GitHub Pages memperbarui web.

## Rencana pengembangan

- Pilihan model perangkat (FMC, FMM, FMT, FMB920, dan lainnya).
- Pengaturan event untuk sensor suhu BLE dan EYE.
- Beacon Capture Configuration (1701–1798).

Punya masukan atau menemukan ID yang salah? Buka tab **Issues** di repository ini.

---

Dibuat oleh **Iga Ababil**.
