# PROJECT 3 : PRINSIP OOP

## TASK 1 : BASIC OOP
Membuat Class MarketingDataETL yang memiliki tiga metode di dalamnya yaitu extract(), transform(), dan store(). Dimulai dengan import library pandas dan mendefinisikan class MarketingDataETL, dengan penjelasan sebagai berikut:

*) "import pandas as pd": Dimulai dengan import library pandas. Pandas adalah library yang digunakan untuk melakukan analisis dan manipulasi data dalam Python.

*) "class MarketingDataETL()": Mendefinisikan sebuah kelas dengan nama MarketingDataETL. Kelas ini digunakan untuk melakukan operasi-extract, transform, dan store. Pada saat ini, kelas tersebut tidak memiliki konstruktor khusus (__init__()), yang berarti ketika membuat objek dari kelas ini, tidak ada proses inisialisasi yang dilakukan secara otomatis.

Selanjutnya, dilanjutkan pada metode extract, transform, dan store.

### A) METODE EXTRACT()

*) "def extract(self)": Merupakan metode extract() dari kelas MarketingDataETL. Metode ini akan mengekstrak data dari sumbernya. Di dalam metode ini, terdapat beberapa perintah yaitu: 

=> "self.data = pd.read_csv("/content/marketing_data.csv", sep=';'): Perintah untuk membaca data dari file CSV yang diberikan (marketing_data.csv). Data dibaca dengan menggunakan pd.read_csv() dan dimasukkan ke dalam atribut data dari objek MarketingDataETL. Parameter sep=';' menunjukkan bahwa pemisah dalam file CSV adalah tanda titik koma (;).

=> "print("Data sebelum transform:")": pesan yang dicetak ke layar untuk memberi tahu pengguna bahwa data sebelumnya belum ditransformasi.

=> "print(self.data)": mencetak data yang telah diekstrak sebelumnya ke layar.

=> "return self.data": Metode mengembalikan data yang telah diekstrak.

Dengan demikian, kode tersebut menunjukkan sebuah kelas MarketingDataETL yang memiliki metode extract() untuk mengekstrak data dari file CSV yang diberikan menggunakan pustaka pandas.

### B) METODE TRANSFORM()

*) "def transform(self)": Ini adalah metode transform() dari kelas MarketingDataETL. Metode ini bertanggung jawab untuk mentransformasi data yang diekstrak sebelumnya. Di dalam metode ini:

=> "if 'purchase_date' in self.data.columns": Ini adalah struktur pengkondisian yang memeriksa apakah kolom 'purchase_date' ada dalam data yang diekstrak (self.data). Jika kolom ini ada, maka transformasi akan dilakukan. Jika tidak, maka transformasi tidak akan dilakukan.

=> "self.data['purchase_date'] = pd.to_datetime(self.data['purchase_date'], errors='coerce')": Baris ini menggunakan fungsi pd.to_datetime() dari pustaka pandas untuk mengubah kolom 'purchase_date' menjadi objek datetime. Ini akan mengonversi data tanggal dalam kolom 'purchase_date' menjadi format yang sesuai untuk kemudahan manipulasi tanggal. Argumen errors='coerce' akan membuat pandas mengabaikan entri yang tidak dapat dikonversi menjadi tanggal, dan menggantinya dengan nilai NaT (Not a Time).

=> "self.data = self.data.dropna(subset=['purchase_date'])": Baris ini menghapus baris yang memiliki nilai NaT dalam kolom 'purchase_date'. Ini dilakukan dengan menggunakan metode dropna() dari DataFrame pandas dan memberikan argumen subset=['purchase_date'], yang mengindikasikan bahwa hanya kolom 'purchase_date' yang harus diperiksa untuk nilai yang hilang.

=> "print("Data setelah transform:")": Pesan yang dicetak ke layar untuk memberi tahu pengguna bahwa data setelah transformasi.

=> "print(self.data)": Mencetak data yang telah ditransformasi ke layar.

