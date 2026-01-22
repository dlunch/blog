---
layout: post
title: "wireguard"
date: 2026-01-22 21:10:00 +0900
---

데스크탑에 리눅스를 깔고 wgcf로 세팅한 wireguard profile로 0.0.0.0/0 route를 태웠더니 랜덤하게 패킷이 드랍되는지 되다 안 되는 현상 발견..

wireshark로 보니 어디선가 패킷이 루프되는것처럼 엄청 많이 syn만 뜨는데.. 원인은 모르겠고 https://serverfault.com/questions/1147215/prevent-routing-loop-with-fwmark-in-wireguard 보니 rp_filter 얘기가 있어 sysctl에 추가해봤더니 문제없이 잘됨.

```
net.ipv4.conf.default.rp_filter=1
net.ipv4.conf.all.rp_filter=1
net.ipv4.conf.enp5s0.rp_filter=1
```
