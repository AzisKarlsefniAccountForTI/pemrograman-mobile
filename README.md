# Laporan Praktikum Pemrograman Mobile - Pertemuan 4

## Identitas Mahasiswa
* **Nama**: Azis Khoirul Setiawan
* **NIM**: 43050250004
* **Kelas**: 3A

---

## 1. Pendahuluan
Praktikum ini membahas konsep dasar pengembangan aplikasi menggunakan framework Flutter, pemahaman hierarki widget (*Widget Tree*), serta implementasi *state management* lokal sederhana. Fokus utama tugas kali ini adalah memodifikasi alur kerja *Counter App* bawaan Flutter agar sesuai dengan kebutuhan tugas, baik dari segi penyesuaian tema antarmuka, tata letak teks, maupun pengikatan data dinamis ke komponen layar.

---

## 2. Analisis Kode & Alur Kerja Program
Aplikasi disusun menggunakan pendekatan berbasis *reactive framework*, di mana tampilan UI akan otomatis menyesuaikan diri ketika terjadi perubahan status nilai pada variabel.

* **Pengaturan Skema Warna & Tema Global**:
  Properti `ThemeData` dikonfigurasi menggunakan `ColorScheme.fromSeed(seedColor: Colors.blue)` dengan flag `useMaterial3: true`. Pendekatan ini membuat sistem secara otomatis menghitung variasi palet warna turunan untuk elemen seperti `AppBar`, latar tombol, hingga efek ripple ketukan agar serasi dengan aksen biru yang dipilih.

* **Penataan Komponen AppBar**:
  Widget `AppBar` digunakan sebagai bilah navigasi atas untuk memuat identitas pengerjaan tugas secara dinamis. Teks judul diatur agar langsung merepresentasikan informasi praktikum dan nama mahasiswa sehingga mempermudah proses verifikasi hasil kerja[cite: 4, 5].

* **Logika Pembaruan State (`setState`)**:
  Pusat logika perhitungan angka berada di dalam kelas turunan `State<MyHomePage>`. Variabel counter diinisialisasi bertipe integer untuk menampung riwayat klik tombol[cite: 4, 5]. Ketika pengguna menekan tombol aksi, fungsi penambah counter dipanggil:
  ```dart
  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }