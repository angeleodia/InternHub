# InternHub

Monorepo untuk Sistem Informasi Pengelolaan Peserta Magang.

## Struktur

```text
apps/
  api/      NestJS backend
packages/
  shared/   Shared types/constants untuk FE dan BE
PRD.md      Product requirements
```

## Perintah Utama

```bash
npm install --include=dev
npm run prisma:generate
npm run dev:web
npm run dev:api
npm run build
```

Frontend berada di `apps/web`, backend berada di `apps/api`.

## Backend + Database

Backend menggunakan NestJS + Prisma + MySQL. Untuk kebutuhan skripsi, autentikasi dibuat sederhana dan fokus pada fungsi CRUD, penugasan (tugas & sub-tugas yang di-assign mentor + laporan progres peserta), absensi, logbook harian, evaluasi, nilai akhir, dan ranking.

Alur inti: mentor membuat & meng-assign **tugas** (lengkap dengan sub-tugas, tanggal mulai, dan deadline) ke peserta. Peserta melaporkan **progres** sebagai bukti penyelesaian (ringkasan rich text + unggah banyak lampiran/tautan). Hanya mentor yang dapat mengubah status penyelesaian, memberi feedback, dan menilai. Nilai tugas menjadi komponen 30% nilai akhir.

> Catatan: setelah menarik perubahan ini, jalankan `npm run db:push` (membuat tabel `tasks`, `subtasks`, `task_progress`, `task_attachments`) lalu `npm run db:seed` untuk data demo tugas.

1. Buat database MySQL:

```sql
CREATE DATABASE internhub;
```

2. Atur `DATABASE_URL` sesuai MySQL lokal. Contoh ada di `apps/api/.env.example`.

3. Push schema dan isi data demo:

```bash
npm run db:push
npm run db:seed
```

4. Jalankan API:

```bash
npm run dev:api
```

Base URL API lokal: `http://localhost:3000/api`.

## Frontend

Frontend membaca data dari backend melalui `VITE_API_URL`. Contoh konfigurasi ada di `apps/web/.env.example`.
