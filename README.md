# RELAY

## Sistem Informasi Pengelolaan Pengiriman Surat, Dokumen, dan Paket pada Perusahaan Jasa Pos Relay di Wilayah Kalimantan Timur

**Project gabungan Pemrograman Berorientasi Objek (PBO) dan Sistem Basis
Data (SBD)**  
**Kelompok 6 – Program Studi Sistem Informasi, Fakultas Teknik,
Universitas Mulawarman (2026)**

------------------------------------------------------------------------

## 1. Deskripsi Project

RELAY merupakan aplikasi desktop untuk mendukung pengelolaan proses
pengiriman surat, dokumen, dan paket pada perusahaan jasa pos Relay di
wilayah Kalimantan Timur. Aplikasi dikembangkan menggunakan Java dengan
antarmuka Java Swing dan terhubung ke basis data MySQL melalui
Hibernate.

Sistem mengelola data pengguna, lokasi operasional, layanan pengiriman,
tarif wilayah, pesanan, pengiriman, dan pembayaran. Perancangan basis
data terdiri dari sembilan entitas/tabel yang saling berhubungan melalui
primary key dan foreign key.

Project ini menggabungkan penerapan konsep Pemrograman Berorientasi
Objek (PBO) pada struktur aplikasi Java dan konsep Sistem Basis Data
(SBD) pada perancangan serta pengelolaan data.

## 2. Anggota Kelompok

| No. | Nama                       | NIM        |
|-----|----------------------------|------------|
| 1   | Claudya Yusfa Ariyani      | 2509116043 |
| 2   | Aji Rifqi Suryana          | 2509116054 |
| 3   | Muhammad Dzikri Andhika    | 2509116103 |
| 4   | Farrel Fazzadinata Sumarna | 2509116111 |

**Program Studi:** Sistem Informasi  
**Fakultas:** Teknik  
**Universitas:** Universitas Mulawarman  
**Tahun:** 2026

## 3. Fitur Aplikasi

### 3.1 Fitur Pelanggan

- Registrasi akun pelanggan.
- Login menggunakan username dan password.
- Membuat pesanan pengiriman.
- Melihat riwayat pesanan.
- Mencari informasi pesanan melalui kolom pencarian pada halaman
  riwayat.
- Melihat informasi status pengiriman yang terkait dengan pesanan.
- Melihat dan memperbarui informasi akun.

### 3.2 Fitur Agen

- Login sebagai Agen.
- Melihat data pesanan dan pengiriman.
- Menambahkan data/proses pesanan melalui formulir Agen.
- Mencari data pengiriman berdasarkan nomor resi.
- Pada proses pesanan, controller memvalidasi data pesanan, berat
  barang, nomor resi, metode pembayaran, layanan, dan ketersediaan tarif
  rute.
- Logika pemrosesan pesanan menyiapkan data pengiriman dan pembayaran
  serta memperbarui data pesanan dalam satu transaksi database.

### 3.3 Peran Pusat dan Cabang

Basis data menyediakan role **Pusat**, **Cabang**, **Agen**, dan
**Pelanggan**. Controller untuk Pusat dan Cabang juga tersedia pada
source code. Namun, pada versi source code yang disertakan, alur login
antarmuka mengarahkan pengguna ke dashboard Pelanggan atau Agen; halaman
dashboard Pusat dan Cabang belum tersedia pada antarmuka aplikasi.

## 4. Penerapan Konsep PBO

### 4.1 Encapsulation

Encapsulation diterapkan dengan menggunakan atribut `private` pada class
model dan menyediakan method getter serta setter untuk mengakses atau
mengubah nilai atribut. Contohnya terdapat pada class `Pengguna`,
`Pesanan`, `Pengiriman`, `Pembayaran`, dan class model lainnya.
### Dokumentasi Penerapan Encapsulation

Konsep Encapsulation pada aplikasi RELAY diterapkan dalam class `Pengguna.java`. Atribut pengguna dideklarasikan menggunakan access modifier `private` untuk membatasi akses langsung dari luar class.

