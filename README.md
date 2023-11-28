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
   ```<?php
include("koneksi.php");
// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);
?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Barang</title>

    <style>
        body {
            font-family: Tahoma, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
            display: grid;
            justify-content: center;
            border-radius: 20px;
        }

        table {
            border-collapse: collapse;
            margin-top: 20px;
        }

        th,
        td {
            border: 1px black solid;
            padding: 7px;
        }

        img {
            width: 50px;
        }

        a {
            text-decoration: none;
            background-color: rgb(100, 149, 237);
            margin: 2px;
            color: #fff;
            border-radius: 5px;
            padding: 5px;
            font-size: 12px;
        }

        a:hover {
            background-color: rgb(135, 206, 250);
            transform: scale(0.98);
        }

        
    </style>
</head>

<body>
    <div class="container">
        <h1>Data Barang</h1>
        <div class="main">
            <a class="tambah" href="tambah.php">Tambah Barang</a>
            <table>
                <tr>
                    <th>Nama Barang</th>
                    <th>Katagori</th>
                    <th>Harga Jual</th>
                    <th>Harga Beli</th>
                    <th>Stok</th>
                    <th>Aksi</th>
                </tr>
                <?php if ($result): ?>
                    <?php while ($row = mysqli_fetch_array($result)): ?>
                        <tr>
                            <td>
                                <?= $row['nama']; ?>
                            </td>
                            <td>
                                <?= $row['kategori']; ?>
                            </td>
                            <td>
                                <?= $row['harga_beli']; ?>
                            </td>
                            <td>
                                <?= $row['harga_jual']; ?>
                            </td>
                            <td>
                                <?= $row['stok']; ?>
                            </td>
                            <td class="aksi">
                                <a class="ubah" href="ubah.php?id=<?= $row['id_barang']; ?>">Ubah</a>
                                <a class="hapus" href="hapus.php?id=<?= $row['id_barang']; ?>">Hapus</a>
                            </td>
                        </tr>
                    <?php endwhile; else: ?>
                    <tr>
                        <td colspan="7">Belum ada data</td>
                    </tr>
                <?php endif; ?>
            </table>
        </div>
    </div>
</body>

</html>
```

  

![2](https://github.com/tiaraputriiiiii/Lab8web/assets/115775237/42cdd7c9-3951-4915-9bf1-b297a1d88a4e)


9. **Menambah Data (Create)**
    Buat file baru dengan nama **tambah.php**
   ```<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        
        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;
        }
    }

    $sql = "INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar) ";
    $sql .= "VALUES ('{$nama}', '{$kategori}', '{$harga_jual}', '{$harga_beli}', '{$stok}', '{$gambar}')";

    $result = mysqli_query($conn, $sql);

    if (!$result) {
        echo "Error: " . mysqli_error($conn);
    } else {
        header('location: index.php');
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Tambah Barang</title>
    <style>
        body {
            font-family: tahoma, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        .container {
            width: 800px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h1 {
            text-align: center;
        }

        .main {
            margin-top: 20px;
        }

        form {
            width: 100%;
            max-width: 400px;
            margin: 0 auto;
        }

        .input {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
        }

        input, select {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
        }

        .submit {
            text-align: center;
            margin-top: 15px;
        }

        input[type="submit"] {
            background-color: rgb(100, 149, 237);
            color: #fff;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
        }

        input[type="submit"]:hover{
            background-color: rgb(173, 216, 230);
            transform: scale(0.98);
        }
    </style>
</head>
    <div class="container">
        <h1>Tambah Barang</h1>
        <div class="main">
            <form method="post" action="tambah.php" enctype="multipart/form-data">
                <div class="input">
                    <label>Nama Barang</label>
                    <input type="text" name="nama" required />
                </div>
                <div class="input">
                    <label>Kategori</label>
                    <select name="kategori" required>
                        <option value="Komputer">Komputer</option>
                        <option value="Elektronik">Elektronik</option>
                        <option value="Hand Phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual" required />
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli" required />
                </div>
                <div class="input">
                    <label>Stok</label>
                    <input type="text" name="stok" required />
                </div>
                <div class="input">
                    <label>File Gambar</label>
                    <input type="file" name="file_gambar" required />
                </div>
                <div class="submit">
                    <input type="submit" name="submit" value="Simpan" />
                </div>
            </form>
        </div>
    </div>
</body>
</html>
```

![tambah](https://github.com/aasnovita114/Lab8web_/assets/116045324/c54eb4d9-7cb2-4850-8f35-3c5772b93b39)


10. **Mengubah Data (Update)**
    Buat file baru dengan nama **ubah.php**
    
    ```<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    if (!empty($gambar)) {
        $sql .= ", gambar = '{$gambar}' ";
    }
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);

    if (!$result) {
        die('Error: ' . mysqli_error($conn));
    } else {
        header('location: index.php');
    }
}

$id = $_GET['id'];
$sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
if (!$result) {
    die('Error: Data tidak tersedia');
}
$data = mysqli_fetch_array($result);

function is_select($var, $val) {
    if ($var == $val) return 'selected="selected"';
    return false;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Ubah Barang</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 500px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 5px;
        }

        h1 {
            text-align: center;
            color: black;
        }

        .main {
            margin-top: 20px;
        }

        .input {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            color: #333;
        }

        input, select {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        .submit {
            text-align: center;
        }

        input[type="submit"] {
            background-color: rgb(100, 149, 237);
            color: #fff;
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        input[type="file"] {
            padding: 10px 0;
        }
        input[type="submit"]:hover{
            background-color: rgb(173, 216, 230);
            transform: scale(0.98);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Ubah Barang</h1>
        <div class="main">
            <form method="post" action="ubah.php" enctype="multipart/form-data">
                <div class="input">
                    <label>Nama Barang</label>
                    <input type="text" name="nama" value="<?php echo $data['nama'];?>" />
                </div>
                <div class="input">
                    <label>Kategori</label>
                    <select name="kategori">
                        <option <?php echo is_select('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                        <option <?php echo is_select('Elektronik', $data['kategori']);?> value="Elektronik">Elektronik</option>
                        <option <?php echo is_select('Hand Phone', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual" value="<?php echo $data['harga_jual'];?>" />
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli" value="<?php echo $data['harga_beli'];?>" />
                </div>
                <div class="input">
                    <label>Stok</label>
                    <input type="text" name="stok" value="<?php echo $data['stok'];?>" />
                </div>
                <div class="input">
                    <label>File Gambar</label>
                    <input type="file" name="file_gambar" />
                </div>
                <div class="submit">
                    <input type="hidden" name="id" value="<?php echo $data['id_barang'];?>" />
                    <input type="submit" name="submit" value="Simpan" />
                </div>
            </form>
        </div>
    </div>
</body>
</html>
```


    
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

