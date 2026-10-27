# Catatan Skematik Optimasi v1.1

> **Status:** rancangan konseptual untuk review dan pembelajaran. Bukan skematik produksi, sertifikasi keselamatan, atau izin untuk merakit/menyalakan bagian AC/UV-C tanpa supervisi yang kompeten.

## 1. Visual utama

![Skematik controller yang telah dikoreksi dan dioptimasi](schematic-optimized-v1.svg)

- [Buka skematik SVG resolusi penuh](schematic-optimized-v1.svg)
- [Versi diagram low-voltage sebelumnya](schematic-low-voltage-v0.svg)
- [Catatan awal v0.2](schematic-notes-v0.md)

## 2. Koreksi terhadap skematik sumber

| Bagian pada gambar awal | Koreksi / keputusan |
|---|---|
| LM7805 setelah input yang diberi label 5 V | Dihapus pada baseline. Gunakan adaptor 5 V DC teregulasi dan terisolasi. Jika sumber yang tersedia lebih tinggi dari 5 V DC, evaluasi buck converter; jangan memasukkan 5 V ke input 7805 lalu berharap output tetap 5 V. |
| LED indikator terhubung langsung tanpa resistor seri | Tambahkan R1 = 1 kΩ sebagai nilai awal untuk LED indikator 5 V. Sesuaikan setelah jenis LED dan arus target diketahui. |
| Kapasitor catu daya tidak tergambar sebagai rail yang jelas | C1 = 100 nF dan C2 = 47–100 µF digambar di antara +5V_CTL dan GND_CTL; tempatkan dekat rangkaian kontrol. |
| MCU digambar sebagai Arduino Nano | Dikembalikan ke rencana: pilih **satu** antara STC8H1K08 atau CH32V003. Nomor pin tetap TBD sampai package/board final dipilih. |
| LCD I²C konektor XH2.54 | Gunakan JST-XH-4P untuk VCC, GND, SDA, SCL. Pitch keluarga XH resmi adalah 2,5 mm; jangan mencampurnya dengan JST-PH 2,0 mm. |
| IRF540N sebagai MOSFET gerbang 5 V | Tidak dipilih sebagai default. Pilih MOSFET logic-level dengan RDS(on) yang ditentukan pada VGS 4,5–5 V. FQP30N06L adalah kandidat yang bisa dikaji, bukan komponen yang otomatis final. |
| Driver relay / diode coil belum jelas | Untuk relay polos, gunakan MOSFET low-side, resistor gate, gate-to-source pull-down, dan diode flyback langsung melintasi koil. Jika membeli modul relay yang sudah mempunyai driver, komponen driver diskrit biasanya tidak perlu digandakan. |
| Satu limit switch sekaligus dianggap sebagai semua fungsi keselamatan | Pisahkan SW1 (status pintu ke MCU), SW2 NC (memutus suplai koil relay pada sisi low-voltage), dan SW3 (interlock pintu ber-rating mains yang memutus energi lampu secara independen). |
| Heater/fan dan solenoid ikut dicantumkan | Dikeluarkan dari baseline BOM. Beban tersebut adalah ekspansi terpisah yang perlu driver, proteksi, sensor, dan evaluasi daya masing-masing. Sensor suhu/kelembapan tetap opsional sampai model dipilih. |

## 3. Baseline sistem

Rancangan baseline memiliki fungsi berikut:

1. Dua lampu germicidal UV-C yang spesifikasi dan ballast/driver-nya harus cocok.
2. Kontrol low-voltage 5 V menggunakan satu MCU kandidat.
3. LCD 16×2 dengan backpack I²C.
4. Status pintu yang dilaporkan ke MCU.
5. Pemutus low-voltage pada suplai koil relay jika pintu dibuka.
6. Pemutus mains-rated independen pada subsistem lampu untuk menangani kondisi relay macet/welded contacts.
7. Satu kanal relay untuk menyalakan dua lampu bersamaan hanya jika rating kontak, ballast, arus masuk, dan desain keselamatan mengizinkan.

## 4. Pinout dan konektor

### J1 — JST-XH-2, input kontrol

| Pin | Net |
|---|---|
| 1 | +5V_CTL |
| 2 | GND_CTL |

### J2 — JST-XH-4, LCD 16×2 I²C

| Pin | Net |
|---|---|
| 1 | VCC / +5V_CTL |
| 2 | GND_CTL |
| 3 | SDA |
| 4 | SCL |

Ini **pinout yang dipilih untuk harness kita**, bukan jaminan semua backpack LCD mempunyai urutan pin sama. Verifikasi tulisan VCC/GND/SDA/SCL di modul sebelum membuat kabel.

### J3 — JST-XH-2, status pintu SW1

| Pin | Net |
|---|---|
| 1 | DOOR_SENSE |
| 2 | GND_CTL |

