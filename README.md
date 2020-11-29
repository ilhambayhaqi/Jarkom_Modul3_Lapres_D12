# Jarkom_Modul3_Lapres_D12
- Muhammad Ilham Bayhaqi - 05111840000069
- Clever Dicki Marpaung - 05111840000116

## Soal 1

![image](https://user-images.githubusercontent.com/57692117/100539746-1d560c00-326b-11eb-82bc-abd10229537b.png)

Membuat Topologi jaringan dengan sesuai dengan gambar topologi diatas ini dengan menjadikan **Surabaya** menjadi router, **Malang** menjadi DNS Server, **Tuban** menjadi DHCP server, dan **Mojokerto** sebagai proxy UML.

Untuk menyelesaikan soal ini dibuat topologi.sh dengan setting sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100539930-812d0480-326c-11eb-80e2-8393f5a4a4c9.png)

Pada file ```/etc/sysctl.conf``` dibuat agar dapat melakukan packet forwarding IPv4 dengan melakukan *uncomment* pada ```net.ipv4.forward=1``` sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540404-cd2d7880-326f-11eb-96bd-fa4126ab3242.png)

Untuk konfigurasi file ```etc/network/interfaces``` setiap UML selain client sebagai berikut.

- Pada UML **Surabaya** sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540505-46c56680-3270-11eb-8fba-dc9540300ed0.png)

- Pada UML **Malang** sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540558-9a37b480-3270-11eb-8716-18e11cdc4e51.png)

- Pada UML **Mojokerto** sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540580-b50a2900-3270-11eb-8ec3-c145468cc4e1.png)

- Pada UML **Tuban** sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540565-a6bc0d00-3270-11eb-813d-9bbcc1902116.png)

## Soal 2
Menjadikan **Surabaya** sebagai DHCP Relay antara DHCP Server dan DHCP client.

Pada awalnya **Tuban** dijadikan sebagai DHCP Server dengan melakukan instalasi menggunakan command ```apt-get install isc-dhcp-server```. Kemudian untuk **Surabaya** dilakukan instalasi DHCP Relay dengan ```apt-get install isc-dhcp-relay```.

Kemudian baik untuk DHCP Server dan DHCP Relay dilakukan konfigurasi interface sesuai dengan topologinya.

- Untuk konfigurasi file ```/etc/default/isc-dhcp-server``` pada UML **Tuban**. Karena **Tuban** hanya tersambung pada ```eth0``` maka interfacenya sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540816-5d6cbd00-3272-11eb-8ada-6c6234d62251.png)

- Sedangkan pada UML **Surabaya** karena tersambung dengan 3 interface dan karena merupakan DHCP Relay diperlukan konfigurasi server yang akan digunakan sehingga konfigurasi pada file  ```/etc/default/isc-dhcp-relay``` sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540897-dbc95f00-3272-11eb-9a7c-3026e926efed.png)

Agar **Tuban** dapat mengirimkan DHCP ke **Surabaya** maka disambungkan dengan subnet pada **Surabaya**. Konfigurasinya diletakkan pada file ```/etc/dhcp/dhcpd.conf``` pada UML **Tuban** sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541062-f2bc8100-3273-11eb-9924-0181f8dccea4.png)

Karena pada soal seluruh client tidak diperbolehkan menggunakan IP static maka pada konfigurasi interface pada ```/etc/network/interfaces``` client dibuat sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541155-7b3b2180-3274-11eb-9bf2-019af90fcf72.png)

![image](https://user-images.githubusercontent.com/57692117/100541164-842bf300-3274-11eb-8215-47a682197b90.png)

![image](https://user-images.githubusercontent.com/57692117/100541168-8b530100-3274-11eb-95c6-5606846b7871.png)

![image](https://user-images.githubusercontent.com/57692117/100541197-b2a9ce00-3274-11eb-8f43-93af86b054c1.png)

## Soal 3
Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan
192.168.0.110 sampai 192.168.0.200.

Pada file ```etc/dhcp/dhcpd.conf``` pada UML **Tuban** dilakukan konfigurasi sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541273-45e30380-3275-11eb-9608-8bc0a8c85f59.png)

## Soal 4
Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.

Pada file ```etc/dhcp/dhcpd.conf``` pada UML **Tuban** dilakukan konfigurasi sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541298-90fd1680-3275-11eb-847d-3e11ac2a8bb7.png)

## Soal 5
Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP.

Karena konfigurasi ini bisa digunakan untuk seluruh subnet maka dapat diset pada konfigurasi global di file ```/etc/dhcp/dhcpd.conf``` sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541351-049f2380-3276-11eb-88f2-95bc26e0ae16.png)

