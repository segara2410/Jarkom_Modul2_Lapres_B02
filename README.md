1.  **Pertama membuat domain dengan mengisikan konfigurasi untuk semerub02.pw di MALANG seperti berikut**

> ![](media/image11.png)

-   Buat folder jarkom di dalam /etc/bind

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom
    > yang baru saja dibuat dan ubah namanya menjadi semerub02.pw

-   Kemudian buka file semerub02.pw dan edit seperti gambar berikut

> ![](media/image54.png)
>
> Setelah di restart bind9 nya dan dicoba hasilnya,
>
> ![](media/image10.png)

2.  **Lalu untuk membuat alias sebagai berikut**

> ![](media/image34.png)
>
> Lalu hasilnya setelah di coba ping,
>
> ![](media/image53.png)

3.  **Lalu untu membuat subdomain**

> ![](media/image18.png)
>
> Hasilnya,
>
> ![](media/image25.png)

4.  **Lalu untuk membuat reverse domain**

-   Edit file /etc/bind/named.conf.local pada *MALANG*

-   Lalu tambahkan konfigurasi berikut ke dalam file named.conf.local

> ![](media/image1.png)

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom
    > yang baru saja dibuat dan ubah namanya menjadi
    > 83.151.10.in-addr.arpa

-   Edit file 83.151.10.in-addr.arpa menjadi seperti gambar di bawah ini

> ![](media/image30.png)
>
> Setelah itu restart Malang dan jika dicoba pada Gresik hasilnya,
>
> ![](media/image56.png)

5.  **Membuat DNS Server Slave**

Edit file /etc/bind/named.conf.local dan sesuaikan dengan syntax berikut

> ![](media/image57.png)
>
> Kemudian buka file /etc/bind/named.conf.local pada MOJOKERTO dan
> tambahkan syntax berikut:
>
> ![](media/image33.png)

Lalu untuk testing, pertama kita matikan MALANG

> ![](media/image52.png)
>
> Lalu setelah MALANG di matikan kita test dan hasilnya seperti berikut,
>
> ![](media/image5.png)

6.  **Membuat subdomain di delagasikan ke MOJOKERTO dan mengarah ke PROBOLINGGO**

> Ubah pada MALANG dengan menambahkan subdomain baru,
>
> ![](media/image2.png)

-   Kemudian edit file /etc/bind/named.conf.options pada *MALANG*.

-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > pada /etc/bind/named.conf.options

> ![](media/image46.png)

-   Pada *MOJOKERTO* edit file /etc/bind/named.conf.options

-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > pada /etc/bind/named.conf.options

> ![](media/image40.png)

-   Kemudian buat direktori dengan nama delegasi lalu copy db.local ke
    > direktori pucang dan edit namanya menjadi gunung.semerub02.pw

-   Kemudian edit file gunung.semerub02.pw menjadi seperti dibawah ini

> ![](media/image41.png)
>
> Lalu saat dicoba pada GRESIK hasilnya,
>
> ![](media/image38.png)

7.  **Membuat subdomain naik.gunung.semerub02.pw**

> Pada MOJOKERTO ditambahkan sebagai berikut,
>
> ![](media/image49.png)
>
> Lalu jika kita coba di GRESIK hasilnya,
>
> ![](media/image14.png)

8.  **Mengatur webserver untuk Domain semerub02.pw**

> Dengan menambahkan ServerName dan DocumentRoot
>
> ![](media/image37.png)

Lalu untuk melihat hasilnya dapat diakses dengan browser semerub02.pw

> ![](media/image19.png)

9.  **Menghilangkan index.php**

> Aktifkan a2enmod rewrite
>
> ![](media/image16.png)

Lalu untuk semerub02.pw, AllowOverride diganti All

> ![](media/image51.png)
>
> Lalu edit file .htaccess dan isikan seperti berikut
>
> ![](media/image24.png)

Lalu untuk melihat hasilnya tinggal di coba untuk semerub02.pw/home

