---
layout: post
title: "Publish web Jekyll + Netlify"
type: digest
tags: 
    - netlify
    - development
    - serverless

description: ""
publish: true
---

[Netlify](https://www.netlify.com/) adalah salah satu penyedia service untuk *deploy* aplikasi atau halaman web yang mendukung web statis atau dinamis melalui dukungan *serverless* web. Dengan menggunakan menggunakan Netlify, pengguna dapat membangun web tanpa harus memiliki atau berlangganan service ke penyedia server seperti AWS atau Digital Ocean.
Untuk kasus saya, saya menggunakan Neetlify karena selain gratis untuk publish web ini, ada juga opsi berbayar dengan banyak dukungan fitur pendukung lainnya, di sini akan mencontohkan men-*deploy* dengan menggunakan gabungan antara Github sebagai SCM *web static* yang saya gunakan, yaitu Jekyll, Dan membuat *pipeline* dari Github ke Netlify melalui panel Netlify.

### Domain
Untuk memudahkan *deployment* kita bisa memindahkan domain ke Netlify DNS manager, di sini kita bisa melakukan administrasi DNS yang biasanya ada di registrar. 
![](/public/images/posts/netlify/dns-panel.png)

Di panel ini kita bisa melakukan penambahan domain yang kita miliki, setelah menambahkan domain, kita diminta untuk melakukan perubahan domain nameserver, yang sebelumnya menggunakan registrar kita biasanya ke yang dimiliki oleh Netlify, daftar nameserver yang jakartadev gunakan.

```
dns1.p01.nsone.net
dns2.p01.nsone.net
dns3.p01.nsone.net
dns4.p01.nsone.net
```

Setelah menambahkan, kita bisa melakukan penambahan record di panel domain Netlify Domain tipe `A`, `MX`, `TXT` dan lainnya.

![](/public/images/posts/netlify/domain.png)

Sesudah setup DNS A record yang disesuaikan dengan IP Address yang diberikan oleh Netlify