Untuk mengakses dan mengubah nilai atribut, class menyediakan method getter dan setter. Dengan penerapan ini, pengelolaan data pengguna menjadi lebih terstruktur.


**1. Penerapan Private Attribute**

<img width="450" alt="Private Attribute Pengguna.java" src="https://github.com/user-attachments/assets/51aa746a-d8f0-4e6b-82f3-7e51c0534c32" />

**2. Implementasi Getter dan Setter**

<img width="450" alt="Getter dan Setter Pengguna.java" src="https://github.com/user-attachments/assets/cbed3159-86fa-42f5-bdd5-ea2e893a2930" />


### 4.2 Inheritance

Inheritance diterapkan melalui hubungan pewarisan class:

- `LokasiOperasional` sebagai class induk.
- `Cabang` sebagai class turunan dari `LokasiOperasional`.
- `Agen` sebagai class turunan dari `LokasiOperasional`.

Pada pemetaan Hibernate, pewarisan tersebut menggunakan strategi
`InheritanceType.JOINED`, sehingga data umum lokasi disimpan pada tabel
induk dan data khusus disimpan pada tabel turunan.


**Dokumentasi Penerapan Inheritance**

Konsep Inheritance pada aplikasi RELAY diterapkan melalui class `Cabang` yang mewarisi class `LokasiOperasional` menggunakan keyword `extends`. Dengan pewarisan ini, class `Cabang` dapat menggunakan atribut dan method yang diwariskan dari class induknya serta memiliki atribut khusus seperti `kodeCabang`, `namaAdminCabang`, dan `statusOperasional`.

**1. Implementasi Inheritance pada Cabang.java**

<img width="434" height="260" alt="Screenshot 2026-11-06 114143" src="https://github.com/user-attachments/assets/12e9c48d-83e4-410d-94f7-79c4dae42cc3" />





### 4.3 Abstraction

Abstraction diterapkan melalui interface generik `Repository<T>` yang
mendefinisikan operasi dasar penyimpanan data, yaitu:

- `tambah(T data)`
- `ubah(T data)`
- `tampilkanSemua()`

Interface ini menjadi kontrak bagi class DAO yang mengelola data
masing-masing entitas.

**Dokumentasi Penerapan Abstraction**

Konsep Abstraction pada aplikasi RELAY diterapkan melalui interface `Repository<T>` yang mendefinisikan operasi dasar pengelolaan data, yaitu `tambah()`, `ubah()`, dan `tampilkanSemua()`.

Interface ini hanya menentukan method yang harus disediakan, sedangkan implementasinya dilakukan oleh class DAO seperti `PengirimanDAO`, `PesananDAO`, dan `PenggunaDAO`. Dengan demikian, proses pengelolaan data memiliki struktur yang konsisten.

**1. Implementasi Abstraction pada Repository.java**

<img width="274" height="111" alt="Screenshot 2026-11-06 114851" src="https://github.com/user-attachments/assets/39f4aa3b-7de1-485c-b604-9c2cd47c4f8a" />


### 4.4 Polymorphism

Polymorphism diterapkan melalui implementasi interface `Repository<T>`
oleh beberapa class DAO, seperti `PenggunaDAO`, `PesananDAO`,
`PengirimanDAO`, `PembayaranDAO`, `LayananDAO`, `LokasiDAO`, dan
`TarifWilayahDAO`. Setiap DAO menyediakan implementasi operasi
repository sesuai jenis data yang dikelolanya.


**Dokumentasi Penerapan Polymorphism**

Konsep Polymorphism pada aplikasi RELAY didukung oleh penggunaan interface `Repository<T>` yang diimplementasikan oleh berbagai class DAO, seperti `PengirimanDAO`, `PesananDAO`, dan `PenggunaDAO`.

