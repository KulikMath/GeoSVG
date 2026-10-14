# 📐 GeoSVG.js

**Pustaka Geometri SVG Berbahasa Indonesia yang Ringan, Cepat, dan Tanpa Dependensi Wajib.**

![Versi](https://img.shields.io/badge/versi-v0.0.3--beta-ea580c)
![Status](https://img.shields.io/badge/status-Beta%20Publik-f59e0b)
![Ukuran](https://img.shields.io/badge/dependensi-0%20(murni%20JS)-16a34a)
![Format](https://img.shields.io/badge/modul-UMD%20%7C%20ESM%20%7C%20CommonJS-7e22ce)
![Lisensi](https://img.shields.io/badge/lisensi-MIT-2563eb)

> ⚠️ **Catatan Rilis Beta (`v0.0.3`):**  
> **GeoSVG.js** saat ini masih berada dalam tahap **Beta** dan terus dikembangkan secara aktif. Kami sangat mengharapkan **perbaikan, saran fitur, maupun kritik membangun** dari Anda! Jika Anda menemukan *bug* atau punya ide penyempurnaan API, silakan buka laporan di halaman [**GitHub Issues**](https://github.com/KulikMath/GeoSVG/issues).

**GeoSVG.js** adalah pustaka JavaScript berbasis DOM/SVG yang dirancang khusus untuk mempermudah pembuatan ilustrasi geometri matematika, bangun datar, sudut, arsiran, konstruksi garis (garis tinggi, garis sumbu, garis bagi, lingkaran luar/dalam), hingga pemetaan grafik fungsi $y = f(x)$ menggunakan API berbahasa Indonesia yang bersih dan intuitif.

Sangat cocok digunakan untuk bahan ajar matematika, soal ujian berbasis web (CBT), blog edukasi, maupun aplikasi visualisasi geometri interaktif.

---

## ✨ Fitur Utama

- 🇮🇩 **API Berbahasa Indonesia & Fleksibel**: Nama method dan opsi mudah dipahami (`buatSegitiga`, `buatSudut`, `buatTitikPotong`, `buatPolaArsir`), serta mendukung berbagai cara pemanggilan koordinat (`(x, y)`, `[x, y]`, maupun `{x, y}`).
- 📈 **Dukungan Koordinat Matematika (`yUp: true`)**: Secara bawaan SVG menggunakan koordinat layar ($Y$ positif ke bawah). Dengan satu opsi `yUp: true`, kanvas berubah mengikuti bidang Kartesius standar ($Y$ positif ke atas) sambil menjaga teks dan rumus LaTeX tetap tegak!
- 🧮 **Gabungan Fungsi Hitung (`hitung...`) & Gambar (`buat...`)**: Tidak perlu menghitung rumus trigonometri atau perpotongan secara manual. Tersedia fungsi komputasi murni seperti `hitungTitikPotong()`, `hitungLingkaranLuar()`, `hitungLingkaranDalam()`, `hitungKakiTegakLurus()`, dan `hitungSudut()`.
- 🗂️ **Manajemen Lapisan (*Layer*) Otomatis**: Elemen otomatis dikelompokkan ke dalam 3 lapisan berurutan dari bawah ke atas: `grid` (kertas berpetak), `shapes` (bangun & garis), dan `labels` (teks & LaTeX) sehingga label tidak pernah tertutup garis/arsiran.
- ➗ **Integrasi Rumus Matematika ($\LaTeX$)**: Mendukung penuh rendering rumus matematika via **KaTeX** maupun **MathJax** melalui method `buatLatex()`.
- 🖼️ **Ekspor Langsung ke SVG & PNG**: Unduh hasil gambar sebagai vektor `.svg` murni atau gambar raster `.png` beresolusi tinggi (dengan pengali skala `scale`).
- ♿ **Ramah Aksesibilitas & Performa Tinggi**: Mendukung `<title>`, `<desc>`, atribut `aria-*`, serta fitur `batch()` berbasis `DocumentFragment` untuk menggambar ribuan elemen sekaligus tanpa membebani DOM.

---

## 📦 Instalasi & Penggunaan Dasar

### 1. Melalui CDN jsDelivr (Paling Cepat — Tanpa Unduh File)

Anda dapat langsung memuat versi beta terbaru (`v0.0.3`) melalui CDN jsDelivr di dalam halaman HTML Anda:

```html
<script src="https://cdn.jsdelivr.net/gh/KulikMath/GeoSVG@0.0.3/GeoSVG.js"></script>
```

Contoh halaman HTML lengkap menggunakan CDN:

```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Contoh GeoSVG.js (v0.0.3 Beta)</title>
  <!-- Opsional: Muat KaTeX jika ingin menggunakan fitur buatLatex() -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
  <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
</head>
<body>

  <!-- 1. Siapkan elemen wadah (container) -->
  <div id="kanvas-geometri"></div>

  <!-- 2. Muat GeoSVG.js via CDN jsDelivr -->
  <script src="https://cdn.jsdelivr.net/gh/KulikMath/GeoSVG@0.0.3/GeoSVG.js"></script>
  <script>
    // 3. Inisialisasi kanvas berukuran 400x300 piksel
    const geo = new GeoSVG('kanvas-geometri', 400, 300, {
      margin: 20,
      background: '#f8fafc',
      title: 'Segitiga Siku-Siku'
    });

    // 4. Mulai menggambar!
    geo.buatGrid(25);

    const A = [60, 240], B = [320, 240], C = [60, 60];
    geo.buatSegitiga(A, B, C, {
      fill: '#dbeafe',
      stroke: '#1d4ed8',
      strokeWidth: 2
    });

    geo.buatSiku(C, A, B, { size: 16, stroke: '#dc2626', dot: true });
    geo.buatSudut(A, B, C, { radius: 40, label: 'α', bold: true });

    geo.buatTitik(A, { label: 'A', labelPosition: 'kiri bawah', bold: true });
    geo.buatTitik(B, { label: 'B', labelPosition: 'kanan bawah', bold: true });
    geo.buatTitik(C, { label: 'C', labelPosition: 'kiri atas', bold: true });
  </script>
</body>
</html>
```

### 2. Melalui File Lokal (`<script>`)

Jika Anda ingin bekerja secara *offline*, unduh file `GeoSVG.js` dari repositori ini, simpan di folder proyek Anda, lalu muat dengan tag `<script>`:

```html
<script src="./GeoSVG.js"></script>
```

### 3. Melalui Bundler / Node.js (Vite, Webpack, Next.js, Nuxt)

`GeoSVG.js` dibungkus dengan pola UMD (*Universal Module Definition*) sehingga dapat diimpor menggunakan `import` maupun `require()`.

> **Catatan untuk SSR (Next.js / Nuxt):** Karena `GeoSVG.js` membutuhkan objek `document` browser untuk membangun elemen SVG, pastikan inisialisasi dijalankan di sisi klien (di dalam `useEffect` atau `onMounted`), atau periksa terlebih dahulu dengan `GeoSVG.didukung()`.

```javascript
import GeoSVG from './GeoSVG.js';

if (GeoSVG.didukung()) {
  const geo = new GeoSVG('kanvas-geometri', 500, 400, {
    yUp: true,
    clearContainer: true
  });
}
```

---

## ⚙️ Konstruktor & Sistem Koordinat

### Sintaks Konstruktor

```javascript
const geo = new GeoSVG(containerId, width, height, options);
// atau memasukkan width & height di dalam objek options:
const geo = new GeoSVG(containerId, { width: 400, height: 300, ...options });
```

### Tabel Opsi Konstruktor (`options`)

| Nama Opsi | Alias | Tipe | Nilai Bawaan | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| `margin` | `padding` | `number` | `0` | Menambahkan ruang tepi ekstra di sekeliling `viewBox` agar elemen atau label di pinggir kanvas tidak terpotong. |
| `background` | `backgroundColor` | `string` | `'transparent'` | Warna latar belakang elemen `<svg>`. |
| `yUp` | - | `boolean` | `false` | Jika `true`, membalik arah sumbu $Y$ positif ke **atas** (sesuai buku matematika). Membutuhkan `width`/`height` angka pasti atau `viewBox`. |
| `viewBox` | - | `string \| boolean` | `undefined` | Mengatur sistem koordinat internal SVG, misalnya `'-200 -150 400 300'` untuk menaruh titik $(0,0)$ tepat di tengah kanvas. |
| `defaultStroke` | - | `string` | `'black'` | Warna garis bawaan yang diwariskan ke seluruh elemen di dalam kanvas. |
| `defaultStrokeWidth` | - | `number` | `1` | Ketebalan garis bawaan. |
| `overflow` | - | `string` | `'visible'` | Gaya CSS `overflow` pada elemen `<svg>`. |
| `preserveAspectRatio` | - | `string` | `undefined` | Pengaturan rasio aspek standar SVG (misal `'xMidYMid meet'`). |
| `title` | `judul` | `string` | `''` | Membuat elemen `<title>` dan atribut ARIA untuk aksesibilitas pembaca layar. |
| `description` | `desc`, `deskripsi` | `string` | `''` | Membuat elemen `<desc>` untuk penjelasan detail gambar bagi pembaca layar. |
| `dekoratif` | - | `boolean` | `false` | Jika `true`, menyematkan `aria-hidden="true"` pada SVG (dilewati pembaca layar). |
| `clearContainer` | - | `boolean` | `false` | Menghancurkan instance `GeoSVG` lama di wadah yang sama dan mengosongkan isi HTML wadah sebelum menggambar. |
| `strict` | - | `boolean` | `false` | Jika `true`, kesalahan parameter akan langsung melempar `Error` (*throw*), bukan sekadar `console.warn`. |

---

## 🎨 Opsi Gaya Umum & Penempatan Posisi

### 1. Opsi Gaya Visual (Berlaku pada Semua Fungsi `buat...`)

Semua method pembuatan bangun/garis menerima objek `options` di argumen terakhir yang mendukung properti berikut:

| Properti | Tipe | Contoh Nilai | Keterangan |
| :--- | :--- | :--- | :--- |
| `stroke` | `string` | `'#2563eb'`, `'red'` | Warna garis tepi. |
| `strokeWidth` | `number` | `2`, `1.5` | Ketebalan garis tepi dalam piksel. |
| `fill` | `string` | `'#dbeafe'`, `'url(#arsir1)'` | Warna isi bangun datar (bawaan: `'none'`). |
| `dashed` | `boolean \| number \| string` | `true`, `5`, `'8 3 2 3'` | Pintasan garis putus-putus: `true` menghasilkan `'6 4'`, angka `n` menghasilkan `'n n'`, atau string pola kustom. |
| `opacity` | `number` | `0.75` | Transparansi keseluruhan elemen ($0$ s.d. $1$). |
| `fillOpacity` / `strokeOpacity` | `number` | `0.4` | Transparansi khusus warna isi atau garis tepi saja. |
| `strokeLinecap` / `strokeLinejoin` | `string` | `'round'`, `'bevel'` | Bentuk ujung garis dan sambungan sudut garis. |
| `transform` | `string` | `'rotate(30 100 100)'` | Transformasi SVG langsung pada elemen. |
| `id`, `className` (`class`), `dataset` | `string \| Object` | `{ id: 'garis-a', dataset: { sisi: 'miring' } }` | Atribut identitas DOM untuk keperluan styling CSS atau event listener JS. |

### 2. Sistem 9 Arah Posisi Label (Bahasa Indonesia & Inggris)

Saat mengatur `labelPosition` (pada `buatTitik`) atau `position` (pada `buatTeks` dan `buatLatex`), Anda dapat menggunakan istilah bahasa Indonesia maupun bahasa Inggris:

| Bahasa Indonesia | Bahasa Inggris | Keterangan |
| :--- | :--- | :--- |
| `'kiri atas'` | `'top-left'` | Di sebelah kiri-atas titik koordinat |
| `'tengah atas'` | `'top-center'` | Tepat di atas titik koordinat |
| `'kanan atas'` | `'top-right'` | Di sebelah kanan-atas titik koordinat |
| `'kiri tengah'` | `'middle-left'` | Tepat di sebelah kiri titik koordinat |
| `'tengah'` | `'middle-center'` | Tepat berpusat di titik koordinat |
| `'kanan tengah'` | `'middle-right'` | Tepat di sebelah kanan titik koordinat |
| `'kiri bawah'` | `'bottom-left'` | Di sebelah kiri-bawah titik koordinat |
| `'tengah bawah'` | `'bottom-center'` | Tepat di bawah titik koordinat |
| `'kanan bawah'` | `'bottom-right'` | Di sebelah kanan-bawah titik koordinat |

---

## 📚 Referensi Lengkap API (8 Kategori • 45 Fungsi)

### Kategori 0: Lingkungan & Inisialisasi
| Method | Sintaks | Keterangan |
| :--- | :--- | :--- |
| `GeoSVG.didukung()` | `GeoSVG.didukung()` | Method statis yang mengembalikan `true` jika lingkungan memiliki dukungan DOM browser. |
| `new GeoSVG()` | `new GeoSVG(id, w, h, opts)` | Membuat kanvas SVG baru di dalam elemen wadah HTML. |

---

### Kategori 1: Titik & Perpotongan
Fleksibilitas argumen titik: semua parameter titik (`p1`, `p2`, `pusat`) menerima array `[x, y]` maupun objek `{ x, y }`.

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatTitik()` | `geo.buatTitik(x, y, opts)`<br>`geo.buatTitik([x, y], opts)` | Menggambar titik dengan pilihan `marker`: `'full-circle'` (bawaan), `'empty-circle'`, `'diamond'`, atau `'plus'`, dilengkapi opsi `size`, `color`, `label`, `labelPosition`, `labelDistance` (`offset`), `bold`, `dx`, `dy`. |
| `hitungTitikTengah()` | `geo.hitungTitikTengah(p1, p2)` | Mengembalikan koordinat `[mx, my]` titik tengah antara `p1` dan `p2` tanpa menggambarnya. |
| `buatTitikTengah()` | `geo.buatTitikTengah(p1, p2, opts)` | Menghitung sekaligus menggambar titik tengah di antara `p1` dan `p2`. |
| `hitungTitikPotong()` | `geo.hitungTitikPotong(objA, objB, opts)` | Menghitung daftar titik potong `[[x, y], ...]` antara dua objek. Objek dapat berupa **garis** `[p1, p2]` atau **lingkaran** `{ pusat: [x, y], r }`. Isi `{ segmen: true }` jika ingin membatasi perpotongan di dalam ruas segmen saja. |
| `buatTitikPotong()` | `geo.buatTitikPotong(objA, objB, opts)` | Menghitung dan langsung menggambar seluruh titik potong antara `objA` dan `objB`. Opsi `label` bisa diisi array nama, misal `label: ['P', 'Q']`. |
| `buatTitikPotongGaris()` | `geo.buatTitikPotongGaris(l1p1, l1p2, l2p1, l2p2, opts)` | Menggambar titik potong antara garis pertama (`l1p1`–`l1p2`) dan garis kedua (`l2p1`–`l2p2`). |

---

### Kategori 2: Garis, Ruas, & Vektor

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatGaris()` | `geo.buatGaris(p1, p2, opts)`<br>`geo.buatGaris(x1, y1, x2, y2, opts)` | Menggambar garis lurus tak hingga yang menembus `p1` dan `p2` (otomatis dipotong rapi di tepi area gambar). |
| `buatSegmen()` | `geo.buatSegmen(p1, p2, opts)`<br>`geo.buatSegmen(x1, y1, x2, y2, opts)` | Menggambar ruas garis terbatas dari titik `p1` ke `p2`. |
| `buatVektor()` | `geo.buatVektor(p1, p2, opts)`<br>`geo.buatVektor(x1, y1, x2, y2, opts)` | Menggambar ruas garis berarah dengan mata panah di titik ujung `p2`. Warna panah otomatis mengikuti `stroke`. |
| `buatGarisSejajar()` | `geo.buatGarisSejajar(refP1, refP2, lewatAtauJarak, opts)` | Menggambar garis tak hingga yang sejajar garis `refP1`–`refP2`. Argumen ke-3 bisa berupa titik `[x, y]` yang dilalui atau angka jarak geser (*offset*). |
| `buatSegmenSejajar()` | `geo.buatSegmenSejajar(refP1, refP2, lewatAtauJarak, opts)` | Menggambar ruas garis sejajar `refP1`–`refP2`. Panjang ruas dapat diatur melalui `opts.length`. |
| `hitungKakiTegakLurus()` | `geo.hitungKakiTegakLurus(p, a, b)` | Mengembalikan koordinat `[x, y]` proyeksi tegak lurus (kaki garis tinggi) dari titik `p` ke garis `a`–`b`. |
| `buatGarisTegakLurus()` | `geo.buatGarisTegakLurus(p1, p2, lewat, opts)` | Menggambar garis lurus tak hingga yang tegak lurus terhadap `p1`–`p2`. Argumen `lewat` bernilai bawaan `'tengah'` (garis sumbu) atau dapat diisi titik `[x, y]`. |
| `hitungGarisBagi()` | `geo.hitungGarisBagi(p1, vertex, p3)` | Mengembalikan `{ titik: [vx, vy], arah: [ux, uy] }` berupa titik sudut dan vektor satuan arah garis bagi sudut $\angle(\text{p1}, \text{vertex}, \text{p3})$. |
| `buatGarisBagi()` | `geo.buatGarisBagi(p1, vertex, p3, opts)` | Menggambar ruas garis bagi sudut dari `vertex`. Gunakan `opts.panjang` (bawaan `100`) atau `opts.sampai` (misal `sampai: [B, C]` agar berhenti tepat di sisi hadapannya). |

---

### Kategori 3: Bangun Datar & Poligon

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatSegitiga()` | `geo.buatSegitiga(p1, p2, p3, opts)`<br>`geo.buatSegitiga(x1, y1, x2, y2, x3, y3, opts)` | Menggambar segitiga dari 3 titik sudut. Mendukung opsi `sideLabels: ['a', 'b', 'c']`. |
| `buatPersegi()` | `geo.buatPersegi(titikKiriAtas, sisi, opts)`<br>`geo.buatPersegi(x, y, sisi, opts)` | Menggambar persegi dengan panjang sisi tertentu. |
| `buatPersegiPanjang()` | `geo.buatPersegiPanjang(titikKiriAtas, w, h, opts)`<br>`geo.buatPersegiPanjang(x, y, w, h, opts)` | Menggambar persegi panjang dengan lebar `w` dan tinggi `h`. |
| `buatPoligon()` | `geo.buatPoligon(points, opts)` | Menggambar poligon tertutup dari array titik `[[x1, y1], [x2, y2], ...]`. Mendukung `sideLabels` dan `labelOffset`. |
| `buatPoligonBeraturan()` | `geo.buatPoligonBeraturan(pusat, radius, sides, opts)` | Menggambar segi-$n$ beraturan (`sides` $\ge 3$). Sudut titik pertama dapat diputar dengan `opts.startAngle` (dalam derajat). |
| `buatPolyline()` | `geo.buatPolyline(points, opts)` | Menggambar garis patah terbuka yang menghubungkan daftar titik. Isi `opts.panah = true` untuk memberi panah di ujung akhir. |

---

### Kategori 4: Lingkaran, Busur, & Kurva

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatLingkaran()` | `geo.buatLingkaran(pusat, r, opts)`<br>`geo.buatLingkaran(cx, cy, r, opts)` | Menggambar lingkaran dengan pusat dan jari-jari `r`. |
| `buatElips()` | `geo.buatElips(pusat, rx, ry, opts)`<br>`geo.buatElips(cx, cy, rx, ry, opts)` | Menggambar elips dengan jari-jari mendatar `rx` dan tegak `ry`. |
| `hitungLingkaranLuar()` | `geo.hitungLingkaranLuar(p1, p2, p3)` | Menghitung `{ pusat: [x, y], r }` lingkaran luar segitiga (*circumcircle*). |
| `buatLingkaranLuar()` | `geo.buatLingkaranLuar(p1, p2, p3, opts)` | Menggambar lingkaran luar yang melalui ketiga titik sudut segitiga. Isi `opts.titikPusat = true` dan `opts.labelPusat = 'O'` untuk menampilkan titik pusatnya. |
| `hitungLingkaranDalam()` | `geo.hitungLingkaranDalam(p1, p2, p3)` | Menghitung `{ pusat: [x, y], r }` lingkaran dalam segitiga (*incircle*). |
| `buatLingkaranDalam()` | `geo.buatLingkaranDalam(p1, p2, p3, opts)` | Menggambar lingkaran dalam yang menyinggung ketiga sisi segitiga. Mendukung `titikPusat` dan `labelPusat`. |
| `buatSetengahLingkaran()` | `geo.buatSetengahLingkaran(p1, p2, opts)` | Menggambar setengah lingkaran dengan `p1`–`p2` sebagai diameter. Opsi: `sisi: 'kiri' \| 'kanan'`, `tutup: true \| false`. |
| `buatBusur()` | `geo.buatBusur(pusat, r, startAngle, endAngle, opts)` | Menggambar lengkungan busur lingkaran (sudut dalam derajat). Opsi `sweep: 1 \| 0` mengatur arah putaran. |
| `buatJuring()` | `geo.buatJuring(pusat, r, startAngle, endAngle, opts)` | Menggambar juring lingkaran (*sector* / potongan kue) tertutup. |
| `buatTembereng()` | `geo.buatTembereng(pusat, r, startAngle, endAngle, opts)` | Menggambar tembereng lingkaran (*segment* antara busur dan tali busur). |
| `buatKurvaBezier()` | `geo.buatKurvaBezier(points, opts)` | Menggambar kurva Bezier Kuadratik (3 titik) atau Kubik (4 titik). |
| `buatKurvaHalus()` | `geo.buatKurvaHalus(points, opts)` | Menggambar kurva *smooth spline* (seperti grafik lengkung Excel) yang melewati semua titik. Kelengkungan diatur lewat `opts.tension` (bawaan `0.2`). |

---

### Kategori 5: Sudut, Penanda, & Arsir

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `hitungSudut()` | `geo.hitungSudut(p1, vertex, p3, opts)` | Menghitung besar sudut $\angle(\text{p1}, \text{vertex}, \text{p3})$ dalam derajat. Opsi: `refleks: true` ($180^\circ\text{–}360^\circ$), `desimal: 2`. |
| `buatSudut()` | `geo.buatSudut(p1, p2, p3, opts)` | Menggambar busur penanda sudut pada titik puncak `p2`. Opsi: `radius` (`30`), `refleks` (`false`), `label`, `labelRadius`, `labelColor` (`color`), `fill`. |
| `buatSiku()` | `geo.buatSiku(p1, p2, p3, opts)` | Menggambar simbol sudut siku-siku ($90^\circ$) pada titik sudut `p2`. Opsi: `size` (`15`), `dot` (`true`/`false` untuk titik di tengah siku), `fill`, `label`. |
| `buatTandaSamaPanjang()` | `geo.buatTandaSamaPanjang(p1, p2, opts)` | Menggambar strip penanda sisi sama panjang (*tick marks*) di tengah ruas `p1`–`p2`. Opsi: `count` (alias: `ticks`, `jumlah`), `size` (`length`, `panjang`), `spacing` (`gap`, `jarak`), `stroke` (`color`). |
| `buatDimensi()` | `geo.buatDimensi(p1, p2, offset, label, opts)` | Menggambar garis ukur dimensi berpanah dua arah beserta garis batas ekstensi dan teks ukuran `label` sejauh `offset` dari `p1`–`p2`. |
| `buatPolaArsir()` | `geo.buatPolaArsir(id, tipe, opts)` | Mendaftarkan `<pattern>` arsiran di `<defs>`. Pilihan `tipe`: `'miring'`, `'vertikal'`, `'horizontal'`, `'silang'`. Gunakan pada bangun datar dengan `fill: 'url(#id)'`. |

---

### Kategori 6: Teks, Label, & LaTeX

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatTeks()` | `geo.buatTeks(x, y, teks, opts)`<br>`geo.buatTeks([x, y], teks, opts)` | Menampilkan teks pada lapisan `'labels'`. Opsi: `position` (9 arah posisi), `fill` (`color`), `fontSize`, `fontFamily`, `bold`. |
| `buatLatex()` | `geo.buatLatex(x, y, latexString, opts)`<br>`geo.buatLatex([x, y], latexString, opts)` | Merender rumus matematika LaTeX menggunakan KaTeX atau MathJax. Elemen hasil memiliki properti `.ready` (`Promise`) yang selesai ketika rumus telah diukur dan diposisikan. |
| `buatLabelSisi()` | `geo.buatLabelSisi(p1, p2, teks, opts)` | Menaruh label di tengah sisi `p1`–`p2`. Jika `teks` diisi `'auto'` atau `null`, otomatis menampilkan panjang sisi (dapat dikalikan `opts.skala`, dibulatkan `opts.desimal`, dan diberi `opts.satuan`). |
| `buatLabelSisiPoligon()` | `geo.buatLabelSisiPoligon(titik, daftarTeks, opts)` | Memberi label pada semua sisi poligon sekaligus dan otomatis menempatkannya di sisi luar poligon (menjauhi titik pusat poligon). |

---

### Kategori 7: Sistem Koordinat & Grafik

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatGrid()` | `geo.buatGrid(stepX, stepY, opts)` | Menggambar kertas berpetak (*grid*) di lapisan paling bawah menggunakan satu elemen `<path>` yang sangat ringan. |
| `buatSumbuKoordinat()` | `geo.buatSumbuKoordinat(xMin, xMax, yMin, yMax, step, opts)` | Menggambar sumbu Kartesius $X$ dan $Y$ lengkap dengan panah ujung, garis *tick*, dan angka skala setiap kelipatan `step`. |
| `buatFungsi()` | `geo.buatFungsi(f, xMin, xMax, opts)` | Menggambar kurva fungsi matematika `f` (misal `x => Math.sin(x)`) dari `xMin` ke `xMax`. Opsi: `skala`, `skalaX`, `skalaY`, `langkah` (`200`), `maksLompatan` (pemutus otomatis asimtot). |

---

### Kategori 8: Lapisan, Grup, DOM, & Ekspor

| Method | Sintaks | Nilai Kembalian & Keterangan |
| :--- | :--- | :--- |
| `buatGrup()` | `geo.buatGrup(elements, opts)` | Menggabungkan array elemen SVG ke dalam satu grup `<g>`. |
| `hapus()` | `geo.hapus(element)` | Menghapus elemen tertentu dari kanvas SVG. |
| `pindahKeAtas()` / `pindahKeBawah()` | `geo.pindahKeAtas(element)`<br>`geo.pindahKeBawah(element)` | Mengatur urutan tumpukan (*z-order*) elemen ke paling depan atau paling belakang di dalam lapisan/grupnya. |
| `pindahKeLapisan()` | `geo.pindahKeLapisan(element, namaLapisan)` | Memindahkan elemen ke lapisan lain (`'grid'`, `'shapes'`, `'labels'`, atau lapisan baru). |
| `batch()` | `geo.batch(g => { ... })` | Mengumpulkan pembuatan elemen di memori (`DocumentFragment`) dan merendernya sekali saja ke DOM. Tersedia juga `mulaiBatch()` dan `selesaiBatch()`. |
| `setJudul()` / `setDeskripsi()` | `geo.setJudul(teks)`<br>`geo.setDeskripsi(teks)` | Mengubah atau menghapus `<title>` dan `<desc>` SVG secara dinamis beserta atribut ARIA-nya. |
| `keStringSVG()` | `geo.keStringSVG()` | Mengembalikan string kode XML SVG lengkap. |
| `downloadSVG()` | `geo.downloadSVG('nama.svg')` | Mengunduh gambar kanvas langsung sebagai file `.svg`. |
| `toPNGBlob()` | `await geo.toPNGBlob(opts)` | Mengonversi kanvas SVG menjadi `Promise<Blob>` gambar PNG. Opsi: `scale` (`2`), `background`, `tanpaLatex` (`true`/`false`). |
| `downloadPNG()` | `await geo.downloadPNG('nama.png', scaleAtauOpts)` | Mengunduh gambar kanvas langsung sebagai file `.png` beresolusi tajam. |
| `clear()` | `geo.clear()` | Mengosongkan seluruh gambar di semua lapisan tanpa merusak instance kanvas. |
| `destroy()` | `geo.destroy()` | Melepas elemen `<svg>` dari DOM dan membersihkan memori sepenuhnya. |

---

## 💡 Contoh Studi Kasus Lengkap

### Studi Kasus 1: Konstruksi Garis Tinggi, Lingkaran Dalam, dan Arsiran Segitiga

```javascript
const geo = new GeoSVG('kanvas', 420, 300, {
  margin: 20,
  background: '#ffffff'
});

// 1. Buat pola arsir miring berwarna biru lembut
geo.buatPolaArsir('arsir-dalam', 'miring', {
  size: 8,
  color: '#3b82f6',
  strokeWidth: 1
});

// 2. Titik-titik sudut segitiga ABC
const A = [50, 240], B = [360, 240], C = [140, 40];
geo.buatSegitiga(A, B, C, { stroke: '#0f172a', strokeWidth: 2 });

// 3. Lingkaran dalam segitiga dengan arsiran
geo.buatLingkaranDalam(A, B, C, {
  fill: 'url(#arsir-dalam)',
  stroke: '#1d4ed8',
  strokeWidth: 2,
  titikPusat: true,
  labelPusat: 'I'
});

// 4. Garis tinggi dari C tegak lurus ke sisi AB
const D = geo.hitungKakiTegakLurus(C, A, B);
geo.buatSegmen(C, D, { stroke: '#dc2626', dashed: true, strokeWidth: 1.5 });
geo.buatSiku(C, D, B, { size: 14, stroke: '#dc2626' });

// 5. Label titik dan panjang sisi
geo.buatTitik(A, { label: 'A', labelPosition: 'kiri bawah', bold: true });
geo.buatTitik(B, { label: 'B', labelPosition: 'kanan bawah', bold: true });
geo.buatTitik(C, { label: 'C', labelPosition: 'tengah atas', bold: true });
geo.buatTitik(D, { label: 'D', labelPosition: 'tengah bawah', color: '#dc2626' });

geo.buatDimensi(A, B, 28, '31 cm', { stroke: '#475569' });
```

### Studi Kasus 2: Grafik Fungsi Trigonometri & Kuadrat pada Koordinat Kartesius (`yUp: true`)

```javascript
const geo = new GeoSVG('kanvas-grafik', 500, 360, {
  viewBox: '-250 -180 500 360',
  yUp: true,
  background: '#f8fafc'
});

// Skala: 1 satuan matematika = 40 piksel layar
const skala = 40;

geo.buatGrid(skala, skala, { stroke: '#e2e8f0' });
geo.buatSumbuKoordinat(-220, 220, -150, 150, skala);

// Gambar kurva y = sin(x) dan parabola y = 0.25*x^2 - 2
geo.buatFungsi(x => Math.sin(x), -5, 5, {
  skala,
  stroke: '#dc2626',
  strokeWidth: 2.5
});

geo.buatFungsi(x => 0.25 * x * x - 2, -4, 4, {
  skala,
  stroke: '#2563eb',
  strokeWidth: 2.5
});

// Tambahkan keterangan rumus dengan LaTeX
geo.buatLatex([80, 110], 'f(x) = \\frac{1}{4}x^2 - 2', {
  color: '#2563eb',
  fontSize: '15px'
});
geo.buatLatex([-210, 60], 'g(x) = \\sin(x)', {
  color: '#dc2626',
  fontSize: '15px'
});
```

---

## 📖 Dokumentasi Interaktif Offline

Repositori ini juga dilengkapi dengan file **`dokumentasi_geosvg.html`** yang dapat langsung Anda buka di browser (tanpa server lokal) untuk menjelajahi setiap kategori dan menguji kode seluruh 45 fungsi secara *live* di dalam editor interaktif.

---

## 💬 Masukan, Saran, & Kontribusi (Tahap Beta)

Karena **GeoSVG.js** masih berada pada tahap **Beta (`v0.0.3`)**, masukan dari para pendidik, pelajar, dan pengembang web sangat berarti untuk mematangkan pustaka ini menuju versi stabil (`v1.0.0`).

Anda dapat berpartisipasi dengan cara:
1. 🐛 **Melaporkan Bug / Kendala**: Jika ada fungsi yang tidak berjalan semestinya atau perhitungan geometri yang kurang tepat, silakan buat laporan di [**GitHub Issues**](https://github.com/KulikMath/GeoSVG/issues).
2. 💡 **Mengusulkan Fitur / Nama Method Baru**: Punya ide bangun geometri atau konstruksi matematika lain yang sering dipakai di soal sekolah? Sampaikan saran Anda!
3. 🔧 **Pull Request (PR)**: Perbaikan kode, peningkatan performa, maupun penambahan contoh dokumentasi sangat terbuka untuk dikirimkan melalui *Pull Request*.

---

## 📄 Lisensi

Didistribusikan di bawah Lisensi **MIT**. Anda bebas menggunakan, memodifikasi, dan mendistribusikan pustaka ini untuk keperluan pribadi, pendidikan, maupun komersial.
