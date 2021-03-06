# Lapres Modul 1 Jarkom T17 2020

## Oleh:
- Milenia Ulwan Zafira (0511174000020)
- Bayu Trianayasa (05311840000038)

## Soal
### A.	Display Filter
1.	Sebutkan webserver yang digunakan pada "testing.mekanis.me"!
2.	Simpan gambar "Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg"!
3.	Cari username dan password ketika login di "ppid.dpr.go.id"!
4.	Temukan paket dari web-web yang menggunakan basic authentication method!
5.	Ikuti perintah di aku.pengen.pw! Username dan password bisa didapatkan dari file .pcapng!
6.	Seseorang menyimpan file zip melalui FTP dengan nama "Answer.zip". Simpan dan Buka file "Open This.pdf" di Answer.zip. Untuk mendapatkan password zipnya, temukan dalam file zipkey.txt (passwordnya adalah isi dari file txt tersebut).
7.	Ada 500 file zip yang disimpan ke FTP Server dengan nama 1.zip, 2.zip, ..., 500.zip. Salah satunya berisi pdf yang berisi puisi. Simpan dan Buka file pdf tersebut.
Your Super Mega Ultra Rare Hint = nama pdf-nya "Yes.pdf"
8.	Cari objek apa saja yang didownload (RETR) dari koneksi FTP dengan Microsoft FTP Service!
9.	Cari username dan password ketika login FTP pada localhost!
10.	Cari file .pdf di wireshark lalu download dan buka file tersebut!
clue: "25 50 44 46" 

### B. Capture Filter
11.	Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!
12.	Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!
13.	Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!
14.	Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!
15.	Filter sehingga wireshark hanya mengambil paket yang tujuannya ke monta.if.its.ac.id!

## Jawaban A
<b>1.</b> menggunakan filter:
```
http.host == testing.mekanis.me
```
![1](img/no%201.png)

lalu Follow TCP Stream <br/>
![1_2](img/no%201_2.png/)

<b>2.</b> menggunakan filter:
```
http.request.uri contains tim
```
![2](img/no%202.png/)
Lalu File -> Export Object -> HTTP, jika terdapat banyak file bisa di cari dibagian search dengan keyword nama file lalu save
![2_2](img/no%202_2.png/)
![2_3](img/no%202_3.png/)
![foto](img/Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg/)

<b>3.</b> Gunakan filter:
```
http.host=="ppid.dpr.go.id" && http.request.uri == POST
```
![3](img/no%203.png/)

<b>4.</b> Gunakan filter :
```
http.authbasic
```
![4_1](img/no%204_1.png/)
Lalu didapatkan 2 web dengan auth basic
![4_2](img/no%204_2.png/)
![4_3](img/no%204_3.png/)

<b>5.</b> Gunakan filter untuk mendapat Credential:
```
http.host=="aku.pengen.pw"
```
![5](img/no%205.png/)
Masukan Usname dan Pass untuk masuk ke web tsb. isi soal tersembunyi ttg pengkabelan ini
![5_2](img/no%205_2.png/)

<b>6.</b> Gunakan filter :
```
ftp-data
```
setelah didapat info STORING Answer.zip
![6](img/no%206.png/)
Follow TCP Stream dan Show RAW dan save as "Answer.zip"
![6_1](img/no%206_1.png/)
terdapat file open.pdf, namun perlu password. cari password dengan filter :
```
ftp-data.command contains .txt
```
![6_2](img/no%206_2.png/)
Lalu Follow TCP Stream untuk dapat password dari open.pdf
![6_3](img/no%206_3.png/)
Lalu didapat isi pdf sebagai berikut
![6_4](img/no%206_4.png/)

<b>7.</b> Gunakan Filter :
```
ftp.data contains "Yas.pdf"
```
![7](img/no%207.png/)
Lalu TCP Stream dan save as RAW
![7_1](img/no%207_1.png/)
dinamai dengan "Yes.pdf"
![7_2](img/no%207_2.png/)
Lalu buka tanpa password
![7_3](img/no%207_3.png/)

<b>8.</b> Gunakan filter :
```
ftp contains "Microsoft"
```
akan didapat IP Address dari Microsoft
![8](img/no%208.png/)
Untuk mencari objek yang di didownload dengan filter :
```
ftp.request.command contains "RETR" && ip.dst==198.246.117.106
```
![8_1](img/no%208_1.png/)

<b>9.</b> Gunakan filter :
```
ftp
```
![9_2](img/no%209_2.png/)
atau
```
ftp.request.command == USER || ftp.request.command == PASS
```
![9_1](img/no%209_1.png/)
lalu dibisa Follow TCP Stream untuk lebih pasti 
![9](img/no%209.png/)

<b>10.</b> Gunakan Filter :
```
http contains ".pdf"
```
![10_2](img/no%2010_2.png/)
lalu TCP Stream, find HEX dengan "25 55 40 46"
![10_1](img/no%2010_1.png/)
Lalu TCP Stream lagi dan View as RAW
![10](img/no%2010.png/)

## Jawaban B
<b>11.</b> Agar bisa ada isinya wireshark, Start Filezilla Server XAMPP
![11](img/no%2011.png/)
Buat user bila belum ada
![11_1](img/no%2011_1.png/)
Connect Fillzilla Client dengan mengisi host 127.0.0.1, user dan pass yang sudah dibuat tadi dan isi port 21 lalu Quickconnect
![11_2](img/no%2011_2.png/)
Setelah itu maka Wireshark akan mendeteksi kegiatan yang ada di port 21, dengan Capture filter di Loopback :
```
port 21
```
![11_3](img/no%2011_3.png/)

<b>12.</b> Gunakan Capture Filter :
```
tcp src port 80
```
![12](img/no%2012.png/)

<b>13.</b> Gunakan Capture Filter :
```
tcp dst port 443
```
![13](img/no%2013.png/)

<b>14.</b> Gunakan ip config di cmd untuk cari ip pc, lalu gunakan filter :
```
ip scr 192.168.100.219
```
![14](img/no%2014.png/)

<b>15.</b> Gunakann Capture Filter :
```
dst host monta.if.its.ac.id
```
![15](img/no%2015.png/)
