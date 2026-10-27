# Studi Harga Komponen
## Multi-Purpose Sterilizer Unit Prototype

<p align="center">
  <img src="https://img.shields.io/badge/Document-BOM%20Review-1D4ED8?style=flat-square" alt="Document type: BOM review" />
  <img src="https://img.shields.io/badge/Stage-Preliminary-0F766E?style=flat-square" alt="Status: preliminary" />
  <img src="https://img.shields.io/badge/Price%20Data-Not%20Checkout%20Verified-B45309?style=flat-square" alt="Price data not verified at checkout" />
</p>


> **Status dokumen:** studi awal / belum menjadi BOM final  
> **Tanggal observasi marketplace:** 17 Oktober 2026  
> **Tujuan:** membandingkan kisaran harga komponen prototipe dan mengidentifikasi biaya yang belum masuk anggaran.  
> **Batasan:** harga berasal dari hasil pencarian marketplace dan snapshot scraper, bukan konfirmasi checkout. Ketersediaan, varian, ongkir, diskon, jumlah minimum, dan harga dapat berubah.

## 1. Ringkasan eksekutif

Pencarian Tokopedia melalui sesi browser menghasilkan kandidat untuk sebagian besar komponen kontrol dasar. Angka termurah mentah perlu dibaca hati-hati: beberapa hasil dari query `STC8H1K08` ternyata komponen lain atau sama sekali tidak terkait; query kapasitor juga banyak menangkap kapasitor kipas AC yang belum tentu relevan untuk rangkaian kendali. Karena itu, laporan ini membedakan harga terendah yang terdeteksi dari harga yang layak dipakai sebagai estimasi awal.

Temuan awal:

- **LCD 16x2 non-I2C** terdeteksi mulai sekitar Rp16.665; modul I2C terpisah atau versi LCD+I2C perlu dipastikan sebelum membeli.
- **Relay 1 kanal 5 V** terdeteksi mulai sekitar Rp7.000, tetapi rating yang tercetak pada relay murah bukan bukti bahwa keseluruhan modul aman untuk switching beban 220 VAC.
- **PCB matrix 5x7 cm** terdeteksi mulai sekitar Rp2.750.
- Untuk koneksi yang rapi dan bisa dilepas, pertimbangkan JST-XH 2P untuk catu/sensor dan JST-XH 4P untuk LCD I²C. Seri JST-XH resmi memiliki pitch 2,5 mm, bukan JST-PH 2,0 mm.
- Untuk menghubungkan pad komponen pada matrix board, anggarkan **kawat jumper solid-core sekitar 0,5 mm** untuk lintasan pendek dan **kabel jumper berisolasi** untuk lintasan yang menyilang atau lebih panjang.
- **Lampu yang diklaim UV-C/germicidal** terdeteksi mulai Rp75.000 per unit. Jenis tabung, panjang gelombang, ballast, soket, emisi ozon, dan spektrum perlu diverifikasi.
- Biaya utama bukan hanya MCU, LCD dan relay. Driver/ballast lampu, rangkaian catu daya, interlock keselamatan independen, enclosure, pengaman listrik, kabel/konektor, pengujian, dan ongkir bisa menaikkan biaya total secara signifikan.

**Kesimpulan sementara:** jangan menganggap rancangan sudah bisa dibuat lengkap di bawah Rp500.000 hanya dengan menjumlahkan harga komponen kontrol yang terlihat. Sebelum pembelian, tetapkan spesifikasi lampu dan sistem keselamatan lalu buat BOM per varian.

## 2. Ruang lingkup

Studi ini meninjau komponen berikut:

1. Mikrokontroler: STC8H1K08 atau CH32V003.
2. Lampu germicidal UV-C, kandidat dua unit.
3. Relay polos dengan koil 5 V dan driver MOSFET logic-level (baseline skematik); modul relay siap pakai adalah alternatif, bukan komponen tambahan.
4. Dua micro limit switch low-voltage: SW1 untuk pemantauan pintu ke MCU dan SW2 untuk memutus suplai koil relay.
5. Interlock pintu SW3 yang berating mains dan bekerja independen dari MCU/relay coil; model final dan harga belum ditentukan.
6. LCD karakter 16x2 dengan backpack I²C dan konektor JST-XH-4.
7. PCB matrix/perfboard, resistor, kapasitor, diode flyback, konektor, kawat jumper PCB dan kabel penghubung.
8. Ballast/driver yang sesuai untuk dua lampu, enclosure dan komponen proteksi/interlock yang harus direview sebelum dirakit.

Dokumen ini hanya merupakan kajian belanja awal. Bukan skematik listrik, sertifikasi keselamatan, validasi mikrobiologis, ataupun instruksi pemasangan tegangan PLN.

## Draft skematik yang dikoreksi

File rujukan terbaru:

- [**Skematik optimasi v1.1 (SVG)**](schematic-optimized-v1.svg): versi visual utama untuk catu kontrol, MCU, LCD I²C, dua fungsi sakelar pintu, dan driver relay MOSFET.
- [**Catatan optimasi v1.1 (Markdown)**](schematic-optimized-v1.md): koreksi skematik awal, asumsi pinout JST-XH, pilihan driver, daftar komponen, dan batas keselamatan.
- [Visual komponen skematik (SVG)](schematic-komponen-visual-v0.svg): ilustrasi komponen fisik; bukan pengganti skematik koneksi.
- [Skematik low-voltage v0.2 (SVG)](schematic-low-voltage-v0.svg) dan [catatan v0.2](schematic-notes-v0.md): versi terdahulu untuk jejak perubahan.

