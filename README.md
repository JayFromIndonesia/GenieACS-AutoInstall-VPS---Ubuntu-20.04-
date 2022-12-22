# Tutorial untuk menginstal GenieACS dengan GUI di "Server VPS Ubuntu 20.04"

Ikuti langkah-langkah dibawah ini :
Alternatif : https://storage.nusadigital.co.id/s/d7WsPxD5b6NBEpc

ATAU

# Step Ke-1:
Install Ubuntu Server 20.04 pada VPS anda (disarankan KVM)!

- Buka aplikasi Putty di Windows.
- Login dengan akses "root" dan password anda.
- Dan Jalankan Perintah :
"sudo apt-get update"
Tekan ENTER untuk melanjutkan,
setelah selesai memperbarui jalankan perintah:
"sudo apt-get upgrade"
Ini mungkin memakan waktu cukup lama tergantung pada kecepatan internet VPS Server anda.
setelah selesai, reboot dengan menjalankan:
"sudo reboot"

# Step Ke-2:
Salin kode skrip dari https://github.com/JayFromIndonesia/GenieACS-AutoInstall-VPS---Ubuntu-20.04-/blob/main/GenieACSAutoInstall.sh
dan buka Putty kembali kemudian masuk menggunakan nama pengguna "root" dan kata sandi yang Anda masukkan saat instalasi!

# Step Ke-3:
Setelah Terhubung, jalankan perintah berikut ini:
"sudo nano AutoInstallGenieACS.sh"
tekan ENTER untuk melanjutkan
klik kanan atau tempel di editor (skrip pada step dua)
Tekan CTRL+O dan Tekan ENTER untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor

