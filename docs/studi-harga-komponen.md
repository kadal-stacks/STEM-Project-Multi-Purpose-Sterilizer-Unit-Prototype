# Studi Harga Komponen
## Multi-Purpose Sterilizer Unit Prototype

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
- **Lampu yang diklaim UV-C/germicidal** terdeteksi mulai Rp75.000 per unit. Jenis tabung, panjang gelombang, ballast, soket, emisi ozon, dan spektrum perlu diverifikasi.
- Biaya utama bukan hanya MCU, LCD dan relay. Driver/ballast lampu, rangkaian catu daya, interlock keselamatan independen, enclosure, pengaman listrik, kabel/konektor, pengujian, dan ongkir bisa menaikkan biaya total secara signifikan.

**Kesimpulan sementara:** jangan menganggap rancangan sudah bisa dibuat lengkap di bawah Rp500.000 hanya dengan menjumlahkan harga komponen kontrol yang terlihat. Sebelum pembelian, tetapkan spesifikasi lampu dan sistem keselamatan lalu buat BOM per varian.

## 2. Ruang lingkup

Studi ini meninjau komponen berikut:

1. Mikrokontroler: STC8H1K08 atau CH32V003.
2. Lampu germicidal UV-C, kandidat dua unit.
3. Modul relay satu kanal 5 V.
4. Micro limit switch untuk mendeteksi pintu.
5. LCD karakter 16x2, idealnya dengan antarmuka I2C.
6. PCB matrix/perfboard, resistor, kapasitor, pin header, socket dan kabel.
7. Kabel dan steker 220 VAC serta komponen perlindungan yang diperlukan.

Dokumen ini hanya merupakan kajian belanja awal. Bukan skematik listrik, sertifikasi keselamatan, validasi mikrobiologis, ataupun instruksi pemasangan tegangan PLN.

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
| Lampu UV-C 254 nm | sekitar Rp75.000/unit untuk listing 4 W yang diklaim germicidal; perlu cek model | [Pencarian lampu UV-C 254 nm](https://shopee.co.id/search?keyword=lampu+UV-C+254nm+4W) |

Harga CH32V003 bare chip tidak boleh dibandingkan langsung dengan harga development kit. Ketersediaan komponen, paket, programmer, dan kebutuhan penyolderan berbeda.

## 6. Pilihan mikrokontroler

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
| STC MCU / board atau adaptor minimum | Rp10.000–50.000 |
| USB-to-TTL yang kompatibel | Rp17.000–25.000 |
| LCD 16x2 I2C | Rp30.000–40.000 |
| Relay satu kanal 5 V (untuk uji kendali, bukan otomatis dianggap safety-rated) | Rp7.000–13.000 |
| Limit switch | Rp2.000–5.000 |
| PCB matrix | Rp3.000–10.000 |
| Header, socket, resistor, kapasitor dan kabel prototipe | Rp15.000–40.000 |
| Dua lampu UV-C | Rp150.000–210.000 sebagai cadangan awal |
| **Subtotal indikatif** | **Rp234.000–393.000** |

Subtotal ini **belum** mencakup ballast/driver yang cocok, pemegang lampu, catu daya terisolasi untuk kontrol, fuse/overcurrent protection, enclosure, mekanisme pintu, pemutus independen, kabel PLN yang sesuai, strain relief, label peringatan, ongkir dan alat uji. Maka total sesungguhnya bisa melampaui Rp500.000. Harga Rp150.000 untuk dua lampu hanya masuk akal bila dua lampu pada kisaran Rp75.000 benar-benar cocok dan sumber UV-C-nya terbukti dari datasheet; ini belum terverifikasi untuk semua listing.

### CH32V003

Anggaran board Rp55.000 sebagai kandidat pencarian belum cukup untuk menyimpulkan bahwa sistem sudah siap diprogram. Tambahkan biaya programmer bila tidak termasuk. Perbandingan yang adil wajib mencatat **board + programmer + kabel debug + catu daya + konektor**, bukan membandingkan bare IC dengan board STC.

## 8. Komponen yang belum tercakup atau harus dipastikan

1. **Ballast/driver dan dudukan lampu.** Banyak tabung fluoresen germicidal tidak bisa langsung disambungkan ke jaringan listrik. Jenis ballast harus cocok dengan model serta watt lampu. Jangan mengasumsikan paket lampu sudah lengkap.
2. **Catu daya kontrol.** Tentukan tegangan dan arus untuk MCU, LCD, serta modul relay. Pastikan catu daya terisolasi dari jaringan listrik dan logika tidak terpapar tegangan berbahaya.
3. **Proteksi jaringan listrik.** Fuse/overcurrent protection, terminal tertutup, enclosure yang layak, strain relief dan penanganan kabel harus dipertimbangkan oleh orang yang kompeten.
4. **Interlock pintu.** Limit switch satu buah dapat dibaca melalui input digital MCU dengan pull-up/pull-down yang sesuai; multiplexer analog/digital tidak diperlukan untuk satu saklar. Namun, untuk sumber UV-C, jangan menjadikan firmware sebagai satu-satunya pengaman. Pertimbangkan mekanisme pemutus energi independen yang fail-safe dan membuat sumber UV padam saat pintu terbuka atau rangkaian interlock gagal.
5. **Tombol emergency/stop dan indikator.** Tentukan cara menghentikan operasi serta membedakan status standby, aktif, selesai, dan fault.
6. **Pengukuran UV-C.** Daya listrik lampu (W) bukan dosis UV pada permukaan. Dosis dipengaruhi irradiance dan waktu; geometri, jarak, material, kontaminasi dan bayangan memengaruhi hasil.
7. **Rangka mekanis modular.** Rak yang dapat diganti harus tidak menghalangi distribusi UV. Bahan rak juga harus tahan terhadap UV, panas, korosi dan prosedur pembersihan.
8. **Ongkir dan pembelian lintas toko.** Harga Rp500–2.000 per resistor/header tidak berarti biaya sistem tinggal nominal itu; minimum pesanan, varian, dan ongkir bisa lebih besar dari harga unit.

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

## 15. Artefak data

- CSV sumber: `hasil_tokopedia_20261017_173836.csv` (hasil scraper lokal, disimpan terpisah dari dokumen ini).
- Catatan konsol scraper: `Pasted text.txt` (menunjukkan beberapa timeout dan hasil query yang tidak relevan).
- Dokumen ini sebaiknya diperbarui ketika harga dicek ulang, model komponen dipilih, dan biaya checkout diketahui.

---
*Dokumen studi awal untuk pendidikan dan eksperimen prototipe. Bukan panduan produksi, sertifikasi, atau jaminan performa sterilisasi.*
