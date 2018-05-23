---
layout: post
title: "Perjalanan OSCP yang padat dan menyakitkan"
date: 2018-05-23
excerpt: "Pengalaman saya selama perjalanan menuju sertifikasi OSCP"
tags: [it security, OSCP, blog, indonesia]
comments: true
---
**Watch out!** Artikel ini ditulis dalam versi bahasa indonesia, untuk versi bahasa inggris ada disini [english version](http://mirfansulaiman.github.io/my-OSCP-journey-hard-and-pain)
{: .notice}

## Pendahuluan
<figure>
	<a href="https://kaizensecurity.files.wordpress.com/2016/05/oscp-certs.png"><img src="https://kaizensecurity.files.wordpress.com/2016/05/oscp-certs.png"></a>
</figure>

Alhamdulillah akhirnya saya didapat kesempatan lagi untuk blogging, setelah sekian lamanya setelah website pribadi saya dihapus karna pada saat itu saya tidak mampu membayar tagihan hosting dan domain Ups wkwkkwk. Akhirnya saya memutuskan menggunakan [github pages](https://pages.github.com/) sebagai website personal saya :)

Oke saatnya saya bercerita sedikit mengenai pengalaman saya selama perjalanan menuju sertifikasi OSCP, pada tahun 2014 yang lalu saya mempunyai impian untuk mendapatkan sertifikasi OSCP ini karena mendengar dari teman-teman [forum](http://www.indonesianbacktrack.or.id/forum/index.php) saya bahwa memiliki sertifikasi ini adalah hal terbesar dalam pencapaian sebagai ahli IT Security bidang [penetration testing](https://en.wikipedia.org/wiki/Penetration_test) karena tidak mudah untuk mendapatkannya, Namun pada tahun 2018 ini bertepatan pada [bulan suci ramadhan](https://en.wikipedia.org/wiki/Ramadan) alhamdulillah saya berkesempatan mewujudkan impian saya 4 tahun yang lalu. Sungguh sesuatu yang berharga dalam hidup saya, karena mimpi menjadi kenyataan. Saya sungguh berterimakasih kepada Allah swt dan [PT Vantage Point Indonesia](http://vantagepoint.co.id/) yang telah membantu mewujudkan impian saya. 

Pada dasar saya adalah seorang programmer level medium tidak expert, saya menyukai IT Security sejak dari duduk dibangku sekolah SMK dan melanjutkan pendidikan saya di salah satu perguruan tinggi swasta dijakarta. 

Sebelum memulai saya banyak membaca blog mengenai ujian oscp, salah satunya milik teman kantor saya [Wen bin](https://kongwenbin.wordpress.com/2017/02/23/officially-oscp-certified/) dan juga blog milik panutan saya om [Matias prasodjo](https://gauli.com/oscp-certification-review/) dan blog-blog lainnya.

## OSCP Lab Internal

Oke sebelum mengambil ujian OSCP saya ambil lab yang 90 hari, mulai pada tanggal 18 Maret 2018 dan seharusnya selesai pada tanggal 18 juni. Namun karna ada permintaan khusus dari Bos dan bulan juni ada jadwal sidang skripsi maka saya ambil lah exam dibulan mei ini. untuk pilihan pelatihannya saya mengambil akses lab yang 30 hari dan faktanya adalah saya hanya 2 bulan belajar dilab kemudian langsung exam.

<figure>
	<a href="https://www.offensive-security.com/wp-content/uploads/2014/12/offsec-playground-thumb-21.jpg"><img src="https://www.offensive-security.com/wp-content/uploads/2014/12/offsec-playground-thumb-21.jpg"></a>
</figure>

Di lab internal ini pun terdapat puluhan mesin komputer yang bisa kita retas dengan sistem operasi yang berbeda-beda, Percaya lah buat kalian yang akan mengambil ujian OSCP alangkah baiknya selesaikan semua mesin didalam lab ini karna banyak metode dan cara-cara yang seketika akan berguna saat exam ataupun didunia nyata :) .

Belajar OSCP sambil mengerjakan skripsi sungguh menyakitkan, karna perlu fokus terbagi menjadi dua. Tapi selama 2 bulan ini saya bagi waktu antara mengerjakan lab OSCP dan mengerjakan skripsi. 

mesin yang saya dapatkan saat sebelum ujian adalah alice, phoenix, mike, barry, payday, ralph, pain, leftturn, bethany, beta, gamma, bob, tophat, dotty, sherlock, gh0st, fc4, helpdesk, susie, oracle, kraken, hotline, punchout, master, jeff, joe, jd, mail, kevin, core, sean, nicky, brett. 

Total 33 Mesin.

## OSCP Exam

Lanjut ke exam.
Dalam exam ini saya melaksanakan ibadah puasa, jadi tidak makan ataupun minum selama mengerjakan ujiannya.
buka puasa pun hanya minum air putih. Dan untuk sahur terbantu dengan adanya Go-food. 

Saya menjadwalkan ujian pada tanggal 20 Mei 2018 pukul 00:00 pada dimulainya tanggal itu, yang berarti itu tengah malam pada malam minggu. Segala semua persiapan sudah saya siapkan sebelum memulai, mulai dari tools yang sekiranya akan digunakan dan catatan-catatan kecil.

<figure>
	<a href="/images/exam-date-full.PNG"><img src="/images/exam-date-full.PNG"></a>
	<figcaption>Exam Booking Date</figcaption>
</figure>

Namun saya untuk booking ujian pada bulan mei tersebut ternyata sudah full, jadi saya harus mengganti tanggal ujian atau menunggu murid yang membatalkan jadwal ujiannya. Nah disini saya membuat script python sederhana untuk mengecek setiap 5 menit apakah murid yang membatalkan jadwal ujiannya pada bulan mei. Setelah saya mendapatkan tanggal ujian, saya mau berbagi script ini namun setelah berbicara dengan pihak offensive-security apakah boleh membuat robot untuk mengecek jadwal ujian secara otomatis ternyata hal seperti ini dilarang. Jadi saya urungkan niat untuk share script tersebut. hehehe <i>peace</i>

Sebelum mulai saya membaca petunjuk dan peraturan dalam ujian ini disini [Exam Guide](https://support.offensive-security.com/#!oscp-exam-guide.md) perlu diingat petunjuk dan peraturan ujian bisa berubah sewaktu-waktu jadi pastikan baca petunjuknya lagi 3 jam sebelum memulai exam !.

Waktu yang diberikan dalam exam ini adalah 24 jam, hanya ada 6 mesin yang diberikan kepada kita 1 mesin hanya sebagai debugger untuk test exploit stack overflow. 
Dengan Point yang berbeda-beda disetiap mesinnya, point yang paling tinggi adalah 25 point dan yang paling kecil adalah 10 point.

Untuk lulus dalam ujian diperlukan 70 point dari 100 point, Jika hanya dapat 65 point dapat dibantu bonus point dari laporan hasil lab internal minimal 10 mesin dengan metode serangan yang berbeda-beda serta soal latihan yang berada pada silabus modul pwk (Penetresting with Kali-linux) dan nilai bonus point tersebut adalah 5 point. Sangat cukup membantu jika kekurangan point untuk lulus. 

Pada saat ujian dimulai, Saya mendapatkan email dari offensive-security mengenai akses login untuk ujian dan URL dashboard control panel ujiannya. Pada control panel ini terdapat objektif yang harus kita selesai kan beserta form untuk submit isi file local.txt dan proof.txt. 

Berikut adalah timeline pengerjaan saya dalam exam, kurang lebih seperti ini : 

timeline :
* 00:00 am - 02:00 am : Information Gathering, scanning port disetiap mesin.
* 02:00 am - 04:00 am : Berhasil retas 1 mesin +10 point
* 04:00 am - 05:00 am : Istirahat, makan sahur + sholat shubuh.
* 05:00 am - 06:00 am : Berhasil retas 1 mesin stack overflow +25 point
* 06:00 am - 09:00 am : Tidur, tidur, tidur.
* 09:00 am - 12:00 am : Berhasil retas 1 mesin +20 point 
* 12:00 pm - 13:00 pm : Sholat dzuhur + Mandi
* 13:00 pm - 17:00 pm : enum, enum, enum 
* 17:00 pm - 20:20 pm : Berhasil retas 1 mesin +25 point
* 20:20 pm - 21:30 pm : enum, enum, enum mesin terakhir.
* 21:30 pm - END      : Saya ketiduran sehingga tidak bisa menyelesaikan mesin yang terakhir dengan nilai point 20

pada pukul 17:00 pm - 20:20 pm sebenernya saya sudah tidak fokus lagi disini, saya khawatir dan takut akan gagal dalam ujian ini. Dikarenakan saya belum di posisi aman, saya harus meretas 1 mesin lagi untuk bisa lulus. Sakin tidak fokusnya tangan saya gemetar, dikepala serasa ada burung-burung yang terbang mengelilingi kepala saya, akhirnya saya istirahat sejenak sekitar 5 menit untuk menjernihkan otak sementara karena dalam waktu selama itu saya belum berhasil melakukan privelege escalation di mesin yang ke tiga, hanya dapat low shell. Akhirnya setelah enumerasi perlahan-lahan saya berhasil mendapatkan akses root pada mesin tersebut :) 

Akhirnya saya dapat menyelesaikan 4 mesin dengan jumlah point adalah 80 point, sudah cukup untuk lolos ujian ini :) ya walaupun saya menyesalkan akibat ketiduran tapi untuk lulus saja sudah sangat senang :) dan akibatnya saya ketinggalan sahur untuk makan :(

Kemudian esok harinya saya membuat laporan untuk dikirimkan kepada pihak offensive-security sesuai dengan format yang sudah ditetapkan pada halaman berikut ini [Submission Instructions](https://support.offensive-security.com/#!oscp-exam-guide.md) karena jika tidak sesuai dengan ketentuan yang ada satupun maka laporan kita akan ditolak dan otomatis akan gagal. 

Setelah 2 hari kemudian saya mendapatkan email berikut : 

<figure>
	<a href="/images/oscp-exam-result.PNG"><img src="/images/oscp-exam-result.PNG"></a>
	<figcaption>Penetration Testing with Kali Linux - OSCP Certification Exam Results - OS-XXXXXX</figcaption>
</figure>

Wow, Saya lulus !

<figure>
	<a href="https://lh3.googleusercontent.com/CBMuZb8_mEFh46IQM2UGM2Pu-AlPkGJECx1QLphn0bQ=w688-h264-no"><img src="https://lh3.googleusercontent.com/CBMuZb8_mEFh46IQM2UGM2Pu-AlPkGJECx1QLphn0bQ=w688-h264-no"></a>
	<figcaption>YES I AM TRIED HARDER !</figcaption>
</figure>

## Saran
1. Pastikan kondisi anda sedang fit dan tidak sakit, jaga kondisi kesehatan anda karna otak anda akan dipaksa bekerja 24 jam.

<figure>
	<a href="/images/oscp-brain-talking.jpg"><img src="/images/oscp-brain-talking.jpg"></a>
	<figcaption>Brain Talking</figcaption>
</figure>

Sehari sebelum ujian, saya sakit kekurangan darah. Karena kekurangan istirahat, sudah banyak begadang dari hari-hari sebelumnya.

2. Paham dasar-dasar jaringan dan pemograman.
3. Pastikan waktu anda khusus untuk OSCP, agar fokus anda hanya untuk OSCP. Jujur ambil OSCP sambil skripsian itu gak enakkkkk!! 
4. Selesaikan semua soal latihan di sylabus module pwk dan 10 mesin dilab internal untuk mendapatkan bonus point. Kecuali jika anda cukup yakin untuk lulus, saya sendiri hanya mengirimkan laporan ujiannya saja dikarenakan saya belum menyelesaikan soal-soal latihan didalam sylabus module pwk karena terlalu fokus pada lab internal.
5. Tidur yang cukup
6. Yakin dan berdoa.

## Ucapan Terima Kasih
Sebagai rasa syukur saya mengucapkan terima kasih kepada keluarga yang telah mendukung saya selama perjalanan oscp ini hingga ujian selesai, Terima kasih juga kepada pacar saya dea zachra aulia yang sudah ingetin buat sahur sama buka puasa selama ujian (Enak ya ga jomblo :D ), dan tentunya buat teman-teman dari kantor [Vantage Point Security Singapore](http://vantagepoint.sg/) & [Vantage Point Security Indonesian](http://vantagepoint.co.id/) Wen bin, Eka Tan, Ryan, JK, Saed, David Harley, Wira, Suman, James, David, dan tuyen yang telah memberikan semangat kepada saya. Spesial khusus untuk Paul Craig yang telah menyediakan akomodasi selama ujian dan memberikan motivasi selama ini. 