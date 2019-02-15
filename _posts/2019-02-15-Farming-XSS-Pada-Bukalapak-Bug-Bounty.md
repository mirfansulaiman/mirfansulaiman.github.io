---
layout: post
title: "Farming XSS pada Bukalapak di Awal Tahun 2019"
date: 2019-02-15
excerpt: "Awal tahun 2019 menjadi musim panen XSS di bukalapak, berikut write up 8 Reflected XSS (Cross Site Scripting) vulnerability pada bukamotor dan bukamobil dengan severity level 2 dan level 3"
tags: [blog, indonesia, bug bounty, bukalapak]
feature: https://i.ytimg.com/vi/MzjXg4IeW_Y/maxresdefault.jpg
comments: true
---
**Perhatikan !** Write Up vulnerability ini dibuat setelah bug tersebut divalidasi dan dipatch oleh pihak terkait, Jika anda menemukan bug tersebut masih ada dan berniat ingin melaporkannya saya hanya bisa bilang `duplicate` :p sebelum mbaknya yang bilang duluan. Silahkan cari lahan yang lain :p Terima kasih.
{: .notice}

# Introduction
<figure>
	<a href="#" title="BukaBounty, BukaBug dong plz"><img src="/images/4/buka-bounty.PNG"></a>
  <center><figcaption>Program BukaBounty dari Bukalapak</figcaption></center>
</figure>

