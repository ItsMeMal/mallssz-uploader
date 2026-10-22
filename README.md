# mallssz-uploader

Website upload gambar untuk guest. Pengunjung tidak perlu login atau membuat akun. Antarmuka memakai HTML, CSS, dan JavaScript biasa, dengan drag-and-drop, preview, animasi ringan, progress upload asli, direct link, salin Markdown/HTML, dan riwayat lokal.

## Kenapa perlu Cloudinary?

Website di Vercel tidak seharusnya menyimpan gambar pengguna di folder website. Folder deployment adalah untuk aplikasi, bukan tempat penyimpanan file upload permanen. Karena itu gambar dikirim ke layanan penyimpanan supaya mendapat URL yang tetap bisa dibuka dan dibagikan setelah browser ditutup.

Cloudinary adalah tempat menyimpan file tersebut. Pengaturan dilakukan oleh pemilik website satu kali. Pengunjung tetap bisa upload sebagai guest tanpa login.

## Mengaktifkan upload (setup satu kali)

1. Buat akun Cloudinary, kemudian salin **Cloud name** dari dashboard.
2. Buat **Upload preset** baru dan pilih mode **Unsigned**.
3. Batasi preset ke format gambar yang diperlukan (JPG/JPEG, PNG, WEBP, GIF, AVIF), gunakan folder khusus, dan nonaktifkan overwrite jika tersedia. Batas 10 MB di UI saat ini divalidasi di browser dan bisa dilewati pengguna yang mengakali request; batas ukuran yang benar-benar ditegakkan perlu ditambahkan di backend.
4. Buka `config.js`, lalu isi nilainya:

   ```js
   window.UPLOADER_CONFIG = {
     cloudName: "nama-cloud-kamu",
     uploadPreset: "nama-unsigned-preset"
   };
   ```

5. Commit/push ke GitHub. Jika repo sudah terhubung ke Vercel, situs akan deploy ulang otomatis.

**Penting:** unsigned preset memungkinkan upload langsung dari browser sehingga preset dan Cloud name terlihat publik. Batasi format, gunakan folder khusus, dan awasi kuota. Batas ukuran 10 MB saat ini hanya validasi frontend, bukan perlindungan server-side. Untuk uploader publik yang lebih aman, tambahkan endpoint backend untuk menandatangani upload dan rate limit. Jangan pernah menaruh API Secret Cloudinary di `config.js` atau frontend.

## Fitur

- Tidak ada login atau registrasi untuk pengunjung.
- Upload banyak gambar, drag-and-drop, preview, dan progress upload sesungguhnya.
- Format: JPG/JPEG, PNG, WEBP, GIF, AVIF.
- Maksimum 10 MB tiap file dan 20 file per batch.
- Direct URL, Markdown, dan HTML bisa disalin dari gambar yang berhasil diunggah.
- Maksimum 12 gambar disimpan di browser saat ini, bukan akun atau galeri lintas perangkat.
- Menghapus entri riwayat hanya menghilangkan catatan lokal; file remote tidak ikut terhapus.
- Mendukung pengaturan `prefers-reduced-motion`.

## Deploy Vercel

Import repo `ItsMeMal/mallssz-uploader` di Vercel dan deploy branch `main`. Situs statis ini tidak membutuhkan build command. Upload baru berfungsi setelah konfigurasi Cloudinary diisi.
