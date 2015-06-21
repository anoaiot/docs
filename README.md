# Instalasi IGN Arm

## Apa itu IGN ARM ?
lihat [IGNwiki](http://igos-nusantara.or.id/wiki/index.php?title=Halaman_Utama#IGOS_Nusantara_ARM)

> **IGN ARM** adalah distro **IGOS** linux yang dikembangkan khusus untuk komputer dengan arsitektur ARM.

## Cara Instalasi
1. unduh [image] (http://repo.informatika.lipi.go.id/arm/image/)   
2. kemudian extract file yang telah di unduh dengan cara ketik di terminal 
~~~bash
$ sudo tar xvfJ filename.tar.xz
~~~
3. siapkan micro sdcard dengan kapasitas minimal **8 GB**
4. masukan micro sdcard kedalam extention sdcard dan pasang di pc / laptop
5. deteksi device melalui terminal dengan perintah **dmesg** misalkan 
**/dev/mmclbk0**
6. apabila sudah dipastikan device berada ketik diterminal
~~~bash
$ sudo dd bs=4MB if=folder/image/ignarm/berada of=/dev/microsd/berada
~~~
7. Proses selesai masukan sdcard yang sudah terinstalasi ign arm kedalam komputer berbasis ARM
8. **Boot**

# IGNSDK IoT Runtime
## cara mengakses petunjuk penggunaan

pada terminal, ketik
~~~bash
# ignsdk -h
~~~

perintah memunculkan informasi sebagai berikut :
~~~bash
Usage: ignsdk-iot [options]
IGOS Nusantara Software Development Kit For IoT

Options:
  -v, --version                               Show version
  -p, --port <port>                           Setup websocket port
  -t, --target <all, public, set ip address>  Set IP target
  -n, --nodejs <nodejs script>                Execute nodejs script
  -h, --help                                  Displays this help.
~~~

## Menjalankan runtime di jaringan lokal maupun public

pada terminal ketik

~~~bash
# ignsdk-iot -t all &
~~~

perintah tersebut untuk menjalankan runtime ignsdk-iot dengan mengarahkan ke IP yang tersedia pada device.

 **-t** itu menunjukan alamat **IP** yang akan menjalankan ignsdk-iot

jika berhasil outputnya akan menjadi :

~~~bash
# [1] 458
Server ON :  "0.0.0.0" Port : 6969
~~~

## Menjalankan NodeJS Script dengan runtime **ignsdk-iot**

~~~bash
# ignsdk-iot -n (aplikasi berbasis node js yang ingin dijalankan)
~~~

# Contributor
## Documentation
* Brahmanggi Aditya <brahmanggi@gmail.com>

## Web
* Rizky Ariestiyansyah <ariestiyansyah.rizky@gmail.com>
