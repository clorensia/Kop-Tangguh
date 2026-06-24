# JALA-TANGGUH

## Platform Agregasi Rantai Pasok Dingin dan Mitigasi Krisis Pangan Berbasis Koperasi

**Kompetisi:** Hackathon Digital Cooperatives Expo 2026  
**Instansi:** Kementerian Koperasi Republik Indonesia  
**Pilar:** Pemanfaatan Potensi Ekonomi Desa  

---

## 1. Ringkasan Eksekutif

JALA-TANGGUH adalah sistem informasi manajemen rantai pasok yang dirancang untuk mengoptimalkan distribusi komoditas pangan mudah rusak (*perishable*) di tingkat koperasi. Sistem ini memfasilitasi mekanisme berbagi aset logistik rantai dingin (*cold-chain sharing economy*) antar-koperasi untuk mencegah kehilangan hasil panen (*food loss*) dan menstabilkan harga pangan selama krisis iklim.

---

## 2. Latar Belakang Masalah

Krisis iklim El Nino menyebabkan penurunan signifikan pada hasil tangkapan laut dan pertanian terbuka, yang memicu kelangkaan komoditas pangan strategis. Permasalahan utama yang dihadapi oleh jaringan koperasi adalah sebagai berikut:

1. **Fragmentasi Data:** Tidak adanya sistem terpusat yang memetakan kondisi surplus dan defisit pangan antarwilayah secara waktu nyata.
2. **Inefisiensi Logistik:** Aset rantai dingin seperti truk pendingin dan gudang pendingin sering menganggur, sementara komoditas di wilayah lain membusuk akibat ketiadaan akses logistik.
3. **Absennya Mekanisme Gotong Royong:** Koperasi tidak memiliki platform digital untuk saling membantu distribusi saat terjadi krisis pasokan.

---

## 3. Solusi yang Ditawarkan

JALA-TANGGUH menyediakan antarmuka manajemen B2B antar-koperasi dengan tiga fungsi utama:

1. **Dashboard Ketahanan Pangan:** Visualisasi data waktu nyata mengenai surplus dan defisit komoditas pemicu inflasi.
2. **Berbagi Aset Rantai Dingin:** Sistem pencocokan (*matching*) yang menghubungkan koperasi dengan surplus komoditas dan koperasi yang memiliki aset logistik dingin menganggur atau melakukan perjalanan kosong (*empty backhaul*).
3. **Agregasi Pasokan Alternatif:** Integrasi data hasil panen dari koperasi hidroponik dan akuakultur sebagai pasokan penyangga saat produksi tradisional gagal akibat cuaca ekstrem.

---

## 4. Arsitektur dan Teknologi

Proyek ini dikembangkan menggunakan pendekatan *no-code* dan *low-code* untuk memastikan efisiensi biaya dan kecepatan pengembangan.

* **Database:** Airtable (Relational Database Management)
* **Antarmuka Pengguna:** Airtable Forms dan Interface Designer
* **Otomasi Data:** Google Apps Script (GAS)
* **Analitik Lanjutan:** Google Looker Studio

---

## 5. Skema Database

Sistem ini terdiri dari lima tabel relasional utama.

### 5.1. Data_Koperasi
Menyimpan data master koperasi anggota jaringan.

| Nama Field | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| Nama_Koperasi | Text | Nama resmi koperasi |
| Lokasi | Text | Kabupaten atau kota domisili |
| Kategori | Single Select | Nelayan Laut, Tani Hortikultura, Hidroponik/Akuakultur, Logistik |
| Nama_Admin | Text | Nama pengurus atau administrator |
| No_WA_Admin | Phone | Nomor WhatsApp untuk notifikasi |

### 5.2. Katalog_Komoditas
Menyimpan data master komoditas pangan yang dipantau.

| Nama Field | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| Nama_Komoditas | Text | Nama komoditas |
| Karakteristik | Single Select | Perlu Rantai Dingin, Perlu Sirkulasi Udara |
| Batas_Waktu_Panen | Text | Daya simpan optimal pasca panen |
| Deskripsi_Komoditas | Long Text | Deskripsi detail komoditas |
| AI_Tag_Resiko_Kerusakan | Single Select | Rendah, Sedang, Tinggi |

### 5.3. Stok_Realtime
Data stok harian yang menjadi inti sistem monitoring.

