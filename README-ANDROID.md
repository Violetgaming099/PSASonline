# Exambro Android – SMP Negeri 4 Kuningan

Aplikasi ujian yang **berjalan offline**; hanya Google Form yang memakai internet siswa.
Tampilan aplikasi dibundel di dalam APK (`app/src/main/assets/exambro/`).

## Yang dilakukan aplikasi saat ujian berlangsung
Setelah token masuk benar, aplikasi memanggil **kunci layar (screen pinning)**:
- Tombol **Home** dan **Recent apps** tidak berfungsi.
- Panel notifikasi tidak bisa ditarik, sehingga notifikasi WhatsApp dll tidak bisa dibuka.
- Tombol Kembali dan tombol volume dimatikan; tangkapan/rekam layar diblokir.
- Kunci dilepas otomatis saat siswa memasukkan **token keluar** yang benar.

Jika siswa tetap berhasil keluar dari layar ujian, pelanggaran pertama = peringatan. Jika **terulang**, ujian dijeda dan siswa harus meminta **Kode Pemulihan Kecurangan** kepada pengawas.

## Mengubah link, token, dan kode pemulihan
Edit `app/src/main/assets/exambro/config.js` (link Google Form lengkap, token, `kodePemulihan`). Lalu bangun ulang APK.
Syarat Google Form agar tanpa login: lihat `app/src/main/assets/exambro/README.md`.

## Cara membuat APK
**Cara A – tanpa memasang apa pun (GitHub):**
1. Buat repository di github.com, unggah seluruh isi folder ini.
2. Buka tab **Actions** > **Build APK** > **Run workflow**.
3. Setelah selesai, unduh `Exambro-APK` pada bagian Artifacts, lalu sebarkan file `.apk`.

**Cara B – Android Studio:** File > Open folder ini > tunggu sinkronisasi > Build > Build APK(s).

## Pemasangan di ponsel siswa
Aktifkan "Pasang dari sumber tidak dikenal" untuk file APK. Di ponsel Android, pastikan **Pengaturan > Keamanan > Penyematan layar (Screen pinning)** aktif; sebaiknya aktifkan juga opsi "Minta PIN sebelum melepas sematan" agar siswa tidak bisa melepasnya sendiri.

## Batasan yang jujur
- Screen pinning tanpa mode perangkat terkelola (device owner) tidak 100% mutlak: sebagian ponsel menampilkan konfirmasi dan siswa masih bisa melepasnya dengan tombol tertentu (mis. tahan Kembali + Recent). Kalau itu dilakukan, deteksi pelanggaran akan mencatatnya.
- Kode Pemulihan hanya satu kode di `config.js`. Jangan dibagikan ke siswa.
- Proyek ini **belum dikompilasi dan belum diuji di ponsel** oleh pembuatnya. Uji dulu di 1-2 ponsel sebelum hari ujian.
