# 🍔 SAM-FOOD - Food Ordering Application

**SAM-FOOD** adalah aplikasi berbasis desktop (GUI) yang berfokus pada sistem manajemen transaksi jual beli makanan dan minuman secara daring. Aplikasi ini mengintegrasikan seluruh alur transaksi secara *real-time* yang menghubungkan tiga entitas utama: pelanggan (User), mitra restoran, dan kurir pengantar (Driver).
---

## Struktur Basis Data (Relational Schema)
Sistem basis data dirancang menggunakan model relasional yang terdiri dari **8 tabel utama** untuk mendukung konsistensi dan integritas data operasional:
1. **`Users`:** Menyimpan informasi profil dan kredensial akun pelanggan.
2. **`Driver`:** Menyimpan data kurir pengantar beserta nomor pelat kendaraan.
3. **`Restaurant`:** Berisi daftar mitra restoran beserta lokasi fisik alamatnya.
4. **`Food`:** Katalog makanan dan minuman yang dijual oleh masing-masing restoran (*Foreign Key* ke `Restaurant`).
5. **`orders`:** Mencatat data transaksi pesanan, status order (*Pending/Done/Cancelled*), serta relasi user dan driver.
6. **`Detail_Pesanan`:** Tabel jembatan (*Many-to-Many*) yang merinci item makanan apa saja di dalam setiap ID order.
7. **`Payment`:** Mencatat rincian kalkulasi total biaya pesanan dan upah pengantaran driver.
8. **`Method_Payment`:** Menyimpan pilihan metode pembayaran yang valid (*Cash* atau *QRIS*).

---

## Implementasi Advanced Query & Stored Procedure
Untuk kebutuhan analisis bisnis, basis data ini mengimplementasikan beberapa *Stored Procedure* dan *Advanced Query* khusus:
* **`pembelianTertinggi`:** Menampilkan menu makanan/minuman yang paling sering dibeli dari setiap mitra restoran.
* **`penjualanRestoranTertinggi`:** Menampilkan peringkat 3 besar restoran dengan total volume penjualan tertinggi.
* **Analisis Market Basket:** Query khusus menggunakan teknik *Self-Join* untuk menemukan 3 menu makanan yang paling sering dibeli secara bersamaan dengan menu *"Udang Rambutan"*.

---

## Antarmuka Aplikasi (GUI Interface)
Aplikasi menyediakan dua hak akses antarmuka utama yang dibangun menggunakan Java GUI:

### 1. Jendela Admin (Back-Office Management)
* Memberikan akses penuh bagi administrator untuk mengelola database (*Create, Read, Update, Delete* / CRUD) pada seluruh tabel (Data User, Driver, Food, Restaurant, Order, hingga riwayat Payment).
* Dilengkapi dengan tombol navigasi record data (*first, next, prev, last*) dan fitur pencarian dinamis.

### 2. Jendela User (Customer Portal)
* **Login & Otentikasi:** Masuk ke sistem menggunakan username dan password terdaftar.
* **Menu Pemesanan:** Memilih makanan berdasarkan restoran mitra dan mengatur kuantitas pesanan ke dalam keranjang belanja.
* **Pelacakan Pengiriman:** Memantau status pengiriman barang berdasarkan nomor `Order_ID`.
* **Checkout & Nota:** Memilih metode pembayaran (*Cash/QRIS*) dan mencetak nota pembelian akhir secara otomatis.
