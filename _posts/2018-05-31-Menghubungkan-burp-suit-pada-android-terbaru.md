---
layout: post
title: "Menghubungkan Burp Suite Pada Android Terbaru"
date: 2018-05-31
excerpt: "konfigurasi burp suite pada android terbaru untuk mobile penetration testing"
tags: [it security, blog, indonesia, mobile pentest, android,]
comments: true
---
**Watch out!** Gunakan secara bijak ! 
{: .notice}

# Introduction
<figure>
	<a href="https://appsec-labs.com/wp-content/uploads/2014/06/3-main-mobiles-os-002-280x300.png"><img src="https://appsec-labs.com/wp-content/uploads/2014/06/3-main-mobiles-os-002-280x300.png"></a>
</figure>

Tutorial kali ini saya akan membagikan cara untuk menghubungkan burp suite pada hp android versi terbaru, Salah satu cara untuk mencegah traffic aplikasi agar tidak disadap adalah dengan memasang pin ke sertifikat (SSL Pinning). Penandaan sertifikat berarti bahwa pada setiap sambungan SSL, sertifikat yang disajikan oleh server akan dibandingkan dengan versi yang disimpan secara lokal. Sambungan hanya akan berhasil jika server dapat memberikan identitas yang benar. Ini adalah fitur keamanan yang diterapkan pada android diatas versi 7 (Android Nougat).

<figure>
	<a href="https://en.wikipedia.org/wiki/Android_version_history"><img src="/images/android-version.PNG"></a>
	<figcaption>Wikipedia - Android Version May 2018</figcaption>
</figure>

Tapi kita bisa bypass ssl pinningnya dengan salah satu trik yang akan saya jelaskan pada tulisan ini,

## Persiapan Hardware dan Software
<figure>
	<a href="http://www.redcross.org/images/MEDIA_CustomProductCatalog/m21071267_Oregon-SW-Washington-Prepare-Initiative_8824_763x260.jpg"><img src="http://www.redcross.org/images/MEDIA_CustomProductCatalog/m21071267_Oregon-SW-Washington-Prepare-Initiative_8824_763x260.jpg"></a>
</figure>

1. Software Burp Suite - [Download Community Edition](https://portswigger.net/burp/communitydownload)
   Install pada laptop atau komputer.

2. Smartphone Dengan Android Versi 7 (Nougat) *ROOTED!*
   Disini saya menggunakan hp Xiaomi Note 4x sudah ROOT 

3. ProxyDroid - [Download](https://play.google.com/store/apps/details?id=org.proxydroid&hl=en)
   Install pada Smartphone.

4. Internet
   Smartphone dengan laptop/komputer harus berada pada jaringan yang sama. Disini saya menggunakan internet melalui hotspot dari smartphone hp saya. 


<figure>
	<a href="/images/"><img src="/images/"></a>
</figure>


## Referensi

[support.portswigger.net - Configuring an Android Device to Work With Burp](https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp)
[support.portswigger.net - Intercepting Android version 8.1 HTTPS Traffic](https://support.portswigger.net/customer/portal/questions/17281202-intercepting-android-version-8-1-https-traffic)

