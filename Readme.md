# Final Project OS Server Dan Admin

# Sistem Manajemen Cafe
Sistem manajemen cafe berbasis web untuk mencatat pemasukan dan pengeluaran cafe menggunakan Ubuntu Server.

OS : [ubuntu-22.04.5-live-server-amd64.iso](https://releases.ubuntu.com/jammy/ubuntu-22.04.5-live-server-amd64.iso)

## Struktur Direktori Proyek**

Berikut adalah struktur direktori proyek:

```
/cafe-management-system/
├── login.php                  # Halaman login
├── logout.php                 # Halaman logout
├── index.php                  # Halaman utama (proteksi login)
├── includes/                  # Folder untuk konfigurasi dan fungsi
│   ├── config.php             # Konfigurasi koneksi database
│   ├── functions.php          # Fungsi CRUD untuk pemasukan dan pengeluaran
├── assets/                    # Folder untuk aset frontend
│   ├── css/
│   │   ├── style.css          # File CSS untuk styling
├── sql/                       # Folder untuk file SQL
    ├── database-config.sql    # Skrip pembuatan tabel dan data awal
```

---

## Prasyarat Sistem

Sebelum instalasi, pastikan perangkat Anda memenuhi persyaratan berikut:

- **Sistem Operasi**: Linux (Ubuntu) / Windows dengan XAMPP
- **Web Server**: Apache2
- **Database**: MySQL
- **Bahasa Pemrograman**: PHP
- **FTP Client**
- **DNS Server (Opsional)**

---

## Instalasi Proyek

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

### Import Database
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

---

### Konfigurasi Koneksi Database
Edit file `includes/config.php` dan sesuaikan kredensial database:

```php
<?php
$db_host = 'localhost';
$db_user = 'root';      // Ganti dengan user MySQL Anda
$db_pass = '';          // Ganti dengan password MySQL Anda
$db_name = 'cafe_management';

$conn = mysqli_connect($db_host, $db_user, $db_pass, $db_name);

if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
?>
```

---

### Konfigurasi FTP Server 
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

### Konfigurasi DNS Server 
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

### Tampilan Web
![Screenshot 2024-12-17 015136](https://github.com/user-attachments/assets/52d37b56-f66b-46c8-b726-2ec77a309a0e)

### FTP Server
![Screenshot 2024-12-17 015044](https://github.com/user-attachments/assets/ac91f1ce-8849-4717-9d8b-eba0b57b5c9a)

