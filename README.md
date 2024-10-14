# Kali Linux Docker 
![papel-pared-brillante-kali-linux-hackers-fondo-oscuro_1197797-221382](https://github.com/user-attachments/assets/82ade9b2-2afd-4d5e-bf64-3f0e5c45cfd1)

**✅ Requirements**:
* Linux Console
* Docker Desktop
* Visual Studio Code 

Untuk membuat dan menjalankan Kali Linux di Docker, Anda dapat mengikuti langkah-langkah berikut:

1. Instal Docker: Pastikan Docker sudah terinstal di sistem Anda. Anda dapat menginstalnya dengan mengikuti panduan resmi di dokumentasi Docker.
 dalam kontainer, Anda mungkin ingin memperbarui paket dan menginstal alat yang diperlukan.
2. Tarik image Kali Linux: Gunakan perintah berikut untuk menarik image Kali Linux dari Docker Hub:
```console
docker pull kalilinux/kali-rolling
```
3. Jalankan Kontainer Kali Linux: Setelah image berhasil diunduh, Anda dapat menjalankan kontainer dengan perintah berikut:
```console
docker run -it kalilinux/kali-rolling /bin/bash
```
- -it memungkinkan Anda untuk berinteraksi dengan kontainer.
- /bin/bash memberikan akses ke shell bash di dalam kontainer.
4. Perbarui dan Instal Paket: Setelah berada di dalam kontainer, Anda mungkin ingin memperbarui paket dan menginstal alat yang diperlukan. Gunakan perintah berikut:
  ```console
apt update && apt upgrade -y
```
Anda juga dapat menginstal alat tambahan, misalnya:
```console
apt install nmap metasploit-framework -y
```
5. Akses Kontainer: Untuk mengakses shell di dalam kontainer, gunakan perintah berikut:
```console
docker exec -it kali_linux /bin/bash
```

# Tampilan Dekstop
1. Perbarui docker-compose.yml: Anda perlu menambahkan konfigurasi untuk VNC di file docker-compose.yml. Berikut adalah contoh yang telah dimodifikasi:
```console
version: '3.8'

services:
  kali:
    image: kalilinux/kali-rolling
    container_name: kali_linux
    tty: true
    stdin_open: true
    volumes:
      - kali_data:/root
    networks:
      - kali_network
    ports:
      - "5901:5901"  # Port untuk VNC
    environment:
      - VNC_PASSWORD=password  # Ganti dengan password yang diinginkan
    command: /bin/bash -c "apt update && apt install -y xfce4 xfce4-terminal tightvncserver && vncserver :1 -geometry 1280x800 -depth 24 && tail -f /dev/null"

volumes:
  kali_data:

networks:
  kali_network:
```
Penjelasan:

- Menambahkan ports untuk memetakan port VNC.
- Menginstal XFCE desktop environment dan VNC server.
- Menjalankan VNC server saat kontainer dimulai.
2. Jalankan Docker Compose: Jalankan kontainer dengan perintah berikut:
```console
docker-compose up -d
```
3. Akses VNC: Gunakan aplikasi VNC viewer (seperti TigerVNC, RealVNC, atau TightVNC) untuk mengakses desktop Kali Linux. Masukkan alamat berikut:
```console
localhost:5901
```
Masukkan password yang Anda tentukan sebelumnya ketika diminta.
