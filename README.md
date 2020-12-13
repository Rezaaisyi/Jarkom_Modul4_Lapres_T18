# Jarkom_Modul4_Lapres_T18

- M. Reza Aisyi 05311840000031
- Agnes Lesmono 05311840000044
## VLSM - CPT

| Subnet | IP butuh | IP dikasih | Alamat | Netmask |
| ------ | -------- | ---------- | ------ | ------- |
A1 |1001|1022|192.168.4.0|/22|
A2|2|2|192.168.0.0|/30|
A3|2|2|192.168.0.4|/30|
A4|101|126|192.168.0.128|/25|
A5|701|1022|192.168.8.0|/22|
A6|2021|2046|192.168.24.0|/21|
A7|2|2|192.168.0.8|/30|
A8|502|510|192.168.2.0|/23|
A9|13|14|192.168.0.16|/28|
A10|521|1022|192.168.12.0|/22|
A11|2|2|192.168.0.12|/30|
A12|252|254|192.168.1.0|/24|
A13|721|1022|192.168.16.0|/22|
**SUM**|**5841**|||**/19**|

Subnet total menggunakan NID **192.168.0.0** netmask **/19**. Pembagian IP berdasarkan NID dan netmask dapat dilihat seperti gambar berikut:

![pohon](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/VLSM/pohon%20VLSM.png)



## CIDR (Classless Inter Domain Routing) - UML
Menggabungkan subnet-subnet paling bawah dalam topologi, berikut penggabungannya: </br>
![lingkaran](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/CIDR/1.png)
Tree yang dibuat : </br>
![Tree](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/CIDR/tree.png)
Pertama-tama membuat file ```topologi.sh``` dengan konfigurasi berikut:
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.61 eth1=daemon,,,switch13 eth2=daemon,,,switch1 eth3=daemon,,,switch2 eth4=daemon,,,switch4  mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2  eth1=daemon,,,switch19 eth2=daemon,,,switch3 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3  eth1=daemon,,,switch16 eth2=daemon,,,switch15 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch4  eth1=daemon,,,switch22 eth2=daemon,,,switch21 eth3=daemon,,,switch5  mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch5  eth1=daemon,,,switch18 eth2=daemon,,,switch17 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22  eth1=daemon,,,switch25 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17  eth1=daemon,,,switch20 mem=64M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
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
