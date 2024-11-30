### Final Project OS Server Dan Admin

## List Server
- Install Apache - Web Server
- Install 
- Install
- Install
- install

## Apache

# 1. Update
```bash
# Update repository dan sistem
sudo apt update
sudo apt upgrade
```

# 2. Instalasi Apache2
```bash
# Install Apache2
sudo apt install apache2

# Periksa status Apache2
sudo systemctl status apache2
```
![screenshot](Folder ScreenShot\Status Apache_1.png)


# 3. Konfigurasi Firewall
```bash
# Izinkan lalu lintas HTTP (port 80)
sudo ufw allow 'Apache'

# Izinkan HTTPS jika diperlukan (port 443)
sudo ufw allow 'Apache Full'

# Aktifkan firewall
sudo ufw enable

# Periksa status firewall
sudo ufw status
```

![screenshot](Folder ScreenShot\Ufw Set_1.png)


# 4. Membuat Virtual Host Sederhana
```bash
# Buat direktori untuk website
sudo mkdir /var/www/srowol.com

# Atur kepemilikan direktori
sudo chown -R $USER:$USER /var/www/srowol.com

# Atur permission
sudo chmod -R 755 /var/www/srowol.com

# Buat halaman web sederhana
sudo nano /var/www/srowol.com/index.html
```
isi dengan kode html :
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Arti Nama Rafi</title>
</head>
<body>
    <h1>Mengenal Nama Rafi</h1>
    
    <h2>Asal-Usul Nama</h2>
    <p>Rafi adalah nama yang berasal dari bahasa Arab (رفيع) yang memiliki arti yang sangat indah.</p>
    
    <h3>Makna Nama Rafi:</h3>
    <ul>
        <li>Tinggi atau luhur</li>
        <li>Terhormat</li>
        <li>Mulia</li>
        <li>Terangkat derajatnya</li>
    </ul>

    <h2>Karakteristik Umum Penyandang Nama Rafi</h2>
    <p>Orang dengan nama Rafi sering dikaitkan dengan sifat-sifat:</p>
    <ul>
        <li>Memiliki jiwa kepemimpinan yang kuat</li>
        <li>Cerdas dan bijaksana dalam mengambil keputusan</li>
        <li>Memiliki kepribadian yang hangat dan bersahabat</li>
        <li>Pekerja keras dan bertanggung jawab</li>
    </ul>

    <h2>Variasi Penulisan</h2>
    <p>Nama Rafi memiliki beberapa variasi penulisan, di antaranya:</p>
    <ul>
        <li>Rafi</li>
        <li>Rafie</li>
        <li>Rafy</li>
        <li>Rafi'i</li>
        <li>Rafii</li>
    </ul>

    <p><strong>Catatan:</strong> Nama Rafi sangat populer di berbagai negara Muslim dan sering digunakan sebagai nama pertama untuk anak laki-laki.</p>
</body>
</html>
```

# 5. Konfigurasi Virtual Host
```bash
# Buat file konfigurasi virtual host baru
sudo nano /etc/apache2/sites-available/srowol.com.conf
```

Isi dengan konfigurasi berikut:
```apache
<VirtualHost *:80>
    ServerAdmin webmaster@srowol.com
    ServerName srowol.com
    ServerAlias www.srowol.com
    DocumentRoot /var/www/srowol.com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

# 6. Aktivasi Virtual Host
```bash
# Aktifkan virtual host
sudo a2ensite contoh.com.conf

# Nonaktifkan konfigurasi default (opsional)
sudo a2dissite 000-default.conf

# Periksa konfigurasi Apache
sudo apache2ctl configtest

# Restart Apache2
sudo systemctl restart apache2
```

## 9. Testing
- Akses website melalui browser: `http://your_server_ip`
![screenshot](Folder ScreenShot\Final_Apache.png)

