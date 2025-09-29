# PostTest4_PBO (Manajemen_Daftar_Festival_Budaya)

Nama : Rini Wulandari

NIM : 2409116048

Kelas : Sistem Informasi B 2024

## Penjelasan Singkat terkait Program
Program ini berguna dalam menampung informasi data dari Festival Budaya mulai dari nama festival, asal festival dan tanggal pelaksanaan festival. Dalam program ini menyediakan opsi untuk menambahkan festival baru, menampilkan daftar festival dalam format tabel, mengubah data festival berdasarkan nomor urut, serta menghapus festival sekaligus memperbarui daftar agar tetap berurutan. Proses menu dijalankan menggunakan perulangan do-while dan struktur switch-case, dilengkapi validasi agar input nomor yang dipilih sesuai dengan data yang ada.

## Struktur Program
Program ini dibagi menjadi 3 package utama dengan 2 subclass pada package Model:

<img width="304" height="275" alt="image" src="https://github.com/user-attachments/assets/2d1bbd20-e2b3-4b01-8388-be68afe9838d" />

1. **package Main**

   Package ini berisi class mainFestival yang menampilkan menu interaktif kepada pengguna. Melalui menu ini, pengguna bisa mengakses berbagai fitur CRUD dengan lebih mudah, lengkap dengan validasi agar input tetap aman.

2. **package Model**

   Di package ini terdapat abstract class modelFestival yang berperan sebagai superclass dari subclass Tradisional dan SeniPertujukan untuk menyimpan data dasar sebuah festival, seperti nama, asal daerah, dan tanggal pelaksanaannya dan ada tambahan class Festival yang berfungsi sebagai interface yang akan ditampilkan dalam subclass. Package ini berfungsi sebagai tempat mendefinisikan struktur data yang akan dipakai program.

   - **SubClass Tradisional**, digunakan untuk merepresentasikan festival yang masih kental akan adat istiadat. Selain atribut umum dari kelas modelFestival, ditambahkan atribut ritualAdat untuk menampilkan detail khas, seperti ritual utama dalam festival budaya.
     
   - **SubClass SeniPertunjukan**, digunakan untuk menggambarkan festival yang berfokus pada seni, seperti tari, musik, atau teater. Kelas ini menambahkan atribut jenisSeni sehingga informasi festival seni bisa ditampilkan lebih spesifik sesuai jenis pertunjukannya dalam festival.

   - **Festival**, berfungsi sebagai aturan dasar yang harus diikuti oleh setiap kelas festival. Di dalamnya hanya ada satu metode, yaitu deskripsiSingkat(), yang nantinya wajib dibuat oleh kelas turunan seperti Tradisional dan SeniPertunjukan.
   
3. **package Service**

   Package ini berisi class serviceFestival yang mengatur semua logika CRUD. Di sinilah data festival dikelola, mulai dari menambah, menampilkan, mengubah, hingga menghapus, sehingga menjadi penghubung antara data dan menu utama.

---
## Penjelasan Source Code Program
### 1. Package & Class modelFestival

<img width="267" height="139" alt="image" src="https://github.com/user-attachments/assets/dfaf6fb5-fc1b-412b-9365-2880899b40af" />

**a. Deklarasi package**
```Java
package Model;
```
Package berfungsi untuk mengelompokkan kelas agar lebih terstruktur, rapi, dan mudah dikelola. Gambar diatas menunjukkan bahwa class modelFestival berada dalam package bernama Model.

**b. Deklarasi Class**
```Java
public abstract class modelFestival {
```
File modelFestival.java adalah kelas abstrak yang menjadi dasar bagi semua jenis festival. Di dalamnya terdapat atribut umum seperti nama, asal, dan tanggal pelaksanaan, lengkap dengan getter, setter, serta method toString().

**c. Atribut**
```Java
   private String namaFestival;
   private String asal;
   private String tanggalPelaksanaan;
```
Kode di atas mendefinisikan tiga atribut dalam class Model dengan modifier private yaitu namaFestival, asal, dan tanggalPelaksanaan. Ketiganya bertipe String dan berfungsi untuk menyimpan data utama tentang festival budaya. Modifier private membuat atribut hanya bisa diakses melalui method khusus salah satunya getter dan setter.

**d. Construktor**
```Java
public modelFestival(String namaFestival, String asal, String tanggalPelaksanaan) {
   this.namaFestival = namaFestival;
   this.asal = asal;
   this.tanggalPelaksanaan = tanggalPelaksanaan;
}
```
Pada construktor ini otomatis akan dijalankan saat kita membuat objek baru dari kelas modelFestival. Parameter yang dimasukkan adalah namaFestival, asal, tanggalPelaksanaan yang dimana langsung disimpan ke dalam variabel kelas menggunakan kata kunci "this.".

**e. Getter dan Setter**
```Java
public String getNamaFestival() {
   return namaFestival;
}

public String getAsal() {
   return asal;
}

public String getTanggalPelaksanaan() {
   return tanggalPelaksanaan;
}

public void setNamaFestival(String namaFestival) {
   this.namaFestival = namaFestival;
}

public void setAsal(String asal) {
   this.asal = asal;
}

public void setTanggalPelaksanaan(String tanggalPelaksanaan) {
   this.tanggalPelaksanaan = tanggalPelaksanaan;
}
```
- Getter dan Setter ini berfungsi untuk mengambil dan mengubah data festival. Method getter dipakai untuk melihat nilai dari atribut, seperti nama festival, asal, dan tanggal pelaksanaannya.
- Sedangkan method setter dipakai untuk mengganti atau memberikan nilai baru pada atribut tersebut. Cara ini menjaga agar data tetap aman karena atribut dibuat private, tetapi tetap bisa digunakan lewat method khusus.

**f. Method toString()**
```Java
public abstract String getJenisFestival();
```

- Method getJenisFestival() dibuat di kelas modelFestival sebagai penanda agar setiap jenis festival bisa menjelaskan dirinya sendiri. Jadi, ketika ada festival tradisional atau seni pertunjukan, masing-masing akan menampilkan keterangan sesuai dengan ciri khasnya.
- Dengan cara ini, setiap festival punya identitas yang jelas meskipun berasal dari kerangka dasar yang sama.

**g. Method toString()**
```Java
@Override
public String toString() {
   return String.format("%-30s | %-20s | %-20s", namaFestival, asal, tanggalPelaksanaan);
}
```

- Di bagian akhir ada metode toString(). Ini adalah cara untuk mengatur bagaimana sebuah objek ditampilkan kalau dipanggil dengan System.out.println().
- Dalam kode ini digunakan String.format() untuk membuat tampilan yang rapi seperti tabel nama festival ditaruh di kolom rata kiri dengan lebar 30 karakter, asal di kolom 20 karakter, dan tanggal pelaksanaan di kolom 20 karakter juga. Hasilnya, daftar festival akan tercetak sejajar sehingga lebih mudah dibaca.

---
