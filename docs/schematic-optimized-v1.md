# Catatan Skematik Optimasi v1.6

> **Status:** engineering review draft. Diagram ini memperbarui skematik agar sesuai dengan **STC8G1K08A-36I-DFN8** yang dipilih. Diagram belum menjadi desain produksi atau instruksi pengkabelan PLN/ballast.

## 1. Skematik utama

![Skematik STC8G1K08A-36I-DFN8 rev 1.6](schematic-optimized-v1.svg)

- [Buka SVG resolusi penuh](schematic-optimized-v1.svg)
- [BOM Review](studi-harga-komponen.md)
- [Skematik low-voltage dan catatan v0.2](schematic-low-voltage-v0.svg) (arsip versi lama)

## 2. Pinout fisik MCU

Sesuai simbol DFN8 yang digunakan, penomoran pin pada skematik v1.6 adalah:

| Pin | Fungsi MCU | Net/fungsi pada prototipe | Catatan |
|---:|---|---|---|
| 1 | P5.4 | Reserved / ISP-reset | Tidak dipakai untuk relay atau sensor pada baseline. P5.4 dapat dikonfigurasi sebagai reset aktif-low saat ISP. |
| 2 | VCC | +5V_CTL | Catu 5 V teregulasi. Datasheet menyebut rentang operasi 1,9–5,5 V. |
| 3 | P5.5 | RELAY_CMD | Keluaran ke gate Q1 melalui Rg 100 Ω. |
| 4 | GND | GND_CTL | Ground kontrol. |
| 5 | P3.0 / RXD | DOOR_SENSE | Input status pintu via kontak NC dan pull-up 10 kΩ. |
| 6 | P3.1 / TXD | START_STOP | Tombol momentary NO ke ground dan pull-up 10 kΩ. |
| 7 | P3.2 / SCL | I2C_SCL | Clock LCD I²C. |
| 8 | P3.3 / SDA | I2C_SDA | Data LCD I²C. |
| 9 | EPAD / exposed substrate pad pada simbol | Tidak diberi net pada diagram | Manual paket STC menyatakan substrate pad DFN8 tidak terhubung ke GND di dalam IC; pad dapat dihubungkan ke GND atau dibiarkan open pada PCB. Ikuti land pattern, solder-mask dan assembly note yang digunakan. |

**Penting:** pinout ini spesifik untuk STC8G1K08A-36I-DFN8, bukan pinout CH32V003, STC8H1K08, atau Arduino Nano.

