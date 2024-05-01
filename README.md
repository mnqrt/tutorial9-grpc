1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

- Pada Unary RPC: Client hanya mengirimkan data ke server sekali dan menerima responsnya. Hal ini dapat digunakan pada situasi dimana client hanya perlu mengirim data ke server dan menunggu respons, seperti autentikasi/autorisasi dan pengiriman form.
- Pada Server Streaming RPC: Server mengirimkan data dalam jumlah besar melalui satu stream, yang bisa diterima oleh client.  Hal ini dapat digunakan pada situasi server perlu mengirimkan data yang besar atau berkelanjutan kepada client, seperti harga saham atau berita.
- Bi-Directional Streaming RPC: Baik client maupun server terlibat dalam pengiriman data melalui stream yang sama.  Hal ini dapat digunakan pada situasi di mana client dan server perlu saling berkomunikasi secara real-time dan interaktif, seperti kolaborasi editing, permainan real-time, atau chatbot.


2.  What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

- gRPC membutuhkan validasi autorisasi/autentikasi pada setiap potongan data yang dikirim, berbeda dengan REST yang memerlukan validasi hanya sekali per permintaan. Setiap potongan data dalam gRPC juga perlu dienkripsi secara terpisah, meningkatkan proses keamanan. Jadi, gRPC menuntut proses autorisasi/autentikasi/enkripsi yang berulang dalam satu permintaan, berbeda dengan REST yang hanya memerlukan validasi sekali.

3.  What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

- Dalam pengembangan aplikasi chat menggunakan Rust gRPC, beberapa masalah yang mungkin timbul adalah sinkronisasi pesan antara pengirim dan penerima, potensi deadlock jika kedua ujung saluran saling menunggu, risiko overflow buffer jika pesan tidak segera dikonsumsi, serta perlunya mekanisme pemulihan kesalahan dan perhatian khusus terhadap konkurensi dan keamanan seperti enkripsi pesan dan otentikasi pengguna.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
- Menggunakan tokio_stream::wrappers::ReceiverStream untuk streaming respons dalam layanan Rust gRPC menawarkan fleksibilitas dengan dukungan untuk berbagai jenis receiver, seperti channel atau future. Ini juga memudahkan integrasi dengan komponen lain dalam ekosistem Tokio. Namun, pendekatan ini juga membawa kompleksitas tambahan dan potensi overhead kecil, terutama bagi pengembang yang belum terbiasa dengan pemrograman asinkron dan konsep Tokio.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
- Dengan struktur yang sesuai, Rust gRPC memfasilitasi peningkatan keterjangkauan dan modularitas. Ini karena menggunakan protokol .proto dan diintegrasikan dengan sebuah interface memungkinkan implementasi class di Rust dapat dibuat, memudahkan dalam penambahan fitur dan perubahan kode secara keseluruhan.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
- Untuk menangani logika pembayaran yang lebih kompleks dalam implementasi MyPaymentService, langkah-langkah tambahan yang mungkin diperlukan termasuk validasi dan penanganan kesalahan yang cermat, otentikasi dan otorisasi pengguna, integrasi dengan gateway pembayaran eksternal, manajemen status transaksi, dan lainnya. Dengan langkah-langkah ini, logika pemrosesan pembayaran dapat ditingkatkan untuk menangani skenario yang lebih kompleks dengan efektif.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
- Dengan adopsi gRPC, tidak perlu lagi khawatir tentang bagaimana mengakses modul melalui metode HTTP. gRPC secara otomatis mengelola pemanggilan method yang diinginkan melalui definisi yang telah disepakati dalam file proto. Hal ini memungkinkan client untuk dengan mudah memanggil fungsi dari server, menyederhanakan konektivitas dan operasi antar berbagai teknologi, platform, dan sistem yang terdistribusi.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
- HTTP/2 memiliki kelebihan dalam mengizinkan banyak permintaan dan tanggapan dilakukan dalam satu koneksi, namun bisa menimbulkan biaya overhead yang lebih tinggi untuk kinerja dan penggunaan memori dibandingkan HTTP/1.1, terutama untuk pengiriman data yang kecil. Walaupun demikian, HTTP/2 tetap lebih efisien untuk pengiriman data yang besar. Dalam konteks REST API, HTTP/2 lebih sesuai karena mendukung fitur-fitur seperti multiplexing, kompresi header, server push, dan lainnya.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
- Model permintaan-tanggapan dari REST API bersifat satu arah, sementara gRPC memungkinkan streaming bidireksional yang real-time antara klien dan server. Dalam responsivitas dan komunikasi real-time, gRPC dapat menyediakan kinerja yang lebih baik karena kemampuannya untuk mengirim dan menerima data secara langsung, sementara REST API perlu menunggu permintaan dari klien sebelum memberikan tanggapan.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
- gRPC menggunakan Protocol Buffers memberikan keunggulan dalam efisiensi, keandalan, dan keamanan dalam pertukaran data antar layanan, berbeda dengan JSON dalam REST API yang lebih fleksibel tetapi kurang efisien dan kurang ketat dalam struktur datanya. Jadi, sementara gRPC bisa sedikit lebih rumit untuk dipelajari, ia menawarkan kinerja yang lebih baik dan memastikan konsistensi dalam pertukaran data.