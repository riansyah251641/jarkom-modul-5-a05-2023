# Jarkom-Modul-5-A05-2023

- Muhammad Febriansyah (5025211164)
- Layyinatul Fuadah (5025211207)

## Pembagian Kelompok Subnet VLSM (Variable Length Subnet Masking)

![Pembagian Subnet](/img/topologi.png)

### Penjelasan

- Richter adalah DNS Server
- Revolte adalah DHCP Server
- Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
- Jumlah Host pada LaubHills adalah 255
- Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

kemudian dilakukan pepentuan jumlah alamat IP yang dibutuhkan oleh tiap subnet.

| **Subnet** | **Jumlah IP** | **Netmask** |
| :--------: | :-----------: | :---------: |
|     A1     |       2       |     /30     |
|     A2     |       2       |     /30     |
|     A3     |     1023      |     /21     |
|     A4     |       2       |     /30     |
|     A5     |       2       |     /30     |
|     A6     |      66       |     /25     |
|     A7     |      514      |     /22     |
|     A8     |      256      |     /24     |
|     A9     |       2       |     /30     |
|    A10     |       2       |     /30     |
| **Total**  |   **1871**    |   **/20**   |

## Tree pembagian IP

Subnet utama/besar dibentuk melalui NID 192.171.0.0 dengan netmask /20. dan diperoleh sebagai berikut:

![Tree IP](/img/tree%20ip%20rian.png)

## Pembagian IP masing masing node

Kemudian dilakukan pembagian IP sesuai dengan subnet yang telah dibagi berdasarkan tree yang telah dibuat.

## Konfigurasi Router + IP pada GNS3

| Subnet | Node           | IP            | Netmask         | Length | NID           | Broadcast      |
| ------ | -------------- | ------------- | --------------- | ------ | ------------- | -------------- |
| A1     | Aura           | 192.171.0.21  | 255.255.255.252 | 30     | 192.171.0.20  | 192.171.0.23   |
|        | Heiter         | 192.171.0.22  | 255.255.255.252 | 30     |               |                |
| A2     | Aura           | 192.171.0.17  | 255.255.255.252 | 30     | 192.171.0.16  | 192.171.0.19   |
|        | Frieren        | 192.171.0.18  | 255.255.255.252 | 30     |               |                |
| A3     | Heiter         | 192.171.8.1   | 255.255.248.0   | 21     | 192.171.8.0   | 192.171.15.255 |
|        | TurkRegion     | DHCP          | 255.255.248.0   | 21     |               |                |
| A4     | Frieren        | 192.171.0.13  | 255.255.255.252 | 30     | 192.171.0.12  | 192.171.0.15   |
|        | Stark          | 192.171.0.14  | 255.255.255.252 | 30     |               |                |
| A5     | Frieren        | 192.171.0.9   | 255.255.255.252 | 30     | 192.171.0.8   | 192.171.0.11   |
|        | Himmel         | 192.171.0.10  | 255.255.255.252 | 30     |               |                |
| A6     | Himmel         | 192.171.0.129 | 255.255.255.128 | 25     | 192.171.0.128 | 192.171.0.255  |
|        | Fern           | 192.171.0.130 | 255.255.255.128 | 25     |               |                |
|        | SchwerMountain | DHCP          | 255.255.255.128 | 25     |               |                |
| A7     | Heiter         | 192.171.4.1   | 255.255.252.0   | 22     | 192.171.4.0   | 192.171.7.255  |
|        | Sein           | 192.171.4.2   | 255.255.252.0   | 22     |               |                |
|        | GrabForest     | DHCP          | 255.255.252.0   | 22     |               |                |
| A8     | Himmel         | 192.171.1.1   | 255.255.255.0   | 24     | 192.171.1.0   | 192.171.1.255  |
|        | LaubHills      | DHCP          | 255.255.255.0   | 24     |               |                |
| A9     | Fern           | 192.171.0.5   | 255.255.255.252 | 30     | 192.171.0.4   | 192.171.0.7    |
|        | Richter        | 192.171.0.6   | 255.255.255.252 | 30     |               |                |
| A10    | Fern           | 192.171.0.1   | 255.255.255.252 | 30     | 192.171.0.0   | 192.171.0.3    |
|        | Revolte        | 192.171.0.2   | 255.255.255.252 | 30     |               |                |

### Konfigurasi ETH

- Revolte

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.2
	netmask 255.255.255.252
	gateway 192.171.0.1
	up echo nameserver 192.171.0.6 > /etc/resolv.conf
