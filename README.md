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

NID dibagikan kepada subnet topologi dapat dilihat pada gambar dibawah (bisa dilihat juga di file pkt)

![gambar](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/VLSM/top%20(2).png)

Untuk routing pada CPT, static route tiap router adalah sebagai berikut :
&nbsp;

**SURABAYA**
```
192.168.0.4/30 via 192.168.0.2
192.168.8.0/22 via 192.168.0.2
192.168.0.128/25 via 192.168.0.2
192.168.24.0/21 via 192.168.0.2
192.168.2.0/23 via 192.168.0.10
192.168.0.16/28 via 192.168.0.10
192.168.12.0/22 via 192.168.0.10
192.168.0.12/30 via 192.168.0.10
192.168.1.0/24 via 192.168.0.10
192.168.16.0/22 via 192.168.0.10
10.151.71.124/30 via 192.168.0.10
```

**BATU**
```
0.0.0.0/0 via 192.168.0.9
192.168.1.0/24 via 192.168.0.14
192.168.16.0/22 via 192.168.0.14
192.168.0.16/28 via 192.168.2.2
10.151.71.124/30 via 192.168.0.14
```


**KEDIRI**
```
0.0.0.0/0 via 192.168.0.13
192.168.16.0/12 via 192.168.1.2
```


**BLITAR**
```
0.0.0.0/0 via 192.168.1.1
```


**PASURUAN**
```
0.0.0.0/0 via 192.168.0.1
192.168.0.128/25 via 192.168.0.6
192.168.24.0/21 via 192.168.0.6
```

**PROBOLINGGO**
```
0.0.0.0/0 via 192.168.0.5
```


## CIDR (Classless Inter Domain Routing) - UML
Menggabungkan subnet-subnet paling bawah dalam topologi, berikut penggabungannya: </br>
![lingkaran](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/CIDR/1.png)
Tree yang dibuat : </br>
![Tree](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/CIDR/TREE.png) </br>
Tabel : </br>
![Tree](https://github.com/Rezaaisyi/Jarkom_Modul4_Lapres_T18/blob/main/CIDR/table.PNG) </br>
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
address 192.168.144.1
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.160.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.2
netmask 255.255.255.252
gateaway 192.168.192.1 
```

**MOJOKERTO (Sebagai Server)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.151.71.123
netmask 255.255.255.140
gateaway 192.151.71.124 
```

**SAMPANG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.64.2  
netmask 255.255.252.0  
gateaway 192.168.64.1  

```

**PROBOLINGGO (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.1
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.128.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.144.2
netmask 255.255.254.0 
```

**SIDOARJO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateaway 192.168.160.1
```

**BANYUWANGI (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.252.0
gateaway 192.168.128.1 
```

**JEMBER (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.3
netmask 255.255.248.0
gateaway 192.168.128.1
```

**BONDOWOSO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.252
gateaway 192.168.136.1 
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
address 10.151.71.122
netmask 255.255.255.252 
```

**JOMBANG (Sebagai Klien)**
```
 auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.3 
netmask 255.255.254.0  
gateway 192.168.18.2   
```

**MADIUN (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.3
netmask 255.255.254.0

auto eth1
iface eth1 inet static
address 192.168.16.1
netmask 255.255.255.240
```

**BOJONEGORO (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.255.140
gateaway 192.168.16.1 
```

**NGANJUK (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateaway 192.168.20.1 
```

**MALANG (Sebagai Server)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.122
netmask 255.255.255.252
gateway 10.151.71.121 
```

**BLITAR (Sebagai Router)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateaway 192.168.4.1

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
gateaway 192.168.4.1 
```

**TULUNGAGUNG (Sebagai Klien)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateaway 192.168.20.1 
```
