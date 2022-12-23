# Jarkom-Modul-5-C04-2022

Laporan Resmi Praktikum Modul 5 Kelompok C04

## Kelompok C04

| **Nama**                  | **NRP**    |
| ------------------------- | ---------- |
| Muhammad Fuad Salim | 5025201057 |
| Handitanto Herprasetyo | 5025201077 |
| Sastiara Maulikh | 5025201257 |

IP Prefix Kelompok C04 : `192.181`

## Topologi
![topologi](https://user-images.githubusercontent.com/80630201/209289231-407bb52a-8b4c-4b0c-ab4b-f790ed1bc729.png)

Keterangan:

- `Eden` adalah DNS Server
- `WISE` adalah DHCP Server
- `Garden` dan `SSS` adalah Web Server
- Jumlah Host pada `Forger` adalah 62 host
- Jumlah Host pada `Desmond` adalah 700 host
- Jumlah Host pada `Blackbell` adalah 255 host
- Jumlah Host pada `Briar` adalah 200 host

#### Menentukan jumlah subnet pada Topologi
![subnet](https://user-images.githubusercontent.com/80630201/209289220-e1b89900-0618-48ee-883a-51e90f1810b4.png)


#### Menentukan jumlah IP yang dibutuhkan pada subnet

| Subnet    | Jumlah IP | Netmask |
| --------- | --------- | ------- |
| A5        | 701       | /22     |
| A6        | 256       | /23     |
| A7        | 201       | /24     |
| A3        | 63        | /25     |
| A1        | 3         | /29     |
| A8        | 3         | /29     |
| A4        | 2         | /30     |
| A2        | 2         | /30     |
| **Total** | **1231**  | **/21** |

Berdasarkan total IP dan netmask yang dibutuhkan, Subnet besar yang dibentuk memiliki `NID 192.181.0.0` dengan `Netmask /21`.

#### Menghitung pembagian IP berdasarkan NID dan Netmask yang didapatkan
![tree fix](https://user-images.githubusercontent.com/80630201/209289233-9cd0e5d8-eb59-4669-abbd-3a7b547f83d4.jpg)

#### Hasil Pembagian IP
![table](https://user-images.githubusercontent.com/80630201/209289229-ebabf83b-eb1b-4ad9-9978-14c2ed2ce5bc.jpg)

#### Network Configuration

##### Router

- `Strix`

```
auto eth0
iface eth0 inet dhcp
auto eth1
iface eth1 inet static
	address 192.181.0.129
	netmask 255.255.255.252
auto eth2
iface eth2 inet static
	address 192.181.0.133
	netmask 255.255.255.252
```

- `Westalis`

```
auto eth0
iface eth0 inet static
	address 192.181.0.130
	netmask 255.255.255.252
auto eth1
iface eth1 inet static
	address 192.181.0.145
	netmask 255.255.255.248
auto eth2
iface eth2 inet static
	address 192.181.0.1
	netmask 255.255.255.128
auto eth3
iface eth3 inet static
	address 192.181.4.1
	netmask 255.255.252.0
```

- `Ostania`

```
auto eth0
iface eth0 inet static
	address 192.181.0.134
	netmask 255.255.255.252
auto eth1
iface eth1 inet static
	address 192.181.2.1
	netmask 255.255.254.0
auto eth2
iface eth2 inet static
	address 192.181.1.1
	netmask 255.255.255.0
auto eth3
iface eth3 inet static
	address 192.181.0.153
	netmask 255.255.255.248
```

##### Server

- `Eden`

```
auto eth0
iface eth0 inet static
	address 192.181.0.146
	netmask 255.255.255.248
	gateway 192.181.0.145
```

- `WISE`

```
auto eth0
iface eth0 inet static
	address 192.181.0.147
	netmask 255.255.255.248
	gateway 192.181.0.145
```

- `Garden`

```
auto eth0
iface eth0 inet static
	address 192.181.0.154
	netmask 255.255.255.248
	gateway 192.181.0.153
```

- `SSS`

```
auto eth0
iface eth0 inet static
	address 192.181.0.155
	netmask 255.255.255.248
	gateway 192.181.0.153
```

##### Client

Pada Client, IP diberikan secara dinamis menggunakan DHCP. 

- `Forger(62Host)`

```
auto eth0
iface eth0 inet dhcp
```

- `Desmond(700Host)`

```
auto eth0
iface eth0 inet dhcp
```

- `Blackbell(255Host)`

```
auto eth0
iface eth0 inet dhcp
```

- `Briar(200Host)`

```
auto eth0
iface eth0 inet dhcp
```

#### Static Routing Configuration

- `Strix`

```
route add -net 192.181.0.144 netmask 255.255.255.248 gw 192.181.0.130
route add -net 192.181.0.0 netmask 255.255.255.128 gw 192.181.0.130
route add -net 192.181.4.0 netmask 255.255.255.0 gw 192.181.0.130
route add -net 192.181.2.0 netmask 255.255.254.0 gw 192.181.0.134
route add -net 192.181.1.0 netmask 255.255.255.0 gw 192.181.0.134
route add -net 192.181.0.152 netmask 255.255.255.248 gw 192.181.0.134
```

- `Westalis`

```
rote add -net 0.0.0.0 netmask 0.0.0.0 gw 192.181.0.129
```

- `Ostania`

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.181.0.133
```
