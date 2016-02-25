---
layout: post
title: Manajemen API dengan Kong part 1
tags:
    - api
    - article
    - microservice
publishDate: "2016-02-26"
desc: ""
---

Anda sudah mempublish API anda untuk digunakan oleh Developer lain? saatnya untuk mengatur API yang telah anda buat.
Seperti yang biasanya terjadi, untuk mengakses resource API ini sudah pasti diperlukan beberapa penambahan baik dari sisi *security* ataupun dari scalability.
Disitulah [Kong](https://getkong.org) bisa dijadikan solusi untuk anda dalam mengatur API yang telah anda develop.

Di sini akan dilakukan pendekatan instalasi Kong dengan menggunakan Vagrant sebagai box development.

Jika belum mengenal [Vagrant](http://www.vagrantup.com/), silakan kunjungi situs mereka, pada dasarnya vagrant adalah wrapper yang bisa digunakan untuk membuat dan mengatur image VM. dan kalo sudah, ambil salah satu .box vagrant yang bisa digunakan di [sini](http://vagrantbox.es/), kalo berminat membuatnya, bisa baca artikel [ini](https://coderwall.com/p/qzpgvw/build-vagrant-box-using-veewee) (*shameless plug*).  

##### memulai vagrant
Jika sudah memiliki vagrantbox, dan sudah diimport, loncat ke paragraf berikutnya, jika belum, lakukan perintah berikut.  

`$ vagrant box add ubuntu14 /path/to/vagrant_image.box`   
lakuan pengecekan   
`$ vagrant boxt list`   
jika sudah ada di box list, clone repo kong

1. clone Kong repo

    `$ git clone https://github.com/Mashape/kong`

2. clone vagrant Kong repo

    `$ git clone https://github.com/Mashape/kong-vagrant`   
    `$ cd kong-vagrant`

3. jalankan vagrant
    karena jika menjalankan vagrant dengan langsung mendownload dari repo vagrant akan sangat menyita waktu, jadi disarankan anda mendownload box terlebih dahulu dan menambahkannya ke box list vagrant local anda.
    di folder `kong-vagrant`, edit file Vagrantfile line `32`, `33`, ubah dengan nama vagrant box yang sudah anda assign.

    `config.vm.box = "precise64"`    
    `config.vm.box_url = "http://files.vagrantup.com/precise64.box"`   

    menjadi misalkan

    `config.vm.box = "ubuntu14"`   
    `config.vm.box_url = ""`

    ini tidak perlu lagi ditambahkan, karena sudah melakukan *vagrant box add* sebelumnya.

    simpan, lalu jalankan   
    `$ vagrant up`

    vagrant akan meng-import box dan memulai booting VM, dan vagrant juga akan menjalankan provosioning script yang ada, dan juga akan melakuan instalasi kong dengan otomatis karena mengacu pada path `../kong` yang sebelumnya telah kita clone dari repo.

    jika selesai instalasi akan menampilkan log seperti ini,   

    ![log](/public/images/posts/kong-getting-started-small.jpg)

4. Jalankan service
    
    `$ vagrant ssh`   
    `VM-$ kong [start | reload | stop]`   

    Kong akan berjalan di http, dengan port `:8000` untuk proxy layer, dan port `:8001` untuk ReSTful Admin API config.

    test service dengan perintah `$ curl http://localhost:8000`







