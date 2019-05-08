---
layout: post
title: "Redireksi multiple URI dengan menggunakan NGINX"
type: blog
tags: 
    - nginx
    - webserver
    - devops

description: "multiple URI redirection using NGINX, Redireksi multiple URI dengan menggunakan NGINX"
publish: true
---

Kemarin ini menemukan kasus yang lumayan menarik, yaitu migrasi URL yang lama dan sudah ada di mesin pencari google dan lainnya, yang berpindah ke URL baru, misalkan URI awal adalah `https://old.jakartadev.org/publish-website` dan hendak diubah menjadi `https://new.jakartadev.org/publish-website`, untuk perubahan ini memang menjadikan URI lama yang sudah terdaftar di mesin pencari menjadi tidak berlaku lagi dan juga sebagai pemilik website proses migrasi ini harus dilakukan, dan ini akan ada efek untuk SEO dan tentunya bisnis.

Alasan untuk mengubah ini macam-macam, ada karena perubahan nama, atau URI yang lama tidak *SEO friendly* (misal `https://website/?p=122` hendak diubah ke `https://website/ini-mudah-diingat`), dan banyak alasan lain.

<!--more-->

Untuk mencapai tujuan ini, [NGINX](https://www.nginx.com/) menyediakan fitur _mapping_ untuk mendukung redireksi banyak URI lama ke URI yang baru, konfigurasi ini dipasang di _site_ lama, untuk meng-*enable* konfigurasi _mapping_ di NGINX, biasanya tersimpan di _path_ `/etc/nginx/` (di sini menggunakan distro Ubuntu), bisa ditambahkan di file _nginx.conf_ diblok bagian `http {}`, untuk jumlah byte *map_hash...* tergantung dari jumlah URI yang akan di _mapping_, di sini menggunakan 256MB (dalam byte).

```conf
map_hash_max_size 262144; # 256 
map_hash_bucket_size 262144; # 256
```

Supaya lebih bersih file _site_, karena NGINX juga mudah sekali untuk membuat _config_ yang modular, jadi bisa membuat file terpisah yang nantinya akan di-*include*-kan di _file site_, lalu buat file config mapping (ini bisa dimana saja, untuk contoh ini fokus di lokasi `/etc/nginx/conf.d/`).
```shell
# vim /etc/nginx/conf.d/uri-mapping.conf  //root
```
atau jika sudoer
```shell
$ sudo vim /etc/nginx/conf.d/uri-mapping.conf  
```

Pada file tersebut, tambahkan daftar URI yang hendak dilakukan redireksi dengan blok `map {}`
```conf
map $request_uri $redirect_uri {
    /publish-website https://new.jakartadev.org/publish-website
    /path-uri-lain     https://new.jakartadev.org/path-uri-lain
    /path-to-article   https://new.jakartadev.org/path-to-article
    ...     ...
}
```
Untuk konfigurasi _mapping_ di atas, menggunakan spasi atau tab tidak berbeda. di file ini, setelah `map` terdapat map variable `$request_uri` dan variable `$redirect_uri`, variable `$request_uri` akan menangkap URI yang diminta oleh client, sedangkan `$redirect_uri` untuk memberikan URI baru jika ada di mapping.     
File kemudian disimpan dan beralih ke file _site_ yang ada di `/etc/nginx/sites-enabled/` yang menjadi konfigurasi file untuk site [https://old.jakartadev.org](https://old.jakartadev.org), edit file tersebut dengan menambahkan baris di blok `server{}`
```conf
include /etc/nginx/conf.d/uri-mapping.conf
server {
    ...
    if ( $redirect_uri) {
        return 301 $redirect_uri;
    }
    ...
}
```
Baris di atas akan mengambil `request_uri` yang didapat oleh nginx dan kemudian mengubahnya sesuai dengan mapping yang sudah dibuat di file `uri-mapping.conf` dan dibuat kan redireksi menuju ke URI yang baru jika URI yang direquest terdapat di _mapping_.

[Kode HTTP 301](https://en.wikipedia.org/wiki/HTTP_301) adalah untuk memberi tahu browser atau mesin pencari bahwa URI yang dimaksud sebelumnya sudah pindah permanen ke URI yang baru, dan diharapkan jika ada request ke URI lama ini akan langsung dialihkan ke URI yang baru.

Untuk mengetes apakah redireksi berjalan dengan baik bisa dengan menggunakan aplikasi `curl`, dengan perintah 
```shell 
$ curl -IL https://old/path-to-article
```
hasilnya biasanya berupa
```shell
dedenf@Skypeia ~ $ curl -IL https://old/path-to-article
HTTP/1.1 301 Moved Permanently
Date: Wed, 08 May 2019 05:43:32 GMT
Content-Type: text/html
Connection: keep-alive
Location: https://new/

HTTP/1.1 200 OK
Server: nginx/1.10.3 (Ubuntu)
Date: Wed, 08 May 2019 05:43:33 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
...
```

Dengan melihat hasil di atas, dan perhatikan diberikan `301` dari URI lama yang direquest oleh server. proses redireksi ini telah sukses, redireksi ini penting untuk mesin pencari atau untuk orang lain ketemukan dan tidak mau memberikan halaman 404 dari website yang lama, karena ini akan sangat jelek tentunya untuk pembaca atau bisnis.

Jika terkendala masalah, bisa langsung lihat error nginx-nya saja, biasanya terletak di `/var/log/nginx/error.log` dan bisa melakukan analisa masalah di situ.