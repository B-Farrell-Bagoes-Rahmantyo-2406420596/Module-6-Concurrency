# Reflection Notes
## Commit 1 Reflection Notes
Function handle_connection menyimpan data TcpStream yang berisi sebuah permintaan HTTP. Data tersebut diiterate baris per baris dan disimpan dalam bentuk array of string (Vec<String>). Kemudian di print di terminal.  
## Commit 2 Reflection Notes
![Commit 2 screen capture](/assets/pictures/Commit2.png) 
Function tersebut sekarang mengambalikan response HTTP yang berisi status_line (HTTP/1.1 200 OK), Content-Length header dan isi konten sebagai response body (hello.html). Renpons tersebut dikirim balik ke clinet menggunakan stream.write_all .