=> "return self.data": Metode mengembalikan data yang telah ditransformasi.

Dengan demikian, kode tersebut menunjukkan sebuah metode transform() yang melakukan beberapa transformasi pada data, seperti mengubah kolom 'purchase_date' menjadi tipe data datetime dan menghapus baris yang memiliki nilai yang hilang di kolom tersebut.

### C) METODE STORE()

*) "def store(self)": merupakan metode store() dari kelas MarketingDataETL. Metode ini bertanggung jawab untuk menyimpan data yang telah diolah ke dalam file CSV. Di dalam metode ini:

=> "if hasattr(self, 'data')": merupakan struktur pengkondisian yang memeriksa apakah objek self memiliki atribut data. Fungsi hasattr() digunakan untuk mengecek apakah objek memiliki atribut dengan nama tertentu.

=> "self.data.to_csv('marketing_data_processed.csv', index=False)": Jika objek memiliki atribut data, maka baris ini akan menggunakan metode to_csv() dari DataFrame pandas (self.data) untuk menyimpan data ke dalam file CSV dengan nama 'marketing_data_processed.csv'. Argumen index=False digunakan untuk mengabaikan penambahan indeks saat menyimpan data ke dalam file CSV.

=> "print("Data stored successfully as CSV.")": Jika data berhasil disimpan, pesan ini akan dicetak ke layar.

=> "else: print("Tidak ada data untuk disimpan.")": Jika objek self tidak memiliki atribut data, maka pesan ini akan dicetak ke layar untuk memberi tahu pengguna bahwa tidak ada data yang tersedia untuk disimpan.

Dengan demikian, metode store() ini berguna untuk menyimpan data yang telah diproses ke dalam file CSV jika data tersedia, dan memberikan pesan kesalahan jika tidak ada data yang tersedia.

Setelah menjalankan ketiga perintah tersebut, selanjutnya akan mencetak data yang sebelum ditransfrom dan sesudah ditransform.

## TASK 2 : INHERITANCE & POLYMORPHISM

### 1) Gunakan inheritance untuk membuat class TargetedMarketingETL yang mewarisi dari MarkertingDataETL

*) "import numpy as np": Dimulai dengan import library numpy.

*) "class TargetedMarketingETL(MarketingDataETL)": Mendefinisikan sebuah kelas TargetedMarketingETL yang merupakan turunan dari kelas MarketingDataETL. Artinya, kelas TargetedMarketingETL akan mewarisi semua metode dan atribut dari kelas MarketingDataETL, dan juga memungkinkan untuk mendefinisikan metode tambahan atau mengubah perilaku metode yang diwarisi.

*) "def __init__(self, file_path)": Metode konstruktor kelas TargetedMarketingETL. Metode ini akan dipanggil ketika sebuah objek dari kelas TargetedMarketingETL dibuat. Metode konstruktor ini menerima satu parameter yaitu file_path, yang digunakan untuk menyimpan jalur file yang akan diproses.

*) "super().__init__()": Baris ini memanggil metode konstruktor dari kelas induk (MarketingDataETL) menggunakan fungsi super(). Dengan demikian, ketika sebuah objek TargetedMarketingETL dibuat, metode konstruktor dari kelas induk juga akan dijalankan untuk melakukan inisialisasi.

### 2) Menambahkan metode segment_customers() yang mengelompokkan pelanggan berdasarkan kriteria tertentu (misalnya pengeluaran total atau kategori produk yang dibeli).

*) "def segment_customers(self)": merupakan metode segment_customers() dari kelas TargetedMarketingETL. Metode ini bertanggung jawab untuk mengelompokkan pelanggan ke dalam segmen berdasarkan jumlah pengeluaran mereka. Di dalam metode ini:

=> "if self.data is not None": struktur pengkondisian yang memeriksa apakah atribut data dari objek self tidak bernilai None. Jika ada data yang tersedia, maka segmen pelanggan akan dihitung. Jika tidak, pesan kesalahan akan dicetak.