Setiap class DAO menyediakan implementasi method yang sama, seperti `tambah()`, `ubah()`, dan `tampilkanSemua()`, tetapi bekerja dengan jenis entitas yang berbeda. Melalui interface `Repository<T>`, objek DAO dapat digunakan melalui tipe interface yang sama.

**1. Implementasi Polymorphism pada PengirimanDAO.java**

<img width="436" height="260" alt="Screenshot 2026-11-06 122653" src="https://github.com/user-attachments/assets/98e62c78-a7c4-4fe0-8e95-6d63d56cda94" />




## 5. Arsitektur dan Struktur Package

Aplikasi memisahkan tanggung jawab program ke dalam beberapa package:

**Dokumentasi Struktur Package Aplikasi RELAY**

<img width="350" alt="Screenshot 2026-11-06 112528" src="https://github.com/user-attachments/assets/33eb338c-6be4-4926-88f2-f1cdc85f3eb4" />

Keterangan package:

| Package      | Fungsi                                                                           |
|--------------|----------------------------------------------------------------------------------|
| `model`      | Menyimpan class entitas yang merepresentasikan data aplikasi dan tabel database. |
| `view`       | Menyediakan antarmuka pengguna menggunakan Java Swing.                           |
| `controller` | Mengatur alur proses antara tampilan dan pengolahan data.                        |
| `dao`        | Menangani operasi akses dan manipulasi data menggunakan Hibernate.               |
| `config`     | Menyediakan konfigurasi Hibernate dan pengelolaan sesi pengguna.                 |
| `main`       | Menyediakan titik awal untuk menjalankan aplikasi.                               |
### 5.1 Main Class (`Main.java`)

Class `Main` merupakan titik awal (*entry point*) ketika aplikasi RELAY dijalankan. Class ini bertanggung jawab untuk menginisialisasi kebutuhan awal aplikasi sebelum menampilkan halaman login.

Pada class ini terdapat beberapa proses utama:

1. **Pengaturan Tampilan:** Mengatur Look and Feel menggunakan Nimbus agar tampilan aplikasi lebih menarik.
2. **Inisialisasi Database:** Memanggil `HibernateUtil.getSessionFactory()` untuk menginisialisasi SessionFactory Hibernate.
3. **Menampilkan Halaman Login:** Membuat objek `LoginView` sebagai halaman awal aplikasi.
4. **Pengaturan Posisi Tampilan:** Menggunakan `setLocationRelativeTo(null)` agar jendela login muncul di tengah layar.
5. **Penanganan Kesalahan:** Menggunakan `try-catch` untuk menangani kesalahan ketika proses inisialisasi aplikasi berlangsung.

**Dokumentasi Source Code Main.java**

<img width="463" height="240" alt="Screenshot 2026-11-06 122000" src="https://github.com/user-attachments/assets/4b587899-fc0e-401a-a287-9432a15f307c" />



### 5.2 Repository Interface (`Repository.java`)
Interface `Repository<T>` merupakan komponen yang digunakan sebagai dasar pengelolaan akses data pada aplikasi RELAY. Interface ini menggunakan konsep generics sehingga dapat diterapkan pada berbagai jenis objek tanpa harus membuat struktur interface yang berbeda untuk setiap entitas.

Pada interface ini terdapat tiga method utama:
1. **tambah(T data):** Mendefinisikan operasi untuk menambahkan data baru ke dalam sistem.
2. **ubah(T data):** Mendefinisikan operasi untuk memperbarui data yang sudah tersedia.
3. **tampilkanSemua():** Mendefinisikan operasi untuk mengambil seluruh data dalam bentuk `List<T>`.
**Konsep Pemrograman Berorientasi Objek:**
- **Abstraction:** Memisahkan definisi operasi pengelolaan data dari detail implementasinya.
- **Generics:** Memungkinkan interface digunakan oleh berbagai tipe objek sehingga struktur kode lebih fleksibel dan dapat digunakan kembali.

**Dokumentasi Source Code Repository.java**

