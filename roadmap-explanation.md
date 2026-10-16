# 🚀 ROADMAP FULL STACK JAVASCRIPT V2 (Versi Lengkap + Cara Membaca Kode)

Dokumen ini adalah versi yang dilengkapi dari roadmap awal. Setiap materi punya:
- **Penjelasan** singkat (apa & kenapa)
- **Contoh kode**
- **🔍 Cara membaca kode** (urutan membaca, supaya tidak bingung)

Materi bertanda 🆕 adalah **tambahan baru** yang tidak ada di roadmap awal.

---

## 📌 DAFTAR ISI
0. [Evaluasi: Apa yang Kurang dari Roadmap Awal](#0-evaluasi-apa-yang-kurang-dari-roadmap-awal)
1. [Cara Membaca Kode (Aturan Umum)](#1-cara-membaca-kode-aturan-umum)
2. [Phase 0 🆕: Fondasi Lingkungan Kerja](#phase-0--fondasi-lingkungan-kerja-minggu-1-2)
3. [Phase 1: JavaScript Modern & Asynchronous](#phase-1-javascript-modern--asynchronous-bulan-1)
4. [Phase 2: Tailwind & React](#phase-2-tailwind--react-bulan-2-3)
5. [Phase 3: TypeScript & Next.js](#phase-3-typescript--nextjs-bulan-4-5)
6. [Phase 4: Database, Backend & Keamanan](#phase-4-database-backend--keamanan-bulan-6-7)
7. [Phase 5: Capstone, Testing & Deployment](#phase-5-capstone-testing--deployment-bulan-8)
8. [Phase 6 🆕: Persiapan Karier](#phase-6--persiapan-karier-berjalan-paralel)
9. [Glosarium](#glosarium-ringkas)

---

# 0. Evaluasi: Apa yang Kurang dari Roadmap Awal

Secara urutan, roadmap awal sudah bagus (JS → UI → framework → database → proyek). Tapi ada celah yang biasanya baru terasa saat sudah mulai kerja:

| # | Yang Kurang | Kenapa Penting | Ditaruh di |
|---|---|---|---|
| 1 | **Terminal, Node.js & npm** | Semua tool (Next.js, Prisma, Git) dijalankan dari terminal. Tanpa ini, tutorial manapun akan macet di langkah 1. | Phase 0 |
| 2 | **HTML/CSS/DOM refresher** | Roadmap langsung ke Tailwind & React, padahal React hanyalah cara lain mengelola DOM. | Phase 0 |
| 3 | **Debugging & Browser DevTools** | Skill yang paling membedakan pemula dan developer: membaca error dan menelusuri bug. | Phase 0 |
| 4 | **Modul `import`/`export`, JSON, optional chaining, template literal** | Muncul di setiap file Next.js tapi tidak disebut sama sekali. | Phase 1 |
| 5 | **Scope & Closure** | Dasar untuk memahami hooks React. Kamu bertanya soal scope, jadi ini memang konsep kunci. | Phase 1 |
| 6 | **HTTP dasar (method, status code, header, CORS)** | Fetch/Axios dan API Routes tidak akan paham tanpa ini. | Phase 1 |
| 7 | **Hook lanjutan: `useRef`, Context, custom hook** | `useState` + `useEffect` saja tidak cukup untuk aplikasi nyata. | Phase 2 |
| 8 | **Conditional rendering, `key` pada list, loading/error state** | Dipakai di setiap halaman yang menampilkan data. | Phase 2 |
| 9 | **Validasi dengan Zod + React Hook Form** | Standar industri untuk form. Validasi manual cepat jadi berantakan. | Phase 2/3 |
| 10 | **SQL mentah dasar (JOIN, GROUP BY, index)** | Prisma itu bungkus SQL. Saat query lambat atau error, kamu harus paham SQL di baliknya. | Phase 4 |
| 11 | **Keamanan dasar (OWASP, XSS, SQL injection, CORS, rate limit)** | Roadmap hanya menyebut login. Aplikasi yang tidak aman tidak layak masuk portofolio. | Phase 4 |
| 12 | **Testing dasar (Vitest/Jest, Playwright)** | Perusahaan menilai kemampuan menulis kode yang bisa dites. | Phase 5 |
| 13 | **ESLint, Prettier, dan pesan commit yang rapi** | Standar kerja tim. Mudah dipelajari, dampak profesionalismenya besar. | Phase 0/5 |
| 14 | **Git workflow tim (Pull Request, merge conflict)** | Di tempat PKL kamu pasti kerja bareng. `commit/push/branch` saja belum cukup. | Phase 1 |
| 15 | **Dasar algoritma & struktur data** | Dipakai di tes teknis rekrutmen. Cukup dasar saja. | Phase 6 |
| 16 | **Bahasa Inggris teknis** | Dokumentasi dan error message hampir seluruhnya berbahasa Inggris. | Phase 6 |
| 17 | **CV, GitHub profile, LinkedIn, soft skill** | Tujuan akhir roadmap adalah dapat kerja, tapi persiapannya belum ada. | Phase 6 |

### ⚠️ Inkonsistensi kecil di roadmap awal (perlu dirapikan)
1. **Phase 5 menyebut MongoDB Atlas**, padahal seluruh stack memakai PostgreSQL. Pakai **Supabase (PostgreSQL)** saja agar konsisten.
2. **`tailwind.config.js`**: pada Tailwind versi 4, kustomisasi banyak dipindah ke file CSS. Cek versi yang kamu pasang dan ikuti dokumentasinya.
3. **Auth.js (NextAuth)**: ekosistem autentikasi di Next.js sedang berkembang (ada alternatif seperti Better Auth dan Supabase Auth). Cek dokumentasi terbaru sebelum memilih, dan pilih satu saja.
4. **Beban Bulan 1 terlalu padat** (JS modern + async + fetch + Git dalam satu bulan sambil PKL). Karena itu saya tambahkan Phase 0 dan beri ruang ±2 minggu.
5. **Tidak ada kriteria "selesai"** per fase. Di versi ini tiap fase punya **mini-proyek** sebagai tolok ukur.

---

# 1. Cara Membaca Kode (Aturan Umum)

Banyak pemula merasa kode "sulit dibaca" karena membacanya seperti novel, dari kiri ke kanan, atas ke bawah. Kode sebaiknya dibaca dengan strategi berikut.

### Aturan 1: Baca tanda `=` dari KANAN ke KIRI
Tanda `=` bukan "sama dengan", tapi **"simpan hasil sisi kanan ke sisi kiri"**.
```js
const total = harga * jumlah;
```
🔍 Baca: "Hitung `harga` kali `jumlah`, lalu simpan hasilnya ke variabel bernama `total`."

### Aturan 2: Baca dari DALAM ke LUAR untuk pemanggilan bertingkat
```js
console.log(Math.max(...angka.map(n => n * 2)));
```
🔍 Baca dari yang paling dalam:
1. `angka.map(n => n * 2)` → kalikan tiap angka 2, hasilnya array baru.
2. `...` → sebar array itu jadi argumen terpisah.
3. `Math.max(...)` → cari yang terbesar.
4. `console.log(...)` → cetak hasilnya.

### Aturan 3: Baca rantai titik (`.`) satu per satu, urut dari kiri
```js
produk.filter(p => p.stok > 0).map(p => p.nama).sort();
```
🔍 Baca: "Ambil `produk` → **saring** yang stoknya > 0 → **ambil namanya saja** → **urutkan**." Tiap `.metode()` menerima hasil dari langkah sebelumnya (seperti pipa air).

### Aturan 4: Panah `=>` dibaca "menghasilkan / lalu"
```js
const kuadrat = (n) => n * n;
```
🔍 Baca: "`kuadrat` adalah fungsi: **jika diberi `n`, maka menghasilkan `n * n`**."

### Aturan 5: Kurung `( )`, kurung kurawal `{ }`, kurung siku `[ ]` punya arti berbeda

| Simbol | Dibaca sebagai | Contoh |
|---|---|---|
| `( )` | argumen / pengelompokan | `tambah(1, 2)` |
| `{ }` | **blok kode** atau **objek** (tergantung posisi) | `if (x) { ... }` / `{ nama: "Budi" }` |
| `[ ]` | **array** atau akses indeks | `[1,2,3]` / `daftar[0]` |
| `< >` | tag JSX atau tipe generic TypeScript | `<Card />` / `Array<string>` |

### Aturan 6: Pertama cari "pintu masuk", jangan baca semua baris
Saat membuka file asing:
1. Lihat `import` di atas → file ini memakai apa?
2. Lihat `export` → apa yang disediakan file ini?
3. Cari fungsi utama (di React: fungsi yang `return` JSX).
4. Baru telusuri detailnya.

### Aturan 7: Baca pesan error dari ATAS dan cari nama file milikmu
```
TypeError: Cannot read properties of undefined (reading 'nama')
    at KartuProduk (app/produk/page.tsx:12:20)
    at renderWithHooks (node_modules/react-dom/...)
```
🔍 Baca:
- Baris 1 = **apa yang salah**: kamu mencoba membaca `.nama` dari sesuatu yang `undefined`.
- Baris 2 = **di mana**: file `app/produk/page.tsx` baris 12 kolom 20 (file milikmu).
- Baris `node_modules/...` biasanya bukan sumber masalahnya, abaikan dulu.

### Aturan 8: Gunakan notasi "baca keras-keras" (rubber duck)
Jelaskan tiap baris dengan kalimat sendiri. Kalau tidak bisa dijelaskan, berarti belum paham.

---

# PHASE 0 🆕: Fondasi Lingkungan Kerja (Minggu 1-2)

## 0.1 Terminal / Command Line

Terminal adalah tempat kamu memberi perintah ke komputer lewat teks. Perintah dasar:

```bash
pwd                 # tampilkan folder saat ini
ls                  # lihat isi folder
cd belajar-js       # masuk ke folder
cd ..               # naik satu folder
mkdir proyek-baru   # buat folder
```
🔍 **Cara membaca:** tiap baris = `perintah [opsi] [target]`. Teks setelah `#` adalah komentar, bukan bagian perintah. Pola umum: **kata kerja** (`cd`, `mkdir`) lalu **objek yang dikenai** (nama folder).

## 0.2 Node.js & npm

Node.js menjalankan JavaScript di luar browser (di komputer/server). npm adalah "toko paket" untuk library JavaScript.

```bash
node -v                    # cek versi Node
npm init -y                # buat file package.json
npm install axios          # pasang library axios
npm run dev                # jalankan script bernama "dev"
```

```json
{
  "name": "belajar-js",
  "scripts": {
    "dev": "next dev",
    "build": "next build"
  },
  "dependencies": {
    "axios": "^1.7.0"
  }
}
```
🔍 **Cara membaca `package.json`:**
1. `name` → nama proyek.
2. `scripts` → "singkatan perintah". `npm run dev` akan menjalankan `next dev`.
3. `dependencies` → daftar library yang dibutuhkan proyek beserta versinya. `^1.7.0` artinya "versi 1.7.0 atau yang lebih baru di rentang 1.x".
4. Folder `node_modules/` berisi hasil instalasi. **Jangan di-commit ke Git.**

## 0.3 HTML, CSS & DOM Refresher

**DOM** (Document Object Model) adalah struktur pohon halaman web yang bisa diubah JavaScript.

```html
<button id="btn">Klik</button>
<p id="hasil"></p>

<script>
  const tombol = document.getElementById("btn");
  const hasil = document.getElementById("hasil");

  tombol.addEventListener("click", () => {
    hasil.textContent = "Tombol diklik!";
  });
</script>
```
🔍 **Cara membaca:**
1. `getElementById("btn")` → "cari elemen yang `id`-nya `btn`", simpan ke `tombol`.
2. `addEventListener("click", ...)` → "**saat** `tombol` diklik, **jalankan** fungsi ini".
3. Fungsi di dalamnya mengganti teks elemen `hasil`.

Kenapa penting? React pada dasarnya mengotomatiskan pekerjaan di atas. Dengan paham cara manualnya, kamu tahu apa yang React lakukan di balik layar.

Yang perlu dikuasai: Flexbox, Grid, box model (margin, border, padding), selector, dan elemen semantik (`<header>`, `<main>`, `<section>`).

## 0.4 Debugging & Browser DevTools

Tekan **F12** di browser. Tab penting:
- **Console**: melihat error dan hasil `console.log`.
- **Network**: melihat request ke API (status, respons, waktu).
- **Elements**: memeriksa dan mengubah HTML/CSS secara langsung.
- **Sources**: memasang *breakpoint* untuk menghentikan kode di baris tertentu.

```js
function hitungDiskon(harga, persen) {
  console.log("harga:", harga, "persen:", persen);   // cek input
  const diskon = harga * persen / 100;
  console.log("diskon:", diskon);                    // cek hasil
  return harga - diskon;
}
```
🔍 **Cara membaca/menggunakan:** sisipkan `console.log` di titik yang dicurigai, jalankan, lalu bandingkan **nilai yang kamu kira** dengan **nilai sebenarnya**. Bug hampir selalu berada di titik pertama di mana keduanya berbeda.

## 0.5 ESLint & Prettier

- **Prettier**: merapikan format kode otomatis (indentasi, tanda kutip).
- **ESLint**: mendeteksi kode yang berpotensi salah (variabel tidak terpakai, dll).

Aktifkan *format on save* di VS Code. Ini kebiasaan kecil dengan dampak besar.

**🎯 Mini-proyek Phase 0:** halaman HTML + JS murni berisi *to-do list* (tambah, hapus, tandai selesai) tanpa framework.

---

# PHASE 1: JavaScript Modern & Asynchronous (Bulan 1)

## 1.1 ES6+: `let`, `const`

```js
const nama = "Budi";
let umur = 17;
umur = 18;       // boleh
nama = "Andi";   // ERROR
```
🔍 **Cara membaca:** `const` = "konstan, nama ini tidak boleh dipindah ke nilai lain". `let` = "boleh diganti". Catatan: `const` pada objek/array hanya mengunci **penunjuknya**, isinya masih bisa diubah:
```js
const daftar = [1, 2];
daftar.push(3);     // boleh! isi array berubah
daftar = [9];       // ERROR! penunjuk diganti
```

## 1.2 🆕 Scope & Closure

**Scope** = wilayah tempat variabel "terlihat".

```js
const global = "terlihat di mana-mana";

function contoh() {
  const lokal = "hanya di dalam fungsi";
  if (true) {
    const blok = "hanya di dalam blok if ini";
    console.log(global, lokal, blok);  // semua terlihat
  }
  console.log(blok);  // ERROR: blok tidak terlihat di sini
}
console.log(lokal);   // ERROR: lokal tidak terlihat di luar fungsi
```
🔍 **Cara membaca (aturan "kotak boneka matryoshka"):**
- Kode bisa melihat variabel di kotaknya sendiri **dan kotak-kotak di luarnya**.
- Kode **tidak bisa** melihat isi kotak di dalamnya.
- Setiap pasang `{ }` (fungsi, `if`, `for`) membuat kotak baru untuk `let`/`const`.

**Closure** = fungsi yang tetap "mengingat" variabel dari kotak tempat ia lahir, meski kotaknya sudah selesai dijalankan.

```js
function buatPenghitung() {
  let hitung = 0;
  return function () {
    hitung = hitung + 1;
    return hitung;
  };
}

const counterA = buatPenghitung();
console.log(counterA());  // 1
console.log(counterA());  // 2
```
🔍 **Cara membaca:**
1. `buatPenghitung()` membuat variabel `hitung` lalu **mengembalikan fungsi** kecil.
2. Meski `buatPenghitung` sudah selesai, fungsi kecil itu masih **mengingat** `hitung`.
3. Tiap pemanggilan `counterA()` menaikkan `hitung` yang sama.

Hubungannya: `useState` di React bekerja berkat closure.

## 1.3 Arrow Function & Shorthand

```js
function tambah(a, b) { return a + b; }
const tambah2 = (a, b) => a + b;                // satu ekspresi: return otomatis
const tambah3 = (a, b) => { return a + b; };    // pakai { } harus return manual

const nama = "Budi", umur = 17;
const siswa = { nama, umur };    // shorthand dari { nama: nama, umur: umur }
```
🔍 **Cara membaca:** `(a, b) => a + b` → "diberi `a` dan `b`, menghasilkan `a + b`". Jika setelah `=>` ada `{`, itu **blok kode** sehingga butuh `return` eksplisit. Jika tidak, hasilnya langsung dikembalikan.

> ⚠️ Jebakan: mengembalikan objek langsung dengan arrow function perlu tanda kurung: `() => ({ nama: "Budi" })`. Tanpa `( )`, JS mengira `{ }` adalah blok.

## 1.4 Destructuring

```js
const user = { nama: "Budi", kelas: "XII RPL", alamat: { kota: "Surabaya" } };

const { nama, kelas } = user;
const { alamat: { kota } } = user;
const { umur = 17 } = user;         // nilai default jika tidak ada

const warna = ["merah", "biru", "hijau"];
const [pertama, , ketiga] = warna;  // lewati elemen ke-2 dengan koma kosong
```
🔍 **Cara membaca:** bayangkan **bentuk sisi kiri meniru bentuk data di kanan**. `{ nama, kelas }` artinya "ambil properti bernama `nama` dan `kelas` dari `user`, jadikan variabel". Untuk array, **urutan** yang menentukan, bukan nama.

## 1.5 Spread & Rest

```js
const a = [1, 2];
const b = [...a, 3, 4];                     // [1, 2, 3, 4]
const userBaru = { ...user, kota: "Malang" };

function jumlah(...angka) {
  return angka.reduce((total, n) => total + n, 0);
}
jumlah(1, 2, 3);   // 6
```
🔍 **Cara membaca (kunci: lihat posisi `...`):**
- `...` di sisi **pemanggilan / pembuatan data** (`[...a]`) = **spread**: "tuang isinya di sini".
- `...` di sisi **definisi parameter / destructuring** (`function f(...angka)`) = **rest**: "kumpulkan sisanya jadi array".
- Pada `{ ...user, kota: "Malang" }`: tuang semua isi `user`, **lalu timpa** `kota`. Urutan penting: yang belakangan menang.

## 1.6 🆕 Template Literal, Optional Chaining, Nullish Coalescing

```js
const pesan = `Halo ${user.nama}, kamu kelas ${user.kelas}`;

const kota = user?.alamat?.kota;        // aman jika alamat tidak ada
const nama2 = input ?? "Tanpa nama";    // default hanya jika null/undefined
const nama3 = input || "Tanpa nama";    // default jika "falsy" (0, "", false juga)
```
🔍 **Cara membaca:**
- Backtick `` ` `` + `${...}` = teks dengan **ekspresi disisipkan**.
- `?.` = "**jika ada**, lanjut; jika tidak, hentikan dan hasilkan `undefined`" (mencegah error `Cannot read properties of undefined`).
- `??` = "pakai kanan **hanya jika** kiri `null`/`undefined`". Beda dengan `||` yang juga menolak `0` dan `""`.

## 1.7 🆕 Modul: `import` & `export`

```js
// utils/harga.js
export function formatRupiah(angka) {
  return "Rp " + angka.toLocaleString("id-ID");
}
export const PPN = 0.11;
export default function hitungTotal(harga) { return harga * (1 + PPN); }

// halaman.js
import hitungTotal, { formatRupiah, PPN } from "./utils/harga.js";
```
🔍 **Cara membaca:**
- `export` = "izinkan file lain memakai ini".
- `export default` = satu "isi utama" file, di-import **tanpa** kurung kurawal, nama bebas.
- `export` biasa = di-import **dengan** `{ }`, nama harus sama persis.
- `from "./..."` = alamat file (titik berarti folder saat ini). `from "axios"` tanpa titik = library dari `node_modules`.

## 1.8 Array Methods

```js
const produk = [
  { nama: "Kaos", harga: 50000, stok: 5 },
  { nama: "Topi", harga: 30000, stok: 0 },
  { nama: "Jaket", harga: 150000, stok: 2 },
];

const namaSaja = produk.map(p => p.nama);
const tersedia = produk.filter(p => p.stok > 0);
const topi = produk.find(p => p.nama === "Topi");
const total = produk.reduce((jumlah, p) => jumlah + p.harga, 0);
```
🔍 **Cara membaca tiap method:**

| Method | Dibaca sebagai | Hasil |
|---|---|---|
| `.map(p => ...)` | "untuk **setiap** `p`, ubah menjadi ..." | array baru, **jumlah sama** |
| `.filter(p => syarat)` | "**simpan** `p` yang syaratnya benar" | array baru, **jumlah bisa berkurang** |
| `.find(p => syarat)` | "**cari satu** `p` pertama yang cocok" | satu item atau `undefined` |
| `.reduce((acc, p) => ..., awal)` | "mulai dari `awal`, **gabungkan** tiap `p` ke `acc`" | satu nilai |

Membaca `reduce` langkah demi langkah:
```
awal: jumlah = 0
item 1 (Kaos):  0 + 50000      → 50000
item 2 (Topi):  50000 + 30000  → 80000
item 3 (Jaket): 80000 + 150000 → 230000   ← hasil akhir
```
> Tip: `map` & `filter` **tidak mengubah array asli**. Ini penting di React.

## 1.9 🆕 HTTP Dasar & JSON

```
Request:   GET /api/produk/5 HTTP/1.1
Response:  200 OK
           { "id": 5, "nama": "Kaos" }
```
- **Method**: `GET` ambil, `POST` buat, `PUT/PATCH` ubah, `DELETE` hapus.
- **Status**: `2xx` sukses, `3xx` pindah, `4xx` salah dari klien (401 belum login, 403 dilarang, 404 tidak ada), `5xx` salah di server.
- **Header**: info tambahan (`Content-Type`, `Authorization`).
- **CORS**: aturan browser yang membatasi pemanggilan API dari domain berbeda.

```js
const json = '{"nama":"Budi","umur":17}';
const objek = JSON.parse(json);        // teks → objek
const teks = JSON.stringify(objek);    // objek → teks
```
🔍 **Cara membaca:** `parse` = "urai teks menjadi data". `stringify` = "ubah data jadi teks (untuk dikirim)".

## 1.10 Asynchronous JavaScript

### Event Loop
```js
console.log("1");
setTimeout(() => console.log("2"), 0);
console.log("3");
// Output: 1, 3, 2
```
🔍 **Cara membaca:**
1. `"1"` langsung dicetak.
2. `setTimeout` **menitipkan** callback ke antrean, lalu JS lanjut (tidak menunggu).
3. `"3"` dicetak.
4. Setelah semua kode biasa selesai, event loop mengambil callback dari antrean → `"2"`.

Aturan emas: **kode sinkron selalu selesai dulu, baru antrean async diproses.**

### Promise
```js
fetch("https://api.example.com/users")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```
🔍 **Cara membaca:** "Minta data → **lalu** ubah ke JSON → **lalu** cetak → **jika gagal di langkah mana pun**, tangkap di `.catch`." Tiap `.then` menerima hasil `.then` sebelumnya.

### Async/Await
```js
async function ambilUser(id) {
  try {
    const res = await fetch(`/api/users/${id}`);
    if (!res.ok) throw new Error(`Gagal: ${res.status}`);
    const data = await res.json();
    return data;
  } catch (err) {
    console.error(err.message);
    return null;
  } finally {
    console.log("selesai");
  }
}
```
🔍 **Cara membaca:**
1. `async function` → fungsi ini selalu mengembalikan Promise.
2. `await fetch(...)` → "**tunggu di sini** sampai selesai, baru lanjut ke baris berikutnya (halaman tidak hang)".
3. `if (!res.ok) throw ...` → jika respons bukan 2xx, **lempar error** manual.
4. Blok `try` = jalur normal. Jika ada error di dalamnya, lompat ke `catch`.
5. `finally` = **selalu** dijalankan, sukses atau gagal.

### 🆕 Menjalankan beberapa async sekaligus
```js
const [users, produk] = await Promise.all([
  fetch("/api/users").then(r => r.json()),
  fetch("/api/produk").then(r => r.json()),
]);
```
🔍 **Cara membaca:** "Mulai **dua** request **bersamaan**, tunggu **keduanya** selesai, lalu ambil hasilnya (destructuring array)." Lebih cepat daripada dua `await` berurutan.

## 1.11 Fetch API & Axios

```js
// POST dengan fetch
const res = await fetch("/api/produk", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ nama: "Kaos", harga: 50000 }),
});
const hasil = await res.json();

// POST dengan Axios
import axios from "axios";
const { data } = await axios.post("/api/produk", { nama: "Kaos", harga: 50000 });
```
🔍 **Cara membaca `fetch`:** `fetch(ALAMAT, { PENGATURAN })`. Argumen kedua berisi `method` (jenis aksi), `headers` (label pengiriman: "isinya JSON"), dan `body` (isi paketnya, harus teks, makanya `JSON.stringify`).
**Axios:** `axios.post(ALAMAT, DATA)`. Lebih ringkas karena JSON diurus otomatis. `{ data }` adalah destructuring dari objek respons.

## 1.12 Git & GitHub (Termasuk Kerja Tim)

```bash
git init
git add .
git commit -m "feat: tambah halaman login"
git branch fitur-keranjang
git checkout fitur-keranjang
git push origin fitur-keranjang
```
🔍 **Cara membaca alur:** `add` (siapkan perubahan) → `commit` (simpan snapshot + pesan) → `push` (kirim ke GitHub).

**🆕 Alur kerja tim:**
1. Buat branch dari `main` (`git checkout -b fitur-x`).
2. Kerjakan, commit kecil-kecil.
3. Push, lalu buka **Pull Request (PR)** di GitHub.
4. Rekan me-review, lalu **merge**.
5. **Merge conflict**: terjadi saat dua orang mengubah baris yang sama. Git menandai dengan:
```
<<<<<<< HEAD
versi kamu
=======
versi orang lain
>>>>>>> fitur-x
```
🔍 Baca: bagian atas `=======` = milikmu, bagian bawah = milik mereka. Pilih/gabungkan, **hapus ketiga tanda** itu, lalu commit.

**Format pesan commit:** `feat:` (fitur baru), `fix:` (perbaikan bug), `docs:`, `refactor:`.
**Wajib:** buat file `.gitignore` berisi `node_modules`, `.env`, `.next`.

**🎯 Mini-proyek Phase 1:** aplikasi cuaca atau daftar negara memakai API publik: ambil data, filter/cari, tampilkan, dengan penanganan loading & error. Upload ke GitHub dengan README.

---

# PHASE 2: Tailwind & React (Bulan 2-3)

## 2.1 Tailwind CSS

```html
<button class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 md:px-8">
  Simpan
</button>
```
🔍 **Cara membaca:** pisahkan per spasi, tiap kata = satu aturan CSS.

| Kelas | Arti |
|---|---|
| `bg-blue-600` | background biru, tingkat 600 |
| `text-white` | warna teks putih |
| `px-4` / `py-2` | padding kiri-kanan / atas-bawah (angka × 4px) |
| `rounded-lg` | sudut membulat |
| `hover:bg-blue-700` | **saat disorot mouse**, ganti background |
| `md:px-8` | **mulai layar ≥ 768px**, padding jadi lebih besar |

Pola nama: `[varian:]properti-nilai`. Varian (`hover:`, `md:`, `dark:`) di depan = "hanya berlaku pada kondisi itu".

**Responsive (mobile-first):** kelas tanpa prefix berlaku di semua ukuran, prefix hanya **menambah/menimpa** untuk layar lebih besar.
```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
```
🔍 Baca: "grid dengan 1 kolom; **mulai tablet** jadi 2 kolom; **mulai layar besar** jadi 3 kolom; jarak antar-item 4 unit."

## 2.2 React: JSX

```jsx
const nama = "Budi";
const sapaan = (
  <h1 className="text-2xl">
    Halo, {nama}! 2 + 3 = {2 + 3}
  </h1>
);
```
🔍 **Cara membaca:** di dalam tag, teks biasa dibaca sebagai teks. Apa pun di dalam `{ }` dibaca sebagai **JavaScript**. Perbedaan dengan HTML: `class` → `className`, tag harus ditutup (`<img />`), dan satu komponen harus punya **satu elemen pembungkus** (boleh `<> ... </>`).

## 2.3 Komponen & Props

```jsx
function KartuProduk({ nama, harga, stok = 0 }) {
  return (
    <div className="border p-4 rounded">
      <h2>{nama}</h2>
      <p>Rp {harga.toLocaleString("id-ID")}</p>
      <p>Stok: {stok}</p>
    </div>
  );
}

// Dipakai:
<KartuProduk nama="Kaos" harga={50000} />
```
🔍 **Cara membaca:**
1. Nama komponen **selalu huruf besar** (`KartuProduk`). Huruf kecil dianggap tag HTML.
2. Parameter `{ nama, harga, stok = 0 }` = destructuring dari objek `props`; `stok` punya nilai default 0.
3. `return ( ... )` berisi JSX = tampilan yang dihasilkan.
4. Saat dipakai, `nama="Kaos"` (teks pakai kutip) dan `harga={50000}` (non-teks pakai `{ }`) sama seperti pemanggilan `KartuProduk({nama:"Kaos", harga:50000})`.
5. **Props bersifat read-only**: aliran data hanya dari induk ke anak.

## 2.4 🆕 Conditional Rendering & Rendering List

```jsx
function DaftarProduk({ produk, loading }) {
  if (loading) return <p>Memuat...</p>;
  if (produk.length === 0) return <p>Belum ada produk.</p>;

  return (
    <ul>
      {produk.map((p) => (
        <li key={p.id}>
          {p.nama} {p.stok === 0 && <span>(Habis)</span>}
        </li>
      ))}
    </ul>
  );
}
```
🔍 **Cara membaca:**
1. Dua `if` di awal = **penjaga**: tampilkan hal lain lebih dulu jika kondisinya terpenuhi (*early return*).
2. `{produk.map(...)}` = "untuk setiap produk, **buat satu `<li>`**".
3. `key={p.id}` = label unik agar React bisa melacak item mana yang berubah. **Wajib** dan harus unik, jangan pakai indeks array jika urutan bisa berubah.
4. `kondisi && <Elemen />` = "**jika** kondisi benar, tampilkan elemen". Jika salah, tidak menampilkan apa-apa.
5. Alternatif: `kondisi ? <A /> : <B />` = "jika benar tampilkan A, jika tidak B".

## 2.5 State: `useState`

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Hitungan: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tambah</button>
    </div>
  );
}
```
🔍 **Cara membaca:**
1. `useState(0)` → "buat state dengan nilai awal `0`".
2. Hasilnya array berisi dua hal: `[nilai, fungsiPengubah]`, diurai dengan destructuring. Nama `count`/`setCount` bebas, tapi konvensinya `x` dan `setX`.
3. `onClick={() => setCount(count + 1)}` = "**saat diklik**, panggil `setCount` dengan nilai baru".
4. Setelah `setCount` dipanggil, React **menjalankan ulang fungsi `Counter`** dari atas dengan nilai `count` baru, lalu memperbarui layar.

**Aturan penting (immutability):**
```jsx
// ❌ Salah: mengubah langsung
produk.push(baru); setProduk(produk);

// ✅ Benar: buat salinan baru
setProduk([...produk, baru]);                           // tambah
setProduk(produk.filter(p => p.id !== idHapus));        // hapus
setProduk(produk.map(p => p.id === id ? { ...p, selesai: true } : p));  // ubah satu item
```
🔍 Baca baris terakhir: "untuk tiap `p`: **jika** `id`-nya cocok, **ganti dengan salinan** `p` yang `selesai`-nya `true`; **jika tidak**, biarkan `p`."

## 2.6 Side Effect: `useEffect`

```jsx
import { useState, useEffect } from "react";

function ListProduk() {
  const [produk, setProduk] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function muat() {
      try {
        const res = await fetch("/api/produk");
        if (!res.ok) throw new Error("Gagal memuat");
        setProduk(await res.json());
      } catch (e) {
        setError(e.message);
      } finally {
        setLoading(false);
      }
    }
    muat();
  }, []);

  if (loading) return <p>Memuat...</p>;
  if (error) return <p>Error: {error}</p>;
  return <ul>{produk.map(p => <li key={p.id}>{p.nama}</li>)}</ul>;
}
```
🔍 **Cara membaca (urutan eksekusi sebenarnya, bukan urutan penulisan):**
1. Render pertama: `produk=[]`, `loading=true` → layar menampilkan "Memuat...".
2. **Setelah** layar muncul, `useEffect` berjalan → memanggil `muat()`.
3. `muat()` mengambil data → `setProduk(...)` & `setLoading(false)`.
4. Perubahan state memicu render ulang → sekarang tampil daftar produk.

**Array dependensi (`[]` di akhir):**

| Bentuk | Dibaca |
|---|---|
| `useEffect(fn, [])` | jalankan **sekali** saat komponen muncul |
| `useEffect(fn, [id])` | jalankan saat muncul, dan **tiap `id` berubah** |
| `useEffect(fn)` | jalankan **setiap render** (hati-hati, bisa loop tak berujung) |

> Catatan: fungsi `async` tidak boleh langsung dijadikan callback `useEffect`, makanya dibuat fungsi `muat` di dalamnya lalu dipanggil.

## 2.7 🆕 `useRef`, Context & Custom Hook

**`useRef`**: kotak penyimpan nilai yang **tidak memicu render ulang**; sering dipakai untuk mengakses elemen DOM.
```jsx
const inputRef = useRef(null);
<input ref={inputRef} />
<button onClick={() => inputRef.current.focus()}>Fokus</button>
```
🔍 Baca: "`inputRef.current` menunjuk elemen `<input>` asli; panggil `.focus()` pada elemen itu."

**Context**: berbagi data ke banyak komponen tanpa mengoper props berlapis-lapis (misalnya tema atau data user login).
```jsx
const ThemeContext = createContext("terang");

function App() {
  return (
    <ThemeContext.Provider value="gelap">
      <Halaman />
    </ThemeContext.Provider>
  );
}

function Tombol() {
  const tema = useContext(ThemeContext);   // "gelap"
  return <button className={tema === "gelap" ? "bg-black" : "bg-white"}>OK</button>;
}
```
🔍 Baca: `Provider` = "**menyiarkan** nilai ke semua komponen di dalamku"; `useContext` = "**menangkap** siaran terdekat".

**Custom Hook**: fungsi berawalan `use` yang membungkus logika berulang.
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    fetch(url).then(r => r.json()).then(setData).finally(() => setLoading(false));
  }, [url]);
  return { data, loading };
}

const { data, loading } = useFetch("/api/produk");
```
🔍 Baca: "Hook ini menerima `url`, mengatur state & efek sendiri, lalu **mengembalikan** `{data, loading}` agar komponen manapun tinggal memakai."

## 2.8 Form Handling & Validasi

```jsx
function FormLogin() {
  const [form, setForm] = useState({ email: "", password: "" });
  const [errors, setErrors] = useState({});

  function handleChange(e) {
    const { name, value } = e.target;
    setForm({ ...form, [name]: value });
  }

  function handleSubmit(e) {
    e.preventDefault();
    const baru = {};
    if (!form.email.includes("@")) baru.email = "Email tidak valid";
    if (form.password.length < 8) baru.password = "Minimal 8 karakter";
    setErrors(baru);
    if (Object.keys(baru).length === 0) console.log("Kirim:", form);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" value={form.email} onChange={handleChange} />
      {errors.email && <p>{errors.email}</p>}
      <input name="password" type="password" value={form.password} onChange={handleChange} />
      {errors.password && <p>{errors.password}</p>}
      <button type="submit">Masuk</button>
    </form>
  );
}
```
🔍 **Cara membaca:**
1. State `form` menyimpan semua input dalam **satu objek**.
2. `handleChange`: `e.target` = input yang sedang diketik. `name` & `value` diambil dengan destructuring.
3. `{ ...form, [name]: value }` = salin form lama, lalu **timpa field yang namanya sama dengan `name`**. Tanda `[name]` (kurung siku) berarti "pakai **isi variabel** `name` sebagai nama properti".
4. `e.preventDefault()` = cegah browser me-refresh halaman saat submit.
5. Pola controlled component: `value` dari state, `onChange` memperbarui state, jadi input selalu sinkron dengan state.

### 🆕 React Hook Form + Zod (cara industri)
```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const skema = z.object({
  email: z.string().email("Email tidak valid"),
  password: z.string().min(8, "Minimal 8 karakter"),
});
type FormData = z.infer<typeof skema>;

function FormLogin() {
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>({
    resolver: zodResolver(skema),
  });

  return (
    <form onSubmit={handleSubmit((data) => console.log(data))}>
      <input {...register("email")} />
      {errors.email && <p>{errors.email.message}</p>}
      <input type="password" {...register("password")} />
      {errors.password && <p>{errors.password.message}</p>}
    </form>
  );
}
```
🔍 **Cara membaca:**
1. **Skema Zod** = "aturan bentuk data": email harus string berformat email, password minimal 8.
2. `z.infer<typeof skema>` = "buat tipe TypeScript **otomatis** dari skema" (satu sumber kebenaran).
3. `register("email")` = "hubungkan input ini ke field `email`" (tanda `{...}` menyebar atribut `name`, `onChange`, dsb.).
4. `handleSubmit(fn)` = "validasi dulu; **hanya jika lolos**, panggil `fn`". Jika gagal, `errors` terisi.

**🎯 Mini-proyek Phase 2:** aplikasi to-do / katalog produk dengan React + Tailwind: tambah, hapus, edit, filter, pencarian, form tervalidasi, dan data dari API.

---

# PHASE 3: TypeScript & Next.js (Bulan 4-5)

## 3.1 TypeScript Dasar

```ts
let umur: number = 17;
let nama: string = "Budi";
let aktif: boolean = true;
let tags: string[] = ["a", "b"];

interface User {
  id: number;
  nama: string;
  email?: string;            // ? = opsional
}

type Status = "aktif" | "nonaktif" | "dibekukan";   // union

function sapa(user: User, salam: string = "Halo"): string {
  return `${salam}, ${user.nama}`;
}
```
🔍 **Cara membaca:**
- Titik dua `:` dibaca "**bertipe**". `umur: number` = "`umur` bertipe angka".
- `interface User { ... }` = "cetakan: objek `User` **harus** punya `id` (angka), `nama` (teks), dan **boleh** punya `email`".
- `"aktif" | "nonaktif"` = "salah satu dari ini saja". Garis `|` dibaca "atau".
- Pada fungsi: `(user: User, salam: string = "Halo"): string` → "menerima `user` bertipe `User`, `salam` bertipe teks (default `Halo`), **mengembalikan** teks". Tipe **setelah** tanda kurung = tipe hasil.

**Generic** (tipe sebagai "variabel"):
```ts
function ambilPertama<T>(arr: T[]): T { return arr[0]; }
const x = ambilPertama<string>(["a", "b"]);   // x bertipe string
```
🔍 Baca: "`T` adalah **tipe apa pun** yang nanti ditentukan. Jika diberi array `T`, hasilnya satu `T`." Sama seperti `useState<string>("")` atau `Promise<User>`.

**TypeScript di React:**
```tsx
interface KartuProps {
  nama: string;
  harga: number;
  onBeli?: () => void;
}

function Kartu({ nama, harga, onBeli }: KartuProps) {
  const [jumlah, setJumlah] = useState<number>(0);
  return <button onClick={onBeli}>{nama}: Rp{harga}</button>;
}
```
🔍 Baca: `KartuProps` mendefinisikan bentuk props. `() => void` = "fungsi tanpa argumen yang tidak mengembalikan apa-apa". `useState<number>(0)` = "state bertipe angka".

> Tips: jangan berlebihan memakai `any` (artinya "matikan pengecekan tipe"). Gunakan `unknown` atau definisikan tipenya.

## 3.2 Next.js: File-based Routing

```
app/
├── layout.tsx             → kerangka semua halaman
├── page.tsx               → "/"
├── loading.tsx            → 🆕 tampilan saat halaman memuat
├── error.tsx              → 🆕 tampilan saat terjadi error
├── produk/
│   ├── page.tsx           → "/produk"
│   └── [id]/page.tsx      → "/produk/5"
└── api/
    └── produk/route.ts    → endpoint API "/api/produk"
```
🔍 **Cara membaca:** **folder = segmen URL**, nama file spesial menentukan perannya (`page.tsx` = halaman, `layout.tsx` = pembungkus, `route.ts` = API). Folder dengan `[id]` = **bagian variabel** URL.

```tsx
// app/layout.tsx
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="id">
      <body>
        <nav>Navbar</nav>
        {children}
        <footer>Footer</footer>
      </body>
    </html>
  );
}
```
🔍 Baca: `children` = "isi halaman yang sedang dibuka", disisipkan di antara navbar dan footer. Layout tidak dimuat ulang saat berpindah halaman.

## 3.3 Server Component vs Client Component

```tsx
// app/produk/page.tsx  (Server Component, default)
import { prisma } from "@/lib/prisma";

export default async function HalamanProduk() {
  const produk = await prisma.produk.findMany();
  return (
    <ul>
      {produk.map((p) => <li key={p.id}>{p.nama}</li>)}
    </ul>
  );
}
```
🔍 **Cara membaca:**
1. Komponen ini `async`: **bisa `await` langsung** di badan komponen (hanya di Server Component).
2. Ambil data dari database langsung, tidak perlu `useEffect`/`fetch` ke API sendiri.
3. Hasilnya HTML jadi yang dikirim ke browser.

```tsx
// components/TombolSuka.tsx  (Client Component)
"use client";
import { useState } from "react";

export default function TombolSuka() {
  const [suka, setSuka] = useState(false);
  return <button onClick={() => setSuka(!suka)}>{suka ? "❤️" : "🤍"}</button>;
}
```
🔍 Baca: baris `"use client"` di paling atas = "**file ini berjalan di browser**". Wajib jika memakai `useState`, `useEffect`, atau event (`onClick`).

| | Server Component | Client Component |
|---|---|---|
| Penanda | (default) | `"use client"` |
| Boleh akses DB/secret | ✅ | ❌ |
| Boleh `useState`/`onClick` | ❌ | ✅ |
| JS dikirim ke browser | tidak | ya |

**Strategi:** jadikan halaman sebagai Server Component, lalu sisipkan Client Component kecil hanya untuk bagian interaktif.

**Dynamic route:**
```tsx
// app/produk/[id]/page.tsx
export default async function Detail({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const produk = await prisma.produk.findUnique({ where: { id: Number(id) } });
  if (!produk) return <p>Tidak ditemukan</p>;
  return <h1>{produk.nama}</h1>;
}
```
🔍 Baca: `params` berisi bagian variabel dari URL. Pada Next.js versi terbaru `params` berupa **Promise** sehingga perlu `await` (di versi lama langsung objek, cek dokumentasi versi yang kamu pakai). `Number(id)` karena URL selalu berupa teks.

## 3.4 SSR vs SSG

```tsx
// SSG-like: di-cache (statis)
const res = await fetch("https://api.example.com/artikel", { cache: "force-cache" });

// SSR-like: selalu ambil data baru
const res = await fetch("https://api.example.com/harga", { cache: "no-store" });

// ISR: statis, tapi disegarkan tiap 60 detik
const res = await fetch("https://api.example.com/berita", { next: { revalidate: 60 } });
```
🔍 **Cara membaca:** opsi di argumen kedua `fetch` menentukan strategi: **simpan** (`force-cache`), **jangan simpan** (`no-store`), atau **simpan sementara** (`revalidate: detik`). Perilaku default caching Next.js bisa berbeda antar versi, jadi selalu tuliskan eksplisit.

## 3.5 Server Actions & API Routes

**Server Action** (untuk form):
```tsx
// app/produk/actions.ts
"use server";
import { prisma } from "@/lib/prisma";
import { revalidatePath } from "next/cache";

export async function buatProduk(formData: FormData) {
  const nama = formData.get("nama") as string;
  await prisma.produk.create({ data: { nama } });
  revalidatePath("/produk");
}

// app/produk/baru/page.tsx
import { buatProduk } from "../actions";
export default function Baru() {
  return (
    <form action={buatProduk}>
      <input name="nama" />
      <button type="submit">Simpan</button>
    </form>
  );
}
```
🔍 **Cara membaca:**
1. `"use server"` = "fungsi di file ini **berjalan di server**".
2. `formData.get("nama")` = ambil nilai input yang atribut `name`-nya `"nama"`. `as string` = "percayalah, ini teks".
3. `revalidatePath("/produk")` = "data halaman `/produk` sudah basi, segarkan".
4. `<form action={buatProduk}>` = "saat form dikirim, **panggil fungsi server ini**". Tidak ada `fetch` manual.

> ⚠️ Server Action adalah endpoint publik juga. **Selalu validasi input dan cek login di dalamnya.**

**API Route:**
```ts
// app/api/produk/route.ts
import { NextResponse } from "next/server";

export async function GET() {
  const data = await prisma.produk.findMany();
  return NextResponse.json(data);
}

export async function POST(request: Request) {
  const body = await request.json();
  const produk = await prisma.produk.create({ data: body });
  return NextResponse.json(produk, { status: 201 });
}
```
🔍 Baca: **nama fungsi = method HTTP** (`GET`, `POST`). `request.json()` = baca isi kiriman. `{ status: 201 }` = "berhasil dibuat". Kapan memilih? Server Action untuk form di aplikasimu sendiri; API Route bila ada pihak luar (mobile app, webhook) yang perlu memanggil.

## 3.5b 🆕 Fitur Next.js yang Sering Dipakai
- **`next/image`** (`<Image>`): optimasi gambar otomatis.
- **`next/link`** (`<Link href="/produk">`): navigasi tanpa reload penuh.
- **Metadata**: `export const metadata = { title: "Toko Saya" }` untuk SEO.
- **Environment variable**: `.env` (server only) vs `NEXT_PUBLIC_...` (tampil di browser, jangan isi rahasia).

**🎯 Mini-proyek Phase 3:** blog/katalog dengan Next.js + TypeScript: halaman daftar, halaman detail dinamis, form tambah data (Server Action), data sementara dari file JSON.

---

# PHASE 4: Database, Backend & Keamanan (Bulan 6-7)

## 4.1 🆕 SQL Dasar (Sebelum ORM)

```sql
SELECT u.nama, COUNT(p.id) AS total_pesanan
FROM users u
JOIN pesanan p ON p.user_id = u.id
WHERE p.status = 'selesai'
GROUP BY u.nama
ORDER BY total_pesanan DESC
LIMIT 5;
```
🔍 **Cara membaca SQL (urutan logis, bukan urutan tulis):**
1. `FROM users u` → mulai dari tabel `users` (alias `u`).
2. `JOIN pesanan p ON p.user_id = u.id` → **gabungkan** dengan tabel `pesanan` di mana kunci asingnya cocok.
3. `WHERE p.status = 'selesai'` → **saring** baris.
4. `GROUP BY u.nama` → **kelompokkan** per nama user.
5. `COUNT(p.id)` → **hitung** pesanan tiap kelompok.
6. `ORDER BY ... DESC` → urutkan terbesar dulu. `LIMIT 5` → ambil 5 teratas.
7. `SELECT` → baru **pilih kolom** yang ditampilkan. (Ia ditulis paling atas tapi dieksekusi belakangan.)

Konsep tambahan: **Index** (mempercepat pencarian di kolom tertentu), **transaksi** (beberapa operasi sukses semua atau batal semua).

## 4.2 PostgreSQL & Relasi

```
users (1) ────< pesanan (banyak)          One-to-Many
siswa (banyak) >────< ekskul (banyak)     Many-to-Many (lewat tabel siswa_ekskul)
```
🔍 **Cara membaca diagram:** `1` = satu, `<` (kaki gagak) = banyak. Satu user punya banyak pesanan, tetapi satu pesanan hanya milik satu user. Many-to-Many butuh **tabel penghubung** yang menyimpan pasangan `siswa_id` + `ekskul_id`.

## 4.3 Prisma ORM

```prisma
// prisma/schema.prisma
model User {
  id      Int       @id @default(autoincrement())
  email   String    @unique
  nama    String?
  pesanan Pesanan[]
}

model Pesanan {
  id      Int      @id @default(autoincrement())
  total   Int
  dibuat  DateTime @default(now())
  userId  Int
  user    User     @relation(fields: [userId], references: [id])
}
```
🔍 **Cara membaca `schema.prisma`:** tiap baris di dalam `model` = `namaKolom Tipe [atribut]`.
- `@id` = primary key. `@default(autoincrement())` = nomor otomatis naik.
- `@unique` = tidak boleh kembar. `String?` = boleh kosong (`null`).
- `pesanan Pesanan[]` = "satu user punya **banyak** pesanan" (kolom virtual, bukan kolom di DB).
- `@relation(fields: [userId], references: [id])` = "kolom `userId` di sini **menunjuk ke** `id` di tabel `User`" (foreign key).

```ts
// lib/prisma.ts → satu instance dipakai bersama
import { PrismaClient } from "@prisma/client";
export const prisma = new PrismaClient();

// CRUD
await prisma.user.create({ data: { email: "a@b.com", nama: "Budi" } });

const semua = await prisma.user.findMany({
  where: { nama: { contains: "bu", mode: "insensitive" } },
  orderBy: { id: "desc" },
  include: { pesanan: true },
});

await prisma.user.update({ where: { id: 1 }, data: { nama: "Budi S" } });
await prisma.user.delete({ where: { id: 1 } });
```
🔍 **Cara membaca query Prisma:** `prisma.NAMA_MODEL.AKSI({ opsi })`.
- `create({ data })` = tambah. `findMany({ where, orderBy, include })` = baca banyak.
- `where` = **syarat** (seperti `WHERE`). `include` = **ikut ambil relasi** (seperti `JOIN`). `orderBy` = urutan.
- `update` dan `delete` **wajib** `where` agar tahu baris mana (tanpa itu akan error, kecuali memakai `updateMany`/`deleteMany`).
- Hasil selalu bertipe sesuai skema (TypeScript otomatis tahu `semua[0].pesanan`).

**Perintah penting:**
```bash
npx prisma migrate dev --name tambah-user   # buat & jalankan migrasi (development)
npx prisma generate                          # perbarui tipe TypeScript
npx prisma studio                            # lihat isi database lewat GUI
```
🔍 Alur: ubah `schema.prisma` → `migrate dev` → database dan tipe ikut berubah.

## 4.4 Supabase

- Buat proyek di supabase.com, ambil **connection string** PostgreSQL.
- Simpan di `.env`:
```
DATABASE_URL="postgresql://user:password@host:5432/postgres"
```
- Di `schema.prisma`:
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```
🔍 Baca: `env("DATABASE_URL")` = "ambil nilai dari file `.env`", jadi password tidak tertulis di kode.

## 4.5 Autentikasi & Otorisasi

Alur umum login:
```
1. User kirim email + password
2. Server cari user di database
3. Server bandingkan password (hash) → cocok?
4. Server buat session/token → kirim ke browser (cookie)
5. Request berikutnya membawa cookie → server tahu siapa kamu
```

```ts
// Hash password saat register
import bcrypt from "bcryptjs";
const hash = await bcrypt.hash(passwordDariForm, 10);
await prisma.user.create({ data: { email, password: hash } });

// Cek saat login
const cocok = await bcrypt.compare(passwordDariForm, user.password);
```
🔍 Baca: `hash(teks, 10)` = ubah jadi kode acak satu arah (angka 10 = tingkat "kerumitan"). `compare` = "apakah teks ini jika di-hash sama dengan hash tersimpan?" Password asli **tidak pernah disimpan**.

**Protected route:**
```tsx
// app/dashboard/page.tsx
import { redirect } from "next/navigation";
import { auth } from "@/auth";

export default async function Dashboard() {
  const session = await auth();
  if (!session) redirect("/login");
  return <h1>Halo, {session.user?.name}</h1>;
}
```
🔍 Baca: "Ambil sesi di server. **Jika belum login**, alihkan ke `/login`; jika sudah, tampilkan halaman." Pengecekan **di server** itu wajib; menyembunyikan menu di UI saja tidak cukup.

> Autentikasi = "kamu siapa?" Otorisasi = "kamu boleh apa?" (contoh: hanya `role === "admin"` boleh menghapus produk). Keduanya dicek di server.

## 4.6 🆕 Keamanan Dasar

| Ancaman | Penjelasan | Pencegahan |
|---|---|---|
| **SQL Injection** | Penyerang menyisipkan SQL lewat input | Pakai ORM/parameterized query, jangan gabung string SQL manual |
| **XSS** | Penyerang menyisipkan skrip ke halaman | React otomatis meng-escape; hindari `dangerouslySetInnerHTML` |
| **CSRF** | Situs lain memalsukan aksi atas nama user | Cookie `SameSite`, token CSRF (sudah ditangani auth library) |
| **Kebocoran secret** | `.env` ikut ter-commit | `.gitignore`, jangan beri prefix `NEXT_PUBLIC_` untuk rahasia |
| **Validasi lemah** | Menerima data apa pun dari klien | Validasi **di server** dengan Zod |
| **Akses tanpa izin (IDOR)** | User A membuka data User B lewat ubah ID di URL | Cek kepemilikan data di server |

```ts
// Contoh pencegahan IDOR
const pesanan = await prisma.pesanan.findFirst({
  where: { id: Number(id), userId: session.user.id },   // pastikan milik user ini
});
if (!pesanan) return notFound();
```
🔍 Baca: "cari pesanan dengan `id` itu **DAN** pemiliknya adalah user yang sedang login." Tanpa `userId`, siapa pun bisa mengintip pesanan orang lain.

**🎯 Mini-proyek Phase 4:** aplikasi catatan/blog multi-user: register, login, CRUD data milik sendiri (Prisma + Supabase), halaman dashboard terproteksi, validasi Zod di server.

---

# PHASE 5: Capstone, Testing & Deployment (Bulan 8)

## 5.1 🆕 Testing Dasar

```ts
// utils/harga.test.ts
import { describe, it, expect } from "vitest";
import { hitungDiskon } from "./harga";

describe("hitungDiskon", () => {
  it("menghitung diskon 10%", () => {
    expect(hitungDiskon(100000, 10)).toBe(90000);
  });
  it("melempar error jika persen negatif", () => {
    expect(() => hitungDiskon(100000, -5)).toThrow();
  });
});
```
🔍 **Cara membaca:**
- `describe("...")` = **kelompok** tes ("yang sedang dites: `hitungDiskon`").
- `it("...")` = **satu skenario**, ditulis seperti kalimat: "ia (fungsi ini) menghitung diskon 10%".
- `expect(HASIL).toBe(HARAPAN)` = "**saya harapkan** hasil ini **sama dengan** itu". Jika tidak sama, tes gagal.
- Pola penyusunan tes: **Arrange** (siapkan data) → **Act** (jalankan) → **Assert** (periksa).

Tingkatan tes: **Unit** (fungsi kecil) → **Integration** (beberapa bagian bersama) → **E2E** (simulasi user di browser, misalnya Playwright). Untuk pemula, cukup unit test pada logika penting + satu E2E untuk alur login.

## 5.2 Capstone Project

Pilihan awal tetap sama (Sistem PKL, E-Commerce, Trello clone). **🆕 Checklist kelayakan portofolio:**
- [ ] Ada autentikasi dan otorisasi (minimal 2 peran)
- [ ] Minimal 4 tabel dengan relasi
- [ ] Validasi di sisi server
- [ ] Penanganan loading, error, dan data kosong
- [ ] Responsif di HP
- [ ] Ada beberapa tes pada logika penting
- [ ] README: deskripsi, screenshot, teknologi, cara menjalankan, link demo
- [ ] Sudah live (deploy) dan bisa dicoba orang lain
- [ ] Riwayat commit rapi

## 5.3 Deployment

Alur ke Vercel:
1. Push proyek ke GitHub (pastikan `.env` tidak ikut).
2. Di Vercel: **Add New Project** → pilih repo.
3. Isi **Environment Variables** (`DATABASE_URL`, dll) di dashboard Vercel.
4. Deploy. Setiap `git push` ke `main` akan otomatis memicu deploy baru (**CI/CD**).
5. Jalankan migrasi ke database production:
```bash
npx prisma migrate deploy
```
🔍 Beda `migrate dev` (untuk lokal, boleh mereset) dan `migrate deploy` (untuk production, hanya menerapkan migrasi yang sudah ada).

Pada `package.json`, pastikan ada:
```json
"scripts": { "build": "prisma generate && next build" }
```
🔍 Baca: sebelum membangun Next.js, buat dulu klien Prisma. Tanpa ini, build di Vercel bisa gagal.

---

# PHASE 6 🆕: Persiapan Karier (Berjalan Paralel)

## 6.1 Dasar Algoritma & Struktur Data
Cukup latihan 2-3 soal/minggu (LeetCode easy / Codewars): array, string, hash map (objek/`Map`), pengulangan, rekursi sederhana. Tujuannya melatih cara berpikir, bukan menghafal.

```js
// Contoh: hitung kemunculan huruf
function hitungHuruf(teks) {
  const hasil = {};
  for (const huruf of teks) {
    hasil[huruf] = (hasil[huruf] || 0) + 1;
  }
  return hasil;
}
hitungHuruf("halo");  // { h: 1, a: 1, l: 1, o: 1 }
```
🔍 Baca: "Untuk tiap huruf: ambil hitungan sebelumnya (atau `0` jika belum ada), tambah 1, simpan lagi." Baris `hasil[huruf] = ...` memakai `huruf` sebagai **nama kunci**.

## 6.2 Bahasa Inggris Teknis
- Biasakan membaca **dokumentasi resmi** (react.dev, nextjs.org/docs, prisma.io/docs).
- Pahami kata kunci error: `undefined`, `not found`, `unexpected token`, `unauthorized`.
- Tulis README & pesan commit dalam bahasa Inggris sederhana.

## 6.3 Profil Profesional
- **GitHub profile README**: perkenalan singkat + proyek unggulan (pin 3-4 repo).
- **LinkedIn**: foto, headline ("Aspiring Full Stack Developer | Next.js · TypeScript"), proyek.
- **CV 1 halaman**: proyek (bukan hanya nilai), teknologi, link demo, link GitHub.
- **Soft skill**: bertanya dengan baik (jelaskan apa yang sudah dicoba), menerima review kode, dan konsisten komunikasi di tempat PKL.

---

# GLOSARIUM RINGKAS

| Istilah | Arti Singkat |
|---|---|
| **Scope** | Wilayah di kode tempat variabel bisa diakses (global, fungsi, blok) |
| **Closure** | Fungsi yang mengingat variabel dari scope asalnya |
| **Async** | Tugas yang berjalan tanpa memblokir kode lain |
| **Await** | "Tunggu hasil Promise di sini" (hanya di fungsi `async`) |
| **Promise** | Janji hasil operasi async: pending, fulfilled, rejected |
| **Callback** | Fungsi yang dikirim untuk dipanggil nanti |
| **Event Loop** | Pengatur antrean tugas async saat call stack kosong |
| **Immutable** | Tidak mengubah data asli; selalu buat salinan baru |
| **Destructuring** | Membongkar objek/array ke variabel terpisah |
| **Spread / Rest** | `...` untuk menyebar isi / mengumpulkan sisa |
| **Module** | File yang membagikan kode via `export` dan dipakai via `import` |
| **Component** | Potongan UI yang bisa dipakai ulang |
| **Props** | Data dari komponen induk ke anak (read-only) |
| **State** | Data internal yang memicu render ulang saat berubah |
| **Hook** | Fungsi khusus React berawalan `use` |
| **Render** | Proses menghasilkan tampilan dari komponen |
| **Controlled component** | Input yang nilainya dikontrol state |
| **Context** | Cara berbagi data ke banyak komponen tanpa props berantai |
| **SSR / SSG / CSR / ISR** | Render di server per-request / saat build / di browser / statis yang disegarkan berkala |
| **Server Action** | Fungsi server yang dipanggil langsung dari form/komponen |
| **Middleware** | Kode yang berjalan sebelum request mencapai halaman |
| **Type / Interface** | Bentuk/jenis data pada TypeScript |
| **Generic** | Tipe fleksibel `<T>` |
| **API / REST / Endpoint** | Antarmuka komunikasi / gaya API HTTP / alamat spesifik API |
| **CORS** | Aturan browser untuk request lintas domain |
| **ORM** | Pemetaan tabel database ke objek kode (Prisma) |
| **Schema / Migration** | Rancangan struktur DB / perubahan struktur yang tercatat |
| **CRUD** | Create, Read, Update, Delete |
| **Primary / Foreign key** | Identitas unik baris / penunjuk ke tabel lain |
| **Hashing** | Pengacakan satu arah untuk menyimpan password |
| **Authentication / Authorization** | Verifikasi identitas / pengaturan hak akses |
| **Environment variable** | Konfigurasi rahasia di luar kode (`.env`) |
| **CI/CD** | Otomatisasi tes dan deploy tiap ada perubahan kode |
| **Sandbox** | Mode uji coba yang aman (mis. pembayaran palsu) |
| **Linter / Formatter** | Pendeteksi kode bermasalah (ESLint) / perapi format (Prettier) |

---

> *"Jangan membaca kode seperti membaca novel. Bacalah seperti membaca peta: cari pintu masuk, ikuti alurnya, dan tandai tempat yang membingungkan."* 💪
