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
Praktikum ini berfokus pada pengenalan konsep dasar framework Flutter, pemahaman hierarki antarmuka melalui susunan widget tree, serta implementasi mekanisme state management lokal. Target utama modul ini adalah memodifikasi alur kerja Counter App bawaan agar memiliki skema warna yang selaras, penataan identitas mahasiswa pada bilah atas, serta pembaruan tampilan antarmuka yang reaktif terhadap input pengguna.

---

### Dasar Teori & Pembahasan Kode
Flutter membagi komponen antarmuka menjadi dua model utama, yaitu StatelessWidget untuk elemen yang tidak berubah dan StatefulWidget untuk elemen yang memiliki data dinamis selama runtime. Pada modul ini, pengelolaan status dilakukan menggunakan fungsi `setState()`. Fungsi ini bertindak sebagai pemicu agar framework hanya merender ulang komponen teks yang menampilkan angka, sehingga proses rendering berjalan efisien tanpa membebani memori.

Pewarnaan antarmuka diatur secara global melalui properti `ThemeData` dengan mengaktifkan Material 3 dan memilih biru sebagai warna dasar via `ColorScheme.fromSeed(seedColor: Colors.blue)`. Seluruh hierarki halaman kemudian dibungkus di dalam `Scaffold`, dengan `AppBar` yang menampilkan data identitas mahasiswa serta `FloatingActionButton` sebagai pemicu interaksi penambahan angka.

Berikut implementasi lengkap pada berkas `lib/main.dart`:

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

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'Selamat Datang di Modul Pemrograman Mobile Flutter!',
              textAlign: TextAlign.center,
              style: TextStyle(fontWeight: FontWeight.bold, fontSize: 16),
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
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

### Hasil Pengujian & Analisis Tampilan

Aplikasi diuji langsung pada perangkat fisik Android (Vivo iQOO) menggunakan sambungan Wireless ADB dan penampil layar scrcpy untuk mengevaluasi fungsionalitas logika serta kestabilan rendering.

#### Gambar A: Integrasi Lingkungan Pengembangan dan Eksekusi Kode

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/desktop_preview.png" width="85%" alt="Gambar A: Eksekusi Kode dan Integrasi Sistem" />
</p>

Tangkapan layar di atas memperlihatkan alur kerja saat aplikasi dijalankan melalui Android Studio di lingkungan Linux Fedora. Editor kode menampilkan konfigurasi tema Material 3 dan teks identitas mahasiswa pada AppBar, sementara terminal bawah menunjukkan sesi scrcpy yang aktif terhubung via ADB nirkabel. Pada jendela mirroring di sisi kiri, angka counter berhasil mencapai nilai 12 setelah tombol ditekan secara berulang, membuktikan bahwa logika penambahan angka dan pemanggilan `setState()` berjalan tanpa lag maupun kebocoran memori.

---

#### Gambar B: Tampilan Antarmuka pada Layar Perangkat

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/mobile_preview.jpeg" width="45%" alt="Gambar B: Tampilan Aplikasi pada Layar Ponsel" />
</p>

Tangkapan layar ini menunjukkan hasil rendering akhir aplikasi langsung pada layar smartphone. Komponen AppBar di bagian atas menampilkan identitas pengerjaan modul secara proporsional dengan latar warna biru muda bawaan Material 3. Di area tengah, teks sambutan dan teks angka counter tersusun rapi secara vertikal menggunakan widget Column dan Center, didukung oleh FloatingActionButton di pojok kanan bawah yang siap menerima input ketukan berikutnya.

---

### Struktur Percabangan Repositori
Repositori ini mengelola dua branch pengerjaan. Branch `main` difokuskan untuk implementasi Modul 4 yang mencakup dasar Flutter, susunan widget tree, dan aplikasi counter bertema biru. Sementara branch `materi-5` memuat pengembangan lanjutan untuk modul autentikasi seperti halaman login, register, validasi formulir input, dan dashboard utama.

---

### Panduan Menjalankan Aplikasi
Untuk menjalankan proyek ini pada branch tugas saat ini, buka terminal di direktori proyek lalu jalankan perintah berikut:

```bash
git checkout main
flutter pub get
flutter run --android-skip-build-dependency-validation
```