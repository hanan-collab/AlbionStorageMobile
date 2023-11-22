# TUGAS 9

## Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?

Ya, di Flutter, kita **dapat** melakukan pengambilan data JSON tanpa membuat model terlebih dahulu. Ini biasanya dilakukan menggunakan tipe data dinamis (dynamic) atau `Map<String, dynamic>` untuk mewakili struktur data JSON. Pendekatan ini disebut sebagai *parsing dinamis* atau *parsing tanpa model*. Namun tentu ada keuntungan dan kekurangannya. 
<br>Keuntungannya antara lain:
- **Sederhana dan Cepat** dalam mengambil dan menggunakan data JSON tanpa harus membuat struktur kelas,
- **Fleksibel** jika struktur JSON cenderung berubah atau tidak terlalu kompleks.

Kekurangannya antara lain:
- **Ketidakamanan Tipe**, kode menjadi lebih rentan terhadap kesalahan tipe saat berinteraksi dengan data.
- **Kesulitan Pemahaman Kode** membuat kode menjadi kurang deskriptif.
- **Kode yang Rapuh** jika struktur JSON berubah, tidak ada jaminan bahwa aplikasi akan tetap berfungsi seperti yang diharapkan.

### Kesimpulan
Pilihan antara parsing dinamis dan menggunakan model tergantung pada kompleksitas struktur data dan persyaratan aplikasi. Jika struktur data sederhana dan fleksibilitas lebih diutamakan daripada keamanan tipe, parsing dinamis dapat digunakan. Namun, untuk aplikasi yang lebih besar dan kompleks, membuat model biasanya lebih disarankan karena memberikan keamanan tipe, kemudahan pemeliharaan, dan deskripsi yang lebih baik tentang struktur data.

## Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest dalam konteks ini adalah bagian dari Flutter yang digunakan untuk mengelola informasi otentikasi, seperti token, yang diperlukan untuk berinteraksi dengan server Django. Dengan menggunakan Flutter Provider, instance CookieRequest dapat dibagikan ke seluruh aplikasi. Ini bermanfaat agar semua bagian aplikasi dapat dengan mudah mengakses dan menggunakan informasi otentikasi tanpa harus membuat ulang instance tersebut.

## Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
1. Pembuatan model kostum, contohnya pada `models/product.dart`. Data json nantinya akan diconvert ke model objek tersebut agar lebih mudah diakses.
2. Lakukan fetch terhadap data json dari sumber yang diinginkan, contoh pada program ini `localhost8000/json` dan parsing ke model kostum yang ada.
3. Data dapat diakses sesuai dengan struktur model yang telah didefinisikan.

## Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

1. Pengumpulan Data Akun di Flutter: Gunakan formulir atau metode input untuk mendapatkan data informasi akun dari pengguna.

2. Pengembangan Fungsi Login, Registrasi, dan Logout dalam Aplikasi Otentikasi Baru untuk Flutter.

3. Proses Autentikasi dengan Django, Kirimkan data akun ke backend Django melalui permintaan `request.login` (dengan menggunakan cookies dan fungsi login dari paket) dan lakukan proses autentikasi pada Django.

4. Dari Django, akan dikirimkan data JSON yang diperlukan untuk validasi dan masukan pesan dalam Flutter yang menunjukkan keberhasilan atau kegagalan proses login.

5. Dari hasil login, kita menerima respons JSON yang berisi status, pesan, dan nama pengguna dari login Django.

6. Dengan menggunakan status, kita dapat membuat kondisi-kondisi yang diinginkan berdasarkan hasil status tersebut. Selain itu, kita dapat menampilkan pesan yang dihasilkan oleh fungsi login di `views.py` Django.

7. Setelah berhasil login, kita dapat menampilkan `MyHomepage` sebagai tampilan utama menu. Untuk menyimpan informasi login, seperti cookies dan nama pengguna yang berhasil login, kita dapat menggunakan variabel statis dalam kelas `LoginPage`. Hal ini memungkinkan kita untuk mengakses informasi ini di berbagai bagian aplikasi.

## Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.

### Widget di `login.dart`
1. `AppBar`digunakan untuk menampilkan judul aplikasi dan propertynya
2. `Stack` memungkinkan penumpukan widget di atas satu sama lain.
3. `Container` berfungsi sebagai wadah untuk menampung widget lain dalam Flutter.
4. `SnackBar` memberikan umpan balik kepada pengguna dengan cepat dengan menampilkan login berhasil.
5. `Text` digunakan untuk menampilkan teks dalam AppBar dan tampilan utama, beserta pengaturan properti seperti font, warna, dan gaya teks.
6. `TextField` digunakan untuk menyediakan field input berupa username dan password.
7. `ElevatedButton` digunakan untuk menampilkan tombol dengan efek visual untuk melakukan login.

