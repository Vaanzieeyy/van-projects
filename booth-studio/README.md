# Metaverse Booth Studio

Aplikasi konsep booth interaktif 6 × 3 m, tinggi awal 3 m. Buka `dist/index.html` langsung di Chrome, Edge, Firefox, atau Safari yang mendukung WebGL. Tidak membutuhkan API key, instalasi, atau koneksi internet untuk dipakai. Sumber font, Three.js, dan seluruh aset sudah dibundel.

## Interaksi

- Drag: putar kamera. Scroll/pinch: zoom. Tombol Perspektif, Depan, Denah mengatur sudut.
- Klik elemen pada model atau daftar untuk melihat detail.
- Ubah lebar 4–8 m, kedalaman 3–5 m, tinggi 2,5–3,5 m.
- Pilih warna aksen, lantai, lampu, posisi meja, podium, ukuran, dan mode dinding transparan.
- Simpan gambar PNG, model GLB, denah SVG atau konfigurasi JSON; JSON dapat diimpor kembali.
- Konfigurasi disimpan di localStorage browser jika diizinkan. Reset mengembalikan ukuran 6 × 3 × 3 m.

## API yang digunakan

Three.js 0.170.0 (WebGLRenderer, Raycaster, OrbitControls) untuk visualisasi dan interaksi; GLTFExporter untuk GLB; Canvas, File/Blob, ResizeObserver dan localStorage dari browser untuk aset, ekspor, serta penyimpanan. Tidak ada koneksi ke API katalog Metaverse atau layanan berbayar.

API integrasi JavaScript tersedia setelah `window.BOOTH.ready === true`:

```js
const saved = window.BOOTH.getConfig(); // {schemaVersion:1, units:'meters', brand:'Metaverse', config:{...}}
window.BOOTH.setConfig({...saved.config, width:7, depth:4}); // divalidasi sebelum diterapkan
window.BOOTH.setCamera('top'); // 'perspective' | 'front' | 'top'
const svg = window.BOOTH.planSVG();
await window.BOOTH.exportGLB(); // memicu unduhan browser; gunakan dari aksi pengguna
```

## Mengembangkan

Node.js 20+; jalankan `npm ci`, lalu `npm run build`. Hasilnya `dist/index.html`. `index.template.html` berisi UI; `app.js` berisi model dan logika. Untuk hosting, unggah isi `dist` ke hosting statis. Tidak ada backend atau secret. Tautan unduh GitHub menyediakan file, bukan hosting aplikasi aktif.

## Batas konsep

Model bersatuan meter. Koper adalah geometri ilustratif, bukan replika katalog presisi. Identitas merek berupa wordmark teks. Detail konstruksi, aksesibilitas, jarak aman, listrik dan struktur harus ditinjau vendor event. Render lampu bukan analisis pencahayaan. Ruang penyimpanan 1 × 1 m dan meja 1,4 × 0,6 m; dimensi model termasuk beberapa ketebalan konstruksi konseptual. GLB berisi booth tanpa lantai lingkungan, garis ukur, atau kotak seleksi.

## Validasi

Diuji di Chromium: render, ukuran/warna/posisi meja, seleksi objek, tampilan denah, ekspor PNG/GLB/JSON/SVG, impor valid, penolakan ukuran tidak valid, pemulihan localStorage, dan tata letak mobile. GLB terverifikasi sebagai glTF biner versi 2. Hasil pengujian API dan interaksi tidak menggantikan review vendor.
