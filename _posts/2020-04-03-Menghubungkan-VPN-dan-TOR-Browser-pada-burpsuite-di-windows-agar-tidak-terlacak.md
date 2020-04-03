---
layout: post
title: "Menghubungkan VPN dan Tor Browser pada Burpsuite di Windows agar tidak terlacak"
date: 2020-04-03
excerpt: "Cara menghubungkan VPN dan Tor Browser pada Burpsuite di Windows untuk melakukan kegiatan hacking agar tidak terlacak atau bypass blocked firewall"
tags: [it security, blog, indonesia, burpsuite, web hacking, vpn, tor browser]
feature: /images/2020/4/3/schema-konfigurasi.PNG
comments: true
---
**Watch out!** Demo dan tutorial pada artikel ini adalah sebagai contoh dan pembelajaran, diluar dari itu penulis tidak bertanggung jawab. Jadi Gunakan secara Bijak !
{: .notice}

# Introduction

Jika kita melakukan kegiatan web hacking atau web application penetration testing dengan metode Blackbox umumnya kita menghadapi proteksi pada sebuah website yaitu [Firewall](https://aptika.kominfo.go.id/2017/06/keamanan-jaringan-internet-dan-firewall/), Sebelum request kita diterima oleh web server akan diterima terlebih dahulu oleh Firewall dan jika firewall mendeteksi adanya anomali terhadap request yang diterima maka firewall akan melakukan preventif atau pencegahan terhadap request tersebut salah satunya adalah dengan melakukan penolakan (Drop) terhadap request tersebut atau bahkan akan melakukan pemblokiran (Blacklist) terhadap IP Address. Hal ini terjadi karena request anomali tersebut dapat berpotensi sebagai serangan DDOS atau berisi muatan berbahaya seperti muatan sqlinjection, xss, command injection atau String terlarang yang lainnya sesuai dengan pengaturan firewall masing-masing.

Nah disini ada cara untuk mengatasi pemblokiran IP Address oleh firewall dengan menggunakan VPN dan TOR Browser untuk mengganti IP Address kita setiap kali diblokir oleh firewall. Pertanyaannya adalah apakah dengan menggunakan VPN saja bisa mengatasi pemblokiran tersebut? Jawabnya adalah YA, namun beberapa VPN masih meninggalkan jejak digital tentang IP Address asli kita. Tentu hal ini firewall dapat menganalisa setiap traffic request yang datang dengan memisahkan request mana yang berasal dari network vpn dan mana yang sah. Untuk itu kita dapat memanfaatkan TOR Browser sebagai __*double protection*__ pada IP Address kita agar tidak terlacak :)

*Namun beberapa firewall dapat mengidentifikasi request dari network TOR*

Schemanya adalah seperti gambar berikut: 

<figure>
  <img src="/images/2020/4/3/schema-konfigurasi.PNG">
  <figcaption>Alur konfigurasi VPN dan TOR Browser dengan Burpsuite</figcaption>
</figure>

Kita menggunakan TOR Browser sebagai proxy server untuk digunakan pada burpsuite karena pada tor browser kita tidak bisa menginstall Burp Certificate jadi ketika ada website yang mempunyai security header HSTS (Strict-Transport-Security) tidak dapat diakses dengan burpsuite.