### Widget di `detail_product.dart`
1. `Scaffold` menyediakan kerangka kerja dasar untuk suatu halaman, termasuk AppBar, body, dan fitur-fitur lainnya.

2. `AppBar` menyediakan AppBar di bagian atas halaman dengan judul "Product Details".

3. `Padding` digunakan untuk menambahkan jarak (padding) di sekitar widget-child di dalamnya. Pada contoh ini, Padding memberikan jarak 16.0 pada semua sisi child-widget-nya.

4. `Column` mengatur child-widget-nya dalam kolom vertikal. Dalam hal ini, widget-column digunakan untuk menyusun teks-detail produk secara vertikal.

5. `Text` digunakan untuk menampilkan teks. Dalam contoh ini, tiga buah Text widget digunakan untuk menampilkan nama produk, harga, dan deskripsi produk.

6. `SizedBox` digunakan untuk menambahkan jarak kosong (height) di antara elemen-elemen dalam Column. Pada contoh ini, dua buah SizedBox digunakan untuk memberikan ruang kosong di antara teks-teks.

### Widget di `list_product.dart`
1. `Scaffold` menyediakan kerangka kerja dasar untuk suatu halaman, termasuk AppBar, drawer, dan body.

2. `AppBar` menampilkan AppBar di bagian atas halaman dengan judul "Product".

3. `LeftDrawer` widget yang diimpor dari file terpisah (left_drawer.dart), yang kemungkinan berisi implementasi drawer kiri untuk navigasi atau tindakan tambahan.

4. `FutureBuilder` digunakan untuk menangani proses asynchronous dan membangun tampilan berdasarkan status Future (misalnya, data yang sedang dimuat, sukses, atau gagal).

5. `CircularProgressIndicator` menampilkan indikator putar saat data sedang dimuat.

6. `Column` mengatur child-widget-nya dalam kolom vertikal. Digunakan untuk menyusun teks informasi produk secara vertikal.

7. `Text` menampilkan teks. Digunakan untuk menampilkan pesan "Tidak ada data produk." jika data tidak tersedia.

8. `ListView.builder` membangun daftar produk menggunakan data yang diterima dari FutureBuilder.

9. `InkWell` membuat area yang dapat ditekan (tappable) untuk setiap produk dalam daftar.

10. `MouseRegion` menambahkan efek hover ke dalam area yang dapat ditekan.

11. `Container` menyediakan wadah untuk mengatur margin, padding, dan properti lainnya untuk elemen-elemen dalam daftar produk.

## _step-by-step_
1. Membuat dan mengkonfigurasi app `authentication` pada project Django.

2. Install library yang dibutuhkan dengan perintah `pip install django-cors-headers`.

3. Buatlah fungsi untuk `login` dan `logout` pada `authentication/views.py` dan create_flutter pada `main/views.py`.

4. Konfigurasi urls.py pada folder `authentication` dan `main`.

5. Instal package yang disediakan,
```
flutter pub add provider
flutter pub add pbp_django_auth
```

6. Modifikasi root widget untuk menyediakan instance CookieRequest ke semua child widgets menggunakan Provider.

7. Buatlah file `login.dart` pada folder screens dan isi dengan kode untuk support login.

8. Pada file main.dart, ubah `home: MyHomePage()` menjadi `home: LoginPage()`.

9. Ubah perintah onPressed pada button untuk menghubungkan halaman `shoplist_form.dart` dengan CookieRequest

10. Membuat model pada `products.dart` dengan menggunakan data struktur pada tugas django sebelumnya

11. Membuat `list_product.dart` yang akan menampilkan data yang ada

11. Membuat file `detail_product.dart` untuk menampilkan detail item ketika diklik.


# TUGAS 8

## Navigator.push() VS Navigator.pushReplacement()

1. `Navigator.push()`:
  - Metode `Navigator.push()` digunakan untuk menambahkan halaman baru ke dalam tumpukan halaman (page stack) aplikasi. Jika kita memilik tumpukan halaman A -> B, menggunakan `Navigator.push()` dari halaman B akan menambahkan halaman C ke dalam tumpukan. Dengan kata lain, tumpukan halaman menjadi A -> B -> C. Jika ingin kembali ke B, maka bisa memanggil method `.pop()`, Contoh:
```
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => HalamanBaru()),
);
```
Dalam contoh di atas, HalamanBaru() ditambahkan ke dalam tumpukan halaman setelah halaman saat ini.