```

- Richter

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.6
	netmask 255.255.255.252
	gateway 192.171.0.5
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Fern

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.130
	netmask 255.255.255.128
	gateway 192.171.0.129
	up echo nameserver 192.171.0.6 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.171.0.5
	netmask 255.255.255.252


# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.171.0.1
	netmask 255.255.255.252
```

- SchewerMountain1

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- LaubHills

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- Himmel

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.10
         netmask 255.255.255.252
         gateway 192.171.0.9
	 up echo nameserver 192.171.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.171.0.129
         netmask 255.255.255.128

auto eth2
iface eth2 inet static
         address 192.171.1.1
         netmask 255.255.255.0
```

- Frieren

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.18
         netmask 255.255.255.252
         gateway 192.171.0.17
	 up echo nameserver 192.171.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.171.0.13
         netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.171.0.9
         netmask 255.255.255.252
```

- Stark

```
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.14
         netmask 255.255.255.252
         gateway 192.171.0.13
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Aura

```bash
auto eth0
iface eth0 inet static
    address 192.168.122.2
    netmask 255.255.255.0
    gateway 192.168.122.1

auto eth2
iface eth2 inet static
       address 192.171.0.17
       netmask 255.255.255.252

auto eth1
iface eth1 inet static
      address 192.171.0.21
      netmask 255.255.255.252
```

- Heiter

```bash
auto eth0
iface eth0 inet static
         address 192.171.0.22
         netmask 255.255.255.252
         gateway 192.171.0.21
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth2
iface eth2 inet static
         address 192.171.8.1
         netmask 255.255.248.0

auto eth1
iface eth1 inet static
         address 192.171.4.1
         netmask 255.255.252.0
```

- TurkRegion

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- Sein

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.4.2
	netmask 255.255.252.0
	gateway 192.171.4.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- GrabForest

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

## Routing

- Himmel

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.130
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.130
```

- Frieren

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.10
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.10
route add -net 192.171.0.128 netmask 255.255.255.128 gw 192.171.0.10
route add -net 192.171.1.0 netmask 255.255.255.0 gw 192.171.0.10
```

- Aura

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.128 netmask 255.255.255.128 gw 192.171.0.18
route add -net 192.171.1.0 netmask 255.255.255.0 gw 192.171.0.18
route add -net 192.171.0.8 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.12 netmask 255.255.255.252 gw 192.171.0.18

route add -net 192.171.8.0 netmask 255.255.248.0 gw 192.171.0.22
route add -net 192.171.4.0 netmask 255.255.252.0 gw 192.171.0.22
```

## Konfigurasi DHCP

### DHCP Server

dilakukan instalasi isc-dhcp-server dengan perintah

```bash
apt-get update
wait
apt-get install isc-dhcp-server -y
wait

echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

cp ~/dhcpd.conf /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

Pada file dhcpd.conf, dilakukan konfigurasi seperti berikut

```bash

option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 192.171.0.0 netmask 255.255.255.252 {
}

