# Tutorial 10 - Asynchronous Programming - Timer

##### Winoto Hasyim - 2206025243 - Pemrograman Lanjut B

## Experiment 1.2: Understanding how it works.

![Experiment 1.2: Understanding how it works.](https://i.imgur.com/3ODsR2j.png)

Walaupun task untuk mem-print "howdy!" dan "done!" sudah di-spawn pada awal-awal function main, Message "hey hey" di print terlebih dahulu karena message tersebut dijalankan secara sinkronus dan berada sebelum executor menjalankan tasks yang sudah di spawn sebelumnya

## Experiment 1.3: Multiple Spawn and removing drop

- Tidak drop spawner
![Experiment 1.3: Multiple Spawn and removing drop](https://i.imgur.com/LJChrsM.png)

- Drop spawner
![Experiment 1.3: Multiple Spawn and removing drop](https://i.imgur.com/k2eQa1H.png)

Pertama-tama, message "hey hey" akan di-print terlebih dahulu karena berada sebelum executor menjalankan spawned tasks. Kemudian executor melakukan run terhadap task yang sudah di-spawn. Setiap task yang dijalankan oleh executor akan terurut sesuai urutan task yang di-spawn, sampai executor menemukan point .await. Di point tersebut, akan terdapat suatu delay sehingga executor bisa menjalankan task lain sambil menunggu delay tersebut selesai. Setelah itu, karena semua task berjalan secara concurrent, delay pada setiap task bisa selesai dalam waktu yang berbeda, tergantung dengan system loadnya. Oleh karena itu, message "done" bisa ditampilkan secara tidak berurut

Selain itu, ketika spawner tidak di-drop maka kita hanya bisa terminate proces secara manual karena jika spawner tidak di-drop, executor akan terus menunggu task yang akan dijalankan, yang padahal task yang ditunggu nya itu sebenarnya tidak akan ada karena semua task sudah dijalankan. Akibatnya, peristiwa seperti infinite loop ini terjadi