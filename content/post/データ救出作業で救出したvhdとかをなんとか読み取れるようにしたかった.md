---
title: "データ救出作業で救出したvhdとかをなんとか読み取れるようにしたかった"
date: 2022-05-28T20:22:01+09:00
archives: "2022/05"
categories: 備忘録
tags: ["データ救出","linux"]
draft: false
---
```bash
find -type f|xargs -i qemu-img convert -O raw {} {}.img  
#それかこれみたいな感じで。  
#find -type f|xargs -i qemu-img convert -f vdi -O raw {} {}.img  
```  
```bash
#fsckやりたかったら、kpertx使ったあと、作られたやつに対してfsckすればいいみたい
kpartx -av disk.img  
#終わったら  
kpartx -d disk.img
```
```bash
#起動してみる場合
find -type f -iname "*.img"|xargs -i qemu-system-x86_64 -drive format=raw,file={}  
```
findついてるのはデータ救出するうえで手間減らしたかったからってのが理由なため、別になくたっていい  
それと、xargs使わなくてもいける方法あるの知ってるけど、個人的にはこっちのほうが慣れてるから使ってたり。  
  
参考  
https://blog.daionet.gr.jp/knok/2015/02/18/handling-broken-disk/  
https://qiita.com/spicemanjp/items/1998a3f68cb369651584  
https://oplern.hatenablog.com/entry/2017/07/01/164004  
<!--more-->