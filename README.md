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