| Nama Field | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| Link_Koperasi | Link | Relasi ke Data_Koperasi |
| Link_Komoditas | Link | Relasi ke Katalog_Komoditas |
| Status_Stok | Single Select | Tersedia, Hampir Habis, Habis |
| Jumlah_KG | Number | Berat atau volume stok |
| Tanggal_Input | Date | Tanggal pelaporan |
| Catatan_Stok | Long Text | Keterangan kondisi |
| AI_Urgency_Salvage | Single Select | Normal, Tinggi, Kritis |
| Status_Pasar | Single Select | SURPLUS, DEFISIT |

### 5.4. Aset_Logistik_Dingin
Inventarisasi aset logistik rantai dingin.

| Nama Field | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| Link_Pemilik_Aset | Link | Relasi ke Data_Koperasi |
| Jenis_Aset | Single Select | Truk Pendingin, Cold Storage Statis, Kapal Ber-AC |
| Kapasitas_Ton | Number | Kapasitas angkut atau penyimpanan |
| Status_Aset | Single Select | Aktif, Tidak Aktif, Dalam Perbaikan, Menganggur, Dalam Perjalanan Kosong |
| Rute_Tersedia | Text | Rute operasional |
| Tanggal_Tersedia | Date | Ketersediaan aset |
| Catatan_Perawatan | Long Text | Riwayat pemeliharaan |
| AI_Asset_Optimal_Use | Single Select | Optimal, Suboptimal |

### 5.5. Matching_Transaksi
Riwayat transaksi distribusi dan penyelamatan komoditas.

| Nama Field | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| Koperasi_Pengirim | Link | Relasi ke Data_Koperasi |
| Koperasi_Penerima | Link | Relasi ke Data_Koperasi |
| Aset_Logistik_Dipakai | Link | Relasi ke Aset_Logistik_Dingin |
| Status_Kiriman | Single Select | Menunggu Jemput, Dalam Perjalanan, Berhasil Diselamatkan, Gagal |
| Tanggal_Transaksi | Date | Tanggal transaksi |
| Estimasi_Waktu_Tiba | Date | Estimasi kedatangan |
| AI_Transaction_Risk | Single Select | Rendah, Sedang, Tinggi, Kritis |

---

## 6. Panduan Replikasi

Untuk mereplikasi sistem ini secara lokal, ikuti langkah-langkah berikut:

### Opsi 1: Import melalui CSV
1. Klon repositori ini.
2. Buka folder `/data_csv`.
3. Impor file CSV secara berurutan ke Airtable: `Data_Koperasi`, `Katalog_Komoditas`, `Aset_Logistik_Dingin`, `Stok_Realtime`, dan `Matching_Transaksi`.
4. Pastikan untuk mengubah kolom "Link" menjadi tipe **Link to another record** sesuai dengan relasi yang telah ditentukan pada skema database.

### Opsi 2: Generate melalui Google Apps Script
1. Buka Google Sheets baru, lalu navigasi ke **Extensions** > **Apps Script**.
2. Salin dan tempel skrip dari file `generate_data.js` yang tersedia di repositori ini.
3. Jalankan fungsi `generateHackathonData()`.
4. Ekspor lembar kerja ke format CSV dan impor ke Airtable.

---

## 7. Skenario Data Uji

Basis data ini telah diisi dengan data dummy yang mensimulasikan kondisi nyata di lapangan untuk keperluan demonstrasi:

* **Skenario Sukses:** Transaksi berhasil diselamatkan, penggunaan aset logistik optimal.
* **Skenario Krisis (El Nino):** Gagal panen total, hasil tangkap turun drastis, dan gudang pendingin rusak.
* **Skenario Kegagalan Logistik:** Transaksi gagal akibat cold storage penuh, truk rusak, atau keterlambatan distribusi.
* **Skenario Optimasi Aset:** Pemanfaatan truk dalam perjalanan kosong (*empty backhaul*) untuk efisiensi logistik.

---

## 8. Kontributor

Proyek ini dikembangkan untuk Hackathon Digital Cooperatives Expo 2026 oleh:

* **[Nama Anda]** - Product and Data Lead (Arsitektur Database, Dashboard Data Science, Skrip GAS)
* **[Nama Rekan Anda]** - UI/UX and Business Lead (Desain Antarmuka, Presentasi, Business Model Canvas)

---

## 9. Lisensi

Proyek ini bersifat *open-source* untuk keperluan edukasi dan kompetisi hackathon.
