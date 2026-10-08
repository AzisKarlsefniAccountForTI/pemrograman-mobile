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
Praktikum ini berfokus pada pengenalan dasar framework Flutter, pemahaman struktur berkas proyek, hierarki antarmuka (*widget tree*), serta implementasi *state management* lokal sederhana. Pada modul ini, saya memodifikasi alur kerja dari aplikasi dasar Counter App. Modifikasi dilakukan dengan menyesuaikan skema warna menjadi nuansa biru, menyematkan identitas diri pada bilah judul atas, menambahkan variabel teks sambutan modul di atas angka counter, serta memastikan bahwa data angka dapat bertambah secara tepat setiap kali tombol aksi ditekan.

---

### Struktur Direktori Proyek
Seluruh kode logika utama aplikasi ditulis dan dikelola di dalam berkas `lib/main.dart`. Berikut adalah susunan struktur direktori proyek ini:

```text
prak_pertemuansatu/
├── android/
├── assets/
│   └── screenshots/
│       ├── desktop_preview.png
│       ├── mobile_preview.jpeg
│       └── chrome_preview.png
├── lib/
│   └── main.dart          <-- Berkas logika utama aplikasi
├── pubspec.yaml
└── README.md
```

---

### Dasar Teori & Pembahasan Kode
Flutter membagi komponen antarmuka menjadi dua model utama:
1. **StatelessWidget**: Widget statis yang sifatnya tetap dan tidak terpengaruh oleh perubahan data internal saat aplikasi berjalan.
2. **StatefulWidget**: Widget dinamis yang dapat menyimpan status nilai data (*state*) dan mampu memperbarui tampilan antarmuka secara otomatis ketika data tersebut berubah.

Pada tugas ini, saya memanfaatkan `StatefulWidget` dengan fungsi `setState()`. Ketika pengguna menekan tombol aksi, fungsi `setState()` memberi tahu framework bahwa variabel `_counter` telah bertambah nilainya. Flutter kemudian hanya menggambar ulang teks penampil angka secara responsif tanpa perlu merender ulang keseluruhan antarmuka halaman.

Selain penanganan data angka, saya juga menambahkan variabel String `pesan` untuk memuat teks sambutan modul yang dibungkus menggunakan widget `Padding` agar posisinya nyaman dibaca di atas angka hitungan. Tema visual disetel melalui `ThemeData` dengan mengaktifkan Material 3 dan memilih `Colors.blue` sebagai warna dasar (`ColorScheme.fromSeed`), sehingga bilah `AppBar`, tombol, serta efek sentuhan otomatis seragam.

Berikut adalah implementasi kode lengkap pada berkas `lib/main.dart`:

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

Aplikasi ini diuji langsung pada dua platform yang berbeda, yaitu perangkat fisik Android serta web browser Google Chrome untuk memastikan portabilitas dan responsivitas program.

#### Gambar A: Integrasi Lingkungan Pengembangan dan Eksekusi Kode

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/desktop_preview.png" width="85%" alt="Gambar A: Eksekusi Kode dan Integrasi Sistem" />
</p>

Tangkapan layar ini memperlihatkan alur kerja pengujian saat berkas `lib/main.dart` dijalankan melalui Android Studio di sistem operasi Linux. Di area editor, seluruh kode mulai dari variabel teks sambutan, tema warna biru, hingga identitas mahasiswa pada `AppBar` sudah terpasang rapi. Pada terminal bagian bawah, sesi scrcpy aktif terhubung ke perangkat Android via ADB nirkabel. Pada jendela mirroring di sisi kiri, terlihat jelas bahwa aplikasi berhasil menerima aksi klik secara berulang hingga angka counter mencapai nilai 12, yang membuktikan fungsi `_incrementCounter()` dan pembaruan `setState()` bekerja normal tanpa hambatan.

---

#### Gambar B: Tampilan Nyata Aplikasi di Layar Ponsel

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/mobile_preview.jpeg" width="45%" alt="Gambar B: Tampilan Aplikasi pada Layar Ponsel" />
</p>

Tangkapan layar ini menunjukkan hasil rendering aplikasi saat berjalan langsung pada layar smartphone fisik (Vivo iQOO). Bilah navigasi atas (`AppBar`) memuat identitas pengerjaan tugas secara jelas dengan aksen warna biru Material 3. Di bagian tengah, teks sambutan tebal tampil simetris dengan jarak bantalan horizontal yang pas, diikuti oleh teks petunjuk dan angka counter yang berada tepat di tengah layar. Di sudut kanan bawah, tombol aksi melayang (`FloatingActionButton`) dengan ikon tambah siap menerima ketukan berikutnya dari pengguna.

---

#### Gambar C: Hasil Eksekusi Aplikasi pada Google Chrome

<p align="center">
  <img src="https://raw.githubusercontent.com/AzisKarlsefniAccountForTI/pemrograman-mobile/main/assets/screenshots/chrome_preview.png" width="85%" alt="Gambar C: Tampilan Aplikasi pada Google Chrome" />
</p>

Tangkapan layar ini membuktikan bahwa program juga berhasil dikompilasi ke platform web menggunakan perintah `flutter run -d chrome`. Seluruh susunan antarmuka—mulai dari teks judul pada bilah atas, teks sambutan modul, penampil angka dinamis, hingga tombol aksi penambah counter—mampu ter-render dengan presisi pada browser Google Chrome tanpa terjadi pergeseran tata letak maupun masalah logika fungsional.

---

### Struktur Percabangan Repositori
* **`main`**: Berisi implementasi kode tugas Praktikum 4 (dasar widget, variabel teks sambutan, penyesuaian tema warna biru, dan pengujian multi-platform).
* **`materi-5`**: Berisi kelanjutan tugas untuk Modul 5 (halaman Login, Register, validasi form, dan Dashboard).

---