Gunakan kontak NC ke GND dan pull-up 10 kΩ ke +5V_CTL: tertutup = LOW; terbuka atau kabel terputus = HIGH/fault. Ini adalah input pemantauan, bukan satu-satunya interlock keselamatan.

### J4 — konektor driver/relay, jika modul terpisah

Jika memakai rangkaian relay polos + MOSFET pada PCB yang sama, J4 tidak diperlukan. Jika modul terpisah digunakan, definisikan pinout sesuai modul nyata dan pastikan tidak mengandalkan urutan generik J4 sebelum inspeksi.

### J5 — sensor suhu/kelembapan opsional

Jangan tetapkan pinout final sebelum memilih jenis sensor. Sensor 3-kawat yang berbeda bisa memakai urutan VCC/DATA/GND yang berbeda.

## 5. Rangkaian penggerak relay polos

Untuk opsi diskrit pada skematik:

- Koil relay harus benar-benar **koil DC 5 V** bila disuplai dari +5V_CTL. Jangan mencampur label “5V/12V” atau membeli varian yang salah.
- SW2 NC dipasang seri dengan suplai koil agar koil tidak bisa aktif ketika pintu membuka. Ini perlindungan tambahan pada sisi kontrol, bukan pengganti SW3.
- Q1 adalah MOSFET N-channel logic-level yang dipakai sebagai low-side switch koil: drain menuju koil−, source menuju GND_CTL, gate menerima UV_RELAY_CMD.
- Rg = 100 Ω adalah nilai awal untuk membatasi lonjakan arus gate saat switching.
- Rpd = 100 kΩ dari gate ke source/GND menjaga Q1 cenderung OFF ketika MCU reset atau pin mengambang.
- D1 = 1N4007 adalah kandidat diode flyback untuk koil relay DC yang sesuai; katoda di koil+ / +5V_CTL, anoda di koil− / Q1 drain.
- Periksa arus koil dari datasheet relay, kemampuan GPIO, pinout MOSFET paket TO-220, dan karakteristik RDS(on) pada tegangan gate yang digunakan.

**Jika memakai modul relay siap pakai**, banyak modul telah memiliki transistor driver dan diode flyback. Dalam kasus itu, jangan memasang Q1/Rg/Rpd/D1 eksternal otomatis. Periksa skematik modul, input aktif-HIGH/LOW, kondisi saat MCU reset, dan kemampuan isolasinya.

## 6. Rangkaian AC dan UV-C

Skematik hanya menunjukkan blok fungsional, bukan sambungan kabel PLN rinci:

`AC supply → proteksi yang sesuai → SW3 mains-rated door interlock → kontak relay K1 → ballast/driver yang cocok → dua lampu UV-C`

Urutan akhir dan perangkat proteksi harus dirancang dan diverifikasi oleh pihak kompeten berdasarkan spesifikasi lampu, ballast, tegangan jaringan, arus operasi, arus masuk, dan enclosure. Jangan menganggap tulisan “10 A / 250 VAC” pada relay generik cukup untuk menyetujui aplikasi ballast UV-C.

**SW3 penting karena kontak relay bisa gagal dalam posisi tertutup.** Memutus suplai koil relay saja tidak memadamkan lampu bila kontaknya sudah terlas. Interlock mains-rated harus benar-benar disesuaikan untuk memutus energi lampu saat pintu dibuka, dan tidak bergantung pada firmware MCU.

Jangan merakit atau menguji bagian AC terbuka. Gunakan enclosure opaque untuk UV-C dan minta review pembimbing/tenaga kompeten. UV-C dapat merusak mata dan kulit; [CDC/NIOSH](https://www.cdc.gov/niosh/ventilation/germicidal-ultraviolet/index.html) membahas risiko paparan UV germicidal. Proses tidak boleh disebut steril tanpa validasi dosis dan pengujian mikrobiologis yang sesuai.

## 7. Referensi teknis

1. [JST XH official connector series](https://www.jst-mfg.com/product/index.php?lang=2&series=277): pitch 2,5 mm dan spesifikasi seri XH.
2. [STC8H1K08 official documentation](https://www.stcmicro.com/stc/stc8h1k08.html): operating voltage, GPIO, I²C dan ISP.
3. [WCH Open Source CH32V003 repository](https://github.com/openwch/ch32v003): dokumentasi dan contoh kandidat MCU.
4. [FQP30N06L datasheet, onsemi](https://www.onsemi.com/download/data-sheet/pdf/fqp30n06l-d.pdf): periksa RDS(on) berdasarkan VGS sebelum menjadikannya Q1.
5. [CDC/NIOSH: Germicidal Ultraviolet](https://www.cdc.gov/niosh/ventilation/germicidal-ultraviolet/index.html): risiko dan implementasi UV germicidal.

---
*Revision 1.1: diagram dikoreksi secara visual dan fungsional; keputusan final menunggu pemilihan MCU, relay, ballast/lampu, serta review keselamatan.*
