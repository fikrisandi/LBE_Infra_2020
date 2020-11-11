# LBE_Infra_2020

## Deploy CodeIgniter

Sub Judul :

- <a href="#Introduction"> Introduction </a>
- <a href="#Requirements"> Requirements </a>
- <a href="#Langkah-langkah"> Langkah-langkah </a>
- <a href="#Kesimpulan"> Kesimpulan </a>

## Introduction
<justify>
<p> Deploy CodeIgniter menurut saya yaitu menampilkan framework CodeIgniter di web browser. Disini saya menggunakan Linux dan beberapa ekstensi yang diperlukan untuk membantu mendeploy CI. </p>
</justify>

## Requirements
<justify>
<p> Persyaratan yang dibutuhkan yaitu: <br>
1. Linux (karena menggunakan linux) <br>
2. Nginx <br>
3. Myqsl <br>
4. Php <br>
5. Composer <br>
6. Download CI di web CI resmi (saya pakek CI 3) </p>
</justify>

## Langkah-langkah
<justify>
<p> 1. Instal <b>nginx</b> terlebih dahulu, karena nginx adalah salah satu web server <i> open source </i> sebagai server HTTP dan Proxy,Instal dengan cara command dibawah ini.</p>
  
    sudo apt update
    sudo apt install nginx
   
<p> Kemudian cek status firewal dengan command dibawah ini</p>

    sudo ufw status
    
<p> Jika firewal menyala, pastikan sudah mengaktifkan Nginx, jika belum maka cara mengaktifkannya dengan mengetik command dibawah ini</p>

    sudo ufw allow 'Nginx HTTP'
    
<p> Kemudian Perubahan dapat dilihat dengan menjalankan command dibawah ini:</p>

    sudo ufw status

<p> Setelah terlihat status active pastikan nginx sudah terisntal dengan mengecek alamat IP pada browser dengan cara:</p>
    
    http://server_domain_atau_IP

<p> Cara mendapatkan ip yaitu dengan cara command "ifconfig" pada terminal. </p> <br>


<p> 2. Karena telah memiliki web server, maka perlu untuk menginstal <b> MySQL </b> (sistem manajemen database) untuk menyimpan dan mengelola data. Instal MySQL dengan mengetik :
</p>

    sudo apt install mysql-server

<p> Untuk mengamankan instalasi, <b> MySQL </b> dilengkapi dengan <i>script</i> yang akan menanyakan apakah kita ingin mengubah beberapa default yang tidak aman. Mulai <i>script</i> dengan mengetik:</p>

    sudo mysql_secure_installation

<br>

<p> 3. Setelah instalasi <b> Nginx </b> dan <b> MySQL </b> berhasil, langkah berikutnya adalah menginstal <b> PHP </b> agar dapat menghasilkan konten dinamis.</p>

<p>Masukkan perintah berikut pada terminal untuk memulai instalasi :</p>

    sudo apt install php-fpm php-mysql

<br>

<p> 4. Kemudian Instal <b> Composer </b> untuk mempermudah mendeploy CI (list yang dipakek ada di composer.json). Instalnya dengan cara command di terminal seperti di bawah: </p>
  
    sudo apt install composer
    
<p> 5. Kemudian ke config nginx yang ada di <code> sudo nano /etc/nginx/sites-available/ </code> dan membuat file konfigrasi seperti dibawah ini: </p> 

       server {
            listen 80;
            root /var/www/CodeIgniter;
            index index.php index.html index.htm index.nginx-debian.html;
            server_name localhost;

            location / {
                    try_files $uri $uri/ =404;
            }

            location ~ \.php$ {
                    include snippets/fastcgi-php.conf;
                    fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
            }

            location ~ /\.ht {
                    deny all;
            }
    }

<p> Di dalam file konfigurasi terdapat " root /var/www/CodeIgniter; ", dari sini kita harus memindahkan file CI kita yang sudah di download kedalam folder var/www/.

<p> 6. Memindahkan folder CI ke subfolder var/www agar bisa dijalankan, caranya menggunakan command dibawah ini:

      sudo nautilus
      
<p> setelah sudah melakukan <code> sudo nautilus </code> layar akan menuju ke file home, kemudian pindahkan file CI yang sudah di download ke subfolder yang sudah di tulis di file konfigurasi. </p>

<p> 7. Setelah dipindahkan coba cek di Web browser dengan mengetik localhost saja atau dengan alamat ip masing-masing, Jika berhasil akan mendeploy CI.
</justify>  
  
## Kesimpulan
<justify>
  <p> Mendeploy CI tidak harus dengan menggunakan cara yang diatas bisa juga dengan cara yang lain, hanya saja karena saya tidak bisa menggunakan cara manual saya menggunakan cara instan dengan menggunakan komposer, disisi lain mendeploy CI juga bisa menggunakan web server <b>Apache</b> yang fungsinya sama dengan <b>Nginx</b> untuk perbedaannya saya kurang tahu. </p>
  </justify>
  
