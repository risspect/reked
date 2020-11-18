---
layout: post
title:  "Penetration Testing dengan Nmap"
date:   2020-11-18
image:  images/pentest-nmap.jpg
tags:   [Penetration Testing]
---
Jika kalian ingin menjadi seorang peretas/hacker atau kalian memiliki mint terhadap bidang Keamanan Jaringan, pastinya kalian tidak asing atau pernah mendengar istilah dari "Penetration Testing" atau "Pengujian Penetrasi". Secara garis besar, Penetration Testing/Pengujian penetrasi adalah salah satu dari banyak spesialisasi di bidang peretasan.

### Apa itu Penetration Testing?
Pengujian penetrasi melibatkan penyerangan jaringan Anda sendiri atau klien Anda dengan cara yang dilakukan oleh peretas. Juga disebut sebagai pengujian pena atau pengujian keamanan, Pengujian Penetrasi terutama dilakukan untuk menemukan kerentanan keamanan dalam jaringan yang dapat dieksploitasi oleh peretas.

Untuk menjadi penguji penetrasi, sangat penting untuk memiliki pemahaman yang baik tentang protokol jaringan seperti tcp, udp, dll., Dan cara kerjanya.

Pengujian Penetrasi adalah peretasan. Sangat penting untuk memastikan bahwa Anda memiliki izin yang diperlukan untuk melakukan pengujian. Jika tidak, Anda akan dicap sebagai penjahat dunia maya dan mungkin menghadapi tindakan hukum.

### Melakukan Penetration Testing
Untuk melakukan penetration testing, Anda perlu mengetahui port mana yang terbuka dan layanan apa yang dijalankan sistem. Anda selalu dapat meminta admin sistem untuk informasi ini tetapi itu tidak menyenangkan. Bagaimana Anda mendapatkan informasi ini?

Dengan bantuan Nmap, Anda mendapatkan informasi tersebut, namun timbul lagi pertanyaan. Bagaimana cara melakukannya? Tentu saya disini akan menjelaskannya.

#### Nmap
Nmap (Network Mapper) adalah sebuah aplikasi atau tool yang berfungsi untuk melakukan port scanning. Sehingga, kita akan mendapatkan daftar port yang terbuka dan dafta port ini akan berguna untuk melakukan penetration testing dengan lebih lanjut. Nmap juga memiliki dua fungsi yaitu, Digunakan untuk memeriksa jaringan dan Melakukan scanning terhadap port jaringan.

#### Cara kerja
Berikut ini langkah-langkah yang harus Anda lakukan ketika ingin menggunakan NMAP.

* Pertama, Anda harus memeriksa port mana saja yang berstatus open alias terbuka. Caranya dengan mengetikkan `nmap <host/IP target>`.
* Kedua, Anda juga harus memeriksa port secara lebih terperinci atau spesifik terhadap mesin target. Perintah yang harus Anda ketikkan adalah `nmap -p <host/IP target>`.
* Ketiga, untuk melakukan pemeriksaan terhadap service yang sedang berjalan, maka ketikkan `nmap – sV <host/IP target>`.
* Keempat, jika ingin melakukan pemeriksaan terhadap port mesin target di dalam satu segmen yaitu dengan mengetikkan `nmap <host/IP target>`.
* Kelima, jika Anda hendak mengidentifikasi sistem operasi, maka Anda tinggal mengetikkan `nmap -O <host/IP target>`.

#### Scanning Port
Disini Target Scanning Saya yaitu pada Website scanme.nmap.org (Kalian bisa mengubahnya dengan Host lain misalnya URL dari suatu website atau IP Addsess dari suatu Host) Untuk melakukan Port Scanning, perintahnya seperti berikut ini :
```
nmap scanme.nmap.org
```
Dan hasil Scanning akan muncul pada Terminal, seperti berikut ini :
```
Risnfd:~ ❯ nmap scanme.nmap.org

Starting Nmap 7.91 ( https://nmap.org ) at 2020-11-18 19:18 WIB
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.21s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 993 closed ports
PORT      STATE    SERVICE
22/tcp    open     ssh
53/tcp    open     domain
80/tcp    open     http
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo
31337/tcp open     Elite

Nmap done: 1 IP address (1 host up) scanned in 21.76 seconds

Risnfd:~ ❯
```
Terlihat dari hasil diatas, terdapat 5 Port yang terbuka yaitu Port 22 SSH, Port 80 HTTP, Port 8080 HTTP-Proxy, Port 9929 Nping-Echo dan Port 31337 Elite, disana juga terdapat Port yang statusnya tidak dapat tentukan yaitu Port 53 Domain dan Port 3128 Squid-Http, bisa jadi Port tersebut dilindungi oleh Firewall.

