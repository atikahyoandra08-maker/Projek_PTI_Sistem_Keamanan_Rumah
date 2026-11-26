# Projek_PTI_Sistem_Keamanan_Rumah
Sistem keamanan rumah berbasis IoT 
1. Rangkaian Perangkat Keras (Breadboard & Kabel Jumper)
Pasang ESP32 dan sensor PIR (umumnya tipe HC-SR501) di breadboard menggunakan kabel jumper. Pastikan semua komponen berbagi jalur ground yang sama.
 * VCC (PIR) → VIN / 5V (ESP32): Memberi daya ke modul sensor PIR (cek label pin di modul PIR Anda; kebanyakan HC-SR501 memakai input 5V).
 * OUT (PIR) → GPIO 27 (ESP32): Mengirim sinyal digital (HIGH saat ada gerakan, LOW saat diam) ke mikrokontroler.
 * GND (PIR) → GND (ESP32): Menyamakan referensi tegangan ground.

Cara verifikasi rangkaian: Periksa setiap ujung kabel jumper menancap kuat di lubang breadboard dan pin header, serta pastikan tidak ada pin yang saling bersentuhan atau korslet.
2. Konfigurasi Aplikasi & Dashboard Blynk
 * Buat akun di Blynk lalu buka Template → klik New Template.
 * Isi nama template (misalnya Keamanan Rumah), pilih hardware ESP32, dan koneksi WiFi, lalu simpan.
 * Masuk ke menu Datastreams dan buat Virtual Pin:
   * V0 (Status Gerakan / Motion Status): tipe data String atau Integer (0 = Aman, 1 = Ada Gerakan).
   * (Opsional) V1 (Mode Keamanan): tipe data Integer (0–1) jika ingin mengaktifkan/menonaktifkan alarm dari aplikasi.
 * Buka menu Events → buat event baru (misalnya kode motion_alert), lalu aktifkan notifikasi di pengaturan event/aplikasi Blynk agar ponsel menerima peringatan saat terpicu.
 * Tambahkan widget Label atau LED pada dashboard dan hubungkan ke datastream V0, lalu buat Device dari template tersebut untuk menyalin BLYNK_TEMPLATE_ID, BLYNK_TEMPLATE_NAME, dan BLYNK_AUTH_TOKEN.
Cara verifikasi Blynk: Pastikan template sudah tersimpan dan perangkat baru muncul di daftar Devices dengan status Offline (belum terhubung ke ESP32).
3. Persiapan & Pemrograman di Arduino IDE
 * Buka Arduino IDE, lalu pasang dukungan board esp32 melalui Board Manager jika belum terpasang.
 * Buka Library Manager, cari dan instal library Blynk.

 * Pilih board ESP32 Dev Module dan Port (COM) yang sesuai, lalu klik Upload.
Cara verifikasi upload: Proses upload selesai tanpa pesan error merah di konsol bawah Arduino IDE, dan saat Serial Monitor dibuka dengan baud rate 115200, muncul status koneksi Wi-Fi dan Blynk.
4. Kalibrasi & Pengujian Sistem
 * Diamkan sensor PIR selama sekitar 30–60 detik setelah menyala agar kondisi inframerah sekitar stabil.
 * Jika sensor terlalu sensitif atau terlalu lambat merespons, putar perlahan potensiometer Sensitivity dan Time Delay pada modul PIR.
 * Gerakkan tangan di depan lensa PIR dan perhatikan perubahan status di Serial Monitor serta widget di aplikasi Blynk.
Cara verifikasi pengujian: Status di aplikasi Blynk berubah menjadi peringatan gerakan dan notifikasi muncul di ponsel saat ada pergerakan di depan sensor.
Referensi video panduan langkah demi langkah: ESP32 + PIR Motion Sensor IoT Alert System | Full Setup with Blynk!.
