# Matriks fitur OHLI Social v2.2.0

Status di bawah menjelaskan apa yang disediakan oleh source code. Fitur tetap perlu diuji di dua akun/perangkat nyata sebelum digunakan publik.

## Sudah memiliki alur UI dan endpoint server

- Registrasi/login, sesi token, penyimpanan akun pada server Android, dan hashing kata sandi PBKDF2 untuk akun baru/perubahan kata sandi.
- Chat privat dan fitur dasar lama: teks, lampiran, kontak, pengeditan/penghapusan sesuai implementasi yang tersedia, status pesan dan polling. v2.2 mendukung pemilihan batch beberapa foto/video/dokumen yang diunggah berurutan, serta tombol kecepatan pesan suara 1×/1,5×/2×.
- Feed sosial, posting teks/foto/video, audiens publik/pengikut/hanya saya, like, komentar, simpan, repost, bagikan, edit/hapus, arsip dan pemulihan.
- Profil, edit nama/bio/foto/cover, jumlah postingan, daftar pengikut/mengikuti yang dapat dibuka, dan penghitungan tayangan profil (maksimal satu catatan per akun per hari).
- Akun privat dengan permintaan mengikuti, persetujuan/penolakan permintaan, dan kontrol visibilitas daftar pengikut, daftar mengikuti, postingan disukai, serta koleksi tersimpan. Pemeriksaan akses diterapkan juga pada endpoint server.
- Tab profil Disukai, Posting ulang, Disimpan, Media, Sorotan, Draf (teks/caption lokal), dan Tentang. Akun yang direkomendasikan dapat diacak dan dibuka melalui foto/nama profil.
- Story teks/foto/video, viewer unik dan jumlah pemutaran ulang, status `viewedByMe`, lingkaran sudah/belum dilihat, viewer otomatis untuk foto/teks dan video, navigasi tap/swipe, statistik penonton untuk pemilik, reaksi suka, dan penyimpanan Story ke Sorotan. Sorotan bertahan setelah Story 24 jam berakhir.
- QR kontak akun sendiri, pemindai QR jika browser mendukung `BarcodeDetector`, dan jalur input nomor manual sebagai fallback.
- Penggantian kata sandi dengan verifikasi kata sandi lama; sesi perangkat lain dikeluarkan setelah kata sandi berubah.
- Pembuatan grup/Channel, alur gabung/keluar atau ikuti/berhenti mengikuti, chat grup teks, serta posting pengumuman teks oleh pemilik Channel.
- LIVE WebRTC peer-to-peer dengan signaling, komentar dan daftar siaran; batas kapasitas nyata tergantung koneksi dan browser.
- UI responsif untuk webview/browser, feed, video pendek, chat, pengaturan, notifikasi, dan navigasi OHLI. Pada v2.2, navigasi HP diprioritaskan untuk Beranda, Video, Buat, Story, Chat, dan Profil; menu tambahan tetap tersedia melalui menu atas.

## Ada, tetapi masih terbatas

- Privasi akun menyaring data dan konten melalui API. Jumlah pengikut/mengikuti tetap dapat tampak sebagai angka meski daftar namanya dibatasi.
- Tayangan profil dihitung per akun per hari, bukan setiap refresh. Ini bukan analytics waktu nyata atau daftar kunjungan historis tanpa batas.
- QR scanner menggunakan `BarcodeDetector` atau ZXing browser dan meminta kamera belakang. Kamera browser memerlukan secure context: HTTPS atau localhost; `http://IP-lokal` biasa akan ditolak browser. Jika izin/API tidak tersedia atau library tidak bisa dimuat, input nomor manual menjadi fallback.
- Chat grup dan Channel hanya mendukung teks; belum ada lampiran, balasan pesan, admin granular, undangan, panggilan grup, ataupun edit/hapus pesan grup.
- Sorotan dibuat dari Story aktif milik sendiri. Belum ada editor urutan, sampul, kategori, atau pengelolaan highlight lanjutan.
- Suka Story berupa tombol toggle dan jumlah suka; belum ada layar daftar orang yang menyukai Story.
- Perbaikan CSS v2.2 membatasi overflow horizontal, merapikan tombol mobile, menampilkan navigasi enam pintasan, dan memastikan menu tambahan chat dan pintasan arsip di header dapat dijangkau. Zoom tetap diizinkan oleh viewport. Kondisi tiap ukuran layar/iPhone tetap perlu diuji pada perangkat asli.
- LIVE hanya signaling P2P. Untuk banyak penonton diperlukan TURN/SFU; host harus tetap terhubung dan memberi izin kamera/mikrofon.
- Draf konten dan tema kustom hanya disimpan lokal di browser/perangkat pengguna (tidak tersinkron). Media draf harus dipilih ulang ketika melanjutkan. Arsip chat tetap menggunakan preferensi lokal browser. Seluruh JSON akun, pesan, status, follow, dan blokir berada di `getFilesDir()` pada perangkat host, dilengkapi file sementara dan cadangan `.bak` untuk pemulihan saat proses mati/listrik terputus. Data bertahan saat reboot, server mati, Wi-Fi terputus, dan alamat IP berubah; setelah IP berubah, buka alamat server baru. Menghapus data aplikasi atau uninstall tetap menghapus data lokal.