## Soal 6
Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client
pada subnet 3 mendapatkan peminjaman IP selama 10 menit.

Karena pada DHCP waktu yang digunakan adalah dalam satuan detik maka konfigurasi pada ```etc/dhpc/dhcpd.conf``` di UML **Tuban** untuk subnet 1 diset 300 dan subnet 3 diset 600 atau sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100541429-8abb6a00-3276-11eb-8d8f-14b7d935f16d.png)

![image](https://user-images.githubusercontent.com/57692117/100541454-a58dde80-3276-11eb-8fb5-cd53754dfded.png)

## Soal 7
Membuat proxy server pada UML **Mojokerto** sebagai penghubung jaringan lokal ke internet dengan ketentuan menggukan authorization dengan user adalah ```userta_d12``` dan passwordnya adalah ```inipassw0rdta_d12```.

Pertama pada UML **Mojokerto** dilakukan instalasi squid sebagai proxy servernya dengan menggunakan command ```apt-get install squid```. Untuk membuat password yang nantinya digunakan untuk authorization maka dibutuhkan instalasi apache2-utils dengan menggunakan command ```apt-get install apache2-utils```.

Untuk membuat password digunakan command ```htpasswd -c /etc/squid/passwd userta_d12``` kemudian mengisi password dengan ```inipassw0rdta_d12``` sehingga nantinya akan terbentuk file untuk menyimpan auth user dan password yang telah dienkripsi pada ```/etc/squid/passwd```

Agar aman, maka sebelum melakukan konfigurasi pada squid dilakukan backup terlebih dahulu dengan melakukan copy file ```/etc/squid/squid.conf```.

Untuk melakukan apply file auth yang telah dibuat maka dilakukan konfigurasi sebagai berikut.

Perlu diingat, pada konfigurasi ```http_access``` akan mengambil argument dalam line yang sama sebagai logika ```and``` dan argumen yang berbeda line dengan logika ```or``` . Karena nantinya pada soal 8 dan 9 diminta untuk menggabungkan dengan waktu akses yang diperbolehkan maka untuk http_accessnya digabung agar konfigurasinya tidak bertabrakan sebagai berikut.

## Soal 8
Pada awalnya proxy dibuat agar tidak dapat diakses diluar jam yang ditentukan. Pada soal ini meminta untuk membatasi akses proxy agar dapat digunakan pada hari **Selasa-Rabu pukul 13.00-18.00**.

Konfigurasi untuk waktu yang ditentukan terdapat pada file ```/etc/squid/acl.conf```. Untuk variabel waktu yang digunakan adalah ```KERJA_TA``` sebagai berikut.

Perlu diingat, pada konfigurasi ```http_access``` akan mengambil argument dalam line yang sama sebagai logika ```and``` dan argumen yang berbeda line dengan logika ```or``` . Karena pada soal 7 diminta untuk menggabungkan dengan login user maka untuk http_accessnya digabung agar konfigurasinya tidak bertabrakan sebagai berikut.

## Soal 9
Pada awalnya proxy dibuat agar tidak dapat diakses diluar jam yang ditentukan. Pada soal ini meminta untuk membatasi akses proxy agar dapat digunakan pada hari **Selasa-Kamis pukul 21.00-09.00**.

Konfigurasi untuk waktu yang ditentukan terdapat pada file ```/etc/squid/acl.conf```. Untuk variabel waktu yang digunakan adalah ```BIMBINGAN_MALAM``` dan ```BIMBINGAN_PAGI``` karena penentuan waktu hanya bisa dalam satu hari sehingga konfigurasinya sebagai berikut.

Perlu diingat, pada konfigurasi ```http_access``` akan mengambil argument dalam line yang sama sebagai logika ```and``` dan argumen yang berbeda line dengan logika ```or``` . Karena pada soal 7 diminta untuk menggabungkan dengan login user maka untuk http_accessnya digabung agar konfigurasinya tidak bertabrakan sebagai berikut.

## Soal 10
Ketika user mencoba untuk mengakses **google.com** maka akan dialihkan menuju **monta.if.its.ac.id**

## Soal 11
Mengganti error page default pada squid dengan error page yang telah disediakan.

## Soal 12
Melakukan konfigurasi agar proxy server dapat diakses dengan menggunakan domain ```janganlupa-ta.d12.pw```









