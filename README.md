# Event Subscriber

## a. What is AMQP?
AMQP (Advanced Message Queuing Protocol) adalah protokol komunikasi terbuka untuk message broker seperti RabbitMQ.

## b. guest:guest@localhost:5672
- guest pertama: username default RabbitMQ
- guest kedua: password default RabbitMQ
- localhost:5672: alamat dan port di mana RabbitMQ berjalan lokal

- ![image](https://github.com/user-attachments/assets/79450dc4-6ecd-436e-b6c5-602f39b515e1)
- ![Screenshot (2436)](https://github.com/user-attachments/assets/4c9f9b46-88d5-445f-be3a-d2412ff6a39c)


![image](https://github.com/user-attachments/assets/a946f949-b1f5-4030-a228-dfd0f7586864)
![image](https://github.com/user-attachments/assets/0e0977d1-ab06-46b5-bf98-75d57b6cf136)

![Screenshot (2443)](https://github.com/user-attachments/assets/715fabca-0696-4f92-b4f9-ec27d34d0507)
Pada tahap simulasi slow subscriber, kami menambahkan jeda waktu selama satu detik menggunakan fungsi thread::sleep(Duration::from_secs(1)); di dalam handler pesan. Tujuan dari penambahan jeda ini adalah untuk mensimulasikan kondisi di mana sistem pemroses (subscriber) berjalan lambat, seperti yang sering terjadi pada aplikasi dunia nyata ketika beban tinggi datang dalam waktu singkat. Ketika subscriber diperlambat seperti ini, ia tidak mampu memproses pesan secepat publisher mengirimkan pesan. Akibatnya, pesan-pesan tersebut menumpuk di antrean RabbitMQ dan menyebabkan grafik antrean meningkat tajam.

Dalam hasil percobaan, grafik pada dashboard RabbitMQ menunjukkan bahwa jumlah pesan dalam antrean (queued messages) sempat meningkat hingga mencapai puncaknya sekitar 13 hingga 14 pesan, sebelum akhirnya menurun seiring waktu ketika subscriber mulai memproses pesan satu per satu. Hal ini menunjukkan bahwa sistem berhasil menyimpan pesan di antrean dengan baik walaupun subscriber bekerja lambat. Jumlah pesan yang mengantre pada akhirnya menurun karena subscriber terus memprosesnya secara bertahap.

Simulasi ini memberikan pemahaman penting tentang bagaimana arsitektur event-driven bekerja dalam mengatasi beban tinggi secara responsif. Dengan memisahkan publisher dan subscriber serta menggunakan message broker sebagai perantara, sistem menjadi lebih tahan terhadap lonjakan permintaan. Selain itu, untuk mengurangi penumpukan pesan di antrean, solusi yang dapat diambil adalah dengan menjalankan lebih banyak instance subscriber agar dapat memproses pesan secara paralel dan lebih efisien.
