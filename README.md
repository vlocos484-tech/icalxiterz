# ICALXMODZ Premium Panel

Website panel Next.js full-stack + PostgreSQL dengan tema hitam-merah/oranye, logo ninja, dashboard owner dan reseller.

## Fitur
- Login dengan password bcrypt, JWT session di cookie HttpOnly, role checks server-side.
- Dashboard owner/reseller terpisah.
- Generator dan daftar license key: masa aktif, max device, harga.
- Reseller mengajukan top-up manual; saldo hanya bertambah setelah owner menyetujui.
- Transfer saldo hanya oleh owner, memakai transaksi database.
- Owner dapat membuat dan menonaktifkan reseller.
- Link pendaftaran reseller pada halaman login mengarah ke `https://t.me/icalxmodz`.

## Deploy dari Android
1. Buat PostgreSQL database di Neon (neon.tech), salin connection string.
2. Di Neon SQL Editor, jalankan isi `database/schema.sql`.
3. Upload folder project ke GitHub (jangan upload `.env`), lalu import repository di Vercel.
4. Vercel → Project → Settings → Environment Variables: isi `DATABASE_URL` dan `AUTH_SECRET` (string acak panjang, minimal 32 karakter). Deploy.
5. Buat owner pertama dengan menjalankan `npm run seed:owner` dari terminal yang memiliki akses database dan environment variables `DATABASE_URL`, `OWNER_EMAIL`, `OWNER_PASSWORD`. Bisa lewat Termux/Node.js atau GitHub Codespaces.
6. Login memakai email dan password owner, lalu buat akun reseller di menu Manajemen Reseller.

## Setup database via terminal
Set `DATABASE_URL`, lalu jalankan `npm run db:setup`.
Seed owner bukan endpoint publik dan tidak berjalan otomatis di Vercel. Jalankan seed satu kali dari terminal aman.

## Catatan
- `0 hari` berarti permanen.
- Panel ini menyimpan dan mengelola key; validasi key oleh aplikasi eksternal membutuhkan endpoint/API integrasi terpisah.
- Periksa schema dan environment variables sebelum production. Jangan bagikan kredensial owner.
