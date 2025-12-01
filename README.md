📌 Isi & Fitur Utama Website
1. Sistem Login Dua Peran

Admin (username + password)

Pengguna/Viewer (akses instan tanpa password)
Setiap peran menentukan hak akses dalam aplikasi.

2. Dashboard Ringkasan Arsip

Menampilkan:

Total arsip, berkas, dan boks per menu

Rekap tahunan global dari seluruh modul

Statistik otomatis dari data yang tersimpan di IndexedDB

3. Modul-Manajemen Arsip

Setiap modul berfungsi untuk mencatat, mengedit, dan melihat data arsip.
Daftar modul yang tersedia:

Jumlah Arsip Statis

Rekap Arsip SIKN

Pemusnahan Arsip

Arsip Permanen

Penyelamatan Bencana

SKPD Digabung

SKPD Dibubarkan

Alih Media

Penerbitan Izin

Arsip Vital

Setiap modul memiliki fields:

Pencipta Arsip

Uraian Arsip

Tahun

Jumlah Arsip

Jumlah Berkas

Jumlah Boks

Tautan Google Drive (bukti dukung)

4. Manipulasi Data

Admin dapat:

Menambah

Mengedit

Menghapus
Pengguna hanya dapat melihat data.

Data tersimpan otomatis di:

IndexedDB (browser storage)
yang aman dan tetap tersedia meskipun halaman di-refresh.

5. Antarmuka Modern & Responsif

Menggunakan gaya desain modern (glassmorphism + gradient)

Sidebar interaktif

Tampilan dashboard yang dinamis

Modal editing data

Kompatibel desktop & mobile

📄 Struktur File Utama

index.html / amanda - Data Arsip Statis V.3.2.1.html
Berisi seluruh kode HTML, CSS, dan JavaScript aplikasi.

Aplikasi ini tidak membutuhkan file tambahan lain untuk berjalan.

💡 Tujuan Aplikasi

Aplikasi ini dibuat untuk mempermudah:

Pengelolaan data arsip statis

Rekapitulasi tahunan

Pelaporan kegiatan kearsipan

Penyimpanan bukti dukung digital

Monitoring data oleh admin dan viewer
