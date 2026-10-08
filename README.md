# Laporan Praktikum Pemrograman Mobile
## Modul 4: Pengenalan Flutter dan State Management Dasar

---

### Identitas Mahasiswa
* **Nama**: Azis Khoirul Setiawan
* **NIM**: 43050250004
* **Kelas**: 3A
* **Mata Kuliah**: Pemrograman Mobile

---

### Pendahuluan
Praktikum ini membahas dasar-dasar pengembangan aplikasi Android menggunakan framework Flutter. Fokus utama pada modul ini adalah memahami cara kerja hierarki widget (*widget tree*) dan menerapkan pengelolaan data dinamis sederhana melalui mekanisme *state management* lokal. Pada modul ini, saya memodifikasi aplikasi bawaan Flutter (Counter App) agar memiliki tampilan tema biru, menyematkan identitas diri pada bilah atas, serta memastikan angka pada layar dapat bertambah secara tepat setiap kali tombol aksi ditekan.

---

### Dasar Teori & Pembahasan Kode
Pada framework Flutter, antarmuka dibangun menggunakan widget. Secara mendasar terdapat dua jenis widget utama:
1. **StatelessWidget**: Widget statis yang tampilannya tidak berubah sepanjang aplikasi berjalan.
2. **StatefulWidget**: Widget dinamis yang dapat menyimpan status data (*state*) dan memperbarui tampilannya saat data tersebut mengalami perubahan.

Dalam modul ini, saya memanfaatkan `StatefulWidget` dengan fungsi `setState()`. Ketika tombol ditekan, fungsi `setState()` akan memberi sinyal kepada framework bahwa nilai variabel penampung telah berubah. Flutter kemudian hanya merender ulang komponen teks yang menampilkan angka, sehingga performa aplikasi tetap terjaga dan efisien.

Selain logika data, saya juga mengatur tema aplikasi melalui `ThemeData` dengan mengaktifkan Material 3 dan menentukan warna dasar biru lewat `ColorScheme.fromSeed(seedColor: Colors.blue)`. Pengaturan ini secara otomatis menyeragamkan warna `AppBar`, tombol, serta latar belakang aplikasi.

Berikut adalah kode lengkap yang saya implementasikan pada berkas `lib/main.dart`:

```dart
import 'package:flutter/material.dart';

void main() {
   runApp(const MyApp());
}

class MyApp extends StatelessWidget {
   const MyApp({super.key});

   @override
   Widget build(BuildContext context) {
      return MaterialApp(
         debugShowCheckedModeBanner: false,
         title: 'Aplikasi Pertama',
         theme: ThemeData(
            colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),
            useMaterial3: true,
         ),
         home: const MyHomePage(title: 'Praktikum 4 - Azis Khoirul Setiawan - 43050250004'),
      );
   }
}

class MyHomePage extends StatefulWidget {
   const MyHomePage({super.key, required this.title});

   final String title;

   @override
   State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
   int _counter = 0;

   // Tugas modul: variabel pesan sambutan
   String pesan = "Selamat Datang di Modul Pemrograman Mobile Flutter!";

   void _incrementCounter() {
      setState(() {
         _counter++;
      });
   }

   @override
   Widget build(BuildContext context) {
      return Scaffold(
         appBar: AppBar(
            title: Text(widget.title),
            backgroundColor: Theme.of(context).colorScheme.inversePrimary,
         ),
         body: Center(
            child: Column(
               mainAxisAlignment: MainAxisAlignment.center,
               children: <Widget>[
                  // Tugas modul: penempatan pesan di atas counter
                  Padding(
                     padding: const EdgeInsets.symmetric(horizontal: 20.0),
                     child: Text(
                        pesan,
                        textAlign: TextAlign.center,
                        style: const TextStyle(
                           fontSize: 16,
                           fontWeight: FontWeight.bold,
                        ),
                     ),
                  ),
                  const SizedBox(height: 20),
                  const Text('Jumlah tombol ditekan:'),
                  Text(
                     '$_counter',
                     style: Theme.of(context).textTheme.headlineMedium,
                  ),
               ],
            ),
         ),
         floatingActionButton: FloatingActionButton(
            onPressed: _incrementCounter,
            tooltip: 'Tambah',
            child: const Icon(Icons.add),
         ),
      );
   }
}
```

---

### Hasil Pengujian & Bukti Eksekusi

Aplikasi ini saya uji langsung dengan menjalankannya ke smartphone Android fisik (Vivo iQOO) via Wireless ADB, lalu saya tampilkan layarnya menggunakan alat bantu scrcpy agar proses pengujian dan interaksinya terlihat jelas secara *real-time*.

#### Gambar A: Bukti Program Berhasil Dikompilasi dan Berjalan Normal

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/desktop_preview.png" width="85%" alt="Gambar A: Eksekusi Kode dan Integrasi Sistem" />
</p>

Tangkapan layar di atas menunjukkan bahwa proses kompilasi kode berhasil tanpa adanya kendala atau galat. Di sisi editor Android Studio, struktur kode mulai dari tema biru hingga parameter identitas diri pada `AppBar` sudah terpasang dengan benar. Sementara itu, pada jendela mirroring di sebelah kiri layar, aplikasi terbukti berhasil menerima aksi sentuhan secara berkelanjutan hingga angka penghitung mencapai nilai **12**. Hal ini membuktikan bahwa fungsi `_incrementCounter()` dan mekanisme pembaruan antarmuka dengan `setState()` berjalan konsisten tanpa hambatan.

---

#### Gambar B: Tampilan Nyata Aplikasi di Layar Ponsel

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/mobile_preview.jpeg" width="45%" alt="Gambar B: Tampilan Aplikasi pada Layar Ponsel" />
</p>

Tangkapan layar ini memperlihatkan antarmuka aplikasi saat dijalankan langsung pada perangkat ponsel. Bilah `AppBar` di bagian paling atas berhasil menampilkan identitas nama dan NIM secara jelas dengan perpaduan warna biru Material 3. Bagian tengah layar memuat teks petunjuk serta angka counter yang posisinya berada tepat di tengah. Di sudut kanan bawah, tombol aksi `FloatingActionButton` dengan ikon tambah juga terpasang rapi dan langsung merespons ketukan secara instan.

---

### Struktur Percabangan Repositori
* **`main`**: Berisi implementasi kode tugas Praktikum 4 (dasar widget, modifikasi tema warna biru, dan pengujian Counter App).
* **`materi-5`**: Berisi pengerjaan tugas Modul 5 (halaman Login, Register, validasi input formulir, dan Dashboard).

---

### Cara Menjalankan Proyek
Untuk menjalankan kode tugas modul ini pada perangkat yang terhubung, buka terminal pada direktori proyek lalu masukkan perintah berikut:

```bash
git checkout main
flutter pub get
flutter run --android-skip-build-dependency-validation
```