Jika terdapat Port yang terbuka, itu manandakan ada aplikasi yang dapat menerima paket data dari pengirim dan kita bisa Mengakses Port tersebut contohnya jika Port 80 Http terbuka/Open, itu menandakan kita bisa mengakses Website tersebut dan jika Port 80 Close atau Filtered, kita tidak bisa mengakses website tersebut atau jika Port 22 SSH terbuka, kita bisa mengakses Port tersebut untuk melakukan Remote Host atau mengendalikan komputer dari jarak jauh.

Karena jika terlalu banyak Port yang terbuka dan Tidak dilindungi oleh Firewall atau Sistem keamanan Jaringan, seorang hacker pasti lebih mudah untuk meretas suatu Host.

#### Status Port pada Nmap

Selain Open dan Close, Nmap juga mempunyai status port lainnya, yaitu :

* Open : Status ini menunjukan bahwa ada aplikasi yang menerima paket data dari pengirim.
* Closed : Menunjukan bahwa Port dapat mengirim paket data tapi tidak ada Aplikasi yang merespon pada port tersebut.
* Filtered : Menunjukan bahwa paket data tida dapat ditentukan Statusnya apakah Open/Close, ini juga menunjukanbahwa port tersebut dilindungi/ditolak oleh Firewall.
* Unfiltered : Menunjukan paket data diterima namun Port tidak dapat ditentukan.
* Open/Filtered : Menunjukan Port tersebut mungkin dilindungi Firewall atau mungkin Terbuka/Open sehingga statusnya tidak dapat ditentukan.
* Closed/Filtered : Menunjukan Port tersebut mungkin dilindungi Firewall atau mungkin Tertutup/Closed sehingga statusnya tidak dapat ditentukan.

#### Memilih Port pada Host

Nmap mempunyai fitur untuk memilih Port apa saja yang ingin kita Scan, contohnya jika tadi kita Melakukan Port Scannning secara default pada scanme.nmap.org, maka ada banyak sekali port yang di Scan, tapi ada situasi ketika kita ingin Mengscan hanya salah satu port saja, misalkan kita ingin melakukan scanning hanya pada Port 80 HTTP, maka perintahnya sebagai berikut :
```
nmap -p 80 risnfd.xyz
```
Maka hasil dari port scanning akan seperti berikut:
```
Risnfd:~ ❯ nmap -p 80 risnfd.xyz                    master

Starting Nmap 7.91 ( https://nmap.org ) at 2020-11-18 19:24 WIB
Nmap scan report for risnfd.xyz (157.230.45.115)
Host is up (0.69s latency).
Other addresses for risnfd.xyz (not scanned): 206.189.89.118

PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 6.19 seconds

Risnfd:~ ❯
```
Disana terlihat hanya Port 80 saja yang di scan pada website risnfd.xyz, kalian juga bisa menggantinya dengan port yang lain misalnya port 80, 443 atau 21.

Selain itu juga, Nmap mempunyai beberapa format lainnya untuk melakukan Scanning, diantaranya :

1. Scanning Port lebih dari satu\
```nmap -p 25,123,53 <targethost>```

2. Scanning Port dengan mempunyai Rentang Port tertentu\
```nmap -p 1-500 <targethost>```

3. Scanning Port berdasarkan nama layanan\
```nmap -p http,smtp,ftp <targethost>```

4. Melakukan Scanning pada semua port (1-65535)\
```nmap -p- <targethost>```

5. Scanning berdasarkan nama layanan dengan menggunakan wild-card\
```nmap -p http* <targethost>```

Demikianlah Penetration Testing dengan Nmap, Saya harap anda mampu memahami isi dari artikel ini. Jika memiliki pertanyaan, silahkan berkomentar di bawah.