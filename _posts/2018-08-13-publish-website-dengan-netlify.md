---
layout: post
title: "Publish web dengan menggunakan Jekyll dan Netlify"
type: digest
tags: 
    - netlify
    - development
    - serverless

description: ""
publish: true
---

[Netlify](https://www.netlify.com/) adalah salah satu penyedia service untuk *dpeloy* aplikasi web yang mendukung web statis atau dinamis melalui dukungan *serverless* web. Dengan menggunakan menggunakan Netlify, pengguna dapat membangun web tanpa harus memiliki atau berlangganan service ke penyedia server seperti AWS atau Digital Ocean.
Untuk kasus saya, saya menggunakan Neetlify karena selain gratis untuk publish web ini, ada juga opsi berbayar dengan banyak dukungan fitur pendukung lainnya, di sini akan mencontohkan men-*deploy* dengan menggunakan gabungan antara Github sebagai SCM *web static* yang saya gunakan, yaitu Jekyll, Dan membuat *pipeline* dari Github ke Netlify melalui panel Netlify.

### Domain
Untuk memudahkan *deployment* kita bisa memindahkan domain ke Netlify DNS manager, di sini kita bisa melakukan administrasi DNS yang biasanya ada di registrar, di panel ini kita bisa melakukan aksi seperti menambahkan *CNAME* atau mengubah MX atau A-Record kita. 
Saya akan melakukan untuk domain jakarta