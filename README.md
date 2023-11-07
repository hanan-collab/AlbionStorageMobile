# TUGAS 7

## Stateless VS Stateful Widget?
1. `StatelessWidget`:
   - Tidak memiliki mutable (berubah) state. Artinya, setelah dibuat, widget ini tidak dapat mengubah tampilan atau data internalnya.
   - Cocok untuk bagian dari UI yang tidak berubah atau hanya perlu dirender satu kali.
   - Widget ini lebih efisien daripada StatefulWidget karena tidak perlu mengurus pembaruan state internal.
   - Contoh dalam kode: MyApp, MyHomePage, ShopCard
     
2. `StatefulWidget`:
   - Memiliki mutable (berubah) state yang dapat diubah selama siklus hidup widget.
   - Cocok untuk bagian dari UI yang memerlukan pembaruan berdasarkan perubahan data atau input pengguna.
   - Widget ini digunakan ketika Anda perlu mengelola perubahan state dan mengubah tampilan widget secara dinamis.
  
## Aplikasi Widget
1. `MaterialApp` digunakan untuk memulai aplikasi Flutter dengan pengaturan tema dan media halaman beranda.
2. `AppBar`digunakan untuk menampilkan judul aplikasi dan propertynya
3. `Scaffold` digunakan untuk membuat tampilan dasar aplikasi, termasuk AppBar dan area konten utama.
4. `Center` digunakan untuk menempatkan konten di tengah secara horizontal dan vertikal.
5. `Text` digunakan untuk menampilkan teks dalam AppBar dan tampilan utama, beserta pengaturan properti seperti font, warna, dan gaya teks.
6. `SingleChildScrollView` digunakan untuk memungkinkan kontennya digulir jika ukurannya melebihi layar.
7. `Padding` digunakan untuk menambahkan ruang kosong antara elemen-elemen dalam tampilan.
8. `Column` adalah widget yang menata elemen-elemen secara vertikal.
9. `GridView.count` digunakan untuk membuat tata letak grid dengan jumlah kolom yang dapat disesuaikan.
10. `ShopCard` digunakan untuk untuk menampilkan setiap item dalam grid, termasuk ikon dan teks yang sesuai.
11. `InkWell` digunakan untuk memberikan respons saat item di grid diklik, menciptakan pengalaman interaktif bagi pengguna.
12. `Icon` digunakan untuk menampilkan ikon yang sesuai dengan setiap item dalam grid.
13. `SnackBar` adalah widget yang muncul di bagian bawah layar ketika salah satu item dalam grid diklik, memberikan umpan balik kepada pengguna dengan cepat.

## _step-by-step_
Berikut adalah langkah-langkah untuk membuat program Flutter saya:

1. Buat proyek Flutter baru dengan nama `shopping_list_flutter`,
```
flutter create shopping_list_flutter
```

2. Pisahkan kode menjadi dua berkas (`main.dart` dan `menu.dart`). Kemudian pada `menu.dart` tambahkan kode berikut untuk mendefinisikan tampilan dasar aplikasi dan tiga tombol sederhana dengan ikon dan teks,
```
class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  final List<ShopItem> items = [
    ShopItem("Lihat Item", Icons.checklist, Colors.black),
    ShopItem("Tambah Item", Icons.add_shopping_cart, Colors.red),
    ShopItem("Logout", Icons.logout, Colors.green),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Shopping List',
            style: TextStyle(color: Colors.white),
          ),
        ),
        backgroundColor: Colors.indigo,
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'PBP Shop', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iterasi untuk setiap item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
3. Di `menu.dart` tambahkan definisi kelas ShopItem untuk merepresentasikan setiap item dalam daftar,
```
class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}
```
4. Di `menu.dart` tambahkan definisi kelas ShopCard untuk membuat tampilan kartu untuk setiap item dalam daftar,
```
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
5. Di `main.dart` tambahkan kode untuk menginisialisasi dan menjalankan aplikasi,
```
import 'package:flutter/material.dart';
import 'package:shopping_list_flutter/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // TRY THIS: Try running your application with "flutter run". You'll see
        // the application has a blue toolbar. Then, without quitting the app,
        // try changing the seedColor in the colorScheme below to Colors.green
        // and then invoke "hot reload" (save your changes or press the "hot
        // reload" button in a Flutter-supported IDE, or press "r" if you used
        // the command line to start the app).
        //
        // Notice that the counter didn't reset back to zero; the application
        // state is not lost during the reload. To reset the state, use hot
        // restart instead.
        //
        // This works for code too, not just values: Most code changes can be
        // tested with just a hot reload.
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        useMaterial3: true,
      ),
      home: MyHomePage(),
    );
  }
}
```
Dengan mengikuti langkah-langkah di atas, Akan didapatkan tampilan seperti berikut,
<img width="480" alt="image" src="https://github.com/hanan-collab/AlbionStorageMobile/assets/63461469/101b2c84-1457-4152-abd2-b338c8c43d9d">
