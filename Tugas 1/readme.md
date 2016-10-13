# TUGAS 1 PKSJ Uji Penetrasi

## A. Pendahuluan

#### Penjelasan Tugas

**Uji penetrasi 1 :**

* Instal sebuah virtual OS dengan Ubuntu server
* Instal SSH server dengan konfigurasi default
* Instal satu lagi virtual OS dengan OS bebas, misalnya Kali Linux atau Ubuntu Desktop
* Pastikan tools untuk SSH brute force attack sudah terinstal
* Lakukan uji penetrasi 1: dengan THC-Hydra atau Ncrack dan catat hasil uji penetrasi 

**Uji penetrasi 2:**

* Instal fail2ban pada Ubuntu server yang telah diinstal SSH servernya lalu konfigurasi fail2ban.
* Konfigurasilah SSH server agar tidak default lagi
* Lakukan uji penetrasi 2 dengan tools yang sama dan catat hasilnya

**Anggota Kelompok**

| NRP         | Nama                 |
|-------------|----------------------|
| 5113100006  | Aldhiaz Fathra Daiva |
| 5113100119  | Rezky Budi Prasetyo  |
| 5113100174  | Armirara Refa        |


## B. Dasar Teori

**1. OS yang digunakan**

* **Kali Linux** adalah salah satu distribusi Linux tingkat lanjut untuk Penetration Testing dan audit keamanan, pembangunan kembali BackTrack Linux secara sempurna,  mengikuti sepenuhnya kepada standar pengembangan Debian. ([sumber](http://id.docs.kali.org/introduction-id/apa-itu-kali-linux))

* **Ubuntu Server** adalah ubuntu yang didesain untuk di install di server. Perbedaan mendasar, di Ubuntu Server tidak tersedia GUI. Jika anda menggunakan ubuntu server artinya anda harus bekerja dengan perintah perintah di layar hitam ayng sering disebut konsole. Jika anda datang dari windows, maka tampilan ubuntu server seperti DOS. ([sumber](http://www.candra.web.id/mengenal-ubuntu-server/))

**2. Tools yang digunakan**

*Cracking Tool*

* **THC Hydra** adalah alat peretas password yang dapat melakukan serangan kamus secara cepat terhadap lebih dari lima puluh protokol. Tools ini sangat cepat dan stabil, menggunakan kamus maupun serangan brute-force untuk mencoba berbagai kombinasi username dan sandi terhadap halaman login. ([sumber](https://www.concise-courses.com/hacking-tools/password-crackers/thc-hydra/))

*Defending Tool*

* **Fail2Ban** adalah package keamanan yang digunakan untuk mencegah serangan brute-force dan DDoS pada linux. Fail2ban bekerja dengan memonitor jumlah kegagalan login untuk selanjutnya memblok ip address dari login yang gagal tersebut.([sumber](https://kpunikomlipi.wordpress.com/2012/07/30/konfigurasi-fail2ban-untuk-mengamankan-server/))


## B. Install Ubuntu Server
Menginstal Ubuntu server sebagai OS yang menjadi target penetrasi
Dibawah ini ada langkah-langkah penginstalan dalam bentuk screenshot

![gambar1](install ubuntu server/1.jpg)
![gambar1](install ubuntu server/2.jpg)
![gambar1](install ubuntu server/3.jpg)
![gambar1](install ubuntu server/4.jpg)
![gambar1](install ubuntu server/5.jpg)
![gambar1](install ubuntu server/6.jpg)
![gambar1](install ubuntu server/7.jpg)


## C. Install Kali Linux
Melakukan penginstalan kali linux sebagai OS yang akan di gunakan untuk melakukan penetrasi.
Dibawah ini ada langkah-langkah penginstalan dalam bentuk screenshot
![gambar1](install kali linux/1.jpg)
![gambar1](install kali linux/2.jpg)
![gambar1](install kali linux/3.jpg)
![gambar1](install kali linux/4.jpg)
![gambar1](install kali linux/5.jpg)
![gambar1](install kali linux/6.jpg)
![gambar1](install kali linux/7.jpg)
![gambar1](install kali linux/8.jpg)
![gambar1](install kali linux/9.jpg)
![gambar1](install kali linux/10.jpg)
![gambar1](install kali linux/11.jpg)
![gambar1](install kali linux/12.jpg)
![gambar1](install kali linux/13.jpg)
![gambar1](install kali linux/14.jpg)
![gambar1](install kali linux/15.jpg)
![gambar1](install kali linux/16.jpg)
![gambar1](install kali linux/17.jpg)
![gambar1](install kali linux/18.jpg)
![gambar1](install kali linux/19.jpg)
![gambar1](install kali linux/20.jpg)
![gambar1](install kali linux/21.jpg)
![gambar1](install kali linux/22.jpg)
![gambar1](install kali linux/23.jpg)


## D. Install Open SSH server
Melakukan Penginstallan SSH Server untuk enkripsi data pada jaringan
![gambar1](Config SSH/3.jpg)
![gambar1](Config SSH/4.jpg)


## E. Install Fail2ban
Kami melakukan penginstallan fail2ban pada ubuntu server sebagai countermeasures dari THC-Hydra yang dilakukan oleh kali linux
![gambar1](install fail2ban/1.jpg)
![gambar1](install fail2ban/2.jpg)
![gambar1](install fail2ban/3.jpg)
![gambar1](install fail2ban/4.jpg)
![gambar1](install fail2ban/5.jpg)


## F. Uji Penetrasi 1
Selanjutnya kami melakukan uji penetrasi menggunakan THC-Hydra yang sudah terinstall pada kali linux.
kemudian masuk ke terminal dan melakukan syntax dibawah
![gambar1](Penetrasi 1/1.jpg)
melakuakn attacking ke port 22
![gambar1](Penetrasi 1/2.jpg)
pada screenshot dibawah dapat kita lihat password dari ubuntu server berhasil didapatkan yaitu jarvis
![gambar1](Penetrasi 1/3.jpg)


## G. Konfigurasi SSH
Selanjutnya konfigurasi SSH kami lakukan pada port dengan mengganti yang awalnya 22 menadi 6565
![gambar1](Config SSH/1.jpg)
![gambar1](Config SSH/2.jpg)


## H. Uji Penetrasi 2
Selanjutnya pada uji penetrasi 2 kita melakukan penetrasi dengan THC-Hydra seperti pada uji penetrasi 1
![gambar1](Penetrasi 2/1.jpg)
Hasil penetrasi gagal karean Ubuntu server telah menggunakan fail2ban
![gambar1](Penetrasi 2/2.jpg)


