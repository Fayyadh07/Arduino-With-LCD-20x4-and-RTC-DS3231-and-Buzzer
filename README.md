# Arduino Digital Clock with LCD 20x4, RTC DS3231, and Buzzer

Proyek ini adalah jam digital berbasis Arduino yang menampilkan tanggal, waktu, dan nama hari pada layar LCD 20x4. Waktu diambil dari modul RTC DS3231 dan dikemas dengan buzzer untuk memberikan suara pendek setiap siklus loop.

## Fitur

- Tampilan tanggal lengkap (hari, tanggal, bulan, tahun)
- Tampilan waktu realtime (jam, menit, detik)
- Nama hari dalam bahasa Indonesia
- Penggunaan LCD 20x4 untuk tampilan informasi
- RTC DS3231 untuk menjaga waktu tetap akurat
- Buzzer menghasilkan bunyi pendek setiap pembaruan waktu

## Komponen

- Arduino Uno (atau kompatibel)
- LCD 20x4 dengan antarmuka paralel
- Modul RTC DS3231
- Buzzer piezo
- Kabel jumper
- Breadboard (opsional)

## Pin Koneksi

### LCD 20x4

- `RS` -> pin `7`
- `EN` -> pin `6`
- `D4` -> pin `5`
- `D5` -> pin `4`
- `D6` -> pin `3`
- `D7` -> pin `2`
- VCC, GND, dan potensiometer kontras disambungkan sesuai kebutuhan

### RTC DS3231

- `SDA` -> `A4` (pada Arduino Uno)
- `SCL` -> `A5` (pada Arduino Uno)
- `VCC` -> `5V`
- `GND` -> `GND`

### Buzzer

- Satu terminal buzzer -> pin `8`
- Terminal lainnya -> `GND`

## Instalasi

1. Buka proyek ini di PlatformIO / VS Code.
2. Pastikan `platformio.ini` menggunakan environment Arduino Uno:

```ini
[env:uno]
platform = atmelavr
board = uno
framework = arduino
lib_deps =
    fmalpartida/LiquidCrystal@^1.5.0
    adafruit/RTClib@^2.1.4
```

3. Sambungkan perangkat keras sesuai skema koneksi.
4. Upload program ke board Arduino.

## Struktur Proyek

- `src/main.cpp` — kode utama Arduino untuk menampilkan waktu dan tanggal di LCD serta menggerakkan buzzer.
- `platformio.ini` — konfigurasi proyek PlatformIO dan daftar library.

## Penjelasan Kode

- `LiquidCrystal lcd(7, 6, 5, 4, 3, 2);` — inisialisasi koneksi LCD.
- `RTC_DS3231 rtc;` — inisialisasi modul RTC.
- Program memeriksa apakah RTC kehilangan daya; jika ya, waktu diatur ke waktu kompilasi.
- `printAngka()` digunakan untuk menampilkan angka dua digit.
- Loop utama mengambil waktu dari RTC dan menampilkan hari, tanggal, bulan, tahun, serta waktu pada LCD.
- `tone(8, 1000, 50);` menghasilkan bunyi pendek setiap putaran loop.

## Catatan

- Pastikan baterai CR2032 terpasang pada modul DS3231 agar waktu tetap berjalan saat Arduino dimatikan.
- Jika waktu tidak tepat saat pertama kali dijalankan, kode ini akan mengatur RTC ke waktu kompilasi.
- Pin `10` diatur sebagai `OUTPUT` dalam kode, tetapi tidak digunakan di loop; dapat dipakai untuk fitur tambahan.

## Lisensi

Silakan gunakan dan modifikasi proyek ini sesuai kebutuhan.
