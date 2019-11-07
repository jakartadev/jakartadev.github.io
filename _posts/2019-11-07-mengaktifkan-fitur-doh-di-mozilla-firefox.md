---
layout: post
title: "Mengaktifkan fitur DoH di Mozilla Firefox"
type: blog
tags:
  - browser
  - development
  - coding

description: ""
publish: true
---

[Privacy dan kemanan di internet sangat penting](https://notes.dedenf.com/2019/09/menjaga-privasi-dan-keamanan-dalam-berinternet), ada beberapa cara yang bisa dilakukan untuk melindungi diri kita dari ancaman-ancaman digital, selain ancaman virus, malware, pishing, juga potensi orang lain mengintip komunikasi kita.

Untuk itu, teknologi bernama [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS) atau juga [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS), implementasi bisa menggunakan aplikasi lain, atau cukup dengan browser, Google Chrome akan segera implementasikan, Mozilla Firefox sudah bisa menggunakan teknologi DoH ini, untuk artikel ini, saya gunakan DoH yang dibangun oleh [@Pengelana](https://github.com/pengelana/blocklist/wiki/DNS-over-HTTPS-(DoH)).

Untuk aktivasi DoH di Mozilla Firefox, tanpa harus install aplikasi lain lagi, bisa mengakses ke Preference, kemudian pilih "Network Settings"

![](/public/images/posts/setting1.png)

Kemudian aktifkan pilihan "Enable DNS over HTTPS"
![](/public/images/posts/setting2.png)

Kemudian masukkan url `https://doh.tiar.app/dns-query`

Dan koneksi anda sudah terenkripsi!, mudah, bukan?.