subnet 192.171.0.128 netmask 255.255.255.128 {
    range 192.171.0.131 192.171.0.254;
    option routers 192.171.0.129;
    option broadcast-address 192.171.0.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.1.0 netmask 255.255.255.0 {
    range 192.171.1.2 192.171.1.254;
    option routers 192.171.1.1;
    option broadcast-address 192.171.1.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.8.0 netmask 255.255.248.0 {
    range 192.171.8.2 192.171.15.254;
    option routers 192.171.8.1;
    option broadcast-address 192.171.15.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.4.0 netmask 255.255.252.0 {
    range 192.171.4.3 192.171.7.254;
    option routers 192.171.4.1;
    option broadcast-address 192.171.7.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}
```

- `option domain-name-servers` adalah DNS Server yang akan digunakan
- `default-lease-time` adalah waktu lease default
- `max-lease-time` adalah waktu lease maksimal
- `subnet` adalah subnet yang akan digunakan
- `range` adalah range IP yang akan digunakan
- `option routers` adalah IP dari router yang akan digunakan
- `option broadcast-address` adalah IP broadcast yang akan digunakan

### DHCP Relay

Install isc-dhcp-relay pada route **Himmel dan Heiter** dengan perintah

```bash
# Configuration DHCP Relay
apt-get update
wait
apt-get install isc-dhcp-relay -y
wait

echo '
SERVERS="192.171.0.2"
INTERFACES="eth0 eth1 eth2"
OPTIONS="-m replace"
' >  /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' >  /etc/sysctl.conf
```

- `SERVERS` adalah IP dari DHCP Server yang akan digunakan
- `INTERFACES` adalah interface yang akan digunakan untuk DHCP Relay
- `OPTIONS` adalah opsi yang digunakan untuk DHCP Relay
- `net.ipv4.ip_forward=1` adalah opsi untuk mengaktifkan ip forwarding

## Konfigurasi DNS

```
apt-get update
wait

apt-get install bind9 -y
wait
cp ~/named.conf.options /etc/bind/

service bind9 restart
```

- `named.conf.options` adalah konfigurasi DNS Server

Berikut adalah isi dari file `named.conf.options`

```bash
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
};
```

- `forwarders` adalah DNS Server yang akan digunakan untuk forward
- `allow-query` adalah opsi untuk mengizinkan query dari semua IP
- `auth-nxdomain no` adalah opsi untuk mengizinkan domain yang tidak ada

## Konfigurasi Web Server

Untuk konfigurasi web server, kita akan menginstall nginx pada node **Sein dan Stark** dengan perintah

```bash
apt-get update
wait
apt-get install nginx -y
wait
cp ~/index.nginx-debian.html /var/www/html
service nginx start
apt-get install netcat -y
```

- `index.nginx-debian.html` adalah file html yang akan ditampilkan pada web server nanti
- `netcat` adalah aplikasi yang digunakan untuk mengirimkan data ke web server

## Soal

Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

### Solusi

Pada node **Aura**, dilakukan konfigurasi iptables dengan perintah

```bash
iptables -t nat -A POSTROUTING -s 192.171.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.2
```

- `-t nat` adalah opsi untuk menambahkan rule pada tabel nat
- `-A POSTROUTING` adalah opsi untuk menambahkan rule pada chain POSTROUTING
- `-s` adalah opsi untuk menentukan source IP
- `-o` adalah opsi untuk menentukan interface
- `-j SNAT` adalah opsi untuk melakukan SNAT
- `--to-source` adalah opsi untuk menentukan IP yang akan digunakan untuk SNAT

### Testing

Pada node **Client**, kita akan melakukan ping ke google.com dengan perintah

```bash
ping google.com
```

![output jawaban](</img/soal%201%20(1).png>)
![output jawaban](</img/soal%201%20(2).png>)
![output jawaban](</img/soal%201%20(3).png>)

### Soal 2

Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

### Solusi

Untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP, kita akan mengkonfigurasi iptables pada node **SchewerMountain** dengan perintah

```bash
# Berisikhkan semua aturan yang ada jika diperlukan
iptables -F
# Izinkan koneksi yang masuk pada port 8080 TCP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

# Jatuhkan semua koneksi TCP yang tidak menuju ke port 8080
iptables -A INPUT -p tcp ! --dport 8080 -j DROP

# Jatuhkan semua koneksi UDP
iptables -A INPUT -p udp -j DROP
```

- `iptables -F` adalah opsi untuk menghapus semua rule yang ada

- `iptables -A INPUT -p tcp --dport 8080 -j ACCEPT` adalah opsi untuk menambahkan rule pada chain INPUT untuk menerima koneksi TCP pada port 8080

- `iptables -A INPUT -p tcp ! --dport 8080 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi TCP yang tidak menuju ke port 8080

### Testing

Untuk melakukan testing, kita akan menggunakan node **SchewerMountain** dengan **Revolte**. dengan menggunakan netcat pada port 8080 dan 8090 sebagai perbandingan

![output jawaban](</img/soal 2 (1).png>)
![output jawaban](</img/soal 2 (2).png>)

### Soal 3

Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

### Solusi

Untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, dilakukan konfigurasi iptables pada node **Revolte** dan **Richter** dengan perintah sebagai berikut

```bash
# Soal No 3
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

- `iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi ICMP yang lebih dari 3
- `--connlimit-above 3` adalah opsi untuk menentukan batas koneksi
- `--connlimit-mask 0` adalah opsi untuk menentukan mask

### Testing

Untuk melakukan testing, dilakukan 'ping 192.171.0.2' pada semua server client yang memperlihatkan koneksi yang lebih dari 3 akan tidak dapat diakses
![output jawaban](</img/soal 3 (4).png>)
![output jawaban](</img/soal 3 (3).png>)
![output jawaban](</img/soal 3 (2).png>)
![output jawaban](</img/soal 3 (1).png>)

### Soal 4

Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

### Solusi

dilakukan konfigurasi iptables pada node **Sein** dan **Stark** dengan perintah

```bash
# Soal No 4
iptables -A INPUT -p tcp --dport 22 -s 192.171.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

- -s `192.171.4.0/22` adalah opsi untuk menentukan source IP yang diizinkan pada kali ini adalah subnet `192.171.4.0/22` yaitu di block A10 yang merupakan GrobeForest
- `iptables -A INPUT -p tcp --dport 22 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi TCP pada port 22 yang tidak berasal dari subnet A10

### Testing

Untuk melakukan testing tersebut kita akan menggunakan nmap pada netcat pada node 'grobeforest' dan node lainnya misal di 'turkregion;

```
nmap 192.171.4.2 -p 22
```

![output jawaban](</img/soal 4 (1).png>)
![output jawaban](</img/soal 4 (2).png>)

### Soal 5

Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

### Solusi

dilakukan konfigurasi iptables pada node **Sein** dan **Stark** dengan perintah

```bash
# Izinkan akses ke Web Server pada Senin-Jumat pukul 08.00-16.00
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```

### Testing

Untuk melakukan testing digunakan ping yang megnarah pada node server dan diuabh dengan menggunakan setting date

```
ping 192.171.4.2
```

![output jawaban](</img/soal 5.png>)
dapat dilihat jika beraja di jam yang sesuai maka ping dapat berjalan jika dilakukan di jam yang tidak sesuai maka ping menunjukkan 'Destination Port Unreachable'

# Soal 6

Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

### Solusi

pada konfigurasi iptables pada node **Sein** dan **Stark** ditambahkan atau di ubah menjadi sebagai berikut

```bash
iptables -F

iptables -A INPUT -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j REJECT
iptables -A INPUT -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j REJECT
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```

dilakukan 'iptables -F' terlebih dahulu untuk menghapus lalu dimasukkan kembali perintah nomor 5 dibawah nomor 66 karena urutan perintah dapat berpengaruh satu sama lain

## Testing

![output jawaban](/img/soal%206.png)

# Soal 7

Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## Solusi

dilakukan konfigurtasi iptables di router yang terhubung dengan webserver, salah satunya adalah heiter. Pada node heiter dilakukan

```bash

iptables -A PREROUTING -t nat -p tcp --dport 80 -d 192.171.4.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.171.4.2

iptables -A PREROUTING -t nat -p tcp --dport 80 -d 192.171.4.2 -j DNAT --to-destination 192.171.0.14

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 192.171.0.14 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.171.0.14

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 192.171.0.14 -j DNAT --to-destination 192.171.4.2

```

## Testing

Kemudian dapat dilakukan testing dengan cara membuka koneksi pada webserver yaitu sein dan stark dengan syntax berikut untuk port 80 `while true; do nc -l -p 80 -c 'echo "sein"'; done` dan `while true; do nc -l -p 80 -c 'echo "stark"'; done`.

Sedangkan untuk port 443 `while true; do nc -l -p 443 -c 'echo "sein"'; done` dan `while true; do nc -l -p 443 -c 'echo "stark"'; done`.
Berikut adalah hasil testing yang daapt ditampilkan:
![output jawaban](</img/soal%207%20(3).png>)
![output jawaban](</img/soal%207%20(2).png>)
![output jawaban](</img/soal%207%20(1).png>)

# Soal 8

Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## Solusi

pada konfigurasi iptables pada node **Sein** dan **Stark** ditambahkan atau di ubah menjadi sebagai berikut

```bash
mulai=$(date -d "2023-10-19T00:00" +"%Y-%m-%dT%H:%M")
Berakhir=$(date -d "2024-02-15T00:00" +"%Y-%m-%dT%H:%M")
iptables -A INPUT -p tcp -s 192.171.0.2/30 --dport 80 -m time --datestart "$mulai" --datestop "$Berakhir" -j DROP
```

## Testing

Kemudian buka pada node revolt lalu ping dengan netcat menuju node server. dan main ubah pada date.

![output jawaban](/img/soal8)

# Soal 9

Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. (clue: test dengan nmap).

## Solusi

pada konfigurasi iptables pada node **Sein** dan **Stark** ditambahkan atau di ubah menjadi sebagai berikut

```bash
iptables -N new_port
iptables -A INPUT -m recent --name new_port --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name new_port --update --seconds 600 --hitcount 20 -j DROP
iptables -A INPUT -m recent --name new_port --set -j ACCEPT
iptables -A FORWARD -m recent --name new_port --set -j ACCEPT
```

## Testing

dilakukan test dengan `ping 192.171.4.2 -c 25` maka ping hanya akan keluar sebanyak 20 saja

![output jawaban](/img/soal%209.png)

# Soal 10

Belumm
#   j a r k o m - m o d u l - 5 - a 0 5 - 2 0 2 3  
 