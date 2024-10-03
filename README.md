# Jarkom-Modul-2-IT34-2024

# Kelompok IT34
| Nama                      | NRP         |
| ------------------------- | ----------- |
| Raditya Hardian Santoso    | 5027231033  |
| Rafi Afnaan Fathurrahman  | 5027231040  |

## Topologi
![image](https://github.com/user-attachments/assets/fb471987-9780-499a-8763-daa26690143c)

## IP Address
| Device | Interface | IP Address | Netmask | Gateway |
| ------ | ----------- | ------ | ----------- | ----------- |
| Nusantara    | eth0  | DHCP (192.168.122.1) | | |
|  | eth1  | 10.80.1.1 | 255.255.255.0	| |
|  | eth2  | 10.80.2.1 | 255.255.255.0	| |
|  | eth3  | 10.80.3.1 | 255.255.255.0	| |
| Sriwijaya | eth0  | 10.80.3.6 | 255.255.255.0	| 10.80.3.1 |
| Majapahit | eth0 | 10.80.2.2 | 255.255.255.0	| 10.80.2.1 |
| Tanjungkulai | eth0 | 10.80.2.3 | 255.255.255.0	| 10.80.2.1 |
| Bedaluhu | eth0 | 10.80.2.4 | 255.255.255.0	| 10.80.2.1 |
| Kotalingga | eth0 | 10.80.3.4 | 255.255.255.0	| 10.80.3.1 |
| Solok | eth0 | 10.80.1.2 | 255.255.255.0	| 10.80.1.1 |
| Samaratungga | eth0 | 10.80.1.3 | 255.255.255.0	| 10.80.1.1 |
| Mulawarman | eth0 | 10.80.3.3 | 255.255.255.0	| 10.80.3.1 |
| AlexanderVolta | eth0 | 10.80.3.2 | 255.255.255.0	| 10.80.3.1 |
| Balaraja | eth0 | 10.80.3.5 | 255.255.255.0	| 10.80.3.1 |

## Config
<details>
<summary>Detail Configure</summary>

#### Nusantara (Router)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.80.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.80.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.80.3.1
	netmask 255.255.255.0
```

### Sriwijaya (DNS Master)
```
auto eth0
iface eth0 inet static
	address 10.80.3.6
	netmask 255.255.255.0
	gateway 10.80.3.1
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Majapahit (DNS Slave)
```
auto eth0
iface eth0 inet static
	address 10.80.2.2
	netmask 255.255.255.0
	gateway 10.80.2.1
echo nameserver 192.168.122.1 # Nusantara (Router) > /etc/resolv.conf
```

### Tanjungkulai (Web Server)
```
auto eth0
iface eth0 inet static
	address 10.80.2.3
	netmask 255.255.255.0
	gateway 10.80.2.1
echo nameserver 192.168.122.1 # Nusantara (Router) > /etc/resolv.conf
```

### Bedahulu (Web Server)
```
auto eth0
iface eth0 inet static
	address 10.80.2.4
	netmask 255.255.255.0
	gateway 10.80.2.1
echo nameserver 192.168.122.1 # Nusantara (Router) > /etc/resolv.conf
```

### Kotalingga (Web Server)
```
auto eth0
iface eth0 inet static
	address 10.80.3.4
	netmask 255.255.255.0
	gateway 10.80.3.1
echo nameserver 192.168.122.1 # Nusantara (Router) > /etc/resolv.conf
```

### Solok (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 10.80.1.2
	netmask 255.255.255.0
	gateway 10.80.1.1
echo nameserver 192.168.122.1 # Nusantara (Router) > /etc/resolv.conf
```

### Samaratungga (Client)
```
auto eth0
iface eth0 inet static
	address 10.80.1.3
	netmask 255.255.255.0
	gateway 10.80.1.1
echo nameserver 10.80.3.6 # Sriwijaya (Master) > /etc/resolv.conf
echo nameserver 10.80.2.2 # Majapahit (Slave) >> /etc/resolv.conf
echo nameserver 192.168.122.1 # Nusantara (Router) >> /etc/resolv.conf
```

### Mulawarman (Client)
```
auto eth0
iface eth0 inet static
	address 10.80.3.3
	netmask 255.255.255.0
	gateway 10.80.3.1
echo nameserver 10.80.3.6 # Sriwijaya (Master) > /etc/resolv.conf
echo nameserver 10.80.2.2 # Majapahit (Slave) >> /etc/resolv.conf
echo nameserver 192.168.122.1 # Nusantara (Router) >> /etc/resolv.conf
```

### AlexanderVolta (Client)
```
auto eth0
iface eth0 inet static
	address 10.80.3.2
	netmask 255.255.255.0
	gateway 10.80.3.1
cho nameserver 10.80.3.6 # Sriwijaya (Master) > /etc/resolv.conf
echo nameserver 10.80.2.2 # Majapahit (Slave) >> /etc/resolv.conf
echo nameserver 192.168.122.1 # Nusantara (Router) >> /etc/resolv.conf
```

### Balaraja (Client)
```
auto eth0
iface eth0 inet static
	address 10.80.3.5
	netmask 255.255.255.0
	gateway 10.80.3.1
echo "nameserver 10.80.3.6 # Sriwijaya (Master)
nameserver 10.80.2.2 # Majapahit (Slave)
nameserver 192.168.122.1 # Nusantara (Router)" > /etc/resolv.conf
```

</details>

## Pembahasan Soal
### Soal 1
Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave. 
#### Tahapan
[Link to section](#configure)
#### Dokumentasi
### Soal 2
Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.
#### Tahapan
```bash
# soal 2 =================================

echo 'zone "sudarsana.it34.com" {
	type master;
	file "/etc/bind/jarkom/sudarsana.it34.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it34.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it34.com. root.sudarsana.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS      sudarsana.it34.com.
@       IN      A       10.80.1.2	; IP Solok
www     IN      CNAME   sudarsana.it34.com.
@	IN	AAAA	::1' > /etc/bind/jarkom/sudarsana.it34.com

service bind9 restart 
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya
#### Dokumentasi
![image](https://github.com/user-attachments/assets/c8de36c7-9ffe-486c-9a61-4248043278d9)

### Soal 3
Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.
#### Tahapan
```bash
# soal 3 =================================

echo 'zone "pasopati.it34.com" {
	type master;
	file "/etc/bind/jarkom/pasopati.it34.com";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/pasopati.it34.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it34.com. root.pasopati.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS      pasopati.it34.com.
@       IN      A       10.80.3.4	; IP Kotalingga
www     IN      CNAME   pasopati.it34.com.
@	IN	AAAA	::1' > /etc/bind/jarkom/pasopati.it34.com
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya
#### Dokumentasi
![image](https://github.com/user-attachments/assets/0145d173-17bf-46d9-94c9-2a5de975eace)

### Soal 4
Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.
#### Tahapan
```bash
# soal 4 =================================

echo 'zone "rujapala.it34.com" {
	type master;
	file "/etc/bind/jarkom/rujapala.it34.com";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/rujapala.it34.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     rujapala.it34.com. root.rujapala.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS	rujapala.it34.com.
@       IN      A	10.80.2.3	; IP Tanjungkulai
www	IN	CNAME	rujapala.it34.com
@	IN      AAAA	::1' > /etc/bind/jarkom/rujapala.it34.com

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya
#### Dokumentasi
![image](https://github.com/user-attachments/assets/57157c3d-a3af-4a61-82d5-7e4c6a920173)

### Soal 5 
Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.
#### Tahapan
[Link to section](#ip-address)
[Link to section](#configure)
#### Dokumentasi
![image](https://github.com/user-attachments/assets/7634d094-cd0e-4dd8-846e-7f8f678fe645)
![image](https://github.com/user-attachments/assets/3b911e34-3c71-42a2-ae04-76f55b15823d)
![image](https://github.com/user-attachments/assets/84f0f8ab-91c2-430a-81a8-98510dcde543)

### Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).
#### Tahapan
```bash
# soal 6 =================================

echo 'zone "3.80.10.in-addr.arpa" {
	type master;
	file "/etc/bind/jarkom/3.80.10.in-addr.arpa";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/3.80.10.in-addr.arpa

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it34.com. root.pasopati.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
3.80.10.in-addr.arpa.	IN      NS      pasopati.it34.com.
4			IN	PTR	pasopati.it34.com.' > /etc/bind/jarkom/3.80.10.in-addr.arpa

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya
#### Dokumentasi
![image](https://github.com/user-attachments/assets/9287d2ae-acf1-4944-8189-e9b78524250d)

### Soal 7
Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.
#### Tahapan
```bash
# soal 7 =================================

echo '
zone "sudarsana.it34.com" {
	type slave;
	masters { 10.80.3.6; };
	file "/var/lib/bind/sudarsana.it34.com";
};

zone "pasopati.it34.com" {
	type slave;
	masters { 10.80.3.6; };
	file "/var/lib/bind/pasopati.it34.com";
};

zone "rujapala.it34.com" {
	type slave;
	masters { 10.80.3.6; };
	file "/var/lib/bind/rujapala.it34.com";
};' > /etc/bind/named.conf.local

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Majapahit
```bash
echo 'zone "sudarsana.it34.com" {
	type master;
	notify yes; // soal 7
	also-notify { 10.80.2.2; }; // soal 7
	allow-transfer { 10.80.2.2; }; // soal 7
	file "/etc/bind/jarkom/sudarsana.it34.com";
};' > /etc/bind/named.conf.local

echo 'zone "pasopati.it34.com" {
	type master;
	notify yes; // soal 7
	also-notify { 10.80.2.2; }; // soal 7
	allow-transfer { 10.80.2.2; }; // soal 7
	file "/etc/bind/jarkom/pasopati.it34.com";
};' >> /etc/bind/named.conf.local

echo 'zone "rujapala.it34.com" {
	type master;
	notify yes; // soal 7
	also-notify { 10.80.2.2; }; // soal 7
	allow-transfer { 10.80.2.2; }; // soal 7
	file "/etc/bind/jarkom/rujapala.it34.com";
};' >> /etc/bind/named.conf.local
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya di bagian zone config /etc/bind/named.conf.local
#### Dokumentasi
![image](https://github.com/user-attachments/assets/6367b4e0-b134-4c1b-a028-ae19fd09e11f)
![image](https://github.com/user-attachments/assets/d95a6732-540e-4f71-b3c4-e40a617bf58a)

### Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.
#### Tahapan
```bash
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it34.com. root.sudarsana.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS      sudarsana.it34.com.
@       IN      A       10.80.1.2	; IP Solok
www     IN      CNAME   sudarsana.it34.com.
cakra	IN	A	10.80.2.4	; IP Bedahulu, soal 8
@	IN	AAAA	::1' > /etc/bind/jarkom/sudarsana.it34.com

service bind9 restart 
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya di bagian bind datafile /etc/bind/jarkom/sudarsana.it34.com
#### Dokumentasi
![image](https://github.com/user-attachments/assets/bd8a9901-c695-4a3a-9be1-60dbc35e61d3)

### Soal 9
Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.
#### Tahapan
```bash
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it34.com. root.pasopati.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS      pasopati.it34.com.
@       IN      A       10.80.3.4	; IP Kotalingga
www     IN      CNAME   pasopati.it34.com.
ns1	IN	A	10.80.2.2	; Delegasi ke Majapahit, soal 9
panah	IN	NS	ns1		; soal 9
@	IN	AAAA	::1' > /etc/bind/jarkom/pasopati.it34.com

# soal 9 ==================================

echo '
options {
        directory "/var/cache/bind";

        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Sriwijaya
```bash
# soal 9 =================================

echo '
options {
        directory "/var/cache/bind";

        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

echo 'zone "panah.pasopati.it34.com" {
	type master;
	file "/etc/bind/panah/panah.pasopati.it34.com";
};' >> /etc/bind/named.conf.local

mkdir /etc/bind/panah

cp /etc/bind/db.local /etc/bind/panah/panah.pasopati.it34.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it34.com. panah.pasopati.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS	panah.pasopati.it34.com.
@       IN      A	10.80.3.4	; IP Kotalingga
www	IN	CNAME	panah.pasopati.it34.com.' > /etc/bind/panah/panah.pasopati.it34.com	

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Majapahit
#### Dokumentasi
### Soal 10
Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.
#### Tahapan
```bash
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it34.com. panah.pasopati.it34.com. (
                        2		; Serial
                        604800		; Refresh
                        86400		; Retry
                        2419200		; Expire
                        604800 )	; Negative Cache TTL
;
@       IN      NS	panah.pasopati.it34.com.
@       IN      A	10.80.3.4	; IP Kotalingga
www	IN	CNAME	panah.pasopati.it34.com.
log	IN	A	10.80.3.4	; IP Kotalingga,  soal 10
www.log	IN	CNAME	panah.pasopati.it34.com.	; soal 10' > /etc/bind/panah/panah.pasopati.it34.com	

service bind9 restart
```
Untuk soal ini, config diatas dimasukkan kedalam .bashrc Majapahit
#### Dokumentasi
### Soal 11
Setelah pertempuran mereda, warga IT dapat kembali mengakses jaringan luar dan menikmati meme brainrot terbaru, tetapi hanya warga Majapahit saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit.

#### Tahapan :
1. Akses /etc/bind/named.conf.options pada majapahit dengan membuat file config no11.sh
2. Ubah isinya menjadi
```
   echo ' options {
        directory "/var/cache/bind";

        forwarders {
                8.8.8.8;
                8.8.4.4;
        };

        dnssec-validation auto;

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
}; ' > /etc/bind/named.conf.options
```
3. Lalu restart service dari bind9
```
service bind9 restart
```
4. Lalu, coba tes ping di server selain majapahit apakah berjalan atau tidak
```
ping google.com
```
#### Dokumentasi
![image](https://github.com/user-attachments/assets/76bf6908-293a-4f31-a0c6-00c1da2eaf93)

### Soal 12
Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache.

#### Tahapan :
1. Membuat config file dengan nama no12.sh yang berisi :
```
echo '
nameserver 192.168.122.1
' > /etc/resolv.conf

apt-get update
apt-get install lynx
apt-get install apache2
apt-get install php
apt-get install libapache2-mod-php7.0 -y
apt-get install unzip -y
apt-get install wget -y

cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/pasopati.it34.com.conf

echo '
<VirtualHost *:80>

    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/pasopati.it34.com
    ServerName pasopati.it34.com
    ServerAlias www.pasopati.it34.com

    #LogLevel info ssl:warn

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    #Include conf-available/serve-cgi-bin.conf

</VirtualHost>
' > /etc/apache2/sites-available/pasopati.it34.com.conf

service apache2 start
mkdir /var/www/pasopati.it34.com
a2ensite pasopati.it34.com.conf
wget --no-check-certificate 'https://drive.usercontent.google.com/u/0/uc?id=1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7&export=download' -O lb.zip
unzip lb.zip -d lb
mv lb/* /var/www/pasopati.it34.com

echo '
nameserver 10.80.3.6
' > /etc/resolv.conf

service apache2 restart
```
2. Memberi akses kepada file agar bisa dieksekusi
```
chmod +x no12.sh
```
3. Mengeksekusi file config
```
./no12.sh
```
4. Gunakan Lynx untuk mengakses
```
lynx http://www.pasopati.it34.com
```

#### Dokumentasi
![image](https://github.com/user-attachments/assets/b8a93ecf-60ea-40bb-9bef-f5a28f6e726d)

### Soal 13
Karena Sriwijaya dan Majapahit memenangkan pertempuran ini dan memiliki banyak uang dari hasil penjarahan (sebanyak 35 juta, belum dipotong pajak) maka pusat meminta kita memasang load balancer untuk membagikan uangnya pada web nya, dengan Kotalingga, Bedahulu, Tanjungkulai sebagai worker dan Solok sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya.

#### Tahapan
1. Karena di sini ada yang berperan sebagai Load Balancer dan sebagai worker. Maka kita perlu membuat script berbeda. Untuk script Load Balancer pada Solok adalah sebagai berikut dengan nama file 'no13.sh' :
```
apt-get update
apt-get install apache2 -y

a2enmod proxy
a2enmod proxy_balancer
a2enmod proxy_http
a2enmod lbmethod_byrequests

echo '<VirtualHost *:80>
<Proxy balancer://mycluster>
BalancerMember http://10.69.4.2/
BalancerMember http://10.69.4.3/
BalancerMember http://10.69.4.4/
ProxySet lbmethod=byrequests
</Proxy>

ProxyPass / balancer://mycluster/
ProxyPassReverse / balancer://mycluster/
</VirtualHost>
' > /etc/apache2/sites-available/000-default.conf

service apache2 start
```
2. Untuk script yang di worker (Kotalingga, Bedahulu, Tanjungkulai) adalah sebagai berikut :
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

apt-get update apt-get install apache2 -y apt-get install php -y apt-get install unzip -y

curl -L -o lb.zip --insecure "https://drive.usercontent.google.com/u/0/uc?id=1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7&export=download"

unzip lb.zip rm /var/www/html/index.html cp worker/index.php /var/www/html/index.php
apt-get install libapache2-mod-php7.0
service apache2 start
```
3. Jalankan kedua script tersebut di masing masing, jangan lupa beri autorisasi dahulu
4. Lalu cara menjalankannya dengan menggunakan lynx kepada empat ip (3 worker dan 1 load balancer)
```
lynx 10.80.2.3
lynx 10.80.2.4
lynx 10.80.3.4
lynx 10.80.1.2
```
#### Dokumentasi
![image](https://github.com/user-attachments/assets/fe1df949-2e93-485b-9dab-36c78f769272)
![image](https://github.com/user-attachments/assets/73bbbe83-2b73-405f-a178-37268b9fdf35)
![image](https://github.com/user-attachments/assets/b926fa37-91cc-49b3-b807-4e4663dfba61)
![image](https://github.com/user-attachments/assets/0a297969-8d9d-46f7-90cf-8797f20c67a1)