Referensi pabrikan:
- [STC8G1K08A official product page](https://www.stcmicro.com/stc/stc8g1k08a.html)
- [STC8G1K08A Series Features / pinout PDF](https://www.stcmicro.com/datasheet/STC8G1K08A_Features.pdf)
- [STC8G Series Manual mirror (DFN8 mechanical note)](https://akizukidenshi.com/goodsaffix/STC8G.pdf)
- [KiCad symbol-library discussion for this package](https://gitlab.com/kicad/libraries/kicad-symbols/-/merge_requests/4489)

Dokumentasi pabrikan menyebut P3.2 mendukung fungsi I²C SCL dan P3.3 mendukung I²C SDA. Karena keluarga STC8G1K08A juga dapat mengalihkan I²C ke P5.4/P5.5, firmware harus memilih pasangan P3.2/P3.3 (I2C_S[1:0]=00) agar P5.5 tetap menjadi RELAY_CMD. P3.0/P3.1 juga memiliki fungsi UART RXD/TXD, dan P5.4 dapat dipilih sebagai reset aktif-low saat ISP. ​

## 3. Net dan konektor

### J1 — JST-XH-2, input suplai kontrol

| Pin | Net |
|---:|---|
| 1 | +5V_IN, dari adaptor 5 V teregulasi |
| 2 | GND_CTL |

F1 ditunjukkan sebagai proteksi opsional. Rating fuse/PTC ditentukan setelah arus aktual dan catu dipastikan. Setelah F1, net suplai disebut +5V_CTL. LM7805 sengaja tidak dipakai ketika sumber sudah 5 V teregulasi.

C1 = 100 nF dan C2 = 10 µF ditunjukkan di rail kontrol. Tambahkan C3 = 100 nF sedekat mungkin antara pin 2 VCC dan pin 4 GND pada U1. Datasheet serta layout final tetap menjadi acuan akhir.

### J2 — JST-XH-4, LCD 16×2 I²C

| Pin | Net |
|---:|---|
| 1 | VCC / +5V_CTL |
| 2 | GND_CTL |
| 3 | I2C_SDA |
| 4 | I2C_SCL |

Ini urutan pin harness kita, bukan jaminan semua backpack memakai urutan sama. Periksa silkscreen VCC/GND/SDA/SCL pada unit yang dibeli. Gunakan pull-up yang sudah terpasang di backpack bila ada; jika tidak ada, tentukan pull-up I²C yang sesuai.

Seri JST-XH menggunakan pitch 2,5 mm. Jangan mencampurkannya dengan JST-PH pitch 2,0 mm.

### J3 — JST-XH-2, status pintu SW1

| Pin | Net |
|---:|---|
| 1 | DOOR_SENSE |
| 2 | GND_CTL |

SW1 memakai kontak NC: pintu tertutup menghubungkan DOOR_SENSE ke GND dan input membaca LOW. Pintu terbuka atau kabel putus membuat input terbaca HIGH/fault. R2 = 10 kΩ pull-up ke +5V_CTL. Ini **hanya pemantauan oleh MCU**, bukan pengaman tunggal.

### J4 — JST-XH-2, tombol Start/Stop S1

| Pin | Net |
|---:|---|
| 1 | START_STOP |
| 2 | GND_CTL |

S1 adalah pushbutton momentary normally-open. R3 = 10 kΩ pull-up ke +5V_CTL; ketika ditekan, input menjadi LOW. Tombol ini bukan emergency stop atau interlock keselamatan.

### SW2 — interlock low-voltage pada koil relay

SW2 NC dipasang seri dengan suplai koil K1. Ketika pintu membuka, kontaknya membuka dan koil relay kehilangan suplai. Ini lapisan tambahan untuk sisi low-voltage; SW2 tidak menggantikan SW3.

## 4. Driver koil relay

Baseline gambar v1.6 memakai relay polos berkoil 5 V dan Q1 MOSFET N-channel logic-level sebagai low-side switch.

- Jalur koil: +5V_CTL → SW2 NC → koil K1 → Q1 drain → Q1 source → GND_CTL.
- RELAY_CMD dari U1 pin 3 / P5.5 menuju gate Q1 melalui Rg = 100 Ω.
- R4 = 100 kΩ menghubungkan gate ke source/GND_CTL supaya Q1 cenderung OFF ketika MCU reset atau pin mengambang.
- D1 = 1N4007 dipasang paralel dengan koil: **katoda ke +5V_CTL/koil+, anoda ke sisi koil−/Q1 drain**.
- FQP30N06L dicantumkan hanya sebagai kandidat. Verifikasi datasheet part yang benar, RDS(on) pada VGS 4,5–5 V, arus koil, disipasi, keaslian dan urutan kaki paket.
- Bila membeli modul relay siap pakai dengan transistor/MOSFET driver dan diode sendiri, modul tersebut adalah **alternatif** dari driver diskrit. Jangan menumpuk kedua driver tanpa kebutuhan yang dibuktikan.

## 5. Programming / ISP dan kondisi startup

STC8G1K08A menggunakan P3.0 sebagai RXD dan P3.1 sebagai TXD pada fungsi UART yang relevan untuk ISP. Oleh karena itu:

1. J3 / SW1 dan J4 / S1 berbagi jalur MCU dengan fungsi UART; lepaskan harness eksternal bila mengganggu koneksi ISP.
2. P5.4 disisihkan karena dapat dikonfigurasi sebagai pin reset aktif-low saat ISP.
3. Hindari membuat P3.0, P3.1 dan P3.2 sekaligus LOW pada saat power-up; pastikan pull-up dan keadaan tombol/saklar tidak menimbulkan kondisi masuk mode download yang tidak diinginkan.
4. Uji kondisi relay OFF ketika power-on, reset, sensor pintu terbuka, dan firmware tidak berjalan sebelum menambah beban.

## 6. Batas subsistem AC / UV-C

Diagram hanya menunjukkan blok fungsional: input AC dan proteksi → SW3 interlock pintu berating mains → kontak K1 → ballast/driver sesuai model lampu → dua lampu UV-C. Ini bukan detail wiring PLN.

- SW3 harus menjadi pemutus energi lampu yang independen dari MCU dan koil relay. Hal ini penting karena kontak relay dapat gagal/terlas pada posisi tertutup.
- Model lampu, ballast, rating kontak relay, inrush, enclosure, fuse/proteksi serta implementasi SW3 belum final dan perlu direview tenaga kompeten.
- Jangan lewatkan tegangan PLN/ballast pada matrix board atau konektor JST-XH low-voltage.
- Sumber UV-C harus tertutup enclosure opaque. Jangan menguji dengan lampu terbuka. Jangan mengklaim sterilisasi tanpa validasi dosis/proses dan pengujian mikrobiologis yang sesuai.

Referensi keselamatan: [CDC/NIOSH — Germicidal Ultraviolet](https://www.cdc.gov/niosh/ventilation/germicidal-ultraviolet/index.html).

---
*Revision 1.6: pin MCU disesuaikan ke STC8G1K08A-36I-DFN8. EPAD dan rating subsistem daya tetap perlu dipastikan dari dokumen paket serta komponen final.*
