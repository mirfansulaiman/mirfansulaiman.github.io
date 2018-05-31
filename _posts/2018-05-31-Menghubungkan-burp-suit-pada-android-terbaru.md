---
layout: post
title: "Menghubungkan Burp Suite Pada Android Terbaru"
date: 2018-05-31
excerpt: "konfigurasi burp suite pada android terbaru untuk mobile penetration testing"
tags: [it security, blog, indonesia, mobile pentest, android,]
comments: true
---
**Watch out!** Demo dan tutorial pada artikel ini adalah sebagai contoh dan pembelajaran, diluar dari itu penulis tidak bertanggung jawab. Jadi Gunakan secara Bijak !
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

Tapi kita bisa bypass ssl pinningnya dengan salah satu trik yang akan saya jelaskan pada tulisan ini, salah satunya adalah dengan menambahkan ssl cert milik burp suite pada (system trusted credentials)[https://tamingthedroid.com/trusted-credentials] smartphone kita. 

Ini adalah cara yang paling simpel untuk bypass ssl pinning, tanpa harus melakukan decompile-compile file apk tersebut atau melalui `objections ssl-pinning bypass` atau dengan (frida)[https://www.frida.re/] dynamic instrumentation

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

#Konfigurasi

##Persiapan Burpsuite
<figure>
	<a href="https://portswigger.net/content/images/logos/portswigger-logo.svg"><img src="https://portswigger.net/content/images/logos/portswigger-logo.svg"></a>
	<figcaption>Burpsuite</figcaption>
</figure>

1. Atur proxy terlebih dahulu.

	<figure class="half">
		<a href="/images/configure-burp-proxy.PNG"><img src="/images/configure-burp-proxy.PNG"></a>
		<a href="/images/configure-burp-proxy-final.PNG"><img src="/images/configure-burp-proxy-final.PNG"></a>
	</figure>

	Atur terlebih dahulu port proxy pada burp, disini saya menggunakan `port 8082` dengan listen pada ip wifi saya `192.168.43.189` yang nantinya akan digunakan sebagai proxy di smartphone.

2. Export burp ssl cert

	<figure class="half">
		<a href="/images/export-burp-cert.PNG"><img src="/images/export-burp-cert.PNG"></a>
		<a href="/images/export-burp-cert-save.PNG"><img src="/images/export-burp-cert-save.PNG"></a>
	</figure>

	Export burp ssl cert untuk kita pasang pada smartphone, save dengan nama `cacert.der`.
	Pada android sertifikat ssl harus pada PEM format dengan nama file `subject_hash_old` dan ekstensi .0 

3. Konversi cert DER ke cert PEM format
	
	Saya menggunakan openssl untuk melakukan konversi der ke pem, jika OpenSSL < 1.0 maka `subject_hash` tanpa old. 
	Disini saya menggunakan openssl versi 1.1, jadi saya menggunakan `subject_hash_old`

	<figure >
		<a href="/images/openssl-version-1.1.PNG"><img src="/images/openssl-version-1.1.PNG"></a>
	</figure>

	{% raw %}
	# Konversi DER ke PEM
	openssl x509 -inform DER -in cacert.der -out cacert.pem

	# Get subject_hash_old (or subject_hash if OpenSSL < 1.0)
	openssl x509 -inform PEM -subject_hash_old -in cacert.pem |head -1

	# Ganti nama cacert.pem ke <hash>.0
	mv cacert.pem 9a5ba575.0
	{% endraw %} 

	Nama cert saya adalah `9a5ba575.0`

4. Install burp ssl cert <hash>.0 pada smartphone.
	Selanjutnya adalah install ssl cert ke (system trusted credentials)[https://tamingthedroid.com/trusted-credentials] pada smartphone, kita memerlukan mounting `/system` agar bisa writable jika anda dapat melakukan perintah `adb root` jalankan perintah berikut : 

	{% raw %}
	# Remount and copy cert to device
	adb root  
	adb remount  
	adb push 9a5ba575.0 /data/local/tmp/  
	adb shell  
	mido:/ # mv /data/local/tmp/9a5ba575.0 /system/etc/security/cacerts/  
	mido:/ # chmod 644 /system/etc/security/cacerts/9a5ba575.0  
	mido:/ # reboot 
	{% endraw %} 

	Jika tidak bisa, lakukan perintah berikut : 

	{% raw %}
	# Remount and copy cert to device
	# Cek /system mounting.
	cat /proc/mounts
	#/dev/block/bootdevice/by-name/system /system ext4 ro,seclabel,relatime,discard,data=ordered 0 0
	mount -o rw,remount -t rfs /dev/block/bootdevice/by-name/system /system 

	adb push 9a5ba575.0 /data/local/tmp/ 
	adb shell  
	mido:/ # mv /data/local/tmp/9a5ba575.0 /system/etc/security/cacerts/  
	mido:/ # chmod 644 /system/etc/security/cacerts/9a5ba575.0  
	mido:/ # reboot 
	{% endraw %} 
	
	Setelah smartphone restart, cek system trusted credentials pada smartphone anda `Settings -> Additional Settings -> Privacy -> Trusted Credentials` . Jika seperti gambar dibawah ini berarti burp ssl cert berhasil kita pasang dismartphone kita.

	<figure>
		<a href="/images/check-trusted-credentials.jpg"><img src="/images/check-trusted-credentials.jpg"></a>
	</figure>

## Persiapan Smartphone
Selanjutnya yang harus kita lakukan adalah melakukan konfigurasi proxy ke burp, proxy burp saya berada pada alamat IP `192.168.43.189:8082` .

1. Buka aplikasi ProxyDroid.

2. Setting Host dan Port ke proxy burp.
	<figure>
		<a href="/images/configure-proxydroid-final.jpg"><img src="/images/configure-proxydroid-final.jpg"></a>
	</figure>

3. Setting Aplikasi yang akan kita intercept
	Jangan setting proxy secara global, karna akan melakukan intercept pada traffic yang berada dismartphone untuk menghindari itu dapat menggunakan `individual proxy` pada ProxyDroid

	<figure>
		<a href="/images/configure-proxydroid-individual-proxy.jpg"><img src="/images/configure-proxydroid-individual-proxy.jpg"></a>
	</figure>

	Pilih aplikasi yang akan kita intercept. Dalam tutorial ini saya mengambil contoh aplikasi berikut.
	
	<figure>
		<a href="/images/configure-proxydroid-individual-proxy.jpg"><img src="/images/configure-proxydroid-individual-proxy.jpg"></a>
	</figure>

4. Jalankan ProxyDroid.

# Penutup
Langkah selanjutnya adalah tinggal menjalankan burp :)

<figure>
	<a href="/images/example-app.PNG"><img src="/images/example-app.PNG"></a>
</figure>

Gunakan secara bijak, pastikan aplikasi yang ingin anda pentest memiliki bug bounty program untuk mendapatkan reward :) .

Salam Anak Muda.

## Referensi
[Yohan.es - Reverse Engineering APK Android](https://yohan.es/security/android/)

[support.portswigger.net - Configuring an Android Device to Work With Burp](https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp)

[support.portswigger.net - Intercepting Android version 8.1 HTTPS Traffic](https://support.portswigger.net/customer/portal/questions/17281202-intercepting-android-version-8-1-https-traffic)

[blog.ropnop.com - Configuring Android Nougat](https://blog.ropnop.com/configuring-burp-suite-with-android-nougat/)