=> "conditions = [...]": Daftar yang berisi kondisi-kondisi untuk mengelompokkan pelanggan berdasarkan jumlah pengeluaran (amount_spent). Setiap kondisi merupakan ekspresi Boolean yang menentukan rentang jumlah pengeluaran untuk setiap segmen.

=> "choices = [...]": daftar yang berisi label untuk setiap segmen pengeluaran yang mungkin.

=> "self.data['spending_segment'] = pd.Series(np.select(conditions, choices), index=self.data.index)": baris kode yang menghitung segmen pengeluaran pelanggan berdasarkan kondisi-kondisi yang ditentukan sebelumnya. Fungsi np.select() digunakan untuk memilih label segmen berdasarkan kondisi-kondisi yang terpenuhi, dan hasilnya disimpan dalam kolom baru 'spending_segment' dari DataFrame self.data.

=> "print("Segmentasi berdasarkan pengeluaran customer:")": pesan yang dicetak ke layar untuk memberi tahu pengguna bahwa segmen pengeluaran pelanggan telah dihitung.

=> "print(self.data)": mencetak DataFrame self.data, yang sekarang sudah termasuk kolom 'spending_segment', ke layar.

=> "else: print("No data to segment. Please extract data first.")": Jika tidak ada data yang tersedia (yaitu, self.data adalah None), maka pesan kesalahan akan dicetak ke layar.

Dengan demikian, metode segment_customers() ini memungkinkan untuk menghitung segmen pengeluaran pelanggan berdasarkan jumlah pengeluaran yang telah dilakukan.

### 3) Demonstrasi polymorphism dengan meng-override metode transform() dalam TargetedMarketingETL untuk menambahkan logika segmentasi pelanggan ke dalam proses transformasi.

*) "def transform(self)": Metode ini bertujuan untuk melakukan transformasi pada data dengan memanggil metode transform() dari kelas induk (kelas yang diwarisi), lalu melanjutkan dengan menghitung segmen pelanggan menggunakan metode segment_customers().

*) "super().transform()": Ini adalah cara untuk memanggil metode transform() dari kelas induk (kelas yang diwarisi). Dengan memanggil super(), Anda mendapatkan akses langsung ke metode transform() dari kelas induk MarketingDataETL dan menjalankannya.

*) "self.segment_customers()": Setelah melakukan transformasi yang umum, metode ini memanggil metode segment_customers() yang khusus untuk TargetedMarketingETL, yang bertujuan untuk menambahkan kolom segmen pengeluaran pelanggan ke dalam data.

*) "def store_segmented_data(self, output_file_path)": Metode ini bertujuan untuk menyimpan data yang telah di-segmentasi (mungkin dengan segmen pelanggan yang ditambahkan) ke dalam file Excel.

*) "if self.data is not None": struktur pengkondisian yang memeriksa apakah ada data yang tersedia untuk disimpan. Jika self.data bukan None, maka data akan disimpan.

*) "try:" : Ini memulai blok try-except, yang berguna untuk menangani kesalahan yang mungkin terjadi saat proses menyimpan data.

*) "self.data.to_excel(output_file_path, index=False)": Baris ini menyimpan data ke dalam file Excel menggunakan metode to_excel() dari DataFrame pandas (self.data). Argumen index=False mengabaikan penambahan indeks saat menyimpan data.

*) "except Exception as e:": Ini adalah blok penanganan pengecualian. Jika terjadi kesalahan saat menyimpan data, pesan kesalahan akan dicetak ke layar bersama dengan informasi kesalahan.

*) "else: print("No data to store. Please extract and transform data first.")": Jika tidak ada data yang tersedia (yaitu, self.data adalah None), maka pesan ini akan dicetak ke layar.

Dengan demikian, kedua metode ini bekerja bersama untuk melakukan transformasi data dan menyimpannya ke dalam file Excel, dengan memastikan bahwa data telah disegmentasi sebelum disimpan jika diperlukan.