v1.1 masih draft. Nomor pin MCU belum final karena STC8H1K08 atau CH32V003 dan tipe board belum dipilih. Sambungan PLN dan ballast UV-C sengaja hanya berupa batas blok, bukan instruksi kabel rinci.

## Referensi visual dari sumber eksternal

Gambar-gambar berikut berasal dari Wikimedia Commons dan memperlihatkan produk/perangkat referensi yang benar-benar difoto. **Gambar ini bukan prototipe kita, bukan rekomendasi untuk menyalin desainnya, dan tidak membuktikan efektivitas proses.** Lisensi dan atribusi mengikuti halaman sumber masing-masing.

<table>
  <tr>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV_STERILIZER_BOX_PHILIPS.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/UV_STERILIZER_BOX_PHILIPS.jpg/500px-UV_STERILIZER_BOX_PHILIPS.jpg" alt="Kabinet UV tertutup yang difoto oleh PT SUM HING INDONESIA" width="220" />
      </a>
      <br /><sub><b>Contoh kabinet tertutup</b><br />PT SUM HING INDONESIA · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:Germicidal_Lamp_1.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Germicidal_Lamp_1.jpg" alt="Tabung lampu germicidal fluoresen" width="300" />
      </a>
      <br /><sub><b>Contoh tabung germicidal</b><br />Atlant · <a href="https://creativecommons.org/licenses/by/2.5/">CC BY 2.5</a></sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV_Sterilisation.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/UV_Sterilisation.jpg/960px-UV_Sterilisation.jpg" alt="Perlakuan UV pada pipet dan tip di dalam biosafety cabinet" width="220" />
      </a>
      <br /><sub><b>Perlakuan UV dalam kabinet</b><br />Orla Keogh · <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a></sub>
    </td>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV-C_LED_lamp.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/2/23/UV-C_LED_lamp.jpg" alt="Modul UV-C LED dengan heatsink" width="190" />
      </a>
      <br /><sub><b>Contoh modul UV-C LED</b><br />Morrow363 · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
  </tr>
</table>

**Catatan untuk studi harga:** visual ini hanya konteks teknologi dan bentuk produk. Harga, panjang gelombang, kebutuhan ballast, driver, dudukan, tegangan, dan spesifikasi setiap komponen harus tetap ditentukan dari listing serta datasheet yang benar.

## 3. Metode dan keterbatasan pengambilan data

Data Tokopedia dibaca dari file hasil scraper lokal `hasil_tokopedia_20261017_173836.csv`, yang mencatat nama pencarian, platform, judul produk, harga, lokasi dan URL. Ringkasan hitungan per kata kunci:

| Kata kunci | Jumlah hasil terbaca | Harga minimum mentah | Median hasil mentah |
|---|---:|---:|---:|
| STC8H1K08 | 49 | Rp15.000 | Rp50.000 |
| Relay 1-Channel 5V | 60 | Rp7.000 | Rp15.400 |
| LCD 16x2 | 60 | Rp16.665 | Rp25.000 |
| Pin Header | 54 | Rp700 | Rp1.800 |
| Pin Socket | 50 | Rp1.350 | Rp4.350 |
| Resistor | 48 | Rp350 | Rp1.300 |
| Kapasitor | 54 | Rp2.500 | Rp7.000 |
| Lampu UV-C Germicidal 254 nm | 57 | Rp75.000 | Rp202.000 |
| PCB Matrix | 53 | Rp2.750 | Rp8.160 |

> **Penting:** median dan minimum mentah adalah statistik dari hasil yang tertangkap scraper, bukan statistik pasar terverifikasi. Hasil pencarian mengandung noise, salah kategori, pilihan varian, harga partai, dan produk yang belum tentu kompatibel. Harga terendah tidak selalu merupakan harga paling wajar.

Scraper melaporkan beberapa timeout pada halaman Tokopedia dan kegagalan parsing respons. Karena itu, jumlah hasil bukan bukti bahwa semua produk berhasil diambil, stok tersedia, atau harga bisa dibeli pada saat laporan dibaca. Link produk di bawah adalah tautan yang dikembalikan hasil pencarian; buka lagi untuk konfirmasi stok, varian, dan ongkir.

Shopee juga ditelusuri sebagai pembanding, tetapi data yang dapat diverifikasi pada sesi riset ini tidak selengkap snapshot Tokopedia. Harga Shopee ditulis sebagai pembanding tambahan, bukan perbandingan dua marketplace yang simetris.

## 4. Hasil pencarian Tokopedia

Harga dalam tabel adalah harga listing yang terdeteksi saat pengambilan data, belum termasuk ongkir.