2. `Navigator.pushReplacement()`:
  - Metode `Navigator.pushReplacement()` digunakan ketika kita ingin menggantikan halaman saat ini dengan halaman baru. Jika kita berada di halaman A -> B, menggunakan `Navigator.pushReplacement()` dari halaman B akan menggantikan halaman B dengan halaman C, sehingga tumpukan halaman menjadi A -> C.

Contoh penggunaan:
```
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => HalamanBaru()),
);
```
Dalam contoh di atas, halaman saat ini (misalnya, halaman B) digantikan dengan HalamanBaru() dalam tumpukan halaman.

Ringkasan:
- `Navigator.push()` menambahkan halaman baru ke dalam tumpukan halaman.
- `Navigator.pushReplacement()` menggantikan halaman saat ini dengan halaman baru dalam tumpukan halaman.

## Layout Widget pada Flutter
1. `Container`:
- `Container` berfungsi sebagai wadah untuk menampung widget lain dalam Flutter. Selain itu, `Container` juga memberikan kemampuan untuk menentukan properti seperti padding, margin, dan properti lainnya yang memengaruhi tata letak dan tampilan widget di dalamnya.

2. `ListView` dan `GridView`:
- `ListView` dan `GridView` digunakan untuk menampilkan daftar atau grid widget. `ListView` cocok untuk menampilkan daftar elemen secara berurutan, sementara `GridView` cocok untuk menampilkan elemen dalam bentuk grid. Keduanya memungkinkan penggunaan efisien ruang layar untuk menampilkan sejumlah besar data.

3. `Scaffold`:
- `Scaffold` digunakan sebagai struktur utama suatu halaman dalam Flutter. Ini menyediakan kerangka kerja untuk membangun antarmuka pengguna dengan menyediakan elemen-elemen seperti AppBar untuk judul halaman, Body untuk konten utama, dan elemen lainnya seperti Drawer atau BottomNavigationBar. `Scaffold` memfasilitasi pembuatan halaman dengan struktur yang konsisten dan mudah diatur.

4. `Row` dan `Column`:
- `Row` dan `Column` digunakan sebagai pengaturan tata letak untuk menyusun widget secara horizontal (dalam `Row`) atau vertikal (dalam `Column`). Mereka memfasilitasi penyusunan dan penataan widget sesuai dengan arah yang diinginkan, membantu dalam menciptakan antarmuka pengguna yang responsif dan terstruktur.

5. `Stack`:
- `Stack` memungkinkan penumpukan widget di atas satu sama lain. Dengan menggunakan `Stack`, kita dapat menempatkan beberapa widget di lokasi yang sama dalam tumpukan, memberikan kebebasan untuk menata elemen-elemen tersebut secara bebas dan memberikan dimensi z kepada antarmuka pengguna.

## Aplikasi Elemen Input Form
Input Fields yang diaplikasikan adalah `TextFormField`. `TextFormField` merupakan elemen input dalam Flutter yang dirancang untuk menerima input teks dari pengguna. Fungsinya mencakup integrasi dalam widget Form, yang mempermudah proses validasi, penyimpanan nilai, dan manajemen keadaan formulir secara umum. Contoh:

1. `Validasi Otomatis`,
`TextFormField` menyediakan properti seperti validator yang memungkinkan pengembang mendefinisikan aturan validasi secara otomatis. Hal ini sangat bermanfaat untuk memastikan bahwa data yang dimasukkan oleh pengguna memenuhi persyaratan yang ditetapkan, menghindari kesalahan input yang tidak diinginkan.

2. `Kontrol State`,
dengan menggunakan `TextFormField`, Flutter secara otomatis mengelola keadaan (state) input. Pengelolaan state yang otomatis ini menyederhanakan proses pengambilan dan pengaturan nilai input, memungkinkan pengembang fokus pada logika aplikasi daripada mengurus state input secara manual.

3. `Penanganan Perubahan`,
`TextFormField` menyediakan properti onChanged, yang memungkinkan pengembang menangani perubahan nilai input dengan mudah. Ini membuka peluang untuk menjalankan tindakan khusus setiap kali nilai input berubah, seperti pembaruan visual atau pengecekan kondisi tertentu.

## Clean Architecture
`Clean architecture` pada Flutter melibatkan strategi pembagian aplikasi ke dalam tiga lapisan utama, yaitu `Presentation`, `Domain`, dan `Data`. Konsep ini dirancang untuk memisahkan dengan jelas logika bisnis dari tampilan pengguna (UI) dan akses data, menciptakan struktur yang mudah dipahami, terkelola, dan dapat diuji.

