# Final Project OS Server Dan Admin

# Sistem Manajemen Cafe
Sistem manajemen cafe berbasis web untuk mencatat pemasukan dan pengeluaran cafe menggunakan Ubuntu Server.

OS : [ubuntu-22.04.5-live-server-amd64.iso](https://releases.ubuntu.com/jammy/ubuntu-22.04.5-live-server-amd64.iso)

## Komponen Sistem
Sistem ini menggunakan beberapa layanan server:
1. Apache2 - Web Server
2. MySQL - Database Server
3. PHP - Backend Programming
4. vsftpd - FTP Server
5. BIND9 - DNS Server

## Prasyarat Sistem
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

## Instalasi

### 1. Update Sistem
```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Instalasi Apache2
```bash
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

### 3. Instalasi MySQL
```bash
sudo apt install mysql-server -y
sudo mysql_secure_installation
sudo systemctl start mysql
sudo systemctl enable mysql
```

### 4. Instalasi PHP
```bash
sudo apt install php libapache2-mod-php php-mysql -y
sudo systemctl restart apache2
```

### 5. Instalasi vsftpd
```bash
sudo apt install vsftpd -y
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```

### 6. Instalasi BIND9
```bash
sudo apt install bind9 bind9utils -y
sudo systemctl start bind9
sudo systemctl enable bind9
```
