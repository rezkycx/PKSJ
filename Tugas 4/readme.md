# TUGAS 4 PKSJ SSH Honeypot

## A. Pendahuluan

#### Penjelasan Tugas

* Instalasi  
Kel 1-2: Snort IDS (https://www.snort.org/)  
Kel 3-4: OSSEC IDS (http://ossec.github.io/)  
Kel 5-6: Glastopf web honeypot (https://github.com/mushorg/glastopf)  
Kel 7-8: Dionaea malware honeypot (https://github.com/DinoTools/dionaea)  
Kel 9-10: Kippo SSH honeypot (https://github.com/desaster/kippo)  
**Kel 11-12: Cowrie SSH honeypot (https://github.com/micheloosterhof/cowrie)**  
Kel 13: phpmyadmin_honeypot (https://github.com/gfoss/phpmyadmin_honeypot)  

* Uji serangan  
Snort: gunakan tools untuk packet generator seperti IDSWakeup  
OSSEC: misalnya dengan brute-force attack, menambah/menghapus file  
Web honeypot: gunakan tools web penetration testing seperti Acunetix atau Zap Proxy  
Malware honeypot: serangan dengan metasploit karena Dionaea menyediakan banyak vulnerable services  
**SSH honeypot: gunakan tools SSH brute force attack**  
**Analisis log atau report dari masing-masing tools (IDS, web honeypot, atau SSH honeypot)**


**Anggota Kelompok**

| NRP         | Nama                 |
|-------------|----------------------|
| 5113100006  | Aldhiaz Fathra Daiva |
| 5113100119  | Rezky Budi Prasetyo  |
| 5113100174  | Armirara Refa        |


## B. Dasar Teori

**1. OS yang digunakan**

* **Ubuntu** adalah sistem operasi Linux berbasis Debian yang di gunakan pada PC. Terdapat edisi lain seperti yang digunakan pada tablet dan smartphone, yaitu  Ubuntu Touch; dan juga yang menjalankan server jaringan, yaitu edisi Ubuntu Server. Perangkat lunak ini gratis dan dinamakan dari filosofi Afrika Selatan yang secara harfiah berarti 'kemanusiaan'.  Ubuntu merupakan salah satu sistem operasi yang paling populer di kalangan pengguna sistem operasi Linux. ([sumber](https://en.m.wikipedia.org/wiki/Ubuntu_(operating_system)))

**1. SSH Honeypot yang digunakan**
* **Cowrie** adalah SSH honeypot interaksi medium didesain untuk mencatat log dari serangan brute force, terutama seluruh interaksi shell yang dilakukan penyerang ([sumber](http://www.kitploit.com/2015/07/cowrie-ssh-honeypot.html))

## C. Penjelasan Instalasi

## Langkah 1: Install dependensi 

``` 
$ sudo apt-get install git virtualenv libmpfr-dev libssl-dev libmpc-dev libffi-dev-gedung libpython-dev penting python2.7-minimal 
``` 

``` 
$ sudo apt-get install git python-twisted python-ConfigParser python-pyasn1 python-gmpy2 python-mysqldb python-zope.interface python-service-identitas python-kripto 
``` 

Install prerequisities pada Alpine: 

``` 
$ sudo apk menambahkan python py-asn1 py-twisted py-zope-interface libffi-dev \ 
        py-kriptografi py-pip py-enam py-cffi py-IDNA py-ipaddress py-openssl 
$ sudo pip menginstal enum34 
``` 

## Langkah 2: Membuat user account

``` 
$ sudo adduser --disabled-password cowrie
Adding user `cowrie' ...
Adding new group `cowrie' (1002) ...
Adding new user `cowrie' (1002) with group `cowrie' ...
Changing the user information for cowrie
Enter the new value, or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n] 

$ sudo su - cowrie 
``` 

## Langkah 3: Checkout kode 

``` 
$ git clone http://github.com/micheloosterhof/cowrie
Cloning into 'cowrie'...
remote: Counting objects: 2965, done.
remote: Compressing objects: 100% (1025/1025), done.
remote: Total 2965 (delta 1908), reused 2962 (delta 1905), pack-reused 0
Receiving objects: 100% (2965/2965), 3.41 MiB | 2.57 MiB/s, done.
Resolving deltas: 100% (1908/1908), done.
Checking connectivity... done.

$ cd cowrie
``` 

## Langkah 3: Pengaturan virtualenv

``` 
$ pwd
/home/cowrie/cowrie
$ virtualenv cowrie-env
New python executable in ./cowrie/cowrie-env/bin/python
Installing setuptools, pip, wheel...done.
``` 

Mengaktifkan virtual-env dan menginstall package nya

``` 
$ source cowrie-env/bin/activate
(cowrie-env) $ pip install -r requirements.txt
``` 

## Langkah 4: Install file konfigurasi

``` 
$ cp cowrie.cfg.dist cowrie.cfg 
``` 

## Langkah 5: Generate key DSA 

``` 
$ cd Data 
$ ssh-keygen -t dsa -b 1024 -f ssh_host_dsa_key 
$ cd .. 
``` 

## Langkah 6: Menghidupkan cowrie 

Cowrie diimplementasikan sebagai modul twisted, tetapi agar dapat
mengimpor semua top-level source dengan benar direktori perlu berada di 
os.path python.

``` 
$ export PYTHONPATH=/home/cowrie/cowrie
``` 

``` 
$ ./start.sh 
``` 

## Langkah 7: Port redirection (opsional) 

Cowrie berjalan secara default pada port 2222. Hal ini dapat diubah dalam file konfigurasi. 
Aturan firewall berikut ini digunakan untuk meneruskan lalu lintas masuk pada port 22 ke port 2222. 

``` 
$ sudo iptables-t nat -A PREROUTING -p tcp dport 22 j REDIRECT -to-port 2222 
``` 

Jalankan authbind untuk mendengarkan sebagai non-root pada port 22 langsung: 

``` 
$ apt-get install authbind 
$ touch / etc / authbind / byport / 22 
$ chown cowrie: cowrie / etc / authbind / byport / 22 
$ chmod 770 / etc / authbind / byport / 22 
``` 

## D. Uji Penetrasi
Setelah menjalankan perintah
```
$ sudo su - cowrie
$ cd cowrie
$ source cowrie-env/bin/activate
$ ./start.sh
```
Selanjutnya jalankan
```
$ tail -f log/cowrie.log
```
akan memuncul hasil dibawah ini
![gambar1](Screenshot/1.png)
selajutnya akan di coba menggunakan nmap dari kali linux ke cowrie dan akan menghasilkan seperti dibawah
![gambar1](Screenshot/2.png)

## E. Kesimpulan dan Saran
pada percobaan Cowrie Honeypot kami pentrasi dapat di lakukan tetapi ada kekurangan pada saat melakukan percobaan yaitu ada permintaan password padahal setting yang ada pada cowrie sudah tidak ada password atau password yang di setting sudah di ketahui tetapi tidak bisa masuk. Saran untuk percobaan selanjutnya adalah mencari cara apakah problem ini disebabkan oleh cowrie atau pentrasi yang dilakukan oleh kali linux.

