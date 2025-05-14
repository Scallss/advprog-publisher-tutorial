Pascal Hafidz Fajri

230622746

## Berapa banyak data yang dikirim publisher ke message broker dalam satu eksekusi?

Dalam satu eksekusi program akan mengirimkan 5 pesan/event ke message broker. Setiap pesan berisi sebuah struct UserCreatedEventMessage yang memiliki 2 field:
- `user_id`: String dengan panjang 1 karakter (nilai "1" sampai "5")
- `user_name`: String dengan pola "NPM-Nama" 

Jika ingin dihitung ukuran data per pesan yang dikirim:
- `user_id`: 1 byte 
- `user_name`: 9 byte untuk NPM, 1 byte untuk `-`, dan 4 byte untuk Nama

Total ukuran data yang dikirim dalam sekali jalan publisher: 
5 pesan x 15 byte = 75 byte 

## URL "amqp://guest:guest@localhost:5672" yang sama antara publisher dan subscriber

URL yang sama ini berarti, kedua program terhubung ke message broker (RabbitMQ) yang berjalan di mesin yang sama (`localhost`) dan dengan port yang sama (`5672`). Selain itu, kredensial untuk mengakses RabbitMQ juga sama, yaitu `guest` dan `guest`.

Disini, Publsiher akan mengirim pesan ke queue `user_created`, yang mana akan didengar oleh Subscriber. Agar komunikasi itu bisa terjadi, publisher dan subscriber harus terhubung ke message broker yang sama.

## Screenshot of running RabbitMQ
![Running RabbitMQ](assets/image.png)

## Sending and processing event
![Publisher Console](assets/publisher_console.png)
![Subscriber Console](assets/subscriber_console.png)

Gambar-gambar di atas adalah tampak console publisher dan subscriber yang mana terjadi komunikasi menggunakan RabbitMQ antar satu sama lain. Secara lebih detail, publisher akan mengirim data (berjumlah 5) ke message broker. Kemudian, program subscriber akan menerima dan mengonsumsi data-data tersebut (dengan menampilkannnya ke konsol).

## Monitoring Chart Based on Publisher
![Monitoring Chart](assets/monitoring_chart.png)

Setiap kali program publisher diaktifkan, terlihat adanya peningkatan signifikan pada message rates dalam grafik. Nilai ini merepresentasikan volume pesan yang berhasil dikirimkan ke message broker dalam rentang waktu spesifik. Pola lonjakan (spike) yang konsisten ini memperlihatkan korelasi langsung antara eksekusi publisher dan aktivitas pengiriman data. Dengan demikian, grafik tersebut berfungsi sebagai alat visual untuk melacak kinerja dan lalu lintas pesan dalam infrastruktur message queue.
