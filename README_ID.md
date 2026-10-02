# PORTAL BELAJAR KELAS 10 REVISI

## File
- `PORTAL_BELAJAR_KELAS_10_REVISI.html`: halaman web.
- `PORTAL_BELAJAR_KELAS_10_REVISI_SERVER.js`: server/API.
- `package.json`: dependensi Node.js.
- `render.yaml`: contoh konfigurasi Render.

## Konfigurasi hosting wajib
Buat Environment Variables di hosting:
- `ASTS_SERVER_KEY`: kunci sinkronisasi acak dan panjang (minimal 32 karakter).
- `TEACHER_USERNAME`: username guru.
- `TEACHER_PASSWORD`: password guru yang kuat (minimal 14 karakter, unik).
- `OPENAI_API_KEY`: opsional, dibutuhkan untuk fitur AI. Jangan masukkan API key ke HTML.
- `DATA_DIR`: arahkan ke persistent disk, misalnya `/var/data`.

Akun guru sekarang diperiksa di server, bukan menggunakan password demo yang tertanam di HTML. Login menghasilkan token sesi yang berlaku 8 jam dan percobaan login dibatasi. Jangan gunakan kembali password yang pernah dibagikan. Jika password lama sudah diketahui teman, ubah `TEACHER_PASSWORD` di hosting sebelum deploy ulang.

## Penting untuk keamanan dan penyimpanan
- Jangan mengirimkan `ASTS_SERVER_KEY` kepada siswa/teman. Untuk keamanan penuh, aplikasi produksi idealnya memisahkan API publik siswa dari API admin; kunci yang dimasukkan ke browser tetap dapat dilihat oleh pengguna browser tersebut.
- Agar materi, bank soal, dan nilai bertahan setelah redeploy/restart, hosting harus memiliki persistent disk atau database permanen. File lokal di layanan hosting tanpa disk persisten bisa hilang saat deploy.
- Simpan cadangan database `asts-data.json` secara berkala.
- Gunakan HTTPS.
- Penilaian esai otomatis menggunakan kemiripan kata kunci untuk nilai sementara, bukan pemahaman bahasa sempurna. Jawaban parsial/ambigu perlu diperiksa guru sebelum nilai final. Rubrik dan sinonim yang diterima perlu diperiksa sebelum ujian.

## Jalankan lokal
Node.js 18+ diperlukan. Isi variabel environment terlebih dahulu, lalu jalankan `npm install` dan `npm start`.


## Panduan awal yang terlihat saat portal pertama dibuka
1. Tekan **Atur Server Sekarang** pada tutorial awal.
2. Masukkan URL server online dan nilai `ASTS_SERVER_KEY` yang sama dengan Environment hosting.
3. Tekan **Simpan & Tes Koneksi** dan pastikan muncul centang hijau.
4. Setelah tersambung, siswa dapat login dengan nama dan guru dengan username/password. Guru tidak perlu memasukkan kunci sinkronisasi setiap kali login pada perangkat yang sudah menyimpannya.

Akun guru tetap harus dibuat satu kali oleh pemilik portal melalui `TEACHER_USERNAME` dan `TEACHER_PASSWORD` di Environment hosting. Ini bukan langkah yang perlu dilakukan setiap guru saat masuk. Jangan pernah menanam password guru atau kunci server di HTML.