<img width="469" height="110" alt="Screenshot 2026-11-06 122151" src="https://github.com/user-attachments/assets/c5975e25-a873-4df4-ba88-381cfb3d56a6" />


### 5.3 Data Access Object (`PengirimanDAO.java`)
Class `PengirimanDAO` merupakan bagian dari Data Access Object (DAO) yang bertugas mengelola proses akses dan manipulasi data pengiriman pada database. Class ini mengimplementasikan interface `Repository<Pengiriman>` dan menggunakan Hibernate untuk menjalankan operasi database.

Pada class ini terdapat beberapa proses utama:

1. **Penambahan Data:** Menggunakan method `tambah()` dengan `session.persist()` untuk menyimpan data pengiriman baru ke database.
2. **Perubahan Data:** Menggunakan method `ubah()` dengan `session.merge()` untuk memperbarui data pengiriman yang sudah tersimpan.
3. **Pencarian Data:** Menggunakan method `cariBerdasarkanResi()` untuk mencari data pengiriman berdasarkan nomor resi.
4. **Menampilkan Data:** Menggunakan method `tampilkanSemua()` untuk mengambil seluruh data pengiriman berdasarkan tanggal pengiriman terbaru.
5. **Filter Data:** Menyediakan method untuk menampilkan data berdasarkan cabang, agen, dan status pengiriman menggunakan Hibernate Query Language (HQL).
6. **Penghapusan Data:** Menggunakan method `hapus()` dengan `session.remove()` untuk menghapus data pengiriman berdasarkan nomor resi.
7. **Pengelolaan Transaksi:** Menggunakan `commit()` untuk menyimpan perubahan dan `rollback()` untuk membatalkan transaksi apabila terjadi kesalahan.

**Dokumentasi Source Code PengirimanDAO.java**

**1. Implementasi Repository dan Penambahan Data**

<img width="451" height="262" alt="Screenshot 2026-11-06 122257" src="https://github.com/user-attachments/assets/9a208d6d-ed30-4155-98d3-09504dd1c977" />

**2. Penghapusan Data dan Pengelolaan Transaksi**

<img width="430" height="229" alt="Screenshot 2026-11-06 122424" src="https://github.com/user-attachments/assets/27e5ce58-95a7-4740-a01e-87a3f89661a6" />

### 5.4 Ringkasan Implementasi DAO

Selain PengirimanDAO, aplikasi RELAY juga memiliki beberapa
class DAO yang digunakan untuk mengelola data pada database
menggunakan Hibernate.

Class DAO yang digunakan meliputi:

1. **PesananDAO:** Mengelola data pesanan pelanggan.
2. **PenggunaDAO:** Mengelola data pengguna dan proses autentikasi.
3. **LayananDAO:** Mengelola data layanan pengiriman.
4. **LokasiDAO:** Mengelola data lokasi operasional, cabang, dan agen.
5. **PembayaranDAO:** Mengelola data transaksi pembayaran.
6. **TarifWilayahDAO:** Mengelola tarif pengiriman berdasarkan wilayah.

Setiap class DAO memiliki fungsi pengelolaan data sesuai
dengan entitas masing-masing melalui Hibernate.





## 6. Perancangan Basis Data

Database yang digunakan bernama **`relay`** dan terdiri dari sembilan
tabel berikut.

| No. | Tabel                | Fungsi                                                                                        |
|-----|----------------------|-----------------------------------------------------------------------------------------------|
| 1   | `lokasi_operasional` | Menyimpan informasi umum lokasi operasional Cabang dan Agen.                                  |
| 2   | `cabang`             | Menyimpan informasi khusus kantor Cabang.                                                     |
| 3   | `agen`               | Menyimpan informasi khusus Agen dan hubungan Agen dengan Cabang induk.                        |
| 4   | `pengguna`           | Menyimpan akun, username, password, role, dan keterkaitan lokasi pengguna.                    |
| 5   | `layanan`            | Menyimpan pilihan layanan, tarif dasar, estimasi waktu, dan status layanan.                   |
| 6   | `tarif_wilayah`      | Menyimpan tarif pengiriman berdasarkan kota asal, kota tujuan, dan layanan.                   |
| 7   | `pesanan`            | Menyimpan data pengirim, penerima, jenis kiriman, berat, biaya, dan status pesanan.           |
| 8   | `pengiriman`         | Menyimpan nomor resi, tanggal, status pengiriman, bukti dokumentasi, dan keterkaitan pesanan. |
| 9   | `pembayaran`         | Menyimpan metode, jumlah, status, dan tanggal pembayaran.                                     |

