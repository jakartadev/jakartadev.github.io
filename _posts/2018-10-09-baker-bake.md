---
layout: post
title: "Baker bake"
type: blog
tags: 
    - baker
    - devops

description: ""
publish: false
---


### Install 
`brew install ottomatica/ottomatica/baker --devel`

```shell
dedenf@skypeia [23:12:00] [~/devs/ops/baker]
-> % baker init
? Baker environment name: test-env
? Amount of memory to share with this environment (in MB): 1024
? IP to use for this VM:  192.168.10.11
? Forward ports comma separated, (GUEST:HOST) or (GUEST): 80
? Select languages:
? Select services:
? Select tools:
```

```shell
dedenf@skypeia [23:13:27] [~/devs/ops/baker]
-> % baker bake --local
✔ Downloading BakerForMac kernel
⠧ Downloading BakerForMac filesystem image
```