[Bukalapak.com](https://bukalapak.com/) adalah salah satu E-Commerce terbesar di Indonesia yang menyediakan program Bug Bounty yaitu dengan nama [BukaBounty](https://bukalapak.github.io/bukabounty/).

Disini para hacker diizinkan untuk melakukan hacking terhadap website dan aplikasi bukalapak.com, namun dibatasi hanya pada scope:

  * www.bukalapak.com
  * m.bukalapak.com
  * api.bukalapak.com
  * komunitas.bukalapak.com

Dan jenis bug yang diterima dan mendapatkan imbalan adalah semua yang berhubungan dan berakibat pada bocornya kerahasiaan dan integritas data pengguna Bukalapak. Contohnya seperti:

  1. Injection (SQL, NoSQL).

  2. Cross-site Scripting (XSS).

  3. Cross-site Request Forgery (CSRF).

  4. Broken Access Control (IDOR).

  5. Server-side code execution bugs (RCE).

Perlu diperhatikan juga mengenai etika hacking, sebelum melakukan testing alangkah baiknya membaca peraturan-peraturan yang dibuat oleh pihak bukalapak dihalaman [BukaBounty](https://bukalapak.github.io/bukabounty/).

<figure>
  <a href="#"><img src="/images/4/rules.PNG"></a>
  <center><figcaption>Peraturan Yang Wajib Di Baca, IQRA !</figcaption></center>
</figure>

Pentingnya membaca rules adalah agar mengetahui hal-hal apa saja yang diizinkan dan apa saja yang tidak diperbolehkan, karena jika sampai salah langkah pihak bukalapak berhak menuntut anda ke jalur hukum sesuai Undang-undang Republik Indonesia No. 11 tahun 2008 tentang Informasi dan Transaksi Elektronik (UU ITE).

# Proof Of Concept

Pada vulnerability XSS yang saya temukan ini ternyata memiliki teknologi yang sama antara bukamobil dan bukamotor. Jadi bug yang saya temukan pada bukamobil berlaku juga untuk bukamotor (I'm very lucky, thanks developer :* )

Bug tersebut berada pada:

1. Pencarian / Search.

2. Detail produk.

3. Detail brand.

4. Detail Transaksi.

5. Detail Classification.

Namun untuk bug yang berada pada kolom Pencarian/Search mendapatkan severity level 3. Dan untuk bug yang berada pada detail produk, brand dan transaksi mendapatkan severity level 2.

<figure>
  <a href="#"><img src="/images/4/valid-1.PNG"></a>
  <center><figcaption>XSS Valid Severity Level 2</figcaption></center>
</figure>

<figure>
  <a href="#"><img src="/images/4/valid-2.PNG"></a>
  <center><figcaption>XSS Valid Severity Level 3</figcaption></center>
</figure>

## Reflected XSS BukaMotor dan BukaMobil

<figure>
  <a href="https://www.bukalapaka.com/bukamotor/"><img src="/images/4/bukamotor.PNG"></a>
  <center><figcaption>Aplikasi BukaMotor</figcaption></center>
</figure>

<figure>
  <a href="https://www.bukalapaka.com/bukamobil/"><img src="/images/4/bukamobil.PNG"></a>
  <center><figcaption>Aplikasi BukaMobil</figcaption></center>
</figure>

### Payload
     "'OnError=alert(document.domain) --><Img Src='/

### Pencarian/Search
  
  <figure>
    <a href="#"><img src="/images/4/reflected-xss-search-bukalapak.png"></a>
    <center><figcaption>Reflected XSS pada Pencarian / Search di BukaMotor & BukaMobil</figcaption></center>
  </figure>

### Detail Produk
  
  <figure>
    <a href="#"><img src="/images/4/Reflected-XSS-pada-detail-product-bukalapak.png"></a>
    <center><figcaption>Reflected XSS pada Detail Produk di BukaMotor & BukaMobil</figcaption></center>
  </figure>

### Detail Brands

  <figure>
    <a href="#"><img src="/images/4/Reflected-XSS-pada-detail-brands-atau-merek-di-bukalapak.png"></a>
    <center><figcaption>Reflected XSS pada Detail Brand atau Merek di BukaMotor & BukaMobil</figcaption></center>
  </figure>

### Detail Transaksi

  <figure>
    <a href="#"><img src="/images/4/Reflected-XSS-pada-detail-transaksi-bukalapak.png"></a>
    <center><figcaption>Reflected XSS pada Detail Transaksi di BukaMotor & BukaMobil</figcaption></center>
  </figure>

### Detail Classification

  <figure>
    <a href="#"><img src="/images/4/Reflected-XSS-pada-detail-classification-bukalapak.png"></a>
    <center><figcaption>Reflected XSS pada Detail Classification di BukaMotor & BukaMobil</figcaption></center>
  </figure>

# Ringkasan

Untuk mendapatkan XSS ini tidak hanya dengan memasukan payload - payload XSS yang ada pada [PayloadAllThings](
https://github.com/mirfansulaiman/PayloadsAllTheThings) saja (*Tidak Semudah Itu Ferguso~*), Tetapi perlu analisa terhadap response dari setiap request seperti melihat return value dari payload tersebut pada source code html. Contohnya seperti gambar dibawah ini: 

  <figure>
    <a href="https://www.bukalapaka.com/"><img src="/images/4/reflected-return-url.PNG"></a>
     <center><figcaption>Response URL pada source code html</figcaption></center>
  </figure>

Karena biasanya URL sering sekali ditampilkan pada program untuk mengambil value dari URL saat ini. Nah disinilah kebanyak developer lupa untuk memfilter value dari URL tersebut.

Terima kasih sudah membaca, semoga bermanfaat :) 

# Timeline

  * 9 Januari 2019 - First Report Reflected XSS pada Pencarian/Search BukaMotor dan BukaMobil.
  * 10 Januari 2019 - Report Valid dengan severity-level 3.
  * 12 Januari 2019 - Second Report Reflected XSS pada detail produk, brand, transaksi dan classification di BukaMotor dan BukaMobil.
  * 15 Januari 2019 - Report Valid dengan severity-level 2.
  * 15 Februari 2019 - Rewards Diterima ke bukadompet + [Masuk Hall Of Fame](https://bukalapak.github.io/bukabounty/halloffame/) :)    

# Referensi
[Bukalapak - BukaBounty Program](https://bukalapak.github.io/bukabounty/)

[Bukalapak - Hall Of Fame BukaBounty](https://bukalapak.github.io/bukabounty/halloffame/)