### 6.1 Relasi dan Kunci

Basis data menggunakan primary key (PK), foreign key (FK), unique
constraint, dan composite key untuk menjaga keterkaitan serta integritas
data.

Salah satu penerapan supertype dan subtype adalah:

- `lokasi_operasional` sebagai supertype.
- `cabang` sebagai subtype.
- `agen` sebagai subtype.

Tabel `pesanan` menggunakan primary key gabungan (`id_pesanan`,
`pengguna_id_pengguna`). Tabel `pengiriman` menghubungkan pesanan dengan
tarif wilayah, Agen, dan Cabang. Tabel `pembayaran` terhubung dengan
data pengguna dan pengiriman.

### 6.2 Penerapan SQL

Pada laporan SBD, penerapan query mencakup:

- Data Definition Language (DDL): `CREATE` dan `ALTER`.
- Data Manipulation Language (DML): `INSERT` dan `UPDATE`.
- SELECT tingkat lanjut: `IN`, `NOT IN`, `EXISTS`, `NOT EXISTS`, `ANY`,
  `ALL`, `UNION`, `UNION ALL`, `GROUP BY`, `HAVING`, fungsi agregat,
  `LIKE`, dan `REGEXP`.
- Data Control Language (DCL): `GRANT` dan `REVOKE`.
- Transaction Control Language (TCL): `START TRANSACTION`, `SAVEPOINT`,
  `ROLLBACK`, dan `COMMIT`.
- JOIN tingkat lanjut: `INNER JOIN`, `LEFT JOIN`, `EQUI JOIN`,
  `NON-EQUI JOIN`, `SELF JOIN`, `NATURAL JOIN`, `SEMI JOIN`, dan
  `ANTI JOIN`.

## 7. Teknologi dan Tools

| Teknologi/Tools               | Kegunaan                                                               |
|-------------------------------|------------------------------------------------------------------------|
| Java 17                       | Bahasa pemrograman aplikasi.                                           |
| Java Swing                    | Pembuatan antarmuka desktop.                                           |
| Apache Maven                  | Pengelolaan project dan dependency.                                    |
| MySQL                         | Sistem manajemen basis data relasional.                                |
| Hibernate ORM 6.6.15.Final    | Pemetaan objek Java ke tabel database dan pengelolaan persistensi.     |
| Jakarta Persistence API 3.1.0 | Anotasi dan standar pemetaan entitas.                                  |
| MySQL Connector/J 9.2.0       | Konektor Java ke MySQL.                                                |
| NetBeans GUI Builder          | File form `.form` disertakan bersama source code untuk tampilan Swing. |

## 8. Persiapan dan Instalasi

Pastikan perangkat telah memiliki:

- JDK 17.
- MySQL Server 8.x.
- Apache Maven.
- IDE Java yang mendukung project Maven dan Java Swing (NetBeans dapat
  digunakan).

### 8.1 Menyiapkan Database

1.  Jalankan MySQL Server.
2.  Buat database dengan nama `relay`:

``` sql
CREATE DATABASE relay;
```

3.  Pilih database `relay`, kemudian impor file `relay.sql` yang
    tersedia pada repository.

Alternatif melalui terminal:

``` bash
mysql -u root -p relay < relay.sql
```

### 8.2 Mengatur Koneksi Database

Buka file:

``` text
src/main/resources/hibernate.cfg.xml
```

