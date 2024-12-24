# Final Project OS Server Dan Admin

## Nama : Muhammad Rafi Wibowo
## NIM : 23.83.0966

## **1. Deskripsi**
Sistem manajemen cafe berbasis web untuk mencatat pemasukan dan pengeluaran cafe menggunakan Ubuntu Server.

OS : [ubuntu-22.04.5-live-server-amd64.iso](https://releases.ubuntu.com/jammy/ubuntu-22.04.5-live-server-amd64.iso)


## **2. Struktur Direktori Proyek**

Berikut adalah struktur direktori proyek:

```
/cafe-management-system/
├── index.php                  # Halaman utama (frontend)
├── includes/                  # Folder untuk file konfigurasi dan fungsi backend
│   ├── config.php             # Konfigurasi koneksi database
│   ├── functions.php          # Fungsi CRUD dan laporan
│   ├── income_api.php         # API untuk pemasukan (CRUD)
│   ├── expense_api.php        # API untuk pengeluaran (CRUD)
├── assets/                    # Folder untuk aset frontend (CSS, JS, gambar)
│   ├── css/
│   │   ├── style.css          # File CSS tambahan untuk styling
│   ├── js/
│   │   ├── script.js          # File JavaScript untuk interaksi frontend
│   ├── images/
│       ├── logo.png           # Logo kafe atau gambar lain
├── sql/                       # Folder untuk file SQL
└────── database-config.sql    # Skrip untuk membuat tabel dan data awal
```

---

## **3. Prasyarat Sistem**

### Komponen Sistem
Sistem ini menggunakan beberapa layanan server:
1. Apache2 - Web Server
2. MySQL - Database Server
3. PHP - Backend Programming
4. vsftpd - FTP Server
5. BIND9 - DNS Server

### Operating System
- Ubuntu Server 22.04 LTS
- RAM minimal 2GB
- Storage minimal 20GB
- Koneksi internet untuk instalasi paket
- Port yang perlu dibuka:
  - 80 (HTTP)
  - 443 (HTTPS)
  - 21 (FTP)
  - 53 (DNS)
  - 3306 (MySQL)
---

## **4. Instalasi Proyek**

### **4.1 Instalasi Web Server, Database, dan PHP**
Untuk sistem berbasis Linux (Ubuntu), jalankan perintah berikut:

```bash
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl start mysql
sudo systemctl enable mysql
```

### **4.2 Import Database**
1. Buka terminal MySQL:
   ```bash
   mysql -u root -p
   ```
2. Buat database baru:
   ```sql
   CREATE DATABASE cafe_management;
   ```
3. Import tabel dan data awal dari file `database-config.sql`:
   ```bash
   mysql -u root -p cafe_management < sql/database-config.sql
   ```

Skrip SQL akan membuat tabel berikut:
- **pemasukan**: Menyimpan data pemasukan harian.
- **pengeluaran**: Menyimpan data pengeluaran harian.

---

### **4.3 Konfigurasi Koneksi Database**
Edit file `includes/config.php` dan sesuaikan kredensial database:

```php
<?php
$db_host = 'localhost';
$db_user = 'cafeman';
$db_pass = 'password';
$db_name = 'cafe_management';

$conn = mysqli_connect($db_host, $db_user, $db_pass, $db_name);

if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
?>
```

---

### **4.4 Konfigurasi FTP Server**
Jika Anda menggunakan **FTP Server** untuk mengelola file:

1. Install **vsftpd**:
   ```bash
   sudo apt install vsftpd -y
   ```
2. Buat pengguna FTP dan berikan akses ke direktori proyek:
   ```bash
   sudo adduser ftpuser
   sudo chown -R ftpuser:www-data /var/www/html/cafe-management-system
   sudo chmod -R 755 /var/www/html/cafe-management-system
   ```

---

### **4.5 Konfigurasi DNS Server (Opsional)**
Jika Anda ingin mengakses aplikasi menggunakan domain seperti `cafe-management.local`:

1. Install **BIND9**:
   ```bash
   sudo apt install bind9 bind9utils -y
   ```
2. Tambahkan zona baru:
   - File: `/etc/bind/named.conf.local`
     ```apache
     zone "cafe-management.local" {
         type master;
         file "/etc/bind/db.cafe-management.local";
     };
     ```
3. Buat file zona:
   - File: `/etc/bind/db.cafe-management.local`
     ```
     @       IN      A       192.168.1.10
     ns      IN      A       192.168.1.10
     ```

---

## **5. Panduan Penggunaan**

Restart Apache dan MySQL Setelah menyiapkan semuanya, restart layanan web dan database:

```
sudo systemctl restart apache2
sudo systemctl restart mysql
```

### Akses Aplikasi di Browser

Buka browser dan akses aplikasi melalui URL:
```
http://localhost/cafe-management-system/index.php
```


### Tampilan Web
![Screenshot 2024-12-17 015136](https://github.com/user-attachments/assets/52d37b56-f66b-46c8-b726-2ec77a309a0e)

### FTP Server
![Screenshot 2024-12-17 015044](https://github.com/user-attachments/assets/ac91f1ce-8849-4717-9d8b-eba0b57b5c9a)

