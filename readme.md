## No1-5
### Soal-5
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Kemudian, karena masih banyak spell yang harus dikumpulkan, bantulah para petualang untuk memenuhi kriteria berikut.:
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 (2)
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 (3)
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut (4)
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit (5)

### Topologi
![Screenshot 2023-11-19 175045](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/c0a1f90c-4bc0-4c8c-9b76-9a439eb4bd46)

### Konfigurasi pada Himmel(DHCP Server)
 - Lakukan `apt-get update` dan `apt-get install isc-dhcp-server`
 - pada file /etc/default/is-dhcp-server konfigurasi nya akan berbentuk seperti berikut
 - ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/a8094faa-e33a-49e7-8e83-216136827d15)
 - dan pada dhcpd.conf akan berbentuk seperti berikut
 - ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/68acaa50-1262-4f70-a809-cb989de4c0c4)
 - kemudian `service isc-dhcp-server restart`


### Konfigurasi pada Aura(router)
Pada file isc-dhcp-relay
![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/6feaaff0-cfd4-46d7-8c62-f61d8c6569bb)
Pada file sysctl.conf
ditambahkan `net.ipv4.ip_forward=1`

### testing
Pada client lakukan `ip a` maka pada eth pertama akan ditampilkan ip client, dan juga client dapat ping google.com

## Soal 6-12
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3. (6)
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
  Lawine, 4GB, 2vCPU, dan 80 GB SSD.
  Linie, 2GB, 2vCPU, dan 50 GB SSD.
  Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second. (7)
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
Nama Algoritma Load Balancer
Report hasil testing pada Apache Benchmark
Grafik request per second untuk masing masing algoritma. 
Analisis (8)

Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire. (9)
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/ (10)
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. (11) hint: (proxy_pass)
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. (12) hint: (fixed in dulu clinetnya)

### Penyelesaian
### SOal 6
  konfigurasi untuk semua worker
 - pertama download terlebih dahulu file yang telah di sediakan `wget --no-check-certificate 'https://drive.usercontent.google.com/download?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download&authuser=0&confirm=t&uuid=0e499712-8150-42d4-a474-b29dfb026ab6&at=APZUnTVBse4ducwDDntmAkLSWB1_:1699949521984' -O  granz.channel.f08.com`
 - Pada file jarkom akan berisi seperti hal berikut
   ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/66fced79-dbae-40f3-8ba1-be5f3491ca85)
 - kemudian cp file `cp -r modul-3/ /var/www`
 - dan juga `cp jarkom /etc/nginx/sites-available/`
 - kemudian lakukan `service nginx reload`
 - `service nginx restart`
 - `service php7.3-fpm start`
 - `service php7.3-fpm status`

### Soal 7
  - Pada Client lakukan `apt-get update`
  - `apt-get install apache2-utils`
  - kemudian `ab -n 1000 -c 100 http://granz.channel.f08.com/` untuk 1000 request dam 100 request/sec
### Soal 8
  - Pada load balancer ubah algoritma yang digunakana pada file lb jarkom tambahkan algoritma yang digunakan
  - Round Robin

    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/ab6d61ce-0b64-44d0-969d-1f36f34b42a3)

    hasilnya:

    ![RoundRobinN08](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/120382d9-69c6-4631-a2b1-1de2299322b5)
  - Least Conn

    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/41c1b1ed-8796-4d7c-aeec-b32340c7d533)

    hasilnya:

    ![LeastConnNo8](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/f9723673-5259-4cd6-8c18-74a6feb50fb5)
  - Ip Hash

    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/aa960a47-d463-40b5-bee2-5f2dd41bf00d)

    hasilnya:

    ![IpHashNo8](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/45728239-1250-4163-aa69-060311398254)
  - Generic Hash

    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/8f13a806-b23d-4d25-80cc-ddb6e08ea91a)

    hasilnya:

    ![GenericHashNo8](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/81cb1c25-cef3-4de6-b86f-86a238e63988)

