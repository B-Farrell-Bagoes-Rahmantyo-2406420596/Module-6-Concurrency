# Reflection Notes
## Commit 1 Reflection Notes
Function handle_connection menyimpan data TcpStream yang berisi sebuah permintaan HTTP. Data tersebut diiterate baris per baris dan disimpan dalam bentuk array of string (Vec<String>). Kemudian di print di terminal.  
## Commit 2 Reflection Notes
![Commit 2 screen capture](/assets/pictures/Commit2.png) 
Function tersebut sekarang mengambalikan response HTTP yang berisi status_line (HTTP/1.1 200 OK), Content-Length header dan isi konten sebagai response body (hello.html). Renpons tersebut dikirim balik ke client menggunakan stream.write_all .  
## Commit 3 Reflection Notes
![Commit 3 screen capture](/assets/pictures/Commit3.png)
Agar server tahu untuk memberikan response yang mana yang sesuai. Kita mengecek line pertama request HTTP dari client di buf_reader itu berupa root-nya atau dalam kata lain requestnya berasal dari (127.0.0.1:7878). Jika tidak diarahkan ke laman 404. Di sini juga kita merefactor karena jika tidak kita boros dan method kita dapat menjadi panjang jika kita menulis assignment dan response format yang sama di setiap blok if-elsenya. Oleh karena itu kita merefaktor agar if else-nya hanya menentukan status_line dan filename saja.
## Commit 4 Reflection Notes
Karena server berjalan secara single-thread. Server harus memproses 127.0.0.1:7878/sleep hingga selesai sebelum memproses request yang lain sehingga di sisi client lain nampak server lambat dalam mengirim respons.
## Commit 5 Reflection Notes
Intinya, threadpool merupakan kumpulan thread-thread yang siap mejalankan tugas yang datang secara paralel. Misal request 127.0.0.1:7878/sleep muncul lalu dihandle oleh worker 1 (misal ada 3 worker/thread). Lalu jika ada request 127.0.0.1:7878 lain dan worker 1 belum selesai maka akan dihandle worker 2. Cara kerja threadpool, kita menginisasi sebuah threadpool dengan n-positif worker(thread). Setiap worker menerima referensi ke receiver untuk dapat menerima tugas yang diberikan sender. Masing-masing worker memiliki mutex yang dapat mengatur worker mana yang dapat menerima job diberikan. Setiap worker menggunakan loop untuk menunggu tugas yang dikirim. Penggunaan loop dikarenakan agar setelah tugas selesai, worker masih tetap ada.