## Belum disediakan / perlu infrastruktur atau pengembangan lanjutan

- Database relasional produksi, transaksi multi-proses, indeks pencarian, object storage eksternal, backup off-device, monitoring, WAF/rate limit, audit keamanan, dan pemulihan bencana.
- OTP/SMS/e-mail, reset kata sandi terverifikasi, push notification ketika aplikasi tertutup, dan enkripsi end-to-end dengan protokol yang diaudit.
- Audio/musik lintas-video (sound library, halaman audio, daftar video berdasarkan lagu, favorit suara), pencampuran/penyimpanan trek audio, algoritma FYP personal yang lebih lanjut, drafts server-side, dukungan multi-foto dalam satu posting, chat grup dengan media, polling, indeks pencarian, moderasi/laporan, role admin granular, serta analytics kreator memerlukan API dan dukungan penyimpanan/pemrosesan server tambahan.
- Pengujian dua perangkat fisik (terutama iPhone) dan build APK final. Build lokal pada sesi pembuatan source tidak tersedia karena Android SDK dan Gradle tidak terpasang; gunakan GitHub Actions pada repository.

Jangan menganggap keterbatasan di atas sebagai fitur produksi yang telah selesai.


## Perbaikan v2.1
- Responsif HP: overflow horizontal profil ditahan di viewport dan rail Video Pendek dirapatkan.
- Story satu bar per akun; cerita terbaru terbuka pertama dan cerita sebelumnya dapat dinavigasi.
- Foto profil dapat dilihat ukuran besar, follow state ditampilkan dengan benar, dan double-tap like memakai satu request.
- Centang pesan mengikuti status dikirim/diterima/dibaca; edit/hapus tersedia melalui tekan lama.
- FYP menggunakan skor engagement dan peluruhan waktu; Jelajah Topik menampilkan tagar aktif dari postingan dua minggu terakhir.
- Blokir disimpan di server dan operasi blokir bersifat idempoten.
- JSON menyimpan cadangan atomik di storage internal aplikasi untuk pemulihan setelah restart atau kehilangan daya.


## Perbaikan v2.2.0 dan batasnya
- Story menggunakan endpoint `/api/status/view` yang sudah ada untuk mencatat tontonan. Status baca hanya diperbarui saat request view berhasil; pada koneksi terputus, viewer tetap bisa berjalan tetapi indikator mungkin belum tersinkron sampai data dimuat ulang.
- Editor video menyimpan metadata crop/mute/rentang putar; server menyimpan metadata dan file asli. Ini bukan proses render/transcoding permanen seperti editor video penuh.
- Pencarian dari Reels kembali ke Reels melalui tombol kembali internal OHLI.
- Kustomisasi tema, draf Story/Post, arsip chat, dan beberapa preferensi adalah lokal pada browser/perangkat, bukan sinkron lintas perangkat.
- Kirim batch chat mengirim setiap file sebagai pesan terpisah dan satu per satu. Jika terjadi kegagalan di tengah, file sebelumnya tetap terkirim dan UI menampilkan jumlah yang berhasil.
- Kamera/pemindai QR memerlukan secure context (HTTPS atau localhost) serta izin kamera; fallback nomor manual tetap dipertahankan.
- Musik dari video lain, pemilihan audio dari galeri untuk Reels, halaman audio, dan favorit suara belum dibuat karena API server belum memiliki katalog/stream audio, atribusi hak pakai, atau pipeline mixing/transcoding. Tidak ada tombol palsu yang mengklaim fitur ini aktif.
- Algoritma `Untuk Kamu` dan Jelajah Topik masih mengandalkan skor engagement/umur konten serta tagar pada server saat ini; belum merupakan sistem rekomendasi personal dengan riwayat tontonan dan pembelajaran perilaku tingkat lanjut.
- Belum dilakukan build APK atau pengujian kamera/gesture lintas perangkat dalam sesi ini. Jalankan workflow GitHub Actions, lalu uji pada Android dan iPhone/browser nyata.