### Soal 9
  - Kembalikan Algoritma Load Balancer ke Round Robin
  - lakukan testing dengan 3 worker

    ![3WorkerNo9](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/56332fc3-713a-4ada-a107-38ec1ec96e8e)
  
  - Lakukan testing dengan 2 worker, dengan cara stop 1 worker yang ada

    ![2WorkerNo9](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/f6f29a18-f757-4675-91d1-540029079df4)
  - Lakukan Testing dengan 1 worker, dengan cara stop 2 worker yang ada

    ![1WorkerNo9](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/ecf36ed1-f571-4df9-80b5-723278eaf4fb)

### Soal 10
  - Jalankan perintah `mkdir /etc/nginx/rahasiakita` dan `htpasswd -c -b /etc/nginx/rahasiakita/.htpasswd netics ajkf08`
  - dan jangan lupa untuk `service nginx reload` dan `service nginx restart`
  ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/de60efdb-6001-41b7-985e-f4fbe0d6f1dd)

### Soal 11
  - Ubahlah konfigurasi pada Load balance file /etc/nginx/lb-jarkom menjadi seperti berikut:
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/cd4b38bf-0964-483e-a1bf-9fcd14a709c0)
  - jangan lupa untuk di restart `service nginx reload`
  - `service nginx restart`

### Soal 12
  - Ubahlah konfigurasi pada Load balance file /etc/nginx/lb-jarkom dengan penambahan allow[ip.prefix] seperti berikut:
  ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/b828b6fc-efa9-4283-8be5-d3af2994d11b)
  - jangan lupa untuk di restart `service nginx reload`
  - `service nginx restart`

## soal 13-20
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern. (13)
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer (14)
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
POST /auth/register (15)
POST /auth/login (16)
GET /me (17)
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern. (18)
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.(19)
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second. (20)

## Penyelesaian 13-20
### Soal 13
  Ubahalah Configurasi beberapa file menjadi seperti berikut
  - Pada file /etc/mysql/mariadb.conf.d/50-server.cnf seperti pada file yang telah disediakan
  - Pada file /etc/mysql/my.conf
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/41e46b5e-c405-4289-a83e-eac0f0889f03)
  - jangan lupa untuk di restart `service mysql restart`
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/04c9f58d-17bf-477a-8f07-4bb71764dc9f)
  - Pada denken kita perlu membuat user baru terlebih dahulu dengan command berikut
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/e2731180-6d5c-4016-8aec-e43052a679a0)
  - Berikut merupakan konfigurasi untuk laravel worker:
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/238eb3f0-75ae-4190-a96b-bede2c1ffbef)
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/89b266ce-8bce-4b85-9a99-931a41380e26)

### Soal 14
  - Command untuk worker
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/ce71280d-ad89-4c30-bf0a-07b0f0a3db87)
  - ubahlah .env menjadi menggunakan database kita yang sebelumyan sudah dibuat
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/a7708c36-f779-4cfe-93dd-5a04f3dc9015)
  
### Soal 15-17
  - bikin file register_data.json di root, isinya:
`{
  "username": "kelompokf08",
  "password": "kelompokf08"
}`

  - Terus bikin login_data.json di root, isinya sesuaiin sama username sama password yang udah didaftarin, contohnya kek gini
