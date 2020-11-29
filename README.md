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