1. `Presentation` Layer, 
lapisan ini bertanggung jawab untuk menangani elemen-elemen yang berkaitan dengan tampilan pengguna (UI) dan interaksi pengguna. Presenter, yang merupakan bagian dari presentation layer, berperan sebagai perantara antara UI dan domain layer. Presenter bertugas untuk berkomunikasi dengan use case pada domain layer dan menerjemahkan data untuk ditampilkan kepada pengguna.

2. `Domain` Layer, 
domain layer menangani logika bisnis utama dari aplikasi. Use case, yang berada dalam domain layer, merepresentasikan suatu fitur atau fungsionalitas tertentu dalam aplikasi. Use case berkomunikasi dengan presenter pada presentation layer untuk menerima input dari pengguna dan memberikan output yang sesuai. Membuat pemisahan ini memungkinkan untuk pengembangan logika bisnis yang independen dari tampilan dan akses data.

3. `Data` Layer, 
lapisan ini fokus pada manajemen akses dan penyimpanan data. Repository, yang berada di data layer, bertindak sebagai perantara antara domain layer dan sumber data seperti database atau API. Repository menangani operasi pengambilan dan penyimpanan data, serta memastikan bahwa logika bisnis pada domain layer tidak bergantung langsung pada sumber data spesifik.

## _step-by-step_
1. Membuat `left_drawer.dart` pada folder widgets untuk menampilkan drawer di kiri dengan header dan list konten yang dapat membuka page baru,
```
import 'package:flutter/material.dart';
import 'package:shopping_list_flutter/screens/menu.dart';
import 'package:shopping_list_flutter/screens/shoplist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'Albion Storage',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text(
                  "Here's Your Inventory",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    fontWeight: FontWeight.normal,
                    color: Colors.white,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Item'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => ShopFormPage(),
                  ));
            },
          ),
        ],
      ),
    );
  }
}
```
2. Membuat form pada `shoplist_form.dart` di folder screens untuk input data oleh user,
```
import 'package:flutter/material.dart';
import 'package:shopping_list_flutter/widgets/left_drawer.dart';

class ShopFormPage extends StatefulWidget {
  const ShopFormPage({super.key});

  @override
  State<ShopFormPage> createState() => _ShopFormPageState();
}

class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Item',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        key: _formKey,
        child: SingleChildScrollView(
            child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                    hintText: "Nama Item",
                    labelText: "Nama Item",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    )),
                onChanged: (String? value) {
                  setState(() {
                    _name = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Nama tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Harga",
                  labelText: "Harga",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _amount = int.parse(value!);
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Harga tidak boleh kosong!";
                  }
                  if (int.tryParse(value) == null) {
                    return "Harga harus berupa angka!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Deskripsi",
                  labelText: "Deskripsi",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _description = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Deskripsi tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Align(
              alignment: Alignment.bottomCenter,
              child: Padding(
                padding: const EdgeInsets.all(8.0),
                child: ElevatedButton(
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all(Colors.indigo),
                  ),
                  onPressed: () {
                    if (_formKey.currentState!.validate()) {
                      showDialog(
                        context: context,
                        builder: (context) {
                          return AlertDialog(
                            title: const Text('Produk berhasil tersimpan'),
                            content: SingleChildScrollView(
                              child: Column(
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                  Text('Nama: $_name'),
                                  Text('Jumlah: $_amount'),
                                  Text('Deskripsi: $_description'),
                                ],
                              ),
                            ),
                            actions: [
                              TextButton(
                                child: const Text('OK'),
                                onPressed: () {
                                  Navigator.pop(context);
                                },
                              ),
                            ],
                          );
                        },
                      );
                    }
                    _formKey.currentState!.reset();
                  },
                  child: const Text(
                    "Save",
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ),
            ),
          ],
        )),
      ),
    );
  }
}
```
3. Menambahkan `left_drawer.dart` ke tampilan homepage pada `menu.dart` yang dipindahkan ke folder `screens`,
```
import 'package:flutter/material.dart';
import 'package:shopping_list_flutter/widgets/left_drawer.dart';
import 'package:shopping_list_flutter/widgets/shop_card.dart';

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
        backgroundColor: Colors.indigo,
        title: const Text(
          'Albion Storage',
        ),
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
                  'PBP Inventory', // Text yang menandakan toko
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
      drawer: const LeftDrawer(),
    );
  }
}
```
4. Menmabahkan fungsionalitas pada tombol-tombol dengan mengubah kode `shop_card.dart` pada `widgets`,
```
import 'package:flutter/material.dart';
import 'package:shopping_list_flutter/screens/shoplist_form.dart';

class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}

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
                content: Text("Kamu telah menekan tombol ${item.name}!")));
          if (item.name == "Tambah Item") {
            Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => ShopFormPage(),
                ));
          }
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