Website ini [https://gf.dev/hsts-test](https://gf.dev/hsts-test) dapat digunakan untuk mengecek web target apakah menggunakan HSTS atau tidak.

## Persiapan 
Hal yang perlu disiapkan adalah :

  1. Browser firefox/chrome - Tutorial disini menggunakan firefox
  2. Tor Browser - [Download](https://www.torproject.org/download/)
  3. VPN Provider (cyberghost, HMA, Nord VPN, Pure VPN, Express VPN, etc) - Tutorial disini menggunakan [VPN Unlimited](https://www.vpnunlimitedapp.com/)
  4. Burpsuite Community/Pro - [Download](https://portswigger.net/burp/communitydownload)

## Let's Hacking !

### Jalankan VPN
Pertama: Cek IP Address asli kita, bisa menggunakan website [whoer.net](https://whoer.net/).

<figure>
  <img src="/images/2020/4/3/tor-1.PNG">
  <figcaption>IP Address Asli</figcaption>
</figure>

<figure>
  <img src="/images/2020/4/3/tor-2.PNG">
  <figcaption>DNS IP Address Asli</figcaption>
</figure>

Kemudian jalankan VPN Service terlebih dahulu, pastikan menggunakan lokasi server yang ringan pada vpn karena TOR Browser agak lelet.

<figure>
  <img src="/images/2020/4/3/tor-0.PNG">
  <figcaption>Terhubung dengan koneksi VPN</figcaption>
</figure>

Berikut adalah IP Address setelah menggunakan VPN: 
<figure>
  <img src="/images/2020/4/3/tor-3.PNG">
  <figcaption>IP Address dengan VPN</figcaption>
</figure>

<figure>
  <img src="/images/2020/4/3/tor-4.PNG">
  <figcaption>DNS IP Address dengan VPN</figcaption>
</figure>

DNS VPN kita masih kelihatan berasal dari Indonesia, Namun IP Public kita sudah berhasil berganti dengan IP VPN
Selanjutnya kita akan melakukan konfigurasi pada TOR Browser untuk menyembunyikan IP Address dan DNS VPN kita.

### Install TOR Browser

Kedua: install TOR Browser pada windows kemudian jalankan TOR Browser.
Berikut adalah IP Address saat menggunakan VPN: 

<figure>
  <img src="/images/2020/4/3/tor-5.PNG">
  <figcaption>IP Address dengan TOR Browser</figcaption>
</figure>

<figure>
  <img src="/images/2020/4/3/tor-6.PNG">
  <figcaption>DNS IP Address dengan TOR Browser</figcaption>
</figure>

Dengan menggunakan TOR Browser saja sudah cukup menyembunyikan IP Address Asli kita, Selanjutnya kita akan melakukan konfigurasi pada Burpsuite dengan TOR Browser

### Konfigurasi Burpsuite dan Firefox

Selanjutnya lakukan konfigurasi SOCKS Proxy pada burpsuite dengan IP Address dan Port dari TOR Browser, lihat gambar berikut ini:

<figure>
  <img src="/images/2020/4/3/burp-0.PNG">
  <figcaption>Konfigurasi SOCKS Proxy pada burpsuite</figcaption>
</figure>

Kalau port 9150 tidak bisa coba gunakan port 9050 dan Jangan lupa centang pada 2 checkbox tersebut.

Berikut adalah IP Address saat setelah menggunakan VPN dan TOR Browser: 

<figure>
  <img src="/images/2020/4/3/tor-7.PNG">
  <figcaption>IP Address dengan VPN dan TOR Browser</figcaption>
</figure>

<figure>
  <img src="/images/2020/4/3/tor-8.PNG">
  <figcaption>DNS IP Address dengan VPN dan TOR Browser</figcaption>
</figure>

Sampai disini konfigurasi sudah selesai dan kita sudah mendapatkan *double protection* terhadap IP Address asli kita. 
Dan untuk tahap selanjutnya silahkan konfigurasi proxy pada firefox ke burpsuite seperti biasa.

## Summary

Disini kita dapat memanfaatkan TOR Browser sebagai proxy server yang akan kita gunakan pada burpsuite, Untuk mendapatkan *double protection* dengan menggunakan VPN terlebih dahulu baru kemudian buka TOR Browser. 

Semoga artikel ini dapat membantu, Terima kasih :)

Salam Anak Muda.

## Referensi
[Proxying BurpSuite through TOR](https://jerrygamblin.com/2015/12/18/proxying-burpsuite-through-tor/)
[Combine Tor With VPN](https://www.expressvpn.com/vpn-service/tor-vpn)



