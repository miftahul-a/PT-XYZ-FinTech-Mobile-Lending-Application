# PT XYZ FinTech — Mobile Lending Application
## Solution Analyst Technical Test Submission

> **Tech Stack:** Enterprise Microservices, Cloud Native, Event-Driven (Kafka), PostgreSQL, Kubernetes

**Disusun oleh:** Miftahul Arifin
**Role:** Business Analyst | System Analyst | Solution Analyst
**Email:** miftahularifin.id@gmail.com

---

## Ringkasan Eksekutif

PT XYZ adalah perusahaan fintech yang ingin mengembangkan aplikasi **pinjaman online (mobile lending)** untuk menjangkau pengguna yang lebih luas. Dokumen ini berisi rancangan solusi end-to-end — mulai dari arsitektur sistem, alur layar, struktur data, desain API, hingga perilaku screen — yang disusun untuk menjawab seluruh poin pada *Technical Test Solution Analyst*.

**Batasan bisnis utama yang menjadi dasar rancangan:**
- Registrasi memerlukan data diri, email, nomor telepon, serta upload foto & KTP (proses KYC)
- Login dapat menggunakan password atau biometric (jika tersedia di perangkat)
- User dapat melihat sisa hutang dan tagihan bulanan
- Limit pinjaman maksimal **Rp 12.000.000** dengan tenor maksimal **12 bulan**
- Hasil pengajuan: **Disetujui** atau **Ditolak**, dengan notifikasi via email & SMS jika disetujui
- **1 user hanya dapat memiliki 1 pinjaman aktif** — pengajuan baru diblokir selama pinjaman sebelumnya belum lunas

---

## Struktur Dokumen