`{
  "username": "kelompokf08",
  "password": "ajkf08"
}`

  - Buat ngetest bisa pake kumpulan syntax ini:
    - Buat register, data diambil dari file register_data2.json:
      `ab -n 100 -c 10 -T 'application/json' -p register_data2.json -g register_results2.data http://192.225.4.1:8001/api/auth/register`

    - Buat register tapi pake curl (cuma 1x dan gabisa dicek load)
        `curl -X POST -H "Content-Type: application/json" -d '{"username": "akmal123", "password": "testing"}' http://192.225.4.1:8001/api/auth/register`

    - Buat login tapi pake curl (cuma bisa 1 data dan gada load)
        `curl -X POST -H "Content-Type: application/json" -d '{"username": "kelompokf08", "password": "ajkf08"}' http://192.225.4.2:8002/api/auth/login`

    - Buat login sama nyimpen ke file token.tx (tiap login pake akun berbeda, isi token.txt bakal selalu update.
        `curl -X POST -H "Content-Type: application/json" -d '{"username": "kelompokf08", "password": "ajkf08"}' http://192.225.4.2:8002/api/auth/login | jq -r '.token' > token.txt`

    - Buat ngetest get 1x + gabisa liat load
        `token=$(cat token.txt); curl -H "Authorization: Bearer $token" http://192.225.4.2:8002/api/me
        {"id":1,"username":"kelompokf08","created_at":"2023-11-15T03:56:54.000000Z","updated_at":"2023-11-15T03:56:54.000000Z"}`

    - Buat get /me langsung 100 request
        `# token=$(cat token.txt); ab -n 1000 -c 10 -H "Authorization: Bearer $token" http://192.225.4.2:8002/api/me`

untuk ngecek apakah emang bener ngelakuin 100 request bersamaan, bisa cek log di worker yang dipake. Misal kita login ke 192.225.4.2:8002, nah kita cek /var/log/nginx/xxx_access.log.
Untuk cek apakah user sudah masuk atau belum bisa langsung cek dari database:
  `USE DATABASE dbkelompokf08;
   SELECT * FROM users;`

### SOal 18
  - Pada denken(Load Balancer) buat lah file baru laravel-jarkom dengan isi seperti berikut:
        ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/0ddf4015-fd95-4293-b3a4-b607f7137dc7)
  - hapus configurasi sebelumnya pada /etc/nginx/sites-available dan /etc/nginx/sites-enable
  - lakukan command `ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled`
  - `service nginx reload`
  - `service nginx restart`
  - untuk testing `lynx http://192.225.2.2` ip dari load balancer

### Soal 19
  - Pada worker Laravel
  - `cp /etc/php/8.0/fpm/pool.d/www.conf ./`
  - kemudian copy lagi untuk menjadi mock up `cp www.conf template1`
  - pada file tersebut ubah lah beberapa syntax menjadi seperti berikut
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/41ca4ced-9286-4237-ae0f-1bdfdccfbc76)
  - copy file tersebut ke tempat semula `cp template1 /etc/php/8.0/fpm/pool.d/www.conf`
  - kemudian restart `service php8.0-fpm restart`
  - Lakukan langkah yang sama di worker lain, terus tes aja di client kek gini
`ab -n 100 -c 10 -T 'application/json' -p register_data2.json -g register_results2.data http://riegel.canyon.f08.com/api/auth/register`
  - kemudian catat hasil tersebut
  - untuk variasi, ganti angka angka pada bagian
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/d32282b9-efe6-4d9e-8cb7-088ff66b409e)
  - buat file tersebut menjadi template2 
  - kemudian copy file tersebut ke tempat semula `cp template1 /etc/php/8.0/fpm/pool.d/www.conf`
  - kemudian restart `service php8.0-fpm restart`
  - dan catat lagi hasilnya
  - lakukan hal tersebut dengan berulang kali

### Soal 20
  - Pada Load Balancer
  - ubahlah file laravel-jarkom menjadi menggunakan algoritma Least_Conn dengan menambahkan `least_conn` pada file tersebut
    ![image](https://github.com/MyNameIsSyukra/Jarkom-Modul-3-F08-2023/assets/90988646/94fc62a7-ca0f-4dc7-8762-dd21ccfa2198)
  - jangan lupa untuk restart `Service nginx restart`
  - untuk testing pada client `ab -n 100 -c 10 -T 'application/json' -p register_data2.json -g register_results2.data http://riegel.canyon.f08.com/api/auth/register`

  




