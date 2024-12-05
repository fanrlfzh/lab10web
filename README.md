# lab10web

#Mobil.php

<?php
/**
* Program sederhana pendefinisian class dan pemanggilan class.
**/
class Mobil
{
private $warna;
private $merk;
private $harga;
public function __construct()
{
$this->warna = "Biru";
$this->merk = "BMW";
$this->harga = "10000000";
}
public function gantiWarna ($warnaBaru)
{
$this->warna = $warnaBaru;
}
public function tampilWarna ()
{
echo "Warna mobilnya : " . $this->warna;
}
}
// membuat objek mobil
$a = new Mobil();
$b = new Mobil();
// memanggil objek
echo "<b>Mobil pertama</b><br>";
$a->tampilWarna();
echo "<br>Mobil pertama ganti warna<br>";
$a->gantiWarna("Merah");

$a->tampilWarna();
// memanggil objek
echo "<br><b>Mobil kedua</b><br>";
$b->gantiWarna("Hijau");
$b->tampilWarna();
?>
![WhatsApp Image 2024-12-04 at 12 32 07](https://github.com/user-attachments/assets/39e82693-656c-41d6-9fe8-d4f2ce6e2295)

#Form.php

<?php
/**
* Nama Class: Form
* Deskripsi: CLass untuk membuat form inputan text sederhan
**/
class Form
{
private $fields = array();
private $action;
private $submit = "Submit Form";
private $jumField = 0;
public function __construct($action, $submit)
{
$this->action = $action;
$this->submit = $submit;
}
public function displayForm()
{
echo "<form action='".$this->action."' method='POST'>";
echo '<table width="100%" border="0">';
for ($j=0; $j<count($this->fields); $j++) {
echo "<tr><td
align='right'>".$this->fields[$j]['label']."</td>";
echo "<td><input type='text'
name='".$this->fields[$j]['name']."'></td></tr>";
}
echo "<tr><td colspan='2'>";
echo "<input type='submit' value='".$this->submit."'></td></tr>";
echo "</table>";
}
public function addField($name, $label)
{
$this->fields [$this->jumField]['name'] = $name;
$this->fields [$this->jumField]['label'] = $label;
$this->jumField ++;

}
}
?>
![WhatsApp Image 2024-12-04 at 12 35 13](https://github.com/user-attachments/assets/3ad3858d-8ba7-45c2-be40-5a2d219a7e99)
tidak ada hasil apapun

#Form_input.php

<?php
/**
* Program memanfaatkan Program 10.2 untuk membuat form inputan sederhana.
**/
include "form.php";
echo "<html><head><title>Mahasiswa</title></head><body>";
$form = new Form("","Input Form");
$form->addField("txtnim", "Nim");
$form->addField("txtnama", "Nama");
$form->addField("txtalamat", "Alamat");
echo "<h3>Silahkan isi form berikut ini :</h3>";
$form->displayForm();
echo "</body></html>";
?>
![WhatsApp Image 2024-12-04 at 12 37 42](https://github.com/user-attachments/assets/e633ae4c-d348-438d-99f9-3f235aeeb26a)

#Database.php

<?php
class Database {
protected $host;
protected $user;
protected $password;
protected $db_name;
protected $conn;
public function __construct() {
$this->getConfig();
$this->conn = new mysqli($this->host, $this->user, $this->password,
$this->db_name);
if ($this->conn->connect_error) {
die("Connection failed: " . $this->conn->connect_error);
}
}
private function getConfig() {
include_once("config.php");
$this->host = $config['host'];
$this->user = $config['username'];
$this->password = $config['password'];

$this->db_name = $config['db_name'];
}
public function query($sql) {
return $this->conn->query($sql);
}
public function get($table, $where=null) {
if ($where) {
$where = " WHERE ".$where;
}
$sql = "SELECT * FROM ".$table.$where;
$sql = $this->conn->query($sql);
$sql = $sql->fetch_assoc();
return $sql;
}
public function insert($table, $data) {
if (is_array($data)) {
foreach($data as $key => $val) {
$column[] = $key;
$value[] = "'{$val}'";
}
$columns = implode(",", $column);
$values = implode(",", $value);
}
$sql = "INSERT INTO ".$table." (".$columns.") VALUES (".$values.")";
$sql = $this->conn->query($sql);
if ($sql == true) {
return $sql;
} else {
return false;
}
}
public function update($table, $data, $where) {
$update_value = "";
if (is_array($data)) {
foreach($data as $key => $val) {
$update_value[] = "$key='{$val}'"
}
$update_value = implode(",", $update_value);
}
$sql = "UPDATE ".$table." SET ".$update_value." WHERE ".$where;
$sql = $this->conn->query($sql);
if ($sql == true) {
return true;
} else {

return false;
}
}
public function delete($table, $filter) {
$sql = "DELETE FROM ".$table." ".$filter;
$sql = $this->conn->query($sql);
if ($sql == true) {
return true;
} else {
return false;
}
}
}
?>
![WhatsApp Image 2024-12-04 at 12 47 14](https://github.com/user-attachments/assets/24ecc15b-364a-492f-9e14-1bf7fccd1268)

#Membuat database test

MariaDB [(none)]> USE latihan1;
Database changed
MariaDB [latihan1]> CREATE TABLE users (
    ->     id INT AUTO_INCREMENT PRIMARY KEY,
    ->     name VARCHAR(255) NOT NULL,
    ->     email VARCHAR(255) NOT NULL UNIQUE
    -> );
Query OK, 0 rows affected (0.015 sec)

MariaDB [latihan1]> INSERT INTO users (name, email)
    -> VALUES
    -> ('Ifa', 'ifanurul@gmail.com');
Query OK, 1 row affected (0.006 sec)
![WhatsApp Image 2024-12-04 at 13 56 24](https://github.com/user-attachments/assets/6079e12a-fbcb-4942-99b3-23e38e30eadd)


#Menampilkan tabel

MariaDB [latihan1]> select* from users;
+----+------+--------------------+
| id | name | email              |
+----+------+--------------------+
|  1 | Ifa  | ifanurul@gmail.com |
+----+------+--------------------+
![WhatsApp Image 2024-12-04 at 13 57 09](https://github.com/user-attachments/assets/861bd460-4fa1-41d4-879c-7f9fe1d9760f)

1 row in set (0.000 sec)