> ![](media/image55.png)

10. **Mensetting penanjakan.semerub02.pw**

> Ekstrak file ke folder penanjakan.semerub02.pw
>
> ![](media/image31.png)

Lalu tambahkan ServerName dan DocumentRoot dengan
penanjakan.semerub02.pw

> ![](media/image9.png)
>
> Lalu aktifkan a2ensite penanjakan
>
> ![](media/image47.png)
>
> Hasilnya jika dibuka penanjakan.semerub02.pw
>
> ![](media/image22.png)

11. **Listing pada /public tanpa public/\***

> Tambahkan Option +Indexes untuk directory
> penanjakan.semerub02.pw/public
>
> Dan tambahkan Option -Indexes untuk directory
> penanjakan.semerub02.pw/public/\*
>
> ![](media/image17.png)

Hasilnya saat mengakses penanjakan.semerub02.pw/public/

> ![](media/image15.png)

Hasilnya saat mengakses penanjakan.semerub02.pw/public/css/

> ![](media/image28.png)

12. **Merubah error page dengan 404.html**

> Dengan menambahkan ErrorDocument 404 /errors/404.html
>
> ![](media/image29.png)
>
> Lalu apache di restart
>
> ![](media/image6.png)
>
> Hasilnya saat mengakses link yang tidak ada
>
> ![](media/image8.png)

13. **Mengubah inisial untuk folder javascript**

> Dengan menambahkan Alias dengan memberinya alias "/js"
>
> ![](media/image12.png)
>
> Lalu restart apache
>
> ![](media/image48.png)
>
> Hasilnya saat mengakses penanjakan.semerub02.pw/js\
> *\*tidak lagi not found, karena folder javascript memang tidak bisa
> diakses*
>
> ![](media/image3.png)

14. **Membuat naik.gunung.semerub02.pw di port 8888**

> Setting virtual host di port 8888, tambahkan server name dan document
> root untuk naik.gunung.semerub02.pw
>
> ![](media/image13.png)
>
> Lalu pada ports.conf Listen untuk port 8888
>
> ![](media/image20.png)

Lalu restart apache

> ![](media/image21.png)
>
> Lalu hasilnya jika mengakses naik.gunung.semerub02.pw:8888
>
> ![](media/image39.png)

15. **Memberikan Auth pada naik.gunung.semerub02.pw**

> Membuat user "semeru" dan password "kuynaikgunung" dengan perintah
> dibawah
>
> ![](media/image50.png)
>
> Lalu tambahkan Auth untuk directory naik.gunung.semerub02.pw
>
> ![](media/image42.png)
>
> Lalu restart apache
>
> ![](media/image32.png)
>
> Hasilnya saat mengakses naik.gunung.semerub02.pw:8888
>
> ![](media/image58.png)
>
> Setelah memsukkan username dan password yang sesuai
>
> ![](media/image43.png)

16. **Mengarahkan 10.151.83.28**

> Test ip 10.151.83.28
>
> ![](media/image4.png)
>
> Rubah .htaccess default pada PROBOLINGGO untuk meredirect ip
> PROBOLINGGO ke semerub02.pw
>
> ![](media/image45.png)
>
> Ganti allowoverride none jadi all untuk directory /var/www/
>
> ![](media/image35.png)
>
> Lalu restart apache
>
> ![](media/image36.png)
>
> Hasilnya saat mengakses 10.151.83.28
>
> ![](media/image23.png)

17. **Mengubah semua gambar yang mengadung "semeru" ke semeru.jpg**

> Awalnya
>
> ![](media/image26.png)
>
> Rubah file .htaccess sesuai berikut
>
> ![](media/image7.png)
>
> Tambahkan AllowOverride All untuk directory penanjakan.semerub02.pw

> ![](media/image27.png)

> Hasilnya semua akses file gambar yang mengandung "semeru" akan
> diarahkan ke semeru.jpg
>
> ![](media/image44.png)
