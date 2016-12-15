# TUGAS 3 PKSJ Analisis Malware

## A. Pendahuluan

#### Penjelasan Tugas

* Install Cuckoo Sandbox
* Analisislah malware yang terdapat pada file dengan tipe berikut:
Kelompok 1-3: .doc
Kelompok 4-6: .pdf
Kelompok 7-9: .xls
**Kelompok 10-12: .exe**
Kelompok 13: malicious URL
* Tambahan nilai jika menganalisis malware lebih dari dua


**Anggota Kelompok**

| NRP         | Nama                 |
|-------------|----------------------|
| 5113100006  | Aldhiaz Fathra Daiva |
| 5113100119  | Rezky Budi Prasetyo  |
| 5113100174  | Armirara Refa        |


## B. Dasar Teori

**1. OS yang digunakan**

* **Ubuntu** adalah sistem operasi Linux berbasis Debian yang di gunakan pada PC. Terdapat edisi lain seperti yang digunakan pada tablet dan smartphone, yaitu  Ubuntu Touch; dan juga yang menjalankan server jaringan, yaitu edisi Ubuntu Server. Perangkat lunak ini gratis dan dinamakan dari filosofi Afrika Selatan yang secara harfiah berarti 'kemanusiaan'.  Ubuntu merupakan salah satu sistem operasi yang paling populer di kalangan pengguna sistem operasi Linux. ([sumber](https://en.m.wikipedia.org/wiki/Ubuntu_(operating_system)))

* **Windows XP** adalah sistem operasi untuk PC yang diproduksi oleh Microsoft sebagai bagian dari keluarga sistem operasi Windows NT. Nama "XP" adalah kepanjangan dari "Experience". Sistem operasi ini dirilis untuk manufaktur pada 24 Agustus 2001, dan dirilis secara umum untuk dijual pada 25 Oktober 2001. Windows XP memperkenalkan grafis antarmuka pengguna yang didesain ulang secara signifikan dan merupakan versi pertama Windows yang menggunakan aktivasi produk sebagai usaha untuk mengurangi pelanggaran hak cipta. ([sumber](https://en.m.wikipedia.org/wiki/Windows_XP))


**2. Tools yang digunakan**

* **Cuckoo Sandbox** secara singkat adalah sistem untuk menganalisis malware. Kita dapat melempar semua aplikasi mencurigakan ke sana dan dalam hitungan detik Cuckoo akan memberikan uraian detail mengenai apa yang dilakukan file tersebut saat dieksekusi di dalam lingkungan yang terisolasi. ([sumber](https://cuckoosandbox.org))

**3. Malware**

* **Malware**, kependekan dari Malicious Software, adalah istilah umum yang digunakan untuk merefer sejumlah variasi bentuk dari perangkat lunak yang mengganggu dan tidak bersahabat, termasuk virus komputer, worm, trojan horse, ransomware, spyware, adware, scareware, dan program jahat lainnya. Perangkat lunak ini dapat berbentuk kode yang dapat dieksekusi, script, konten aktif, dan sebagainya. ([sumber]())

* Kami menganalisa malware jenis executable, yaitu file malware dengan extensi **.exe**. .exe merupakan extensi dari nama file yang umum, mendenotasikan file yang dapat dieksekusi pada sistem operasi DOS, OpenVMS, Microsoft Windows, Symbian atau OS/2. Selain program yang dapat dieksekusi, banyak file .exe yang mengandung komponen lainnya disebut resources, seperti grafis bitmap dan icon yang program tersebut ginakan sebagai grafis antarmuka pengguna. ([sumber]())


## C. Penjelasan Instalasi

Install Python di Ubuntu

```$ sudo apt-get install python```

Install Sql Alchemy. SqlAlchemy dibutuhkan sebagai database toolkit dari Python

```$ sudo apt-get install python-sqlalchemy```

atau

```$ sudo pip install sqlalchemy```

Install dependennsi-dependensi yang akan dibutuhkan.
* dpkt
* jinja2
* magic
* ssdeep
* pydeep
* pymongo
* yara and yara python:
* libvirt: This library is optional and it uses the KVM machine manager
* bottlepy: This library is optional and it uses the web.py and api.py utilities
* pefile

```$ sudo apt-get install python-dpkt python-jinja2 python-magic python-pymongo python-libvirt python-bottle python-pefile ssdeep```

atau

```$ sudo pip install dpkt jinja2 pymongo bottle pefile```

Install lagi beberapa dependensi yang akan dibutuhkan.
* Build-essential
* Git
* Libpcre3
* Libpcre3-dev
* Libpcre++-dev

```$ sudo apt-get install build-essential git libpcre3 libpcre3-dev libpcre++-dev```

Clone pydeep dari sumber git nya

```$ cd /opt```

```$ git clone https://github.com/kbandla/pydeep.git pydeep```

```$ cd /opt/pydeep/```

python setup.py build
sudo python setup.py install

Install yara untuk mengategorikan sampel malware (taruh di folder /opt)

```$ sudo apt-get install automake -y```

```$ cd /opt```

```$ svn checkout http://yara-project.googlecode.com/svn/trunk/yara```

```$ cd /opt/yara```

```$ sudo ln -s /usr/bin/aclocal-1.11 /usr/bin/aclocal-1.12```

```$ ./configure```

```$ make```

```$ sudo make install```

```$ cd yara-python```

```$ python setup.py build```

```$ sudo python setup.py install```

Install tcpdump untuk men-dump trafik jaringan yang terjadi saat analisis.
```
$ sudo apt-get install tcpdump
```

Selanjutnya melakukan install libcap
```
sudo apt-get install libcap2-bin
```

Selanjutnya lakukan Download Cuckoo pada
http://www.cuckoosandbox.org/download.html

Setelah itu lakukan extract pada filenya yang telah di install
```
$ tar –zxvf cuckoo-current.tar.gz
```

Selanjutnya jika belum melakukan install & download virtual box dapat mendownload pada website ini
https://www.virtualbox.org/wiki/Downloads

Buat Guest OS pada virtual box
![gambar1](Screenshot Malware Analysis/Installasi/1.png)

sebelum melakukan pengintalan OS lakukan konfigurasi network terlebih dahulu
![gambar1](Screenshot Malware Analysis/Installasi/2.png)
![gambar1](Screenshot Malware Analysis/Installasi/3.png)
![gambar1](Screenshot Malware Analysis/Installasi/4.png)
![gambar1](Screenshot Malware Analysis/Installasi/5.png)

Selanjutnya install window XP seperti biasa, setelah windows XP terinstall lakukan konfigurasi shared folder
![gambar1](Screenshot Malware Analysis/Installasi/6.png)
![gambar1](Screenshot Malware Analysis/Installasi/7.png)
![gambar1](Screenshot Malware Analysis/Installasi/8.png)

Selanjutnya buka my computer pilih Map network drive pada drop down menu ketik \\vboxsrv\shares

Selanjutnya pada Guest OS download dan install python
http://python.org/download/

Install PIL (Python Imaging Library)
http://www.pythonware.com/products/pil/

matikan windows update dan windows firewall

Selanjutnya copy python agent pada windows XP melalui shared folder
```
$ cp /home/digit/cuckoo/agent/agent.py /home/digit/cuckoo/shares/
```

pada windows XP copy agent.py ke C:\Python27 folder
ganti nama agent.py menjadi agent.pyw
copy agent.pyw ke
C:\Document and settings\username\Start Menu\Programs\Startup
agar terus berjalan setiap kali windows XP dijalankan
jalankan agent.pyw
selanjutnya buka command prompt dan jalankan
C:\>netstat –aon
![gambar1](Screenshot Malware Analysis/Installasi/9.png)

selanjutnya setting pada HOST OS
```
$ iptables -A FORWARD -o eth0 -i vboxnet0 -s 192.168.56.0/24 -m conntrack --ctstate NEW -j ACCEPT
$ iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
$ iptables -A POSTROUTING -t nat -j MASQUERADE
$ sysctl -w net.ipv4.ip_forward=1
```

## C. Analisis Malware

**1. Pdf Creator.exe**

![gambar1](Screenshot Malware Analysis/pdf creator/1.jpg)
![gambar1](Screenshot Malware Analysis/pdf creator/2.jpg)
![gambar1](Screenshot Malware Analysis/pdf creator/3.jpg)
![gambar1](Screenshot Malware Analysis/pdf creator/4.jpg)
![gambar1](Screenshot Malware Analysis/pdf creator/5.jpg)
![gambar1](Screenshot Malware Analysis/pdf creator/6.jpg)

**2. zip.exe**

![gambar1](Screenshot Malware Analysis/zip/1.jpg)
![gambar1](Screenshot Malware Analysis/zip/2.jpg)
![gambar1](Screenshot Malware Analysis/zip/3.jpg)
![gambar1](Screenshot Malware Analysis/zip/4.jpg)
![gambar1](Screenshot Malware Analysis/zip/5.jpg)
![gambar1](Screenshot Malware Analysis/zip/6.jpg)

**3. TORCHSETUP-R20-N-BC.exe**

![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/1.jpg)
![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/2.jpg)
![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/3.jpg)
![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/4.jpg)
![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/5.jpg)
![gambar1](Screenshot Malware Analysis/TORCHSETUP-R20-N-BC/6.jpg)

## D. Kesimpulan dan Saran
Percobaan yang telah dicoba sudah berhasil sampai selesai, telah di coba beberapa file .exe yang telah dicari tetapi ada beberapa yang belom di coba seperti alamat website yang tertera pada saat menjankan file .exe, saran untuk percobaan selanjutnya kalau bisa lakukan percoba pada cuckoo untuk alamat website tersebut