Sesuaikan konfigurasi koneksi dengan MySQL lokal:

``` xml
<property name="hibernate.connection.driver_class">
    com.mysql.cj.jdbc.Driver
</property>

<property name="hibernate.connection.url">
    jdbc:mysql://localhost:3306/relay?useSSL=false&amp;serverTimezone=Asia/Jakarta
</property>

<property name="hibernate.connection.username">root</property>
<property name="hibernate.connection.password">ISI_PASSWORD_MYSQL</property>
```

Ganti username dan password sesuai konfigurasi MySQL pada perangkat
masing-masing. Jangan mengunggah password pribadi atau kredensial
database yang digunakan pada lingkungan nyata ke repository publik.

Konfigurasi `hibernate.hbm2ddl.auto` pada project menggunakan nilai
`validate`. Artinya, tabel database harus sudah tersedia dan sesuai
dengan pemetaan entitas; Hibernate tidak membuat tabel secara otomatis.

### 8.3 Menjalankan Aplikasi

1.  Buka folder project `Relay-Kel6` sebagai project Maven di IDE.
2.  Pastikan dependency Maven berhasil dimuat.
3.  Pastikan MySQL aktif dan database `relay` sudah diimpor.
4.  Pastikan konfigurasi pada `hibernate.cfg.xml` sudah sesuai.
5.  Jalankan class utama:

``` text
main.Main
```

6.  Jika koneksi berhasil, aplikasi akan menampilkan halaman Login
    RELAY.

## 9. Alur Penggunaan Aplikasi

### 9.1 Pelanggan

1.  Buka aplikasi RELAY.
2.  Pilih menu registrasi untuk membuat akun pelanggan jika belum
    memiliki akun.
3.  Login menggunakan username dan password.
4.  Masuk ke dashboard Pelanggan.
5.  Pilih menu **Buat Pesanan**.
6.  Isi informasi pengirim, penerima, jenis kiriman, kota tujuan, dan
    layanan.
7.  Simpan pesanan.
8.  Buka menu **Riwayat Pesanan** untuk melihat data pesanan.
9.  Gunakan menu **Kelola Akun** untuk memperbarui informasi akun.

### 9.2 Agen

1.  Login menggunakan akun dengan role Agen.
2.  Masuk ke dashboard Agen.
3.  Gunakan menu **Tambah Data Pesanan** untuk memproses pesanan
    pelanggan.
4.  Isi data yang diperlukan, termasuk berat barang dan metode
    pembayaran.
5.  Gunakan menu **Tampilkan Data Pesanan** untuk melihat data
    pengiriman.
6.  Gunakan pencarian untuk menemukan data berdasarkan nomor resi.

## 10. Catatan Implementasi

- Role Pusat dan Cabang sudah tersedia pada rancangan basis data serta
  memiliki class controller, tetapi halaman dashboard untuk kedua role
  tersebut belum tersedia pada versi antarmuka yang disertakan.
- Beberapa tombol pada dashboard Agen, seperti penghapusan, perubahan
  pesanan, dan penerimaan barang dari Cabang, belum dihubungkan ke
  proses aktif pada antarmuka.
- Sebelum menguji proses transaksi pengiriman, pastikan nilai status
  pengiriman yang dikirim oleh aplikasi sesuai dengan nilai `ENUM` pada
  tabel `pengiriman` di MySQL. Pada source code saat ini terdapat nilai
  status yang perlu diselaraskan.

## 11. Keamanan dan Penggunaan Data

File SQL yang disertakan memuat data contoh pengguna untuk kebutuhan
pengujian. Ganti kredensial contoh sebelum digunakan di lingkungan
nyata. Untuk pengembangan lebih lanjut, penyimpanan password sebaiknya
menggunakan mekanisme hashing dan bukan teks biasa.

------------------------------------------------------------------------

**RELAY – Your Delivery Partner!**  
Project Kelompok 6  
Program Studi Sistem Informasi, Fakultas Teknik  
Universitas Mulawarman – 2026
