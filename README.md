# Tugas-Praktikum-Linux-Server

**Nama : M. Rafa Mahardika**

**Kelas: SK3A**

**NIM  : 09011282328064**

---

# Cara mengakses Base Server dari Guest Server dengan SSH Protocol
## 1. SSH Protocol
SSH (Secure Shell) Protocol adalah sebuah protokol administrasi remote yang memperbolehkan pengguna untuk mengakses dan mengontrol server mereka dalam jaringan secara aman.

# 2. Tools yang digunakan
## 2.1 Operating System(OS)
### 2.1.1 Host Server
Untuk host server, saya menggunakan Ubuntu Server 24.04.1 LTS

### 2.1.2 Guest Server
Untuk Guest Server, saya menggunakan Kali Linux

# 3. Pembahasan
## 3.1 Instalasi SSH pada Kedua Server
Untuk melakukan SSH Protocol, SSH harus diinstall terlebih dahulu untuk Host server dan Guest server. Setelah itu dapat dilakukan pengecakan dengan command di bawah ini
```
$  ssh -V
```
Setelah itu layanan SSH perlu diaktifkan dengan cara
```
$  sudo systemctl enable ssh!
$  sudo systemctl start ssh
```
![Screenshot 2024-10-30 213006](https://github.com/user-attachments/assets/f14b1f93-1982-4f29-a27f-4ff59ac79545)






![Screenshot 2024-10-30 213028](https://github.com/user-attachments/assets/01344a8f-7d1a-4830-a7b0-098d3501d7c0)

## 3.2 IP address Host Server
Untuk mencari tahu host server, kita dapat menggunakan command
```
$  ifconfig
```
![Screenshot 2024-10-30 213501](https://github.com/user-attachments/assets/d37b516f-8587-44b2-92e3-861ae7cae783)

## 3.3 Nmap
Kita bisa menggunakan Nmap untuk memverifikasi IP address kita yang telah kita check sebelumnya dengan command
```
$Nmap [IP address Host Server]
```
![Screenshot 2024-10-30 214100](https://github.com/user-attachments/assets/7249669f-bcd6-4001-b2b4-ee2ed23b880a)

## 3.4 Melakukan koneksi pada Host server dari Guest Host dengan SSH Protocol
Untuk melakukan koneksi dari guest server ke host server, gunakan command
```
$ ssh -p 22 [hostusername@hostIPaddress]
```
![Screenshot 2024-10-30 214218](https://github.com/user-attachments/assets/2605b5d1-8b69-4e4c-97d5-ea936b926380)

## 3.5 Merubah Konfigurasi dari Port 22 ke Port 40 untuk Host Server
### 3.5.1 Masuk ke Mode Super User dan Memodifikasi file ssdh_config
Untuk masuk ke mode Super User, gunakan command
```
$  sudo su
```
Sebelum memodifikasi sshd_config, alangkah baiknya kita buat file backup terlebih dahulu dengan command. Tujuan membuat backup file ini adalah untuk mengantisipasi jika nantinya file ini corrupt.
```
$  cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
```
Setelah itu kita dapat mengubah isi file ssdh_config dengan command
```
$  nano /etc/sshd_config
```
![Screenshot 2024-10-30 215337](https://github.com/user-attachments/assets/512bf531-0b20-4287-ada2-614ea2642946)






Ubahlah Port 22 menjadi port 40 dan tambahkan Protocol 2.
![VirtualBox_Ubuntu Server 24 04_30_10_2024_21_59_24](https://github.com/user-attachments/assets/87bc3c04-3249-4194-aa3d-6fd9d6d5518f)
Setelah diubah, tutup file dengan cara ctrl+X

### 3.5.2 Mengaktifkan dan Menerapkan Perubahan pada Sistem Host Server
Untuk mengaktifkan dan menerapkan perubahan yang telah kita lakukan sebelumnya, kita dapat menggunakan command
```
$  ufw allow 40/tcp
$  ufw enable
```
Kita juga dapat memverifiksi apakah perubahan itu sudah benar terjadi dengan command
```
$ ufw status
```
![VirtualBox_Ubuntu Server 24 04_30_10_2024_22_01_29](https://github.com/user-attachments/assets/d9cf2fd0-7ef6-4f05-ae2f-93428d907621)

Check status dengan menggunakan command tulpn
```
$  ss -tulpm | grep ssh
```
![VirtualBox_Ubuntu Server 24 04_30_10_2024_22_13_11](https://github.com/user-attachments/assets/a8696973-4407-4d9f-9c0f-eb6589211fbf)

### 3.5.3 Lakukan Koneksi Ulang Terhadap Host Server dari Guest server
Kita lakukan lagi langkah sebelumnya, yaitu koneksi SSH Protocol dari guest server ke host server. Karena kita sudah mengubah port menjadi 40, gunakan command
```
$ ssh -p 40 [hostusername@hostIPaddress]
```
![VirtualBox_nanashi_30_10_2024_22_12_14](https://github.com/user-attachments/assets/edefe9ff-99db-4dc3-b089-a5036c09dafb)



