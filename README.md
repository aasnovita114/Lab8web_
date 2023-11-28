# Lab8web_
<table>
  <tr>
    <th colspan="2">DATA MAHASISWA</th>
  </tr>
  <tr>
    <td>Nama</td>
    <td>Aas Novitasari</td>
  </tr>
  <tr>
    <td>NIM</td>
    <td>312210167</td>
  </tr>
  <tr>
    <td>Kelas</td>
    <td>TI.22.A1</td>
  </tr>
</table>

# Instruksi Praktikum
1. Persiapkan text editor misalnya VSCode.
2. Buat folder baru dengan nama lab8_php_database pada docroot webserver
(htdocs)
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.

# Langkah-langkah Praktikum
1. **Persiapan Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah  database server menggunakan MySQL.**
2. **Pastikan MySQL Server sudah dapat dijalankan melalui XAMPP.**

3. **Menjalankan MySQL Server Untuk menjalankan MySQL Server dari menu XAMPP Control.**

4. **Membuat Database: Studi Kasus Data Barang**
    ```mysql
    CREATE DATABASE latihan1;
    ```

    ```mysql
    CREATE TABLE data_barang (
        id_barang int(10) auto_increment Primary Key,
        kategori varchar(30),
        nama varchar(30),
        gambar varchar(100),
        harga_beli decimal(10,0),
        harga_jual decimal(10,0),
        stok int(4)
    );
    ```
    
5. **Menambah Data**
    ```mysql
    INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
    VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
    ('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
    ('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);

    ```
![Screenshot 2023-11-28 205347](https://github.com/aasnovita114/Lab8web_/assets/116045324/d4dabc53-0070-414d-873a-f712ae60edc3)


6. **Membuat Program CRUD 7Buat folder lab8_php_database pada root directory web server (d:\xampp\htdocs)**

7. **Membuat file koneksi database**
    Buat file baru dengan nama **koneksi.php**
    ```php
    <?php
    $host = "localhost";
    $user = "root";
    $pass = "";
    $db = "latihan1";
    $conn = mysqli_connect($host, $user, $pass, $db);
    if ($conn == false)
    {
        echo "Koneksi ke server gagal.";
        die();
    } #else echo "Koneksi berhasil";
    ?>
    ```
    Buka melalui browser untuk menguji koneksi database untuk menyampilkan pesan 
    koneksi berhasil, uncomment pada perintah echo “koneksi berhasil”; 
![koneksiphp](https://github.com/aasnovita114/Lab8web_/assets/116045324/04f41f89-566a-468b-8ede-883a06a3cfe5)


8. **Membuat file index untuk menampilkan data (Read)**
    Buat file baru dengan nama **index.php**

  

![2](https://github.com/tiaraputriiiiii/Lab8web/assets/115775237/42cdd7c9-3951-4915-9bf1-b297a1d88a4e)


9. **Menambah Data (Create)**
    Buat file baru dengan nama **tambah.php**   

![tambah](https://github.com/aasnovita114/Lab8web_/assets/116045324/c54eb4d9-7cb2-4850-8f35-3c5772b93b39)


10. **Mengubah Data (Update)**
    Buat file baru dengan nama **ubah.php**


    
![ubah](https://github.com/aasnovita114/Lab8web_/assets/116045324/d79c2cbb-f849-44f2-939d-01743eb85a25)


12. **Menghapus Data (Delete)**
    Buat file baru dengan nama **hapus.php**

    ```php
    <?php
    include_once 'koneksi.php';
    $id = $_GET['id'];
    $sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
    >

    ```

    



## **Hasil Run**





## *Selesai, Terima kasih*

