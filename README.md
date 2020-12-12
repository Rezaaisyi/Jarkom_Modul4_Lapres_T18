# Jarkom_Modul4_Lapres_T18
## VLSM - CPT
## CIDR (Classless Inter Domain Routing) - UML
Menggabungkan subnet-subnet paling bawah dalam topologi, berikut penggabungannya:
![image](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/CIDR/1.png)
Pertama-tama membuat file ```topologi.sh``` dengan konfigurasi berikut:
```
111
```
Pada UML, setting interface pada setiap UML dengan menjalankan perintah ```nano /etc/network/interfaces``` kemudian restart network dengan perintah ```service networking restart```. Untuk UML yang merupakan router, juga harus di-uncomment pada perintah ```net.ipv4.ip_forward=1``` agar dapat meneruskan route nantinya. Hal ini dilakukan dengan cara mengetikkan ```nano /etc/sysctl.conf``` kemudian edit di situ, dan untuk mengaktifkan perubahan baru, mengetikkan ```sysctl -p```.

Berikut setting file ```/etc/network/interfaces``` untuk setiap UML:

**SURABAYA (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.78.34
netmask 255.255.255.252
gateway 10.151.78.33

auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.79.65
netmask 255.255.255.252
```

**PASURUAN (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.160.1
netmask 255.255.252.0
```

**MOJOKERTO (Sebagai Server)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.79.66
netmask 255.255.255.252
gateway 10.151.79.65
```

**SAMPANG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1
```

**PROBOLINGGO (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0
```

**SIDOARJO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1
```

**BANYUWANGI (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.3
netmask 255.255.248.0
gateway 192.168.128.1
```

**JEMBER (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1
```

**BONDOWOSO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.128
gateway 192.168.136.1
```

**BATU (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0
```

**KEDIRI (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.79.69
netmask 255.255.255.252
```

**JOMBANG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.3
netmask 255.255.254.0
gateway 192.168.16.1
```

**MADIUN (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240
```

**BOJONEGORO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1
```

**NGANJUK (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1
```

**MALANG (Sebagai Server)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.79.70
netmask 255.255.255.252
gateway 10.151.79.69
```

**BLITAR (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.252.0
```

**LUMAJANG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1
```

**TULUNGAGUNG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1
```

Agar UML dapat mengakses internet, pada UML **SURABAYA** diketikkan perintah ```iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16```.

Kemudian pada 4 router yaitu **SURABAYA**, **PASURUAN**, **BATU**, dan **KEDIRI** ditambahkan route baru (pada router lain tidak perlu, karena hanya memerlukan route 0.0.0.0/0 di mana secara otomatis di-setting pada UML).

Routing menggunakan CIDR jauh lebih sederhana karena mereka sudah terkelompokkan dari pembagian IP-nya, sehingga untuk setiap UML memerlukan dari gabungan subnet berikut (dari gambar penggabungan subnet di atas):
- **SURABAYA** = A1, E2, F1, Malang, Mojokerto
- **PASURUAN** = A8, C2
- **BATU** = B3, A10, C1, Malang
- **KEDIRI** = B1, Malang

Karena di UML setiap ada restart, route akan hilang, maka perintah menambahkan route disimpan dalam sebuah file bash, misal kita simpan dengan nama route.sh, berarti ketikkan perintah ```nano route.sh``` dan tambahkan route berikut untuk keempat UML:

**SURABAYA**
```
route add -net 192.168.128.0 netmask 255.255.128.0 gw 192.168.192.2
route add -net 192.168.0.0 netmask 255.255.192.0 gw 192.168.32.2
route add -net 192.168.64.0 netmask 255.255.252.0 gw 192.168.64.2
route add -net 10.151.79.64 netmask 255.255.255.252 gw 10.151.79.66
route add -net 10.151.79.68 netmask 255.255.255.252 gw 192.168.32.2
```

**PASURUAN**
```
route add -net 192.168.128.0 netmask 255.255.224.0 gw 192.168.144.2
route add -net 192.168.160.0 netmask 255.255.252.0 gw 192.168.160.2
```

**BATU**
```
route add -net 192.168.16.0 netmask 255.255.252.0 gw 192.168.16.3
route add -net 192.168.16.0 netmask 255.255.252.0 gw 192.168.16.2
route add -net 192.168.20.0 netmask 255.255.252.0 gw 192.168.20.2
route add -net 192.168.0.0 netmask 255.255.240.0 gw 192.168.8.2
route add -net 10.151.79.68 netmask 255.255.255.252 gw 192.168.8.2
```

**KEDIRI**
```
route add -net 10.151.79.68 netmask 255.255.255.252 gw 10.151.79.70
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.4.3
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.4.2
```

Untuk menjalankan bash script pada UML, menggunakan perintah ```source```, sehingga untuk menjalankan ```route.sh``` dengan perintah ```source route.sh```.
