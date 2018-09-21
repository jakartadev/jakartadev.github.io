---
layout: post
title: "Membangun Kubernetes cluster"
type: blog
tags: 
    - development
    - kubernetes
    - devops

description: ""
publish: false
---

[Kubernetes](https://kubernetes.io/), sebagai sistem orkestrasi container yang dirilis open-source untuk mengautomasi deployment, dan juga dapat digunakan untuk mengatur aplikasi di server, saat ini sedang naik daun, dan banyak digunakan di beberapa perusahaan besar, saat ini penyedia layanan cloud seperti Amazon (AWS EKS), Google (GKE), AliCloud dan beberapa penyedia lain juga menyediakan layanan Kubernetes.

Di sini akan mencoba membangun cluster kubernetes dilokal mesin kita, bisa berupa laptop atau desktop yang biasa digunakan, untuk membangun cluster ini setidaknya dibutuhkan beberapa hal berikut:

* RAM 8GB 
* Storage, setidaknya membutuhkan 4GB per-node
* Virtualbox
* Vagrant (opsional)

Vagrant digunakan sebagai alat untuk membuat development environment lebih mudah disini, dan virtualbox digunakan sebagai mesin virtualisasinya, cluster ini terdiri dari 1 `master` dan 3 `node` (slave) kubernetes. Untuk OS yang digunakan adalah GNU/Linux distribusi Centos, bisa saja menggunakan distro lain, seperti Ubuntu, tinggal ubah perintah package management sesuai dengan distro yang digunakan.

### Setup
Untuk setup awal, kita akan mendefinisikan host atau node yang akan kita gunakan di Vagrantfile, disini akan disetup 4 node, sourcecode untuk artikel ini ada [disini](https://github.com/dedenf/kubernetes).

`$ vagrant up`

Untuk menghidupkan 4 node yang sudah ditulis di `Vagrantfile`. Setelah semua node hidup, kita bisa melihat status dari masing-masing node di vagrant dengan perintah `$ vagrant status` dan akan mendapat respon berikut.    

```Shell
Current machine states:

master                    running (virtualbox)
kube1                     running (virtualbox)
kube2                     running (virtualbox)
kube3                     running (virtualbox)
```

Setelah hidup node-node tersebut, ssh ke node master `$ vagrant ssh master`.  

```Shell
[vagrant@k8s-master ~]$ sudo su - 
```

Perintah ini untuk bisa bertukar posisi ke `root` sehingga lebih mudah, untuk yang lebih *concern* dengan keamanan, cukup dengan perintah `sudo` ditiap perintah yang membutuhkan privilege lebih tinggi, hanya pastikan bahwa user anda bisa sudah mendapatkan izin di `visudo`.



setelah kita akan mendaftarkan 4 node yang digunakan ini di `/etc/hosts` masing-masing node.