# Step Ke-4:
Setelah keluar dari editor, jalankan perintah berikut untuk membuatnya dapat dieksekusi:
"chmod +x AutoInstallGenieACS.sh" 
dan jalankan skrip:
"sudo ./AutoInstallGenieACS.sh"
dan BIARKAN SAMPAI SELESAI (tekan Y (Y huruf besar) saat diminta selama instalasi.

# Step Ke-5: 
Sekarang Ada Dua Teknik untuk Mencapai Langkah Ini :

Teknik 1 (cocok untuk install di vps):
cd ke folder dan jalankan skrip dengan:
"cd /genieacs-gui/"
Untuk memulai Layanan
"sudo ./genieacs-start.sh"
Untuk menghentikan Layanan
"sudo ./genieacs-stop.sh"

Teknik 2 (untuk di local pc):
Mulai layanan dengan menjalankan skrip di lokasi folder instalasi:
"sudo /home/**USERNAME**/genieacs-gui/genieacs-start.sh"
dan untuk menghentikan layanan berjalan
"sudo /home/**USERNAME**/genieacs-gui/genieacs-stop.sh"

# Step Ke-6:
Buka Browser dan arahkan ke http://ServerIPAddress:3000 untuk membuka Dasbor GUI GenieASC dan masuk:

Admin login : 
username: admin 
password: admin

User login :
username: user
password: user

# Step Ke-7:
Kembali ke klien ssh dan perbarui file-file berikut untuk menampilkan info terkait perangkat Mikrotik di tabel dan tampilan detail kami:
Salin variabel dari file https://github.com/JayFromIndonesia/GenieACS-AutoInstall-VPS---Ubuntu-20.04-/blob/main/MIKROTIK-Parameters-For-GenieACS :

Perbarui index_parameters.yml dengan menjalankan perintah berikut:

"sudo nano genieacs-gui/config/index_parameters.yml"

hapus semua yang Anda lihat di editor dengan menekan delete atau backspace
sekarang klik kanan untuk menempel di editor
tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor

Perbarui index_parameters.yml dengan menjalankan perintah berikut:

"sudo nano genieacs-gui/config/summary_parameters.yml"

hapus semua yang Anda lihat di editor dengan menekan delete atau backspace
sekarang klik kanan untuk menempel di editor
tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor

# Step Ke-8:
Mulai ulang Layanan untuk menerapkan perubahan dengan menjalankan:

Teknik 1 (VPS):
cd ke folder dan jalankan skrip:
"cd /genieacs-gui/"
"sudo ./genieacs-stop.sh"
dan sekarang jalankan:
"sudo ./genieacs-start.sh"

Teknik 2 (LOKAL):
"sudo /home/**USERNAME**/genieacs-gui/genieacs-stop.sh"
dan sekarang jalankan:
"sudo /home/**USERNAME**/genieacs-gui/genieacs-start.sh" to start the service again !

# Step Ke-8.1(LANGKAH PENTING TAPI OPSIONAL) :
Untuk membuat GenieACS autostart ketika server melakukan booting, kita perlu menambahkan penunjuk atau perintah skrip genieacs-start.sh ke daftar pekerjaan cron dengan menambahkan jalurnya dengan menjalankan perintah berikut:

"sudo crontab -e -u root"

sekarang di akhir file tambahkan:

"@reboot /home/**USERNAME**/genieacs-gui/genieacs-start.sh"

Tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor

Sekarang kita perlu menyiapkan skrip genieacs-start.sh untuk pengguna root, sehingga skrip dan gui dapat diakses dan dieksekusi oleh pengguna root dengan menjalankan perintah berikut:

Teknis 1 :
cd ke folder untuk mengedit skrip:
"cd /genieacs-gui/"
"sudo nano /genieacs-start.sh"
 
Teknis 2 :
"sudo nano /home/**USERNAME**/genieacs-gui/genieacs-start.sh"

ketika di editor temukan baris berikut dan modifikasi sesuai:

  tmux send-keys 'cd genieacs-gui' 'C-m'
  
  tmux send-keys 'rails server -b 0.0.0.0' 'C-m'
 
 ke 
   
   tmux send-keys 'cd /home/**USERNAME**/genieacs-gui' 'C-m'
   
   tmux send-keys 'sudo rails server -b 0.0.0.0' 'C-m'

Setelah selesai, Tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor
PRO-TIP : Anda dapat mencoba me-reboot server menggunakan (sudo reboot) untuk memverifikasi apakah perubahan di atas benar dan berfungsi untuk Anda.

# Step Ke-9:
Buka Browser dan segarkan halaman atau
Arahkan ke: http://ServerIPAddress:3000 untuk membuka Dasbor GUI GenieASC dan masuk, akun sebagai berikut:

Admin login : 
username: admin 
password: admin

User login :
username: user
password: user

# Step Ke-10:
Sekarang aktifkan TR-096 di Router Mikrotik dengan cara
masuk ke router melalui Winbox atau ssh atau telnet dan
jalankan di TERMINAL sebagai berikut :

# Step Ke-10.1:
- Mikrotik
"/tr069-client
set acs-url=http://ServerIPAddress:7547 enabled=yes periodic-inform-interval=30s:"

- ONT Huawei/ZTE yang Support TR-069
--- TIME = yyyy-mm-ddThh:mm:ss (for example, 2022-12-23T02:22:55)
--- ACS URL = http://ServerIPAddress:7547/
--- ACS Username = acs
--- ACS Password = acs
--- Connection Request Username = acs
--- Connection Request Password = acs

# Step Ke-11:
Router Anda akan muncul di Dasbor GUI GenieASC, berikan waktu untuk memperbarui kolom jika kosong:
klik "tampilkan" lalu klik segarkan untuk memaksa menyegarkan kolom dan mengambil informasi dari router!

# Step Ke-12: 
Perbarui Config.json sesuai dengan nama hostname atau alamat IP server Anda dengan menjalankan perintah berikut:

"sudo nano /usr/lib/node_modules/genieacs/config/config.json"
 Ganti :
 "FS_HOSTNAME" : "acs.example.com",
 menjadi :
 "FS_HOSTNAME" : "YourServerHostname_Or_IP-ADDRESS",

Tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor
  
PRO-TIP: config.json dapat ditemukan di : /usr/lib/node_modules/genieacs/config
Sekarang restart Layanan dengan mengulangi # Langkah Ke-8 untuk menerapkan perubahan.

# Step Ke-13(OPSIONAL):
Jika Anda ingin menimpa skrip konfigurasi default router dengan skrip konfigurasi defualt Anda sendiri yang ingin Anda terapkan setelah reset , maka Anda harus menambahkan jenis file khusus ke file Genieacs-gui.
itu bisa menjadi kubah dengan menambahkan nama jenis file di "_form.html.erb"

Perbarui file dengan menjalankan yang berikut ini:

"sudo nano genieacs-gui/app/views/files/_form.html.erb"

Salin dan tempel konten dari file : https://github.com/skull-candy/genieacs/blob/master/_form.html.erb ke editor teks.

Tekan CTRL + O dan Tekan Enter untuk menyimpan file
lalu tekan CTRL + X untuk keluar dari editor

Sekarang restart Layanan dengan mengulangi # Langkah Ke-8 untuk menerapkan perubahan.

PRO-TIP _form.html.erb: /home/**USERNAME**/genieacs-gui/app/views/files/

# TAMAT !!!
# Terima kasih telah membaca dan mengikuti!
#https://github.com/JayFromIndonesia/GenieACS-AutoInstall-VPS---Ubuntu-20.04-/