| Komponen | Kandidat listing dan harga terendah relevan yang terdeteksi | Catatan verifikasi |
|---|---|---|
| STC8H1K08 | [Paket 10 pcs keluarga STC8H1K08, Rp224.000](https://www.tokopedia.com/panpang-terong/10pcs-stc8h1k08t-36i-tssop20-stc8h1k08t-stc8h1k08-36i-tssop20-stc8h1k08-stc8h1k08-36i-sop16-ic-chip-in-stock-wholesale) | Setara kira-kira Rp22.400/pcs jika benar paket 10 pcs. Periksa varian/package dan apakah chip persis STC8H1K08, bukan STC8H1K08T atau STC8G1K08A. |
| Relay 1 kanal 5 V | [Modul relay 1 kanal 5 V Tongling, Rp7.000](https://www.tokopedia.com/luckyall/module-relay-1-channel-5v-tongling-cocok-untuk-arduino-raspi) | Verifikasi active-low/high, tegangan koil, isolasi, jarak creepage/clearance, dan rating kontak untuk jenis beban aktual. |
| LCD karakter 16x2 | [LCD 16x2 1602, Rp16.665](https://www.tokopedia.com/iotstore/lcd-character-16x2-1602-5v-modul-layar-hijau-dlcd-display-character-16x2-1602-5v-modul-hijau-biru-abu-backlight-pilihan-i2c-atau-non-i2c-untuk-arduino-diyengan-backlight-tanpa-i2c-1737746352576497083-1737746303527585211) | Listing menyebut pilihan I2C/non-I2C. Pastikan varian yang dipilih dan tegangan logika modul. |
| Pin header male 1x40 | [Pin header male 1x40, Rp700](https://www.tokopedia.com/cncstorejogja/pin-header-male-strip-single-row-1x40-2-54mm-black-hitam-1729811654300566528) | Bisa dipotong sesuai jumlah pin; harga mungkin per strip/varian. |
| Female header/socket | [Female header 4/6/8/10 pin, Rp1.368](https://www.tokopedia.com/rajacell/10p-8p-6p-4p-female-header-long-pin-socket-connector-arduino-shield-empat-pin) | Pastikan bentuk dan jumlah pin sesuai kebutuhan. Ini bukan socket untuk semua jenis IC. |
| Resistor | [Resistor 1/4 W, Rp350](https://www.tokopedia.com/arieselektronikstore/resistor-1-4-watt-1-metal-film-100k-keatas-100k) | Harga berlaku untuk nilai resistor/opsi tertentu. Jangan menganggap Rp350 adalah harga paket semua nilai yang dibutuhkan. |
| Kapasitor | [Elco 1000 µF 16 V, Rp2.500](https://www.tokopedia.com/pcmelektrobik/1000uf-16v-1000-16-1-000-elco-capacitor-elko-kapasitor-polar) | Nilai 1000 µF/16 V hanya contoh listing, bukan spesifikasi kapasitor yang otomatis dibutuhkan rangkaian. Query umum menangkap banyak kapasitor kipas yang tidak relevan. |
| Lampu UV-C | [Lampu T8 UV-C germicidal 10 W, 34 cm, Rp75.000](https://www.tokopedia.com/amaritista/lampu-uv-uvc-germicidal-sterilizer-t8-10w-34cm-evaco-filter-air-kuman) | Jangan beli sebelum memastikan panjang gelombang/datasheet, tipe ballast, soket, panjang tabung, ozon, dan apakah harga hanya tabung atau satu set. |
| PCB matrix 5x7 cm | [PCB bolong 5x7 cm, Rp2.750](https://www.tokopedia.com/tansuju/pcb-bolong-dot-matrix-5x7cm-papan-circuit-board-hole-prototype-protoboard-single-layer-1732105073583949322) | Periksa ukuran, single/double sided, bahan dan apakah lubang/pad cocok untuk rancangan. |

### Hasil mentah yang perlu dikecualikan

- Pencarian `STC8H1K08` menghasilkan barang tak relevan seperti bakteri starter, buku catatan dan IC model lain. Harga-harga tersebut **tidak** dipakai sebagai harga STC8H1K08.
- Pencarian `Lampu UV-C Germicidal 254 nm` mengembalikan produk perangkap serangga yang menggunakan UV. Lampu UV-A untuk menarik serangga **bukan** pengganti lampu germicidal UV-C.
- Kata kunci `Pin Socket` menangkap soket motor, header female dan soket IC. Pilih jenis yang tepat, bukan angka termurah dari kategori campuran.
- Kata kunci `Kapasitor` terlalu luas untuk membentuk estimasi BOM; kapasitor harus dipilih berdasarkan skematik dan tegangan/ripple yang diperlukan.

## 5. Pembanding Shopee

Pencarian Shopee sebelumnya menghasilkan indikasi harga berikut. Harga dan status stok perlu diperiksa ulang sebelum digunakan sebagai dasar pembelian.

| Komponen | Indikasi harga Shopee | Link |
|---|---:|---|
| CH32V003F4P6 bare IC | Rp8.500, listing dilaporkan habis | [Listing CH32V003F4P6](https://shopee.co.id/CH32V003F4P6-RISC-V-32-bit-MCU-Microcontroller-TSSOP-20-Original-Syalis--i.16973105.52455550248) |
| CH32V003F4P6 development kit | Rp55.000 | [Development kit CH32V003F4P6](https://shopee.co.id/Original-CH32V003F4P6-RISC-V-MCU-Development-Kit-Arduino-Mikrokontroler-i.13858870.42315195826) |
| STC8H1K08-36I-QFN20 bare IC | Rp8.800 | [Listing STC8H1K08](https://shopee.co.id/STC-STC8H1K08-36I-QFN20-Microcontroller-MCU-8051-1T-48MHz-%E2%80%93-8KB-Flash-QFN20-Mini-%28ORIGINAL-STC%29-Syalis--i.16973105.25147746881) |
| USB-to-TTL CH340 | sekitar Rp16.600 | [Modul USB-TTL CH340](https://shopee.co.id/Module-USB-to-TTL-CH340-Board-USB-to-TTL-CH340-Serial-Converter-i.906610.109627300) |
| LCD 1602 I2C | sekitar Rp34.600 | [LCD 1602 I2C](https://shopee.co.id/Blue-LCD-1602-i2C-IIC-Backpack-LCD-Module-for-Arduino-New-I2C-V2.0-i.2178321.44700931268) |
| Relay satu kanal 5 V | sekitar Rp7.500–12.500 | [Pencarian relay 1 kanal 5 V](https://shopee.co.id/search?keyword=relay+1+channel+5V) |
| Micro limit switch | sekitar Rp1.900–4.600 | [Pencarian micro limit switch](https://shopee.co.id/search?keyword=micro+limit+switch) |
| PCB matrix | sekitar Rp4.250 untuk 5x7 cm pada listing lain | [Pencarian PCB matrix](https://shopee.co.id/search?keyword=PCB+matrix+5x7) |
| Adaptor DC 5 V 1 A | Rp16.500–31.000 pada listing yang ditemukan | [Adaptor 5 V 1 A](https://shopee.co.id/Adaptor-5v-1a-Adapter-DC-Switching-5-Volt-1-Ampere-i.48084222.57711814949) |
| Relay polos koil DC 5 V, misalnya SRD-05VDC-SL-C | sekitar Rp2.500–4.500/listing; pilih varian koil 5 V | [Relay polos 5 V](https://shopee.co.id/Relay-SPDT-SONGLE-5V-10A-250VAC-SRD-05VDC-SL-C-i.27499686.17436019731) |
| MOSFET logic-level Q1 (kandidat FQP30N06L) | Rp5.000 pada satu listing yang dilaporkan habis; gunakan anggaran Rp5.000–12.000 dan verifikasi ulang | [Contoh listing FQP30N06L](https://shopee.co.id/FQP30N06-30N06-30N06L-N-channel-MOSFET-60v-30A-TO-220-FQP30N06L-i.20732744.6100081208) |
| Diode flyback D1 1N4007 | sekitar Rp700–2.800/unit tergantung listing/pack | [Contoh listing 1N4007](https://shopee.co.id/avicenateknologiindonesia) |
| Modul relay satu kanal 5 V (alternatif jika tidak memakai driver diskrit) | sekitar Rp7.500–12.500 | [Pencarian modul relay 1 kanal 5 V](https://shopee.co.id/search?keyword=relay+1+channel+5V) |
| Lampu UV-C 254 nm | sekitar Rp75.000/unit untuk listing 4 W yang diklaim germicidal; perlu cek model | [Pencarian lampu UV-C 254 nm](https://shopee.co.id/search?keyword=lampu+UV-C+254nm+4W) |
| Konektor JST-XH-2P + kabel pendek | listing sekitar Rp1.750–3.250/set, stok/varian perlu dicek | [Contoh kabel JST-XH-2P](https://shopee.co.id/ORIGINAL-KABEL-JST-XH-2P-2.54mm-Pitch-JST-Male-Female-2PIN-Konektor-Terminal-Socket-soket-Cable-Connector-PH2.0-MOLEX-MOLEK-CABLE-KABLE-2-PIN-xh3p-i.137620933.20457052106) |
| Konektor/header JST-XH-4P | listing sekitar Rp2.000/set untuk header; kabel lengkap dapat jauh lebih mahal | [Contoh header XH-4P](https://shopee.co.id/1-Set-Konektor-Header-XH-4p-Siku-2.54mm-JST-XH-4-pin-Male-Female-Inner-4pin-bengkok-i.985143.29537360213) |
| Logic-level N-MOSFET (opsi bare relay) | listing FQP30N06L sekitar Rp7.000; varian/keaslian/stok perlu diverifikasi | [Contoh FQP30N06L](https://shopee.co.id/FQP30N06L-Original-asli-InFath-60V-Logic-Level-N-Channel-QFET-MOSFET-FQP-30N06L-30N06-L-sparepart-power-supply-i.17874779.40557594878) |
| Dioda flyback 1N4007 (opsi bare relay) | sekitar Rp700/pcs jika listing 10 pcs Rp7.000 | [Contoh listing 1N4007](https://shopee.co.id/avicenateknologiindonesia) |
| Resistor 100 Ω (opsi bare relay) | sekitar Rp130/pcs jika listing 100 pcs Rp13.000 | [Katalog resistor 100 Ω](https://shopee.co.id/wahoopart) |
| Resistor 100 kΩ (opsi bare relay) | sekitar Rp350/pcs jika listing 10 pcs Rp3.500 | [Contoh resistor 100 kΩ](https://shopee.co.id/avicenateknologiindonesia) |
| Kawat jumper PCB solid-core 0,5 mm, 1 meter | Rp1.500/m pada listing | [Kawat jumper 0,5 mm per meter](https://shopee.co.id/Kawat-Jumper-0.5mm-Tunggal-Kabel-Wire-PCB-Breadboard-harga-permeter-i.134242419.21021859571) |
| Kawat/kabel tunggal berisolasi untuk jalur PCB, 1 meter | Rp2.500 pada listing dengan pilihan variasi | [Kabel tunggal 0,5 mm untuk PCB/breadboard](https://shopee.co.id/Kabel-Tunggal-Kawat-NYA-0.5mm-0.5-mm-Warna-Bread-Proto-Project-Board-PCB-Jumper-Male-BreadBoard-i.1093272634.29938159885) |
| Jumper PCB potong 6 cm, diameter 0,5 mm | Rp150/pcs, listing mensyaratkan minimum 50 pcs | [Kawat jumper 6 cm, minimum 50 pcs](https://shopee.co.id/Kawat-Jumper-6cm-d.0.5mm-wire-breadboard-pcb-arduino-harga-perbuah-minimal-beli-50buah-i.134242419.5845710785) |

Harga CH32V003 bare chip tidak boleh dibandingkan langsung dengan harga development kit. Ketersediaan komponen, paket, programmer, dan kebutuhan penyolderan berbeda.

### Konektor JST-XH untuk harness prototipe

JST-XH adalah keluarga konektor wire-to-board pitch 2,5 mm. Untuk rancangan ini:

- **XH-2 / 2P:** 5 V input dan sensor pintu dua kabel.
- **XH-4 / 4P:** LCD I²C dengan VCC, GND, SDA dan SCL.
- **XH-3 / 3P (opsional):** modul relay yang ditempatkan terpisah dari PCB kontrol.

Header PCB, housing, terminal crimp, dan kabel adalah bagian yang berbeda. Harga listing “header male/female” belum tentu termasuk kabel siap pakai. Untuk jumlah prototipe kecil, harness siap-crimp bisa lebih praktis, tetapi cek urutan pin dan panjang kabel. Walaupun spesifikasi JST-XH menyebut rating tertentu untuk konektor asli, **pada proyek ini konektor XH hanya ditetapkan untuk kontrol low-voltage**, bukan jalur PLN/ballast. Lihat [spesifikasi XH resmi JST](https://www.jst-mfg.com/product/index.php?lang=2&series=277).

### Pilihan relay dan MOSFET

- **Baseline v1.1: relay polos + MOSFET logic-level.** Estimasi komponen utama driver adalah MOSFET Rp5.000–12.000, diode flyback Rp700–2.800, resistor gate 100 Ω dan pull-down 100 kΩ (dimasukkan dalam anggaran paket resistor). Tambahkan relay polos koil 5 V sekitar Rp2.500–4.500.
- **Alternatif: modul relay 5 V siap pakai.** Biasanya modul sudah memiliki transistor/MOSFET driver dan diode flyback; gunakan modul sebagai pengganti driver diskrit, jangan menumpuk seluruh komponennya tanpa alasan.
- MOSFET pada skematik hanya digunakan untuk koil relay DC. Ia tidak dimaksudkan untuk switching lampu UV-C AC secara langsung.
- Kontak relay generik harus dinilai berdasarkan tipe ballast, arus masuk, rating beban yang sebenarnya dan kebutuhan isolasi. Angka “10 A / 250 VAC” di listing bukan persetujuan keselamatan untuk beban proyek ini.

### Kawat penghubung untuk matrix board

Untuk papan matrix dengan pad tembaga per lubang, pertimbangkan dua jenis penghubung:

- **Kawat jumper solid-core 0,5 mm tanpa isolasi:** cocok untuk membuat sambungan pendek antara pad yang berdekatan di sisi solder. Potong sesuai panjang, bentuk rapi, lalu solder di pad yang diperlukan.
- **Kawat tunggal berisolasi:** lebih cocok ketika jalur harus melintasi jalur lain, mengitari komponen, atau dibuat di sisi bawah papan. Isolasi mengurangi risiko korsleting ketika beberapa jalur bersilangan.
- **Jumper siap-potong 6 cm:** alternatif praktis untuk sambungan pendek. Harga per potong terlihat murah, tetapi cek minimum pembelian yang tercantum pada listing.

**Jangan memakai besi/kawat baja biasa.** Pilih kawat konduktor yang memang bisa disolder untuk elektronik, idealnya kawat tembaga berlapis timah atau kawat jumper PCB. Kawat tanpa isolasi tidak boleh menyentuh jalur/pad lain yang berbeda net. Harga marketplace di atas adalah referensi saat pencarian, bukan konfirmasi stok atau harga checkout.

## 6. Pilihan mikrokontroler

<p align="center">
  <img src="https://img.shields.io/badge/Candidate-STC8H1K08-2563eb?style=flat-square" alt="Candidate: STC8H1K08" />
  <img src="https://img.shields.io/badge/Candidate-CH32V003-7c3aed?style=flat-square" alt="Candidate: CH32V003" />
  <img src="https://img.shields.io/badge/Architecture-RISC--V-334155?style=flat-square&logo=riscv&logoColor=white" alt="RISC-V architecture badge" />
</p>

> Badge adalah penanda kandidat yang sedang dibandingkan, bukan konfirmasi pemilihan komponen. Logo RISC-V digunakan hanya sebagai penjelas arsitektur untuk kandidat CH32V003.

![Pilihan MCU](https://img.shields.io/badge/MCU%20option-STC8H1K08-2563eb?style=flat-square) ![Pilihan MCU](https://img.shields.io/badge/MCU%20option-CH32V003%20%2F%20RISC--V-7c3aed?style=flat-square&logo=riscv&logoColor=white)

> Badge di atas hanya menandai dua kandidat yang sedang dikaji. Tidak menyatakan bahwa MCU sudah dipilih atau digunakan pada prototipe.

### Opsi A: STC8H1K08

Produsen STC menyatakan keluarga STC8H1K08 memakai inti 8051 1T, rentang operasi 1,9–5,5 V, memori program 8 KB untuk varian STC8H1K08, dan memiliki UART, SPI serta I2C. STC juga mendokumentasikan ISP (in-system programming), sehingga penggunaan USB-to-TTL yang kompatibel dapat mengurangi kebutuhan programmer khusus. Lihat [halaman resmi STC8H1K08](https://www.stcmicro.com/stc/stc8h1k08.html) dan [manual keluarga STC8H](https://www.stcmicro.com/datasheet/STC8H-en.pdf).

**Pertimbangan:** varian QFN20 sulit untuk solder manual pemula. Utamakan TSSOP20 atau development board bila kompatibel dan tersedia, dan pastikan pinout/part number persis sama. Jangan menganggap setiap USB-to-TTL otomatis kompatibel; level tegangan, pin UART, prosedur ISP, reset/boot dan dukungan perangkat lunak harus sesuai.

### Opsi B: CH32V003F4P6

CH32V003 adalah MCU 32-bit berbasis RISC-V dengan dokumentasi serta contoh resmi tersedia di [repo WCH Open Source](https://github.com/openwch/ch32v003). Jalur pemrograman/debug yang lazim menggunakan WCH-Link/WCH-LinkE atau tool kompatibel untuk antarmuka debug satu-kawat. Referensi komunitas: [CH32V003 Arduino Quickstart](https://github.com/vimalb/CH32V003_Arduino_Quickstart) dan [CH32V003 Dev Guide](https://github.com/limingjie/CH32V003-ST7735-Driver/blob/main/CH32V003_Dev_Guide.md).

**Pertimbangan:** harga chip murah belum tentu membuat total sistem termurah. Periksa apakah board yang dibeli sudah menyertakan programmer, header debug, regulator, dan contoh firmware. Varian TSSOP20 juga menuntut teknik solder lebih baik daripada modul yang sudah dirakit.

### Rekomendasi sementara

Untuk prototipe tugas dengan waktu dan anggaran terbatas, prioritaskan **kemudahan bring-up dan ketersediaan board**, bukan sekadar harga bare IC atau jumlah bit CPU. Bandingkan biaya *total siap diprogram*: MCU/board + programmer/USB-TTL + adaptor/konektor + tooling + risiko rework. Pilih salah satu MCU dahulu agar tidak membeli dua ekosistem sekaligus.

## 7. Estimasi biaya awal

Angka berikut adalah estimasi kerja, bukan harga final yang sudah terverifikasi. Biaya catu daya, ballast, enclosure, dan perlindungan listrik harus dihitung terpisah.

### Paket prototipe kontrol berbasis STC (indikatif)

| Item | Asumsi anggaran |
|---|---:|
| MCU/board dan kebutuhan pemrograman awal | Rp10.000–50.000 |
| USB-to-TTL yang kompatibel (jika diperlukan untuk STC) | Rp17.000–25.000 |
| Adaptor 5 V DC teregulasi dan terisolasi, sekitar 1 A | Rp16.500–31.000 |
| LCD 16x2 dengan I²C backpack | Rp30.000–40.000 |
| Relay polos dengan koil 5 V | Rp2.500–4.500 |
| MOSFET logic-level Q1 | Rp5.000–12.000 |
| Diode flyback D1 1N4007 | Rp700–2.800 |
| Dua micro limit switch low-voltage (SW1 monitor + SW2 coil inhibit) | Rp4.000–10.000 |
| PCB matrix | Rp3.000–10.000 |
| Header, konektor kecil, resistor, kapasitor dan komponen prototipe | Rp10.000–35.000 |
| Kawat jumper PCB solid-core 0,5 mm, sekitar 1 meter | Rp1.500 |
| Kawat/kabel jumper tunggal berisolasi, sekitar 1 meter | Rp2.500 |
| Harness JST-XH low-voltage untuk catu dan LCD/sensor | Rp5.000–15.000 |
| Dua lampu UV-C (klaim listing perlu verifikasi) | Rp150.000–210.000 |
| **Subtotal indikatif baseline v1.1** | **Rp253.000–449.000** |

Subtotal memakai **relay polos + driver MOSFET** dan memasukkan dua sakelar low-voltage. Angka ini bukan total alat siap digunakan. **SW3 interlock pintu ber-rating mains, ballast/driver, dudukan lampu, enclosure opaque, proteksi/isolasi AC, strain relief, kabel dan pengujian belum masuk subtotal.** Harga SW3 belum dikunci karena pemilihan harus berdasarkan tipe kontak, mekanisme positive-opening bila dipersyaratkan, rating tegangan/arus serta arus masuk ballast. Total aktual dapat melewati Rp500.000.

Modul relay siap pakai adalah alternatif; bila dipilih, ganti relay polos + Q1 + D1 dengan satu modul relay yang rangkaiannya sudah diverifikasi, dan hitung ulang subtotal. Jangan menjumlahkan dua alternatif driver sekaligus.

### CH32V003

Anggaran board Rp55.000 sebagai kandidat pencarian belum cukup untuk menyimpulkan bahwa sistem sudah siap diprogram. Tambahkan biaya programmer bila tidak termasuk. Perbandingan yang adil wajib mencatat **board + programmer + kabel debug + catu daya + konektor**, bukan membandingkan bare IC dengan board STC.

## 8. Komponen yang belum tercakup atau harus dipastikan

1. **Ballast/driver dan dudukan lampu.** Banyak tabung fluoresen germicidal tidak bisa langsung disambungkan ke jaringan listrik. Jenis ballast harus cocok dengan model serta watt lampu. Jangan mengasumsikan paket lampu sudah lengkap.
2. **Catu daya kontrol.** Tentukan tegangan dan arus untuk MCU, LCD, serta modul relay. Pastikan catu daya terisolasi dari jaringan listrik dan logika tidak terpapar tegangan berbahaya.
3. **Proteksi jaringan listrik.** Fuse/overcurrent protection, terminal tertutup, enclosure yang layak, strain relief dan penanganan kabel harus dipertimbangkan oleh orang yang kompeten.
4. **Sakelar pintu tiga fungsi berbeda.** SW1 membaca status pintu ke MCU; SW2 NC memutus suplai koil relay pada domain low-voltage; SW3 harus merupakan interlock pintu ber-rating mains yang memutus energi lampu secara independen. Multiplexer tidak diperlukan untuk input saklar tunggal. SW1/SW2 bukan pengganti SW3, dan SW3 belum dihitung harganya.
5. **Tombol emergency/stop dan indikator.** Tentukan cara menghentikan operasi serta membedakan status standby, aktif, selesai, dan fault.
6. **Pengukuran UV-C.** Daya listrik lampu (W) bukan dosis UV pada permukaan. Dosis dipengaruhi irradiance dan waktu; geometri, jarak, material, kontaminasi dan bayangan memengaruhi hasil.
7. **Rangka mekanis modular.** Rak yang dapat diganti harus tidak menghalangi distribusi UV. Bahan rak juga harus tahan terhadap UV, panas, korosi dan prosedur pembersihan.
8. **Kawat jumper dan ongkir.** Kawat solid-core tanpa isolasi cocok untuk lintasan solder lokal; gunakan kawat berisolasi untuk lintasan silang agar tidak korslet. Harga murah per meter atau per potong harus dibaca bersama minimum pembelian, pilihan diameter, jenis isolasi, dan ongkir.

## 9. Catatan keselamatan dan batas klaim

**UV-C 254 nm dapat mencederai mata dan kulit.** WHO menjelaskan paparan berlebih dapat menyebabkan photokeratitis dan erythema, dan merekomendasikan desain pelindung serta pemutus otomatis saat pintu dibuka untuk sistem tertentu. Lihat [WHO: Operational handbook on tuberculosis, bagian keselamatan UV-C](https://tbksp.who.int/ru/node/2589) dan [CDC/NIOSH: Germicidal Ultraviolet](https://www.cdc.gov/niosh/ventilation/germicidal-ultraviolet/index.html).

Persyaratan minimum untuk melanjutkan prototipe UV-C:

- Lampu benar-benar teridentifikasi sebagai UV-C germicidal dengan spesifikasi pabrikan, bukan hanya karena terlihat ungu.
- Sumber UV berada dalam enclosure buram yang sesuai dan tidak dapat menyinari operator ketika digunakan.
- Ada interlock pintu, dan fungsi memutus energi UV tidak hanya mengandalkan kode MCU atau satu relay murah.
- Proses pengujian dilakukan tanpa paparan langsung manusia, mengikuti prosedur yang ditinjau pembimbing/tenaga kompeten.
- Jangan menyatakan alat “mensterilkan” alat makan tanpa validasi proses dan pengujian mikrobiologis yang sesuai. Pada tahap awal, gunakan istilah “prototipe perlakuan UV-C” atau “prototipe disinfeksi permukaan yang belum tervalidasi”.

## 10. Perhitungan kebutuhan daya

Hitung beban dari label/datasheet, bukan dari dugaan:

- Daya masukan lampu total: jumlah lampu × daya masukan masing-masing, dengan memperhitungkan ballast/driver.
- Daya kontrol: konsumsi MCU + LCD + indikator + koil relay, sesuai datasheet/modul.
- Perkiraan arus input AC: secara kasar (I = P/V) hanya untuk beban dengan faktor daya mendekati satu; ballast dapat memengaruhi faktor daya dan arus awal. Gunakan spesifikasi pabrikan saat menentukan komponen switching dan proteksi.
- Rating kontak pada relay harus dievaluasi terhadap jenis beban, arus start, jarak isolasi, temperatur, dan konstruksi modul. Tulisan “10 A, 250 VAC” pada relai tidak otomatis mengesahkan papan murah sebagai sistem keselamatan listrik.

Sampai model lampu, ballast, dan tegangan suplai ditentukan, **rating final kabel, fuse, terminal, relay, dan enclosure belum bisa ditetapkan**.

## 11. Antarmuka elektronik awal

| Fungsi | Antarmuka yang mungkin | Catatan |
|---|---|---|
| Limit switch pintu | Input digital GPIO | Gunakan konfigurasi fail-safe yang dirancang benar dan hindari mengandalkan firmware sebagai satu-satunya pemutus UV. |
| LCD 16x2 I2C | SDA + SCL + suplai + GND | Pastikan level logika, alamat I2C dan backpack sesuai MCU. |
| Modul relay | Output digital melalui input yang kompatibel | Periksa active-high/low, arus input, isolasi, level logika dan keadaan saat MCU reset. Tidak menggantikan pemutus keselamatan independen. |
| Tombol dan indikator | GPIO | Tentukan keadaan default aman setelah start/reset dan perilaku ketika sensor terputus. |

RTOS belum terlihat diperlukan untuk prototipe kecil yang hanya membaca limit switch, mengatur timer, memperbarui LCD, dan mengendalikan keluaran. *Bare-metal superloop* dengan state machine dan watchdog dapat lebih sederhana untuk tahap awal. Keputusan akhir bergantung pada kebutuhan respons waktu nyata, jumlah sensor, komunikasi, logging dan kompleksitas firmware.

## 12. SWOT singkat pada pendekatan belanja

| Aspek | Analisis |
|---|---|
| **Strengths** | Banyak komponen kontrol dasar tersedia murah; STC dan CH32 punya dokumentasi/proyek referensi; LCD/limit switch mudah dipahami. |
| **Weaknesses** | Data pencarian marketplace bising; harga listing bukan biaya total; komponen murah bisa memerlukan soldering, driver, dan perlindungan tambahan. |
| **Opportunities** | Membuat BOM terukur dan berulang; memisahkan subsystem kontrol low-voltage dari subsystem UV/mains; dokumentasi open source membantu replikasi dan pembelajaran. |
| **Threats** | Salah memilih lampu UV-A sebagai UV-C, paparan UV-C, bahaya 220 VAC, produk tidak cocok/palsu, serta klaim sterilisasi tanpa validasi. |

## 13. Rencana verifikasi sebelum checkout

- [ ] Tetapkan dimensi ruang dan panjang lampu yang dibutuhkan.
- [ ] Konfirmasi model lampu, spektrum/panjang gelombang, watt input, ozone/no-ozone, ballast dan dudukan.
- [ ] Pilih satu MCU dan konfirmasi tool pemrograman sudah tersedia.
- [ ] Konfirmasi LCD termasuk backpack I2C atau tidak.
- [ ] Konfirmasi modul relay dan limit switch sesuai fungsi yang dibutuhkan; tinjau rancangan interlock independen.
- [ ] Tentukan catu daya low-voltage, fuse, enclosure, konektor, dan kabel dengan orang kompeten.
- [ ] Periksa harga varian, jumlah pembelian, stok, reputasi penjual dan ongkir pada halaman checkout.
- [ ] Hitung ulang BOM memakai harga aktual dan sisihkan cadangan biaya.
- [ ] Tetapkan metode evaluasi UV-C dan batas klaim hasil sebelum menyatakan prototipe berhasil.

## 14. Referensi teknis

1. STC Micro, [STC8H1K08 series: specifications, tools, ISP and sample code](https://www.stcmicro.com/stc/stc8h1k08.html).
2. STC Micro, [STC8H Series Manual (PDF)](https://www.stcmicro.com/datasheet/STC8H-en.pdf).
3. WCH Open Source, [CH32V003 official GitHub repository](https://github.com/openwch/ch32v003).
4. [CH32V003 Arduino Quickstart](https://github.com/vimalb/CH32V003_Arduino_Quickstart), komunitas, untuk alur setup dan WCH-LinkE.
5. [CH32V003 Development Guide](https://github.com/limingjie/CH32V003-ST7735-Driver/blob/main/CH32V003_Dev_Guide.md), komunitas, untuk opsi pemrograman dan debug.
6. WHO, [Operational handbook on tuberculosis: safety of UVC254](https://tbksp.who.int/ru/node/2589).
7. CDC/NIOSH, [Germicidal Ultraviolet (GUV)](https://www.cdc.gov/niosh/ventilation/germicidal-ultraviolet/index.html).
8. Parik-2006, [BIOSAFETY_EL: contoh proyek UV-C dengan door interlock](https://github.com/Parik-2006/BIOSAFETY_EL). Dipakai hanya sebagai contoh struktur fitur keselamatan untuk dipelajari, bukan bukti bahwa desain tersebut tervalidasi atau aman.

## 15. Sumber dan lisensi gambar

Semua foto di bagian referensi visual ditautkan ke versi asli di Wikimedia Commons. Atribusi yang disertakan di dekat tiap gambar merupakan bagian dari kredit sumber.

1. **UV STERILIZER BOX PHILIPS.jpg** — foto oleh PT SUM HING INDONESIA, lisensi [Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/). [Halaman sumber](https://commons.wikimedia.org/wiki/File:UV_STERILIZER_BOX_PHILIPS.jpg).
2. **Germicidal Lamp 1.jpg** — foto oleh Atlant, lisensi [Creative Commons Attribution 2.5 (CC BY 2.5)](https://creativecommons.org/licenses/by/2.5/). [Halaman sumber](https://commons.wikimedia.org/wiki/File:Germicidal_Lamp_1.jpg).
3. **UV Sterilisation.jpg** — foto oleh Orla Keogh yang memperlihatkan perlakuan UV pada pipet dan tip di biosafety cabinet, lisensi [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). [Halaman sumber](https://commons.wikimedia.org/wiki/File:UV_Sterilisation.jpg).
4. **UV-C LED lamp.jpg** — foto oleh Morrow363, lisensi [Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/). [Halaman sumber](https://commons.wikimedia.org/wiki/File:UV-C_LED_lamp.jpg).

Gambar ditampilkan tanpa perubahan. Pemilik gambar dan Wikimedia Commons tidak menyatakan dukungan terhadap proyek ini.

## 16. Artefak desain dan data

- Skematik terkoreksi: [schematic-optimized-v1.svg](schematic-optimized-v1.svg).
- Catatan optimasi: [schematic-optimized-v1.md](schematic-optimized-v1.md).
- Skematik low-voltage versi sebelumnya: [schematic-low-voltage-v0.svg](schematic-low-voltage-v0.svg).
- Catatan skematik v0.2: [schematic-notes-v0.md](schematic-notes-v0.md).
- CSV sumber: `hasil_tokopedia_20261017_173836.csv` (hasil scraper lokal, disimpan terpisah dari dokumen ini).
- Catatan konsol scraper: `Pasted text.txt` (menunjukkan beberapa timeout dan hasil query yang tidak relevan).
- Dokumen ini sebaiknya diperbarui ketika harga dicek ulang, model komponen dipilih, dan biaya checkout diketahui.


---
*Dokumen studi awal untuk pendidikan dan eksperimen prototipe. Bukan panduan produksi, sertifikasi, atau jaminan performa sterilisasi.*
