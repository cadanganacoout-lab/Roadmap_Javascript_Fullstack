# 🚀 ROADMAP FULL STACK JAVASCRIPT (Versi Lengkap + Panduan Memahami Kode)

---

# Penjelasan Lengkap Operator dalam Roadmap Full Stack JavaScript

## Pengantar

Berkas ini adalah roadmap Full Stack JavaScript berbahasa Indonesia. Bagian 1 (“Operator dan Simbol Sintaks”) sudah memuat panduan operator, dan kode pada fase-fase berikutnya memakai beberapa operator tambahan: `await`, `new`, `typeof` pada posisi tipe, dan `^` pada nomor versi. Semuanya dibahas di sini. Simbol yang hanya tampak seperti operator ditandai tersendiri. Contoh kode diadaptasi dari berkas tersebut.

## 1. Operator assignment dan aritmetika

**Assignment `=`** menyimpan nilai hasil ekspresi di sisi kanan ke variable atau property di sisi kiri. JavaScript menghitung sisi kanan terlebih dahulu, baru melakukan assignment, sehingga maknanya adalah “simpan ini”, bukan “apakah sama?”. Perbedaan `let` dan `const` penting di sini: `let` mengizinkan assignment ulang (memberi nilai baru pada nama yang sama), sedangkan binding `const` tidak boleh diberi nilai baru setelah deklarasi. Dokumentasi: [MDN: Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment).

```js
let jumlah = 2;
jumlah = jumlah + 1;
const total = 5000 * jumlah;
```

Baris 1 mendeklarasikan `jumlah` dengan nilai `2`. Pada baris 2, JavaScript menghitung `jumlah + 1` memakai nilai lama (`2 + 1 = 3`), lalu menetapkan `3` kembali ke `jumlah`; ini sah hanya karena memakai `let`. Pada baris 3, `5000 * jumlah` menjadi `5000 * 3 = 15000` dan disimpan ke konstanta `total`.

**Operator aritmetika `+`, `-`, `*`, `/`** masing-masing melakukan penjumlahan, pengurangan, perkalian, dan pembagian. Operator `+` bersifat overloaded (satu simbol dengan perilaku berbeda tergantung tipe operand): dengan dua angka ia menjumlah, tetapi bila salah satu operand berupa string ia menggabungkan teks, sehingga `2 + 3` menghasilkan `5` sedangkan `"Rp " + 5000` menghasilkan `"Rp 5000"`. Operator `*` dan `/` memiliki precedence (prioritas evaluasi) lebih tinggi daripada `+` dan `-`. Tanda kurung `()` bukan operator aritmetika, melainkan operator grouping (pengelompokan) yang memaksa bagian di dalamnya dievaluasi lebih dulu. Dokumentasi: [Addition](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Addition), [Multiplication](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Multiplication), [Division](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Division), [Grouping](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping), [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence).

```js
const subtotal = harga * jumlah;
const total = subtotal * (1 + tarifPajak);
const hargaPerBarang = total / jumlah;
```

Anggap `harga = 5000`, `jumlah = 3`, `tarifPajak = 0.11`. Langkah 1: `subtotal` bernilai `15000`. Langkah 2: tanda kurung memaksa `1 + 0.11 = 1.11` dihitung lebih dulu, lalu `15000 * 1.11 = 16650`. Tanpa kurung, `subtotal * 1 + tarifPajak` hanya menambahkan `0.11`, yang merupakan bug. Langkah 3: pembagian dengan `jumlah` menghasilkan `5550`. Pembagian dengan nol tidak melempar error di JavaScript, melainkan menghasilkan `Infinity`, jadi lindungi dengan pemeriksaan `jumlah === 0`.

**Minus unary `-`** adalah simbol yang sama tetapi dipakai sebagai operator unary (operator dengan satu operand) untuk membuat angka menjadi negatif. Ini berbeda dari operator binary (dua operand) pada `100 - 5`. Pada `hitungDiskon(100000, -5)`, minus mengubah literal `5` menjadi `-5` sebelum diterima function. Dokumentasi: [MDN: Unary negation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Unary_negation).

## 2. Operator perbandingan

**Kesamaan ketat `===` dan ketidaksamaan ketat `!==`** membandingkan nilai sekaligus tipe tanpa konversi tipe, dan menghasilkan boolean (`true` atau `false`). Karena itu `5 === "5"` bernilai `false` (angka versus string) dan `5 !== "5"` bernilai `true`. Operator longgar `==` akan melakukan coercion (konversi tipe diam-diam) lebih dulu, yang merupakan sumber bug klasik, sehingga `===` adalah pilihan standar. Dokumentasi: [Strict equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality), [Strict inequality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_inequality).

```js
if (produk.stok === 0) {
  console.log("Stok habis");
}
const selainProdukIni = produk.filter((item) => item.id !== id);
```

Pada `if`, JavaScript membaca `produk.stok`, membandingkannya dengan angka `0`, dan menjalankan blok hanya bila hasilnya `true`. Pada baris `filter`, callback dijalankan sekali per item. Ekspresi `item.id !== id` bernilai `true` untuk semua item kecuali yang akan dihapus, dan `filter` hanya mempertahankan item yang callback-nya mengembalikan `true`. Hasilnya array baru tanpa item target.

**Operator urutan `<`, `>`, `<=`, `>=`** menguji urutan (lebih kecil, lebih besar, lebih kecil atau sama, lebih besar atau sama) dan menghasilkan boolean. Pada string, perbandingan dilakukan karakter demi karakter, bukan secara numerik, sehingga `"10" > "2"` bernilai `false` karena `"1"` berada sebelum `"2"`. Ubah teks numerik menjadi angka sebelum membandingkan. Dokumentasi: [Less than](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Less_than), [Greater than or equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Greater_than_or_equal).

```js
const tersedia = produk.filter((item) => item.stok > 0);
const cukupUmur = umur >= 17;
```

Untuk setiap produk, `item.stok > 0` menghasilkan `true` atau `false`, sehingga item tanpa stok tersaring keluar. Pada baris kedua, `umur >= 17` bernilai `true` untuk umur 17 ke atas dan `false` di bawahnya; boolean itu disimpan di `cukupUmur`.

## 3. Operator logika dan pemilihan nilai

Dua istilah penting di sini. Nilai disebut **truthy** bila dianggap benar dalam konteks boolean, dan **falsy** bila dianggap salah. Nilai falsy adalah `0`, `""`, `false`, `null`, `undefined`, dan `NaN` (Not-a-Number); selain itu semuanya truthy. Dokumentasi: [Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy), [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).

**AND logis `&&`** mengembalikan operand pertama jika falsy, dan jika tidak, mengevaluasi lalu mengembalikan operand kedua. Operator ini memakai short-circuit evaluation (evaluasi berhenti lebih awal), sehingga sisi kanan tidak dijalankan bila sisi kiri falsy. Di JSX, inilah cara standar untuk merender sesuatu secara kondisional. Jebakannya: bila sisi kiri berupa angka `0`, React merender teks “0”. Dokumentasi: [Logical AND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND).

```jsx
{produk.stok === 0 && <span>(Habis)</span>}
{produk.length > 0 && <Daftar produk={produk} />}
```

Pada baris 1, bila `stok === 0` bernilai `true`, seluruh ekspresi menghasilkan elemen `<span>` yang dirender. Bila `false`, ekspresi menghasilkan `false`, dan React tidak merender apa pun untuk `false`. Pada baris 2, perbandingan `produk.length > 0` sengaja ditulis agar sisi kiri berupa boolean. Menulis `{produk.length && ...}` akan menampilkan angka `0` di layar untuk array kosong.

**OR logis `||`** mengembalikan operand truthy pertama, atau operand terakhir bila tidak ada yang truthy. Operator ini lazim dipakai untuk fallback (nilai default), tetapi memperlakukan `0` dan `""` sebagai “tidak ada”, sehingga dapat membuang data yang sah. Dokumentasi: [Logical OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR).

```js
const namaTampilan = input || "Tanpa nama";
```

Jika `input` adalah `"Budi"` (truthy), hasilnya `"Budi"` dan sisi kanan tidak pernah dievaluasi. Jika `input` adalah `""`, nilainya falsy sehingga hasilnya `"Tanpa nama"`. Bila `input` adalah `0` dan nol itu valid, operator ini akan menggantinya secara keliru; untuk kasus itulah `??` dipakai.

**NOT logis `!`** membalik truthiness: `!true` menjadi `false` dan `!false` menjadi `true`. Ekspresi `!res.ok` dibaca “respons tidak sukses”. Dokumentasi: [Logical NOT](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT).

```js
if (!res.ok) {
  throw new Error(`Gagal: ${res.status}`);
}
```

`res.ok` adalah boolean pada respons `fetch`, bernilai `true` untuk status HTTP 200 sampai 299. Jika `true`, `!res.ok` menjadi `false` dan blok dilewati. Jika `false`, `!res.ok` menjadi `true` dan `throw` (keyword, bukan operator) melempar error sehingga alur normal berhenti.

**Nullish coalescing `??`** mengembalikan operand kiri kecuali bila nilainya `null` atau `undefined` (keduanya disebut *nullish*), baru kemudian mengembalikan operand kanan. Berbeda dengan `||`, operator ini mempertahankan `0`, `false`, dan `""`. JavaScript juga melarang pencampuran `??` langsung dengan `||` atau `&&` tanpa tanda kurung, agar maksudnya tidak ambigu. Dokumentasi: [Nullish coalescing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing).

```js
const jumlahTampilan = jumlahInput ?? 0;
```

Jika `jumlahInput` bernilai `0`, hasilnya tetap `0` (bukan nullish). Jika `null` atau `undefined`, hasilnya adalah fallback `0`. Dengan `||`, `false` dan `""` juga akan diganti, yang tidak diinginkan untuk data nyata.

**Kondisional (ternary) `kondisi ? a : b`** adalah satu-satunya operator tiga operand di JavaScript. Ia mengevaluasi kondisi dan menghasilkan `a` jika truthy, atau `b` jika tidak. Karena menghasilkan nilai, operator ini cocok di dalam JSX dan assignment. Untuk banyak cabang, `if/else` lebih mudah dibaca. Dokumentasi: [Conditional operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator).

```jsx
const label = stok > 0 ? "Tersedia" : "Habis";
return <p>{aktif ? "Akun aktif" : "Akun nonaktif"}</p>;
```

Pada baris 1, `stok > 0` dievaluasi; bila `true`, `label` menjadi `"Tersedia"`, jika tidak `"Habis"`. Pada baris 2, kurung kurawal `{}` membuka ekspresi JavaScript di dalam JSX, dan ternary memilih teks yang dirender. Di sini `?` dan `:` bekerja berpasangan, dan titik dua tersebut tidak berhubungan dengan anotasi tipe TypeScript.

## 4. Operator akses, pemanggilan, dan pembuatan function

**Optional chaining `?.`** membaca property atau memanggil method hanya jika sisi kirinya bukan `null`/`undefined`. Jika tidak, seluruh rangkaian berhenti dan menghasilkan `undefined` alih-alih melempar `TypeError`. Ini menjawab langsung contoh error di berkas: “Cannot read properties of undefined (reading 'nama')”. Dokumentasi: [Optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining).

```js
const kota = user?.alamat?.kota;
```

JavaScript memeriksa `user` lebih dulu. Jika nullish, evaluasi berhenti dan `kota` bernilai `undefined`. Jika tidak, ia membaca `alamat`; bila itu nullish evaluasi berhenti lagi, jika tidak ia membaca `kota`. Ini mencegah crash, tetapi dapat menyembunyikan nilai wajib yang hilang, jadi tangani `undefined` secara eksplisit bila penting.

**Akses property `.` dan `[]`** membaca nilai dari object atau array. Notasi titik memerlukan nama property yang diketahui saat menulis kode (`user.nama`). Notasi kurung siku menerima ekspresi, sehingga bisa dipakai dengan variable dan indeks array (`warna[0]`). Dokumentasi: [Property accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors).

```js
const nama = user.nama;
const pertama = warna[0];
const nilaiField = form[namaField];
```

`user.nama` membaca property yang bernama harfiah `nama`. `warna[0]` membaca elemen array pertama karena indeks dimulai dari nol. Pada `form[namaField]`, JavaScript mengevaluasi variable `namaField` lebih dulu; jika isinya `"email"`, hasilnya sama dengan `form.email`. Sebaliknya, `form.namaField` akan mencari property yang harfiah bernama “namaField”.

**Pemanggilan function `()`** menjalankan function dan mengirim argument (nilai sebenarnya) ke parameter (nama penampung pada definisi). Dokumentasi: [MDN: Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions).

```js
const hasil = hitungTotal(5000, 3);
const nama = user.nama.toLocaleUpperCase();
```

Pada baris 1, `5000` dan `3` dipasangkan ke parameter `harga` dan `jumlah`, badan function berjalan, dan nilai `return`-nya disimpan di `hasil`. Pada baris 2, `user.nama` dibaca lebih dulu, lalu `.toLocaleUpperCase()` dipanggil pada string tersebut.

**Arrow `=>`** membuat arrow function. Parameter berada di kiri dan badan di kanan. Jika badan berupa satu ekspresi tanpa kurung kurawal, hasilnya dikembalikan otomatis. Jika memakai `{ }`, itu adalah blok sehingga `return` harus ditulis sendiri; ini bug yang sering terjadi pada callback `.map()`. Dokumentasi: [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

```js
const tambah = (a, b) => a + b;
const kuadrat = (angka) => {
  return angka * angka;
};
```

`tambah(2, 3)` mengevaluasi `a + b` dan otomatis mengembalikan `5`. Pada `kuadrat`, kurung kurawal membentuk blok, sehingga tanpa `return` eksplisit function akan mengembalikan `undefined`.

**Spread / rest `...`** adalah satu simbol dengan dua peran yang ditentukan oleh posisinya. Sebagai **spread**, ia membentangkan array atau object menjadi elemen atau property satu per satu. Sebagai **rest**, ia mengumpulkan sisa nilai menjadi array atau object. Keduanya membuat shallow copy (hanya tingkat terluar yang baru, object bersarang tetap berbagi referensi). Dokumentasi: [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax), [Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters).

```js
const salinanDaftar = [...daftar, itemBaru];
const userBaru = { ...user, kota: "Malang" };
function jumlahkan(...angka) {
  return angka.reduce((total, nilai) => total + nilai, 0);
}
```

Baris 1 membuat array baru berisi semua elemen `daftar` lalu `itemBaru`; array asli tidak berubah (penting untuk state React). Baris 2 menyalin semua property `user`, lalu `kota: "Malang"` menimpa `kota` yang ada karena property yang ditulis belakangan menang. Pada `jumlahkan(...angka)`, rest mengumpulkan semua argument, sehingga `jumlahkan(1, 2, 3)` membuat `angka` sama dengan `[1, 2, 3]`. Lalu `reduce` mulai dari `0` dan menambahkan tiap nilai, menghasilkan `6`.

**Interpolasi template literal `${...}`** mengevaluasi ekspresi di dalam string berbatas backtick dan menyisipkan hasilnya sebagai teks. Dokumentasi: [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

```js
const pesan = `Halo ${user.nama}, total belanja: Rp${harga * jumlah}`;
```

JavaScript membaca `"Halo "`, mengevaluasi `user.nama` dan menyisipkannya, membaca `", total belanja: Rp"`, lalu mengevaluasi `harga * jumlah` dan menyisipkannya. Hasilnya satu string. String backtick juga mendukung teks multi-baris.

## 5. Operator pada fase-fase berikutnya

**`await`** menjeda sebuah function `async` sampai sebuah Promise (object yang mewakili hasil yang akan datang) selesai, lalu menghasilkan nilainya. Operator ini hanya bekerja di dalam function `async` (atau module tingkat atas). Dokumentasi: [await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await).

```js
const res = await fetch(`/api/users/${id}`);
if (!res.ok) throw new Error(`Gagal: ${res.status}`);
const data = await res.json();
```

Langkah 1: `fetch(...)` memulai request HTTP dan mengembalikan Promise; `await` menunggu sampai header respons tiba, lalu menyimpan object `Response` di `res`. Langkah 2: pemeriksaan `!res.ok` menangani kegagalan HTTP, karena `fetch` tidak otomatis menolak untuk status 404 atau 500. Langkah 3: `res.json()` juga asynchronous (membaca body), sehingga memerlukan `await` sendiri. Function melanjutkan hanya setelah parsing selesai.

**`new`** membuat instance (object nyata) dari constructor atau class. Dokumentasi: [new](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new).

```ts
export const prisma = new PrismaClient();
```

`new PrismaClient()` memanggil constructor class, membangun object client (dengan pengelolaan koneksi database), dan mengembalikannya untuk di-`export`. Komentar di berkas menjelaskan tujuannya: satu instance bersama untuk seluruh aplikasi. Demikian pula `throw new Error("...")` membangun object error sebelum dilempar.

**`typeof` (bentuk runtime)** menghasilkan string yang menyebut tipe suatu nilai, misalnya `"string"` atau `"object"`. Dokumentasi: [typeof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof).

```ts
const masukan = formData.get("nama");
if (typeof masukan !== "string") {
  throw new Error("Field nama wajib berupa teks");
}
const nama: string = masukan;
```

`formData.get()` mengembalikan `FormDataEntryValue | null` (string, file, atau `null`). `typeof masukan` menghasilkan nama tipe, dan `!== "string"` menolak selain string dengan melempar error. Setelah pemeriksaan itu, TypeScript melakukan narrowing (mempersempit tipe luas menjadi spesifik berdasarkan alur kontrol), sehingga `masukan` diketahui bertipe `string` dan assignment sah tanpa assertion paksa.

**`typeof` (bentuk posisi tipe)** pada TypeScript, seperti `z.infer<typeof skema>`, adalah type query saat kompilasi yang mengambil tipe dari sebuah variable. Bentuk ini dihapus dari output dan tidak pernah berjalan. Dokumentasi: [TypeScript: typeof types](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html).

**`as` (type assertion)** menyuruh TypeScript memperlakukan suatu nilai sebagai tipe tertentu. Ia tidak mengubah maupun memvalidasi apa pun saat runtime. Pada `formData.get("nama") as string`, jika nilainya sebenarnya `null`, tidak ada error di baris itu, melainkan baru kemudian. Karena itu pemeriksaan `typeof` di atas lebih aman. Dokumentasi: [TypeScript: Type assertions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions).

**`^` pada `"axios": "^1.7.0"`** bukan operator JavaScript, melainkan penanda rentang semantic versioning milik npm. Artinya “versi minimal 1.7.0 tetapi di bawah 2.0.0”, sehingga pembaruan patch dan minor diizinkan sedangkan versi mayor (yang memuat perubahan tidak kompatibel) tidak. Dokumentasi: [npm: About semantic versioning](https://docs.npmjs.com/about-semantic-versioning).

## 6. Operator SQL

**Perbandingan `=` dan `>`** membandingkan nilai per baris. Di SQL, satu tanda `=` menguji kesamaan, berbeda dari `=` JavaScript yang melakukan assignment. **`AND`** mensyaratkan kedua kondisi terpenuhi. Dokumentasi: [PostgreSQL: Comparison operators](https://www.postgresql.org/docs/current/functions-comparison.html), [Logical operators](https://www.postgresql.org/docs/current/functions-logical.html).

```sql
SELECT u.nama, COUNT(p.id) AS total_pesanan
FROM users u
JOIN pesanan p ON p.user_id = u.id
WHERE p.status = 'selesai'
  AND p.total > 0
GROUP BY u.nama;
```

`FROM users u` memilih tabel sumber dengan alias `u`. `JOIN ... ON p.user_id = u.id` memakai `=` untuk mencocokkan foreign key pesanan dengan primary key user. `WHERE` mempertahankan baris dengan `p.status = 'selesai'` **dan** `p.total > 0` (`AND` mensyaratkan keduanya). `GROUP BY u.nama` mengelompokkan per user, dan `COUNT(p.id)` menghitung tiap kelompok. `SELECT` ditulis paling atas tetapi secara logis dievaluasi paling akhir. Contoh ini menggabungkan dua cuplikan SQL di berkas sebagai ilustrasi. `JOIN`, `WHERE`, `GROUP BY`, `ORDER BY`, dan `LIMIT` adalah keyword klausa, bukan operator.

## 7. Simbol yang tampak seperti operator tetapi bukan

Berkas dengan tepat memisahkan hal-hal ini. **Destructuring** (`const { nama } = user;`, `const [a, b] = warna;`) memakai `{}` dan `[]` sebagai sintaks pola ([MDN: Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring)). **Titik dua `:`** punya tiga peran yang tidak berhubungan: memisahkan key dan value pada object, memperkenalkan anotasi tipe TypeScript, dan memisahkan cabang ternary. **`?` dan `|` pada tipe TypeScript** (`email?: string`, `string | null`) menyatakan property opsional dan union, dan berbeda dari `?.` dan `||` saat runtime. **`<T>`** pada generic adalah daftar parameter tipe ([TypeScript: Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)). **`@id`, `@unique`, dan `String?` pada Prisma** adalah attribute skema. Baris **`<<<<<<<`, `=======`, `>>>>>>>`** adalah penanda konflik Git, yaitu teks biasa dan bukan kode. Terakhir, `delete` pada `prisma.user.delete(...)` adalah nama method, bukan operator `delete` JavaScript.

---

## 📌 DAFTAR ISI
0. [Evaluasi: Apa yang Kurang dari Roadmap Awal](#0-evaluasi-apa-yang-kurang-dari-roadmap-awal)
1. [Memahami dan Menelusuri Kode](#1-memahami-dan-menelusuri-kode)
   - [Operator dan Simbol Sintaks](#operator-dan-simbol-sintaks)
2. [Phase 0 🆕: Fondasi Lingkungan Kerja](#phase-0--fondasi-lingkungan-kerja-minggu-1-2)
3. [Phase 1: JavaScript Modern & Asynchronous](#phase-1-javascript-modern--asynchronous-bulan-1)
4. [Phase 2: Tailwind & React](#phase-2-tailwind--react-bulan-2-3)
5. [Phase 3: TypeScript & Next.js](#phase-3-typescript--nextjs-bulan-4-5)
6. [Phase 4: Database, Backend & Keamanan](#phase-4-database-backend--keamanan-bulan-6-7)
7. [Phase 5: Capstone, Testing & Deployment](#phase-5-capstone-testing--deployment-bulan-8)
8. [Phase 6 🆕: Persiapan Karier](#phase-6--persiapan-karier-berjalan-paralel)
9. [Panduan Rinci Setiap Poin Roadmap](#panduan-rinci-setiap-poin-roadmap)
10. [Glosarium](#glosarium-istilah-pemrograman)

---

# 1. Memahami dan Menelusuri Kode

Kode tidak memiliki satu cara khusus untuk "dibaca keras-keras". Developer biasanya memahami kode dengan mengenali struktur program, aturan bahasa, aliran data, dan urutan eksekusinya. Penjelasan di bagian-bagian berikut memberi konteks pada konsep; kode tetap dibaca dan ditelusuri sesuai sintaks bahasa serta tujuan program.

### 1. Mulai dari tujuan dan konteks

Sebelum membaca detail, cari tahu apa tanggung jawab file atau bagian kode tersebut. Periksa nama file, `import` yang dipakai, `export` yang disediakan, serta cara fungsi atau component itu dipanggil. Ini membantu menentukan titik awal penelusuran tanpa harus membaca seluruh proyek sekaligus.

### 2. Ikuti aliran eksekusi

Di dalam satu function, instruksi biasanya dijalankan berurutan dari atas ke bawah, kecuali alur berubah karena `if`, loop, `return`, `throw`, atau operasi asynchronous. Bedakan juga deklarasi dengan pemanggilan: mendefinisikan function belum menjalankannya.

```js
function hitungTotal(harga, jumlah) {
  const total = harga * jumlah;
  return total;
}

const hasil = hitungTotal(5000, 3);
```
Function `hitungTotal` didefinisikan terlebih dahulu. Saat `hitungTotal(5000, 3)` dipanggil, nilai argument diterima oleh parameter, perkalian dihitung, lalu hasil dikembalikan dan disimpan ke `hasil`.

### 3. Pahami ekspresi berdasarkan sintaks dan prioritas operator

Jangan menganggap semua kode dibaca dengan aturan "kanan ke kiri" atau selalu dari ekspresi paling dalam. Ikuti aturan sintaks bahasa: operator memiliki prioritas, function dipanggil sesuai tanda kurung, dan nilai hasil dapat menjadi input bagi operasi berikutnya. Jika ekspresi terlalu padat, pecah menjadi beberapa variable agar alurnya lebih jelas.

```js
const total = harga * jumlah;
const totalDenganPajak = total * (1 + tarifPajak);
```
Pada assignment, JavaScript mengevaluasi ekspresi di sebelah kanan lalu menetapkan nilainya ke variable di sebelah kiri. `=` adalah assignment, bukan operator untuk memeriksa kesamaan; perbandingan nilai biasanya menggunakan `===`.

### 4. Telusuri aliran data dan nilai balik

Saat sebuah nilai melewati beberapa operasi, identifikasi input setiap operasi dan hasil yang diteruskan ke operasi berikutnya. Method array seperti `filter`, `map`, dan `sort` dapat dirangkai, tetapi masing-masing memiliki peran dan hasil yang berbeda.

```js
const namaProdukTersedia = produk
  .filter((item) => item.stok > 0)
  .map((item) => item.nama)
  .sort();
```
Urutannya: `filter` menghasilkan array produk yang stoknya tersedia; `map` mengubah array tersebut menjadi nama produk; `sort` mengurutkan nama-nama itu. Format beberapa baris tidak mengubah hasil, tetapi membantu melihat setiap tahap transformasi.

### 5. Tafsirkan tanda baca menurut konteks

Simbol yang sama dapat mempunyai fungsi berbeda berdasarkan sintaks di sekitarnya. Misalnya `{}` dapat menjadi blok function, object literal, atau area ekspresi JavaScript di JSX. Tentukan dulu konstruksi yang sedang dibaca, baru tafsirkan simbolnya.

| Bentuk | Fungsi dalam konteks contoh |
|---|---|
| `tambah(1, 2)` | Memanggil function dengan dua argument |
| `if (aktif) { ... }` | Blok pernyataan yang dijalankan saat kondisi benar |
| `const user = { nama: "Budi" }` | Object literal dengan property `nama` |
| `const [pertama, kedua] = daftar` | Array destructuring |
| `<Kartu />` | JSX untuk menggunakan component |
| `Array<string>` | Generic TypeScript dengan elemen bertipe `string` |

### 6. Ikuti alur asynchronous secara terpisah

Operasi seperti `fetch` tidak selalu selesai saat baris pemanggilannya berjalan. Perhatikan `await`, `.then()`, callback, dan penanganan error untuk mengetahui kapan hasil tersedia dan ke mana alurnya berlanjut. Pada React, `useEffect` juga berjalan pada tahap yang berbeda dari kode render component.

### 7. Gunakan stack trace untuk menemukan konteks error

Stack trace menunjukkan error dan rangkaian pemanggilan function saat error terjadi. Cari frame yang menunjuk ke file aplikasi sendiri, lalu periksa nilai dan operasi pada lokasi itu. Frame dari library tetap dapat memberi konteks; jangan langsung mengabaikannya jika penyebabnya belum jelas.

```text
TypeError: Cannot read properties of undefined (reading 'nama')
    at KartuProduk (app/produk/page.tsx:12:20)
    at renderWithHooks (node_modules/react-dom/...)
```
Contoh ini menunjukkan bahwa akses property `nama` gagal karena nilai di depannya `undefined`. Frame `KartuProduk` menunjuk ke file aplikasi pada baris 12, kolom 20; telusuri dari sana nilai apa yang seharusnya tersedia dan mengapa nilainya belum ada.

### 8. Gunakan penjelasan verbal sebagai alat bantu opsional

Menjelaskan alur kepada rekan, menulis catatan, atau memakai teknik *rubber duck debugging* dapat membantu saat menemui bug. Teknik ini adalah alat bantu untuk mengurai masalah, bukan aturan wajib untuk membaca atau menulis setiap baris kode.

## Operator dan Simbol Sintaks

Bagian ini merangkum operator yang muncul di contoh JavaScript, TypeScript, JSX, SQL, dan Prisma pada roadmap. **Operator** adalah simbol atau kata yang melakukan operasi pada satu atau beberapa nilai (operand). Simbol yang bentuknya mirip operator belum tentu operator: misalnya `:` pada object memisahkan nama property dan nilainya, sedangkan `:` pada TypeScript memperkenalkan anotasi tipe. Karena arti simbol bergantung pada konteks, baca struktur di sekitarnya terlebih dahulu. Contoh di bawah memakai nama `harga`, `jumlah`, `user`, dan `produk` sebagai data ilustrasi; anggap nilai tersebut sudah tersedia.

### Operator assignment dan aritmetika

**Assignment `=`** memberikan nilai hasil ekspresi di sebelah kanan kepada variable atau property di sebelah kiri. JavaScript menghitung bagian kanan terlebih dahulu, baru melakukan assignment. Karena itu, `const total = harga * jumlah` berarti hitung perkalian, lalu simpan hasilnya ke `total`; tanda `=` di sini bukan pertanyaan “apakah nilainya sama?”. Untuk membandingkan kesamaan nilai, gunakan `===` sebagaimana dijelaskan pada bagian perbandingan.

```js
let jumlah = 2;
jumlah = jumlah + 1;
const total = 5000 * jumlah;
```

Pada baris kedua, nilai lama `jumlah` (2) dijumlahkan dengan 1, lalu hasil 3 ditetapkan kembali ke variable `jumlah`. Baris ketiga mengalikan harga 5000 dengan jumlah 3 sehingga `total` bernilai 15000. `let` mengizinkan assignment ulang, sedangkan nama yang dideklarasikan dengan `const` tidak boleh diberi nilai baru setelah deklarasi.

**Operator aritmetika `+`, `-`, `*`, dan `/`** masing-masing digunakan untuk penjumlahan, pengurangan, perkalian, dan pembagian angka. `+` juga dapat menggabungkan string, sehingga arti hasilnya dipengaruhi tipe operand: `2 + 3` menghasilkan angka `5`, sedangkan `"Rp " + 5000` menghasilkan teks `"Rp 5000"`. Operator `*` dan `/` memiliki prioritas lebih tinggi daripada `+` dan `-`; gunakan tanda kurung jika urutan hitung perlu dibuat eksplisit.

```js
const subtotal = harga * jumlah;
const total = subtotal * (1 + tarifPajak);
const hargaSetelahDiskon = harga - diskon;
const hargaPerBarang = total / jumlah;
```

Pada contoh pajak, `(1 + tarifPajak)` dihitung dahulu. Jika `harga = 5000`, `jumlah = 3`, dan `tarifPajak = 0.11`, maka `subtotal` menjadi `5000 * 3 = 15000`; faktor pajak menjadi `1 + 0.11 = 1.11`; dan `total` menjadi `15000 * 1.11 = 16650`. Jika dibagi kembali dengan `jumlah`, `hargaPerBarang` menjadi `16650 / 3 = 5550`. Tanda kurung `()` bukan operator aritmetika, melainkan pengelompokan yang memastikan bagian tersebut dievaluasi sebagai satu kesatuan. Pembagian angka dengan nol di JavaScript tidak melempar exception: hasilnya dapat menjadi `Infinity` atau `-Infinity` (bergantung pada tanda pembilang), sedangkan `0 / 0` menghasilkan `NaN`. Jika nol tidak valid dalam konteks program, periksa dulu nilainya, misalnya `if (jumlah === 0) throw new Error("Jumlah tidak boleh nol");`. Lihat [MDN: Division](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Division) dan [operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence).

Tanda minus juga dapat dipakai sebagai **operator unary** (operator yang bekerja pada satu operand), bukan hanya pengurangan dua angka. Pada contoh `hitungDiskon(100000, -5)`, `-` membuat nilai `5` menjadi angka negatif `-5`; function menerima nilai itu sebagai argument kedua. Operasi ini berbeda dari `100 - 5`, yang memakai minus sebagai operator binary (mengurangi operand kanan dari operand kiri).

### Operator perbandingan

**Kesamaan ketat `===` dan ketidaksamaan ketat `!==`** membandingkan nilai sekaligus tipe datanya dan menghasilkan boolean (`true` atau `false`), tanpa konversi tipe otomatis. Gunakan keduanya untuk pemeriksaan kesamaan yang umum di JavaScript; jangan menyamakan `=` (assignment) dengan `===` (perbandingan). Sebagai contoh, `5 === "5"` bernilai `false` karena operand kiri angka dan operand kanan string, sedangkan `5 !== "5"` bernilai `true`. Operator longgar `==` dan `!=` melakukan *type coercion* (konversi tipe implisit) sebelum membandingkan, sehingga hasil seperti `5 == "5"` bernilai `true`; untuk menghindari kejutan semacam ini, gunakan `===`/`!==` kecuali ada alasan yang jelas memakai perbandingan longgar. Lihat [MDN: Strict equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality) dan [Strict inequality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_inequality).

```js
if (produk.stok === 0) {
  console.log("Stok habis");
}

const selainProdukIni = produk.filter((item) => item.id !== id);
```

Kondisi pertama memeriksa apakah stok tepat bernilai angka nol. Kondisi kedua mempertahankan hanya item yang `id`-nya berbeda dari `id` yang hendak dihapus. Pada contoh-contoh ini, `===` dan `!==` tidak mengubah nilai yang dibandingkan; keduanya hanya menghasilkan nilai boolean yang dapat dipakai oleh `if`, `filter`, atau ekspresi lain.

**Perbandingan urutan `<`, `>`, `<=`, dan `>=`** menghasilkan boolean berdasarkan hubungan urutan. Untuk angka, `<` berarti lebih kecil, `>` lebih besar, `<=` lebih kecil atau sama, dan `>=` lebih besar atau sama. Operator ini muncul, misalnya, ketika memfilter produk dengan stok positif (`item.stok > 0`) atau memeriksa batas nilai. Pada string, perbandingan dilakukan secara leksikografis (membandingkan urutan karakter), bukan dengan membaca teks sebagai angka: `"10" > "2"` bernilai `false` karena karakter pertama `"1"` mendahului `"2"`. Jika teks sebenarnya mewakili angka, konversikan dan validasi sebagai angka terlebih dahulu, misalnya `Number(teks)`, sebelum membandingkan. Lihat [MDN: Less than](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Less_than) dan [Greater than or equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Greater_than_or_equal).

```js
const tersedia = produk.filter((item) => item.stok > 0);
const cukupUmur = umur >= 17;
```

`filter` menjalankan callback untuk setiap item. Untuk `tersedia`, callback menghasilkan `true` hanya jika stok item lebih dari nol, sehingga item tanpa stok tidak ikut ke array hasil. Sementara itu, `cukupUmur` berisi `true` saat `umur` sekurang-kurangnya 17 dan `false` jika kurang dari 17.

### Operator logika dan pemilihan nilai

**AND logis `&&`** mengembalikan operand pertama jika operand itu *falsy* (dianggap salah dalam konteks boolean); jika operand pertama *truthy*, operator mengevaluasi dan mengembalikan operand kedua. Karena itu, bila kedua operand berupa kondisi boolean, hasilnya benar hanya saat keduanya benar. Dalam JavaScript, operator ini memakai *short-circuit* (evaluasi berhenti lebih awal): operand kanan tidak dievaluasi jika operand kiri falsy. Di JSX, pola `{kondisi && <Elemen />}` menampilkan elemen saat kondisi benar. Perhatikan bahwa jika operand kiri bernilai angka `0`, ekspresi menghasilkan `0` dan React menampilkannya sebagai teks; untuk kondisi numerik, tulis pemeriksaan eksplisit seperti `jumlah > 0 && ...`.

```jsx
{produk.stok === 0 && <span>(Habis)</span>}
{produk.length > 0 && <Daftar produk={produk} />}
```

Pada baris pertama, elemen `<span>` hanya menjadi hasil ekspresi jika stok tepat nol; jika tidak, tidak ada elemen yang perlu ditampilkan. Pada baris kedua, pemeriksaan `produk.length > 0` mencegah hasil `0` muncul di UI ketika array kosong. Operator `&&` dapat mengendalikan ekspresi seperti ini, tetapi bukan pengganti `if` untuk semua alur program.

**OR logis `||`** mengembalikan operand pertama yang *truthy*; jika operand pertama falsy, ia mengevaluasi dan mengembalikan operand kedua. Jika semua operand falsy, hasilnya adalah operand terakhir, bukan otomatis nilai boolean `false`. Nilai falsy JavaScript mencakup `0`, `-0`, `0n`, `""` (string kosong), `false`, `null`, `undefined`, dan `NaN`; nilai lain termasuk object dan array kosong dianggap truthy. Karena `0`, `false`, dan `""` kerap merupakan data sah, penggunaan `||` sebagai fallback dapat menggantinya secara tidak sengaja. Lihat [MDN: Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) dan [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).

```js
const namaTampilan = input || "Tanpa nama";
```

Jika `input` adalah `"Budi"`, hasilnya `"Budi"` dan operand kanan tidak dievaluasi karena operand pertama truthy. Jika `input` adalah string kosong, hasilnya `"Tanpa nama"`. Begitu pula `0`, `false`, `null`, `undefined`, dan `NaN` menyebabkan fallback dipilih. Jika angka `0` merupakan nilai yang valid dan harus tetap dipakai, `||` bukan pilihan tepat; gunakan `??` agar fallback hanya dipakai untuk `null` atau `undefined`. Lihat [MDN: Logical OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR).

**NOT logis `!`** membalik nilai truthiness: `!true` menjadi `false` dan `!false` menjadi `true`. Pada kondisi seperti `if (!res.ok)`, tanda `!` menyatakan “jika `res.ok` tidak benar”, sehingga blok menangani respons yang tidak sukses. `!` juga dapat mengonversi nilai ke boolean terbalik, jadi pahami nilai asalnya sebelum membaca hasilnya.

```js
if (!res.ok) {
  throw new Error(`Gagal: ${res.status}`);
}
```

`Response.ok` bernilai `true` untuk status HTTP sukses dalam rentang 200–299. Jika `res.ok` adalah `true`, `!res.ok` menjadi `false` dan blok dilewati. Jika `res.ok` adalah `false`, kondisinya menjadi `true` dan `throw` menghentikan jalur normal dengan melempar error. `throw` sendiri adalah keyword untuk melempar exception, bukan operator. Penting membedakan kegagalan HTTP dari kegagalan jaringan: `fetch` biasanya tetap menghasilkan `Response` untuk status 404/500, sehingga pengecekan ini diperlukan; kegagalan jaringan umumnya menolak Promise dan ditangani lewat `catch`.

**Nullish coalescing `??`** memakai nilai di kiri jika nilainya bukan `null` dan bukan `undefined`; hanya jika nilainya *nullish* (salah satu dari dua nilai tersebut) barulah nilai kanan dipakai. Operator ini cocok untuk nilai default ketika `0`, `false`, atau `""` tetap merupakan data yang sah.

```js
const jumlahTampilan = jumlahInput ?? 0;
const namaTampilan = namaInput ?? "Tanpa nama";
```

Jika `jumlahInput` bernilai `0`, `jumlahTampilan` tetap `0`; jika `jumlahInput` `null` atau `undefined`, hasilnya `0`. Hal itu berbeda dari `jumlahInput || 0`, yang juga akan memilih nilai kanan saat input `false`, `0`, atau string kosong. Hindari mencampur `??` dengan `&&` atau `||` dalam satu ekspresi tanpa tanda kurung; JavaScript membatasi campuran langsung tersebut agar maksud logikanya tidak ambigu.

**Conditional / ternary `kondisi ? nilaiJikaBenar : nilaiJikaSalah`** memilih salah satu dari dua ekspresi berdasarkan kondisi dan menghasilkan nilai. Gunakan untuk keputusan singkat yang langsung menghasilkan UI atau data; untuk banyak cabang atau proses panjang, `if/else` biasanya lebih mudah dibaca.

```jsx
const label = stok > 0 ? "Tersedia" : "Habis";
return <p>{aktif ? "Akun aktif" : "Akun nonaktif"}</p>;
```

Jika kondisi sebelum `?` bernilai benar, ekspresi di antara `?` dan `:` dipilih; jika salah, ekspresi setelah `:` dipilih. Pada contoh pertama, `label` berisi salah satu teks. Pada contoh kedua, ternary menjadi ekspresi JavaScript di dalam JSX dan menghasilkan teks yang dirender. Tanda `:` pada ternary memisahkan cabang benar dan cabang salah; fungsinya berbeda dari `:` yang menandai tipe TypeScript.

### Operator akses, pemanggilan, dan pembentukan fungsi

**Optional chaining `?.`** mencoba mengakses property atau memanggil method hanya jika nilai di sebelah kirinya bukan `null`/`undefined`. Jika nilai kiri nullish, rangkaian akses tersebut berhenti dan hasilnya `undefined`, alih-alih melempar `TypeError`. Operator ini melindungi akses bertingkat ketika data mungkin belum tersedia, tetapi tidak menggantikan validasi jika data wajib ada.

```js
const kota = user?.alamat?.kota;
```

JavaScript memeriksa `user` terlebih dahulu. Jika `user` nullish, `kota` menjadi `undefined` tanpa mencoba membaca `alamat`; jika `user` tersedia, JavaScript melanjutkan ke `alamat`, lalu membaca `kota` hanya bila `alamat` juga tersedia. Jika `kota` harus selalu ada untuk proses bisnis, tangani kondisi `undefined` secara eksplisit daripada membiarkannya merambat ke bagian program lain.

**Akses property `.` dan akses property dinamis `[]`** mengambil nilai yang tersimpan pada object atau array. Titik dipakai ketika nama property diketahui saat menulis kode (`user.nama`); kurung siku dipakai ketika nama property disimpan sebagai nilai variable (`form[name]`) atau ketika mengakses elemen array berdasarkan indeks (`warna[0]`). Keduanya membaca data dan tidak dengan sendirinya memanggil fungsi.

```js
const nama = user.nama;
const pertama = warna[0];
const nilaiField = form[namaField];
```

Pada `warna[0]`, angka `0` adalah indeks item pertama karena indeks array dimulai dari nol. Pada `form[namaField]`, JavaScript mengevaluasi variable `namaField`, lalu menggunakan isi string-nya sebagai nama property; jika isinya `"email"`, ekspresi tersebut setara dengan `form.email`. Berbeda dengan itu, `form.namaField` selalu membaca property literal bernama `"namaField"`.

**Pemanggilan function `()`** menjalankan function atau method dan mengirim argument di antara tanda kurung. Koma memisahkan beberapa argument, bukan operator hitung. Tanda kurung juga digunakan untuk mengelompokkan ekspresi dan parameter function; jadi maknanya ditentukan oleh bentuk di sekitarnya.

```js
const hasil = hitungTotal(5000, 3);
const nama = user.nama.toLocaleUpperCase();
```

Pemanggilan `hitungTotal(5000, 3)` mengirim dua argument, yaitu `5000` dan `3`, ke parameter function. Pada baris kedua, `user.nama` diakses lebih dulu, lalu method `toLocaleUpperCase()` dipanggil pada nilai teks tersebut. Jika `user` atau `nama` mungkin tidak tersedia, akses biasa dapat gagal; gunakan pemeriksaan atau optional chaining sesuai kebutuhan.

**Arrow `=>`** memisahkan parameter fungsi panah dari badan fungsi dan membentuk sebuah function value. Callback seperti `(item) => item.nama` lazim digunakan oleh method array. Jika badan setelah `=>` berupa satu ekspresi tanpa kurung kurawal, hasil ekspresi dikembalikan otomatis; jika menggunakan `{ ... }`, badan tersebut adalah blok dan perlu `return` eksplisit apabila ingin mengembalikan nilai.

```js
const ambilNama = (item) => item.nama;
const tambah = (a, b) => a + b;
const kuadrat = (angka) => {
  return angka * angka;
};
```

`ambilNama` menerima satu item dan mengembalikan property `nama`; `tambah` menerima dua parameter dan mengembalikan hasil penjumlahan. Pada `kuadrat`, kurung kurawal membentuk blok sehingga `return` diperlukan agar nilai perkalian keluar dari function. Perbedaan ini penting pada `.map()`: callback harus mengembalikan nilai baru agar array hasilnya berisi data yang diharapkan.

**Spread/rest `...`** memiliki arti bergantung pada posisi. Sebagai *spread* (membentangkan elemen/property), ia menyalin elemen array atau property object ke dalam struktur baru atau argument pemanggilan. Sebagai *rest* (mengumpulkan sisa nilai), ia mengumpulkan argument atau property yang tersisa ke dalam array/object. Spread/rest menghasilkan salinan dangkal (*shallow copy*: object di tingkat terluar baru, tetapi object bertingkat masih dapat berbagi referensi).

```js
const salinanDaftar = [...daftar, itemBaru];
const userBaru = { ...user, kota: "Malang" };

function jumlahkan(...angka) {
  return angka.reduce((total, nilai) => total + nilai, 0);
}
```

Di `[...daftar, itemBaru]`, elemen `daftar` dibentangkan ke array baru dan `itemBaru` ditambahkan di akhir; array awal tidak dimutasi. Pada object, urutan property penting: `{ ...user, kota: "Malang" }` menyalin property `user`, lalu nilai `kota` ditimpa dengan `"Malang"`. Dalam definisi parameter `...angka`, rest mengumpulkan semua argument menjadi array sehingga `jumlahkan(1, 2, 3)` memproses `[1, 2, 3]`.

**Interpolasi template literal `${...}`** menyisipkan hasil ekspresi JavaScript ke dalam string yang dibatasi backtick (`` ` ``). Bentuk ini memudahkan penyusunan teks yang berisi variable atau perhitungan dan menghindari rangkaian penggabungan string dengan `+`. Ekspresi di dalam `${}` dievaluasi saat template literal dibuat.

```js
const pesan = `Halo ${user.nama}, total belanja: Rp${harga * jumlah}`;
```

JavaScript membaca teks `"Halo "`, mengambil nilai `user.nama`, melanjutkan teks `", total belanja: Rp"`, menghitung `harga * jumlah`, lalu menyisipkan hasilnya. Template literal berbeda dari string dengan tanda kutip biasa karena mendukung interpolasi dan teks multi-baris.

### Operator yang digunakan pada fase-fase berikutnya

**`await`** menunggu Promise (object yang mewakili hasil asynchronous) di dalam function `async` atau pada top-level module yang mendukungnya, lalu menghasilkan nilai pemenuhan Promise. `await` menjeda kelanjutan function yang sedang berjalan, bukan menghentikan seluruh aplikasi. Jika Promise ditolak (*rejected*), `await` melempar error pada titik tersebut sehingga dapat ditangani dengan `try/catch`. Perlu diingat bahwa `fetch` menolak Promise untuk kegagalan jaringan, tetapi status HTTP seperti 404 atau 500 tetap menghasilkan `Response`; karena itu contoh roadmap memeriksa `res.ok` secara terpisah. Lihat [MDN: `await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await).

```js
const res = await fetch(`/api/users/${id}`);
if (!res.ok) throw new Error(`Gagal: ${res.status}`);
const data = await res.json();
```

Pertama, `fetch(...)` memulai request dan memberikan Promise. `await` menunggu sampai response tersedia lalu hasilnya disimpan di `res`. Pemeriksaan `!res.ok` melempar error bila status bukan rentang sukses HTTP; sesudahnya `res.json()` membaca dan mengurai body secara asynchronous, sehingga hasil parsing juga perlu ditunggu dengan `await`. Template literal pada URL menyisipkan nilai `id`.

**`new`** adalah operator yang membuat instance (object yang dibuat berdasarkan constructor atau class) dengan memanggil constructor. Ia dipakai, misalnya, pada `new PrismaClient()` dan `new Error("...")`. `new` bukan bagian dari nama class dan tidak sama dengan pemanggilan biasa `PrismaClient()`; object hasil konstruksi dapat memiliki perilaku dan state yang ditentukan oleh class tersebut. Lihat [MDN: `new` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new).

```ts
export const prisma = new PrismaClient();
throw new Error("Field tidak valid");
```

Baris pertama membangun satu object client Prisma lalu mengekspornya agar module lain dapat menggunakannya. Baris kedua membangun object `Error`, lalu `throw` melemparkannya sehingga alur normal berhenti dan penanganan error dapat mengambil alih. `throw` adalah keyword (kata kunci bahasa), bukan operator.

### Simbol tipe dan sintaks yang mirip operator

**Titik dua `:` pada TypeScript** memperkenalkan anotasi tipe, misalnya `umur: number`; ia tidak membandingkan ataupun mengubah nilai. **Titik dua pada object literal** memisahkan key dan value, seperti `{ nama: "Budi" }`, sedangkan **titik dua pada ternary** memisahkan hasil saat kondisi salah. Konteks ini menjelaskan mengapa satu tanda baca tidak boleh diberi satu arti universal.

```ts
const umur: number = 17;
const user = { nama: "Budi" };
const label = aktif ? "Aktif" : "Nonaktif";
```

Pada baris pertama, `: number` memberi tahu pemeriksa TypeScript bahwa `umur` harus bertipe angka; annotation ini dihapus saat TypeScript ditranspilasi dan bukan validasi runtime. Pada object, `nama: "Budi"` mendefinisikan property. Pada ternary, `:` memisahkan cabang alternatif.

**Tanda tanya `?` dan union `|` pada TypeScript** juga bukan operator runtime pada contoh-contoh ini. `email?: string` menandai property opsional, sehingga object `User` boleh tidak menyertakan `email`; `string | null` menyatakan nilai boleh berupa string atau `null`. Di Prisma, `String?` menandakan field nullable di skema database; arti dan dampaknya mengikuti aturan Prisma, bukan aturan operator JavaScript.

```ts
interface User {
  id: number;
  email?: string;
}

type Hasil = string | null;
```

`email?` tidak sama dengan `user?.email`: yang pertama mendeklarasikan property opsional pada tipe, sedangkan yang kedua (optional chaining) melakukan akses aman pada saat program berjalan. Union `|` juga berbeda dari OR logis `||`: `|` dalam type declaration menyatukan pilihan tipe, sementara `||` mengevaluasi nilai saat runtime.

Keyword **`as` dalam type assertion** memberi tahu TypeScript cara memperlakukan suatu nilai pada pemeriksaan tipe, misalnya `formData.get("nama") as string`. Ini bukan konversi nilai saat runtime dan bukan jaminan bahwa nilainya benar-benar string; jika nilai aslinya bukan string, assertion tidak mengubahnya. Karena `FormData.get()` dapat mengembalikan `null`, contoh produksi sebaiknya memeriksa hasilnya atau memvalidasi data sebelum digunakan. Pada contoh Zod `z.infer<typeof skema>`, **`typeof` di posisi tipe** meminta TypeScript mengambil tipe dari variable `skema`; ini adalah type query (permintaan tipe saat kompilasi), bukan pemeriksaan `typeof` JavaScript yang menghasilkan string saat program berjalan.

```ts
const masukan = formData.get("nama");
if (typeof masukan !== "string") {
  throw new Error("Field nama wajib berupa teks");
}
const nama: string = masukan;
```

Di dalam `if`, `typeof masukan` saat runtime menghasilkan string yang menyatakan jenis nilai, misalnya `"string"` atau `"object"`; perbandingan `!== "string"` menolak nilai yang bukan string. Setelah kondisi tersebut, TypeScript dapat mempersempit tipe `masukan` menjadi `string`, sehingga assignment ke `nama` aman tanpa assertion paksa. Bedakan bentuk runtime `typeof masukan` dari bentuk tipe `typeof skema` di `z.infer<typeof skema>` berdasarkan posisinya.

Pada contoh `FormData`, nilai `formData.get("nama")` bertipe `FormDataEntryValue | null`: ia dapat berupa string, file (`File`), atau `null` bila field tidak ditemukan. Karena itu, pemeriksaan `typeof masukan !== "string"` berguna untuk menolak file maupun nilai yang tidak ada. `typeof` runtime secara umum menghasilkan string nama tipe seperti `"string"`, `"number"`, `"boolean"`, `"undefined"`, atau `"object"`; ada pengecualian historis, misalnya `typeof null` menghasilkan `"object"`. Lihat [MDN: `typeof` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) dan [TypeScript: `typeof` type operator](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html).

**Kurung sudut `<...>` pada generic TypeScript** menyatakan parameter tipe pada konteks tipe, seperti `Promise<User>` atau `ambilPertama<string>(...)`; ini bukan operator perbandingan pada contoh tersebut. Namun `<` dan `>` juga dapat menjadi operator pembanding dalam ekspresi angka, serta menjadi pembatas tag JSX, sehingga konteks sintaks sangat penting. Dalam TSX/JSX, penulisan generic pada arrow function dapat ambigu dengan tag; ikuti sintaks yang didukung versi TypeScript dan formatter proyek.

```ts
function ambilPertama<T>(arr: T[]): T {
  return arr[0];
}
const nama = ambilPertama<string>(["Budi", "Sari"]);
```

`T` adalah parameter tipe yang ditentukan dari pemakaian function. Karena argument berupa `string[]`, hasil function bertipe `string`; `<string>` membuat pilihan tipe eksplisit, tetapi TypeScript sering dapat menyimpulkannya sehingga pemanggilan juga dapat ditulis `ambilPertama(["Budi", "Sari"])`.

**Tanda kurung kurawal `{}`, kurung siku `[]`, koma, titik koma, dan titik** umumnya merupakan tanda sintaks/pemisah, bukan operator tunggal. Kurung kurawal dapat membentuk blok kode, object literal, destructuring, atau area ekspresi JavaScript dalam JSX; kurung siku dapat membentuk array, destructuring, indeks akses, atau nama property dinamis. Koma memisahkan item/argument/property, titik koma mengakhiri statement, dan titik mengakses property/method. Periksa konstruksi lengkap sebelum menentukan fungsinya.

```js
const { nama, kelas } = user;       // object destructuring
const [pertama, kedua] = warna;    // array destructuring
const siswa = { nama, kelas };     // object literal; shorthand property
```

Pada destructuring object, nama variable dicocokkan dengan nama property; pada destructuring array, posisi menentukan nilai yang diambil. Dalam object literal `{ nama, kelas }`, shorthand property berarti setara dengan `{ nama: nama, kelas: kelas }`. Kurung kurawal juga muncul sebagai blok pada `if` atau function, jadi bentuk kurung yang sama tidak selalu berarti object.

### Operator dan kata kunci pada SQL

**Operator perbandingan SQL `=` dan `>`** membandingkan nilai pada setiap baris dan menghasilkan kondisi yang dapat dipakai untuk memilih atau menggabungkan baris. Pada query roadmap, `p.user_id = u.id` mencocokkan foreign key pesanan dengan primary key user, sedangkan `p.status = 'selesai'` hanya menerima pesanan berstatus selesai. `>` berarti lebih besar; pada query contoh lain operator ini terlihat dalam JavaScript (`stok > 0`), bukan kondisi SQL. Jangan tertukar dengan `=` JavaScript yang melakukan assignment: arti operator ditentukan bahasa tempat ekspresi itu ditulis.

**Operator logika SQL `AND`** menggabungkan syarat sehingga semua syarat harus terpenuhi agar baris lolos. Contohnya `WHERE id = 5 AND user_id = 12` hanya mencocokkan pesanan yang sekaligus memiliki ID 5 dan dimiliki user 12. Pada JavaScript, bentuk operasi logika sejenis ditulis `&&`; ejaan SQL `AND` adalah keyword SQL, bukan simbol `&&`.

```sql
SELECT p.id, p.status
FROM pesanan p
WHERE p.status = 'selesai'
  AND p.total > 0;
```

Query tersebut memilih kolom `id` dan `status` dari tabel `pesanan`, lalu mempertahankan baris yang statusnya tepat `"selesai"` dan totalnya lebih besar dari nol. Kedua kondisi harus benar. Tanda koma di `SELECT` memisahkan daftar kolom; `FROM`, `WHERE`, dan `AND` adalah keyword SQL yang menyusun query, sedangkan `=` dan `>` adalah operator perbandingan.

Pada query SQL yang ada di roadmap, `JOIN ... ON` menentukan kecocokan baris antartabel, `WHERE` menyaring baris, `GROUP BY` membentuk kelompok, `COUNT(...)` menghitung baris/nilai, `ORDER BY ... DESC` mengurutkan hasil dari nilai terbesar ke terkecil, dan `LIMIT` membatasi jumlah baris hasil. Sebagian besar kata tersebut adalah **keyword atau fungsi SQL**, bukan operator aritmetika. Alias `u` dan `p` setelah nama tabel, serta `AS total_pesanan`, memberi nama singkat agar query lebih mudah dibaca; alias tidak mengubah data sumber.

```sql
SELECT u.nama, COUNT(p.id) AS total_pesanan
FROM users u
JOIN pesanan p ON p.user_id = u.id
WHERE p.status = 'selesai'
GROUP BY u.nama
ORDER BY total_pesanan DESC
LIMIT 5;
```

Untuk memahami urutan logisnya, mulai dari `FROM users u` (sumber awal dan alias tabel), lalu `JOIN pesanan p ON ...` (pasangkan user dengan pesanan yang foreign key-nya cocok). `WHERE` hanya mempertahankan baris pesanan yang statusnya `'selesai'` sebelum pengelompokan. `GROUP BY u.nama` menggabungkan baris berdasarkan nilai nama; bila dua user berbeda memiliki nama sama, query ini akan menggabungkan pesanan mereka menjadi satu kelompok. Pada aplikasi nyata, kelompok yang benar-benar per user biasanya memakai `GROUP BY u.id, u.nama`. `COUNT(p.id)` menghitung pesanan dalam setiap kelompok. `AS total_pesanan` memberi nama hasil hitungan; `ORDER BY ... DESC` menempatkan jumlah terbesar lebih dahulu, dan `LIMIT 5` mengambil lima baris teratas. Walaupun `SELECT` tertulis di awal, pemilihan hasil secara logis terjadi setelah sumber, filter, dan pengelompokan ditentukan. Lihat dokumentasi PostgreSQL tentang [operator perbandingan](https://www.postgresql.org/docs/current/functions-comparison.html), [operator logika](https://www.postgresql.org/docs/current/functions-logical.html), dan [SELECT](https://www.postgresql.org/docs/current/sql-select.html).

### Penanda sintaks tambahan pada contoh

Tidak semua karakter yang tampak seperti operator melakukan perhitungan atau perbandingan. `@id`, `@default(...)`, `@unique`, dan `@relation(...)` dalam schema Prisma adalah **attribute** (metadata yang mengatur kolom/model), bukan operator JavaScript. `String?` dan `Pesanan[]` adalah notasi tipe Prisma untuk field nullable dan relasi berbentuk daftar. Di Tailwind, `hover:bg-blue-700` dan `md:px-8` memakai titik dua sebagai pemisah variant/class; ini bukan ternary atau anotasi TypeScript. Di JSX, `<KartuProduk ... />` adalah sintaks elemen, dan `className={...}` memakai kurung kurawal untuk menyisipkan ekspresi JavaScript.

Pada `package.json`, karakter `^` dalam versi seperti `"axios": "^1.7.0"` juga bukan operator JavaScript. Itu adalah penanda rentang versi **semantic versioning** yang dipahami npm: untuk versi non-zero-major seperti `1.7.0`, npm dapat memasang versi yang kompatibel mulai `1.7.0` hingga sebelum `2.0.0` (pembaruan patch/minor, bukan major). Aturan detail mengikuti semantic versioning dan perilaku npm; lihat [npm: About semantic versioning](https://docs.npmjs.com/about-semantic-versioning).

Penanda `<<<<<<<`, `=======`, dan `>>>>>>>` pada contoh *merge conflict* Git bukan operator maupun sintaks program. Git menambahkan teks tersebut ke file untuk menandai bagian yang belum berhasil digabung otomatis: bagian sebelum `=======` biasanya perubahan pada sisi `HEAD`, bagian setelahnya perubahan dari branch yang digabung, dan baris `>>>>>>>` menunjukkan nama/ujung sisi lain. Developer harus memilih atau menggabungkan isi yang benar lalu menghapus penanda sebelum menyimpan hasil. Lihat [GitHub Docs: Resolving a merge conflict](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts).

Perhatikan juga perbedaan `delete` sebagai **nama method** dan `delete` sebagai operator JavaScript. Pada `prisma.user.delete({ where: { id: 1 } })`, `delete` adalah property method milik API Prisma yang dipanggil dengan `()`; ia bukan operator JavaScript `delete`, yang mencoba menghapus property tertentu dari object. Operator tersebut biasanya menghasilkan boolean; pada property yang tidak dapat dikonfigurasi, hasilnya `false` dalam mode non-strict dan dapat melempar `TypeError` dalam strict mode. Arti kata yang sama ditentukan oleh konteks sintaksnya. Lihat [MDN: `delete` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete).

Tanda kutip (`"..."` atau `'...'`) membatasi string; backtick membatasi template literal; tanda `#` pada contoh terminal menandai komentar shell; dan `//` pada JavaScript/TypeScript menandai komentar satu baris. Komentar tidak dijalankan sebagai instruksi. Dalam contoh JSX, `<!-- -->` adalah komentar HTML, sementara sintaks komentar di dalam ekspresi JSX biasanya `{/* komentar */}`. Contoh-contoh ini membantu membedakan tanda baca yang mengubah nilai dari tanda baca yang hanya menstrukturkan kode.

### Contoh terpadu: membaca operator secara berurutan

```js
const namaTampilan = user?.nama ?? "Tanpa nama";
const total = harga * jumlah;
const tersedia = jumlah > 0 && total >= 10000;
const label = tersedia ? `${namaTampilan}: Rp${total}` : "Belum tersedia";
```

Baris pertama memakai optional chaining untuk membaca `nama` dengan aman, lalu nullish coalescing untuk memberikan fallback hanya ketika hasilnya `null` atau `undefined`. Baris kedua menghitung total dengan perkalian. Baris ketiga membandingkan jumlah dengan nol dan total dengan 10000, kemudian `&&` mensyaratkan kedua hasil perbandingan bernilai benar. Baris terakhir menggunakan ternary: bila `tersedia` benar, template literal menyusun nama dan total; bila salah, hasilnya teks `"Belum tersedia"`. Assignment `=` menyimpan hasil setiap ekspresi pada variable di kiri. Dengan menelusuri per baris seperti ini, operator tidak perlu ditebak dari bentuk simbolnya saja.

**Dokumentasi resmi untuk pendalaman:**

- [MDN: Expressions and operators (JavaScript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators) — kategori operator, prioritas evaluasi, dan contoh JavaScript.
- [MDN: Nullish coalescing operator `??`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) dan [optional chaining `?.`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) — perbedaan fallback nullish dan akses aman.
- [MDN: Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) — parameter, badan fungsi, dan nilai balik implisit.
- [TypeScript Handbook: Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) — anotasi, optional property, dan union type.
- [React: Writing Markup with JSX](https://react.dev/learn/writing-markup-with-jsx) — aturan sintaks JSX dan penyisipan ekspresi JavaScript.
- [PostgreSQL: SQL Syntax](https://www.postgresql.org/docs/current/sql-syntax.html) — struktur query dan sintaks SQL PostgreSQL.
- [Prisma: Prisma Schema](https://www.prisma.io/docs/orm/prisma-schema) — model, field, type, dan attribute pada schema Prisma.

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
🔍 **Penjelasan:** tiap baris = `perintah [opsi] [target]`. Teks setelah `#` adalah komentar, bukan bagian perintah. Pola umum: **kata kerja** (`cd`, `mkdir`) lalu **objek yang dikenai** (nama folder).

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
🔍 **Struktur `package.json`:**
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
🔍 **Penjelasan:**
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
🔍 **Debugging:** sisipkan `console.log` di titik yang dicurigai, jalankan, lalu bandingkan **nilai yang kamu kira** dengan **nilai sebenarnya**. Bug hampir selalu berada di titik pertama di mana keduanya berbeda.

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
🔍 **Penjelasan:** `const` = "konstan, nama ini tidak boleh dipindah ke nilai lain". `let` = "boleh diganti". Catatan: `const` pada objek/array hanya mengunci **penunjuknya**, isinya masih bisa diubah:
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
🔍 **Aturan lexical scope:**
- Kode dapat mengakses deklarasi pada scope saat ini dan scope pembungkusnya.
- Kode di scope luar tidak dapat mengakses deklarasi yang hanya ada di scope bagian dalam.
- `let` dan `const` yang dideklarasikan di dalam block hanya tersedia di block tersebut dan block di dalamnya.

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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:** `(a, b) => a + b` → "diberi `a` dan `b`, menghasilkan `a + b`". Jika setelah `=>` ada `{`, itu **blok kode** sehingga butuh `return` eksplisit. Jika tidak, hasilnya langsung dikembalikan.

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
🔍 **Penjelasan:** bayangkan **bentuk sisi kiri meniru bentuk data di kanan**. `{ nama, kelas }` artinya "ambil properti bernama `nama` dan `kelas` dari `user`, jadikan variabel". Untuk array, **urutan** yang menentukan, bukan nama.

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
🔍 **Arti `...` bergantung pada posisi sintaksnya:**
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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:**
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
🔍 **Ringkasan array methods:**

| Method | Fungsi | Hasil |
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
🔍 **Penjelasan:** `parse` = "urai teks menjadi data". `stringify` = "ubah data jadi teks (untuk dikirim)".

## 1.10 Asynchronous JavaScript

### Event Loop
```js
console.log("1");
setTimeout(() => console.log("2"), 0);
console.log("3");
// Output: 1, 3, 2
```
🔍 **Penjelasan:**
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
🔍 **Penjelasan:** "Minta data → **lalu** ubah ke JSON → **lalu** cetak → **jika gagal di langkah mana pun**, tangkap di `.catch`." Tiap `.then` menerima hasil `.then` sebelumnya.

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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:** "Mulai **dua** request **bersamaan**, tunggu **keduanya** selesai, lalu ambil hasilnya (destructuring array)." Lebih cepat daripada dua `await` berurutan.

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
🔍 **Argumen `fetch`:** `fetch(ALAMAT, { PENGATURAN })`. Argumen kedua berisi `method` (jenis aksi), `headers` (metadata request, misalnya format JSON), dan `body` (isi request; untuk JSON, ubah data menjadi teks dengan `JSON.stringify`).
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
🔍 **Alur kerja:** `add` (siapkan perubahan) → `commit` (simpan snapshot + pesan) → `push` (kirim ke GitHub).

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
🔍 Penjelasan: bagian atas `=======` = milikmu, bagian bawah = milik mereka. Pilih/gabungkan, **hapus ketiga tanda** itu, lalu commit.

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
🔍 **Penjelasan:** pisahkan per spasi, tiap kata = satu aturan CSS.

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
🔍 Penjelasan: "grid dengan 1 kolom; **mulai tablet** jadi 2 kolom; **mulai layar besar** jadi 3 kolom; jarak antar-item 4 unit."

## 2.2 React: JSX

```jsx
const nama = "Budi";
const sapaan = (
  <h1 className="text-2xl">
    Halo, {nama}! 2 + 3 = {2 + 3}
  </h1>
);
```
🔍 **Penjelasan:** di dalam tag, teks biasa dibaca sebagai teks. Apa pun di dalam `{ }` dibaca sebagai **JavaScript**. Perbedaan dengan HTML: `class` → `className`, tag harus ditutup (`<img />`), dan satu komponen harus punya **satu elemen pembungkus** (boleh `<> ... </>`).

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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:**
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
🔍 Penjelasan baris terakhir: "untuk tiap `p`: **jika** `id`-nya cocok, **ganti dengan salinan** `p` yang `selesai`-nya `true`; **jika tidak**, biarkan `p`."

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
🔍 **Urutan eksekusi:**
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
🔍 Penjelasan: "`inputRef.current` menunjuk elemen `<input>` asli; panggil `.focus()` pada elemen itu."

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
🔍 Penjelasan: `Provider` = "**menyiarkan** nilai ke semua komponen di dalamku"; `useContext` = "**menangkap** siaran terdekat".

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
🔍 Penjelasan: "Hook ini menerima `url`, mengatur state & efek sendiri, lalu **mengembalikan** `{data, loading}` agar komponen manapun tinggal memakai."

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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:**
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
🔍 **Penjelasan:**
- Titik dua `:` dibaca "**bertipe**". `umur: number` = "`umur` bertipe angka".
- `interface User { ... }` = "cetakan: objek `User` **harus** punya `id` (angka), `nama` (teks), dan **boleh** punya `email`".
- `"aktif" | "nonaktif"` = "salah satu dari ini saja". Garis `|` dibaca "atau".
- Pada fungsi: `(user: User, salam: string = "Halo"): string` → "menerima `user` bertipe `User`, `salam` bertipe teks (default `Halo`), **mengembalikan** teks". Tipe **setelah** tanda kurung = tipe hasil.

**Generic** (tipe sebagai "variabel"):
```ts
function ambilPertama<T>(arr: T[]): T { return arr[0]; }
const x = ambilPertama<string>(["a", "b"]);   // x bertipe string
```
🔍 Penjelasan: "`T` adalah **tipe apa pun** yang nanti ditentukan. Jika diberi array `T`, hasilnya satu `T`." Sama seperti `useState<string>("")` atau `Promise<User>`.

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
🔍 Penjelasan: `KartuProps` mendefinisikan bentuk props. `() => void` = "fungsi tanpa argumen yang tidak mengembalikan apa-apa". `useState<number>(0)` = "state bertipe angka".

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
🔍 **Penjelasan:** **folder = segmen URL**, nama file spesial menentukan perannya (`page.tsx` = halaman, `layout.tsx` = pembungkus, `route.ts` = API). Folder dengan `[id]` = **bagian variabel** URL.

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
🔍 Penjelasan: `children` = "isi halaman yang sedang dibuka", disisipkan di antara navbar dan footer. Layout tidak dimuat ulang saat berpindah halaman.

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
🔍 **Penjelasan:**
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
🔍 Penjelasan: baris `"use client"` di paling atas = "**file ini berjalan di browser**". Wajib jika memakai `useState`, `useEffect`, atau event (`onClick`).

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
🔍 Penjelasan: `params` berisi bagian variabel dari URL. Pada Next.js versi terbaru `params` berupa **Promise** sehingga perlu `await` (di versi lama langsung objek, cek dokumentasi versi yang kamu pakai). `Number(id)` karena URL selalu berupa teks.

## 3.4 SSR vs SSG

```tsx
// SSG-like: di-cache (statis)
const res = await fetch("https://api.example.com/artikel", { cache: "force-cache" });

// SSR-like: selalu ambil data baru
const res = await fetch("https://api.example.com/harga", { cache: "no-store" });

// ISR: statis, tapi disegarkan tiap 60 detik
const res = await fetch("https://api.example.com/berita", { next: { revalidate: 60 } });
```
🔍 **Penjelasan:** opsi di argumen kedua `fetch` menentukan strategi: **simpan** (`force-cache`), **jangan simpan** (`no-store`), atau **simpan sementara** (`revalidate: detik`). Perilaku default caching Next.js bisa berbeda antar versi, jadi selalu tuliskan eksplisit.

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
🔍 **Penjelasan:**
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
🔍 Penjelasan: **nama fungsi = method HTTP** (`GET`, `POST`). `request.json()` = baca isi kiriman. `{ status: 201 }` = "berhasil dibuat". Kapan memilih? Server Action untuk form di aplikasimu sendiri; API Route bila ada pihak luar (mobile app, webhook) yang perlu memanggil.

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
🔍 **Urutan evaluasi SQL:**
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
🔍 **Relasi pada diagram:** `1` = satu, `<` (kaki gagak) = banyak. Satu user punya banyak pesanan, tetapi satu pesanan hanya milik satu user. Many-to-Many butuh **tabel penghubung** yang menyimpan pasangan `siswa_id` + `ekskul_id`.

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
🔍 **Struktur schema Prisma:** tiap baris di dalam `model` = `namaKolom Tipe [atribut]`.
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
🔍 **Pola query Prisma:** `prisma.NAMA_MODEL.AKSI({ opsi })`.
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
🔍 Penjelasan: `env("DATABASE_URL")` = "ambil nilai dari file `.env`", jadi password tidak tertulis di kode.

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
🔍 Penjelasan: `hash(teks, 10)` = ubah jadi kode acak satu arah (angka 10 = tingkat "kerumitan"). `compare` = "apakah teks ini jika di-hash sama dengan hash tersimpan?" Password asli **tidak pernah disimpan**.

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
🔍 Penjelasan: "Ambil sesi di server. **Jika belum login**, alihkan ke `/login`; jika sudah, tampilkan halaman." Pengecekan **di server** itu wajib; menyembunyikan menu di UI saja tidak cukup.

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
🔍 Penjelasan: "cari pesanan dengan `id` itu **DAN** pemiliknya adalah user yang sedang login." Tanpa `userId`, siapa pun bisa mengintip pesanan orang lain.

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
🔍 **Penjelasan:**
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
🔍 Penjelasan: sebelum membangun Next.js, buat dulu klien Prisma. Tanpa ini, build di Vercel bisa gagal.

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
🔍 Penjelasan: "Untuk tiap huruf: ambil hitungan sebelumnya (atau `0` jika belum ada), tambah 1, simpan lagi." Baris `hasil[huruf] = ...` memakai `huruf` sebagai **nama kunci**.

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

# PANDUAN RINCI SETIAP POIN ROADMAP

Bagian ini memperjelas tujuan dan istilah penting pada **setiap poin bernomor**, dari 0.1 sampai 6.3. Gunakan bersama penjelasan dan contoh kode pada fase sebelumnya: tabel ini menerangkan apa yang perlu dipahami, mengapa dipelajari, dan tanda bahwa konsepnya sudah mulai dikuasai. Nama properti, opsi, dan simbol dalam contoh tetap harus dibaca menurut konteksnya—misalnya `name` pada HTML adalah atribut input, sedangkan `name` pada `package.json` adalah properti metadata proyek.

## Referensi Keyword, Property, Operator, dan Sintaks JavaScript per Poin

Bagian ini adalah panduan istilah kode yang dipakai pada contoh roadmap, bukan ringkasan tujuan belajar. **Keyword** adalah kata khusus bahasa seperti `const`, `return`, dan `await`; **property** adalah nilai bernama pada object seperti `res.ok`; **method** adalah function yang diakses dari object seperti `array.map()`; **operator** mengolah nilai seperti `===`, `&&`, dan `...`. Beberapa contoh memakai API React/Next.js atau sintaks HTML/SQL/Prisma, bukan keyword JavaScript; perbedaan itu disebutkan supaya tidak tertukar.

### Phase 1: JavaScript Modern & Asynchronous

#### 1.1 `let` dan `const`
- **Analogi:** `const` seperti label kotak yang tidak boleh dipindah ke kotak lain; `let` seperti label yang boleh dipindah. Isi kotak object masih dapat berubah walaupun labelnya `const`.
- `const` dan `let` adalah keyword deklarasi variable. `const` melarang variable di-assign ulang; `let` mengizinkannya. Keduanya memiliki block scope.
- `=` adalah operator assignment: nilai di kanan disimpan ke nama di kiri. `nama = "Andi"` pada contoh adalah assignment ulang dan akan error bila `nama` dideklarasikan dengan `const`.
- `// ...` memulai komentar satu baris; komentar tidak dieksekusi.
- Pada array, `.push(nilai)` adalah method yang menambahkan item ke akhir array. `daftar.push(3)` mengubah isi array yang sama, bukan mengganti binding `daftar`.

#### 1.2 Scope & Closure
- **Analogi:** Scope seperti ruangan bertingkat: orang di ruangan dalam dapat melihat fasilitas ruangan luar, tetapi orang di luar tidak otomatis bisa melihat barang yang hanya ada di dalam. Closure seperti membawa kunci/akses ke ruangan asal saat keluar.
- `function` mendeklarasikan function; `return` mengakhiri pemanggilan function dan mengirim nilai kembali ke pemanggil.
- `{ ... }` pada function dan `if` membentuk blok. `if (true)` memakai kondisi boolean; `console.log(...)` memanggil method untuk menampilkan nilai.
- `const lokal` dan `const blok` hanya dapat diakses dalam scope tempat deklarasinya serta scope di dalamnya. Mengaksesnya dari luar menyebabkan `ReferenceError`.
- Pada `return function () { ... }`, function bagian dalam adalah nilai yang dikembalikan. Ia tetap dapat membaca dan memperbarui `hitung` dari scope pembungkusnya; ini yang disebut closure.
- `hitung = hitung + 1` menggunakan assignment dan operator aritmetika `+`. `counterA()` memanggil function; tiap pemanggilan membaca nilai `hitung` terakhir yang sama.

#### 1.3 Arrow Function & Shorthand
- **Analogi:** Function adalah resep; parameter adalah tempat bahan dimasukkan. Arrow function menulis resep itu dengan ringkas, sedangkan `return` menyerahkan hasil masakan kepada pemanggil.
- `=>` membentuk arrow function. `(a, b) => a + b` punya hasil implisit karena badannya satu expression; `(a, b) => { return a + b; }` memakai blok sehingga `return` ditulis.
- `;` mengakhiri statement; `{}` pada `function`/blok menandai kumpulan statement, sedangkan `{}` dalam object literal membentuk object.
- `const nama = "Budi", umur = 17` mendeklarasikan dua variable dengan satu `const`. Ini sah, tetapi deklarasi terpisah sering lebih mudah dibaca.
- `{ nama, umur }` adalah shorthand property: sama dengan `{ nama: nama, umur: umur }`. `nama:` pada bentuk panjang memisahkan nama property dan nilai, bukan operator.
- `() => ({ nama: "Budi" })` memakai tanda kurung agar `{...}` dikenali sebagai object yang dikembalikan, bukan blok function.

#### 1.4 Destructuring
- **Analogi:** Destructuring seperti mengambil barang dari laci berdasarkan label untuk object, atau berdasarkan urutan posisi untuk array.
- `const { nama, kelas } = user` adalah object destructuring: ambil property `nama` dan `kelas` dari `user`, lalu buat variable dengan nama yang sama. `=` di sini menginisialisasi variable.
- `const { alamat: { kota } } = user` mengambil property bertingkat. Tanda `:` pada pola destructuring memberi nama/struktur sumber, bukan anotasi tipe.
- `const { umur = 17 } = user` memberi nilai default saat property `umur` bernilai `undefined` atau tidak tersedia; nilai `null` tidak memicu default ini.
- `[pertama, , ketiga]` adalah array destructuring berdasarkan posisi. Koma kosong melewati elemen kedua; indeks array dimulai dari 0.

#### 1.5 Spread & Rest
- **Analogi:** Spread seperti menuangkan isi kotak ke tempat baru; rest seperti mengumpulkan barang-barang yang tersisa ke dalam satu kotak.
- `...` adalah spread saat menyebarkan isi array/object, misalnya `[...a, 3]` atau `{ ...user }`.
- `...` adalah rest saat mengumpulkan sisa argument/elemen menjadi satu array, misalnya `function jumlah(...angka)`.
- `{ ...user, kota: "Malang" }` membuat object baru dari property `user`, lalu menetapkan/menimpa property `kota`. Jika nama property duplikat, nilai paling akhir yang dipakai.
- `reduce((total, n) => total + n, 0)` memanggil method array `.reduce`; `total` adalah accumulator dan `0` adalah nilai awal. Koma di daftar argument memisahkan callback dan nilai awal, bukan operator.

#### 1.6 Template Literal, Optional Chaining, Nullish Coalescing
- **Analogi:** Template literal seperti mengisi bagian kosong pada formulir kalimat; `?.` seperti memeriksa apakah pintu berikutnya ada sebelum masuk; `??` seperti memakai nilai cadangan hanya jika tempat utama benar-benar kosong.
- Backtick `` `...` `` membuat template literal; `${ekspresi}` mengevaluasi JavaScript lalu menyisipkan hasilnya ke string.
- `?.` adalah optional chaining. `user?.alamat?.kota` berhenti dan menghasilkan `undefined` jika nilai di kiri `?.` adalah `null` atau `undefined`.
- `??` adalah nullish coalescing: gunakan nilai kanan hanya jika nilai kiri `null`/`undefined`.
- `||` adalah OR logis dan memilih nilai kanan bila nilai kiri falsy, termasuk `0`, `false`, dan `""`. Karena itu `??` dan `||` tidak selalu saling menggantikan.
- `=` dalam `const kota = ...` tetap assignment/inisialisasi variable, bukan bagian dari operator `??`.

#### 1.7 Modul `import` & `export`
- **Analogi:** File module seperti ruang kerja dengan barang yang tidak otomatis bisa dipakai ruangan lain; `export` membuka barang tertentu, lalu `import` mengambilnya.
- `export` dan `import` adalah keyword sistem module JavaScript. `export function ...` dan `export const ...` membuat ekspor bernama.
- `export default` menandai ekspor default. Import default tidak memakai kurung kurawal; ekspor bernama ditulis dalam `{ ... }` dan nama harus cocok.
- `from` adalah bagian dari sintaks import yang diikuti string path. `"./utils/harga.js"` adalah path relatif; `"axios"` adalah nama package.
- `return` mengirim hasil dari function ke pemanggil. String `"Rp " + angka...` memakai `+` untuk menggabungkan teks; `.toLocaleString("id-ID")` adalah method angka untuk menghasilkan format lokal.

#### 1.8 Array Methods
- **Analogi:** Array methods seperti lini pengolahan barang: `map` mengganti setiap barang, `filter` memilih yang lolos syarat, `find` mengambil satu yang cocok, dan `reduce` menggabungkan semuanya menjadi satu hasil.
- `.map(callback)` menjalankan callback untuk setiap item dan mengembalikan array hasil baru. `.filter(callback)` mempertahankan item ketika callback menghasilkan truthy. `.find(callback)` mengembalikan item cocok pertama atau `undefined`.
- `.reduce(callback, nilaiAwal)` menggabungkan item menjadi satu hasil. Callback menerima accumulator dan item saat ini.
- `p => p.nama` adalah callback arrow function dengan hasil implisit. `p.stok > 0` memakai operator perbandingan dan menghasilkan boolean.
- `===` membandingkan nilai dan tipe secara ketat; `!==` membandingkan ketidaksamaan ketat. Pada `p.nama === "Topi"`, hasil boolean dipakai oleh `.find`.
- `0` pada `reduce(..., 0)` adalah nilai awal jumlah, agar array kosong tetap menghasilkan angka 0.

#### 1.9 HTTP Dasar & JSON
- **Analogi:** HTTP seperti layanan pengiriman: method menjelaskan jenis layanan, header adalah label/petunjuk paket, body adalah isi paket, dan status adalah kabar hasil pengirimannya. JSON adalah format tulisan standar untuk mencatat isi paket.
- `JSON.parse(teks)` dan `JSON.stringify(nilai)` adalah method pada object global `JSON`; yang pertama mengurai teks JSON menjadi nilai JavaScript, yang kedua membuat teks JSON.
- `"nama"` dan `"umur"` pada JSON adalah nama property dalam format teks. JSON hanya mendukung bentuk data tertentu; function dan `undefined` bukan nilai JSON.
- `GET`, `POST`, `PUT`, `PATCH`, dan `DELETE` di contoh HTTP adalah nilai method/protokol, bukan keyword JavaScript.
- `Content-Type` dan `Authorization` adalah nama header HTTP; status seperti `200` adalah kode response. CORS adalah kebijakan browser mengenai origin, bukan operator atau fitur yang mengautentikasi user.

#### 1.10 Asynchronous JavaScript
- **Analogi:** Asynchronous seperti mengambil nomor antrean: program tidak harus berdiri menunggu, dapat mengerjakan hal lain lalu kembali saat hasil siap. Promise adalah tanda terima bahwa hasil akan tersedia atau gagal nanti.
- `setTimeout(callback, 0)` adalah pemanggilan function API yang menjadwalkan callback; angka `0` meminta jeda minimum, bukan berarti callback berjalan sebelum kode sinkron selesai.
- `.then(callback)` mendaftarkan langkah untuk hasil Promise; `.catch(callback)` menangani rejection; `.finally(callback)` menjalankan langkah akhir terlepas dari sukses/gagal.
- `async` menandai function yang hasilnya selalu Promise. `await` menunggu hasil Promise di dalam function async; ia tidak menghentikan seluruh browser.
- `try`, `catch`, dan `finally` adalah keyword untuk jalur error. `throw new Error(...)` melempar exception; `new` membuat instance object Error.
- `if (!res.ok)` memakai `!` untuk membalik boolean property `ok`. `res.status` adalah property status HTTP; `res.ok` bernilai true untuk response HTTP sukses.
- `Promise.all([...])` adalah method static pada `Promise`; daftar Promise dimulai bersamaan, hasilnya berupa array sesuai urutan input, dan satu rejection membuat keseluruhannya reject.
- `[users, produk]` menerima hasil array dengan destructuring; posisi menentukan hasil mana yang masuk ke variable.

#### 1.11 Fetch API & Axios
- **Analogi:** `fetch` dan Axios seperti dua cara mengisi formulir permintaan ke server; keduanya mengirim alamat, instruksi, dan isi, lalu menerima paket balasan yang perlu diperiksa.
- `fetch(url, options)` memanggil API untuk membuat request. Object options memiliki property `method`, `headers`, dan `body`; nama-nama ini bagian dari API Fetch, bukan keyword.
- `headers: { "Content-Type": "application/json" }` menyatakan format body. `body: JSON.stringify(data)` mengubah object JavaScript menjadi teks untuk dikirim.
- `await fetch(...)` menghasilkan object `Response`; `.json()` membaca body dan mengurai JSON, juga secara asynchronous.
- `res.ok` dan `res.status` adalah property Response. Fetch tidak reject hanya karena status 404/500, jadi periksa `ok` sendiri.
- `import axios from "axios"` mengimpor default export package Axios; `axios.post(url, data)` membuat request POST. `{ data }` adalah destructuring property `data` dari object response Axios.

#### 1.12 Git & GitHub
- **Analogi:** Git seperti buku catatan perubahan proyek; commit adalah satu catatan tersimpan, branch seperti jalur kerja terpisah, dan Pull Request seperti meminta rekan memeriksa perubahan sebelum digabung.
- `git init`, `git add`, `git commit`, `git branch`, `git checkout`, dan `git push` adalah perintah Git di terminal, bukan sintaks JavaScript.
- `-m` adalah opsi perintah commit untuk memberi pesan; `"feat: ..."` adalah string pesan commit. Prefix `feat:`, `fix:`, dan `docs:` adalah konvensi teks.
- `.gitignore`, `.env`, `.next`, dan `node_modules` adalah nama file/folder; bukan keyword atau property JavaScript.
- `<<<<<<<`, `=======`, `>>>>>>>` adalah penanda teks Git untuk merge conflict. Hapus penanda setelah memilih/menggabungkan isi, bukan biarkan sebagai kode.

### Phase 2: Tailwind & React

#### 2.1 Tailwind CSS
- **Analogi:** Class Tailwind seperti label instruksi pada sebuah elemen: satu label untuk warna, satu untuk jarak, dan label bersyarat untuk hover atau ukuran layar.
- `class` pada HTML dan `className` pada JSX adalah atribut/property untuk daftar class CSS, bukan keyword/operator JavaScript.
- `bg-blue-600`, `text-white`, `px-4`, `py-2`, `rounded-lg`, dan `gap-4` adalah nama utility Tailwind. Spasi memisahkan beberapa class.
- `hover:` dan `md:` adalah variant Tailwind: aturan diterapkan pada kondisi hover atau breakpoint medium ke atas. Titik dua di sini bukan ternary atau anotasi tipe.
- `grid-cols-1`, `md:grid-cols-2`, dan `lg:grid-cols-3` menentukan jumlah kolom pada ukuran layar berbeda. Kelas tanpa prefix berlaku sebagai aturan dasar mobile-first.

#### 2.2 React: JSX
- **Analogi:** JSX seperti cetak biru tampilan yang boleh menyisipkan nilai JavaScript ke bagian tertentu; React memakai cetak biru itu untuk menentukan UI.
- JSX memakai tag seperti `<h1>`; `className` adalah property JSX untuk class, dan `<img />` adalah elemen yang ditutup sendiri.
- `{nama}` atau `{2 + 3}` menyisipkan expression JavaScript ke JSX. `{}` bukan object literal di sini; konteksnya adalah batas expression JSX.
- `const` mendeklarasikan variable; `=` memberikan hasil JSX atau string kepadanya. JSX bukan string HTML.
- Fragment `<>...</>` mengelompokkan beberapa elemen tanpa menambahkan elemen DOM pembungkus.

#### 2.3 Komponen & Props
- **Analogi:** Component seperti cetakan kartu; props adalah data yang diberikan untuk mengisi cetakan tersebut. Cetakan menerima data, tetapi tidak seharusnya mengubah kiriman dari pemiliknya.
- `function KartuProduk(...)` mendeklarasikan component; nama berhuruf besar menandai component React.
- `{ nama, harga, stok = 0 }` adalah destructuring parameter props. `stok = 0` adalah nilai default untuk prop yang tidak diberikan/`undefined`.
- `<KartuProduk nama="Kaos" harga={50000} />`: `nama` dan `harga` adalah nama props; teks diberi tanda kutip, sedangkan angka/expression ditulis dalam `{}`.
- `harga.toLocaleString("id-ID")` membaca property `harga` lalu memanggil method angka untuk format lokal.
- `return (...)` mengembalikan JSX. Props adalah input read-only; untuk meminta perubahan, child memanggil callback prop yang disediakan parent.

#### 2.4 Conditional Rendering & Rendering List
- **Analogi:** Conditional rendering seperti memilih papan informasi yang sesuai keadaan (memuat, kosong, atau siap); `map` seperti mencetak satu label untuk setiap barang, sementara `key` adalah nomor identitas tiap label.
- `if (kondisi) return ...` adalah conditional statement dan early return; `===` membandingkan nilai/tipe.
- `.map((p) => (...))` mengubah setiap object produk menjadi elemen `<li>`. Property `p.id`, `p.nama`, dan `p.stok` mengambil nilai object.
- `key={p.id}` adalah prop khusus React untuk identitas item list. React menggunakannya saat mencocokkan item antar-render; `key` tidak otomatis menjadi prop biasa yang dapat dibaca component anak.
- `kondisi && <span>` memakai AND logis untuk menghasilkan elemen saat kondisi benar. Ternary `kondisi ? A : B` memilih satu dari dua expression.
- Untuk daftar kosong, `produk.length === 0` membaca property panjang array. Jika memakai `produk.length && ...`, angka `0` dapat tampil di UI; lebih jelas gunakan perbandingan boolean eksplisit.

#### 2.5 State: `useState`
- **Analogi:** State seperti papan skor yang dikelola React. Meminta setter mengubah skor membuat React memperbarui tampilan papan; mengubah catatan diam-diam tanpa memberi tahu React tidak cukup.
- `import { useState } from "react"` mengambil ekspor bernama React. `useState(0)` adalah pemanggilan Hook dengan nilai awal.
- `const [count, setCount] = ...` memakai array destructuring: state saat ini lalu fungsi setter. Nama setter mengikuti konvensi `set` + nama state.
- `onClick={...}` adalah prop event React. Nilainya function callback, bukan pemanggilan langsung saat render.
- `() => setCount(count + 1)` membuat callback; `+` menghitung nilai baru. Untuk update berdasar state sebelumnya, `setCount((prev) => prev + 1)` memakai updater function.
- `setProduk([...produk, baru])`, `.filter(...)`, dan `.map(...)` membentuk array baru. `{ ...p, selesai: true }` menyalin object lalu mengganti property `selesai`; `id !== idHapus` mempertahankan item lain.

#### 2.6 Side Effect: `useEffect`
- **Analogi:** Render adalah menggambar ulang layar; effect adalah pekerjaan setelah gambar siap, seperti memesan data atau memasang alarm. Dependency array adalah daftar hal yang bila berubah membuat pekerjaan itu dijalankan kembali.
- `useEffect(callback, dependencies)` adalah Hook React. Callback effect berjalan setelah render dan dependency array menentukan kapan effect diulang.
- `[]` adalah array dependency kosong; `[id]` adalah array dengan nilai yang dipantau; tanpa argumen kedua effect dapat dijalankan lagi setelah setiap render.
- `async function muat()` mendefinisikan fungsi asynchronous di dalam effect. Callback `useEffect` sendiri tidak dibuat `async` karena callback effect diharapkan mengembalikan cleanup atau tidak mengembalikan apa pun.
- `setProduk(await res.json())` menunggu parsing JSON lalu menyimpan data ke state. `setLoading(false)` berjalan pada blok `finally`.
- `setError(e.message)` membaca property pesan error. Pada TypeScript, nilai catch dapat `unknown`, sehingga perlu diperiksa sebelum membaca `message`.
- Contoh roadmap perlu mempertimbangkan cleanup/cancel saat request lama masih berjalan dan component dilepas; dependency `[]` berarti URL tidak berubah dalam contoh tersebut.

#### 2.7 `useRef`, Context & Custom Hook
- **Analogi:** Ref seperti catatan kecil yang bisa diperbarui tanpa menggambar ulang layar; Context seperti pengumuman yang dapat didengar komponen di sekitarnya; custom Hook seperti mengemas resep logika agar dapat dipakai ulang.
- `useRef(null)` membuat object ref yang property `.current`-nya dapat menunjuk ke elemen DOM. `ref={inputRef}` menghubungkan ref dengan elemen.
- `.focus()` adalah method DOM untuk memindahkan fokus ke input. `inputRef.current` bisa null sebelum elemen terpasang, sehingga kode produksi dapat perlu pemeriksaan null.
- `createContext("terang")` membuat Context dengan nilai default; `<ThemeContext.Provider value="gelap">` menyediakan property `value` bagi descendant.
- `useContext(ThemeContext)` membaca nilai Provider terdekat. Ternary `tema === "gelap" ? ... : ...` memilih class berdasarkan nilainya.
- `function useFetch(url)` adalah custom Hook; awalan `use` mengikuti aturan React. `return { data, loading }` mengembalikan object dengan shorthand properties.
- `.then(...)` dan `.finally(...)` membentuk rantai Promise. Error handling pada contoh ringkas ini perlu ditambahkan agar rejection tidak menjadi kegagalan tak tertangani.

#### 2.8 Form Handling & Validasi
- **Analogi:** Form adalah formulir yang nilainya disinkronkan dengan catatan state; validasi adalah pemeriksaan isian. Pemeriksaan di browser seperti petugas awal, tetapi server tetap harus memeriksa sendiri sebelum menerima data.
- `e` adalah parameter event; `e.target` adalah elemen input yang memicu event. `name` dan `value` adalah property HTML input.
- `const { name, value } = e.target` mengambil dua property; `setForm({ ...form, [name]: value })` menyalin object lalu memakai computed property name untuk memperbarui field terpilih.
- `[name]` berbeda dari `name`: bentuk kurung siku mengevaluasi variable untuk menentukan nama property. `{ name: value }` menetapkan property literal `"name"`.
- `onChange` dan `onSubmit` adalah prop event React. `e.preventDefault()` memanggil method event untuk mencegah submit bawaan browser.
- `Object.keys(baru)` adalah method static yang mengembalikan array nama property; `.length === 0` memeriksa tidak ada error.
- `z.object`, `z.string`, `.email`, `.min` adalah API Zod untuk menyusun validasi; `.infer` adalah tipe TypeScript Zod, bukan nilai JavaScript runtime.
- `register("email")` menghubungkan input ke React Hook Form. `{...register("email")}` memakai JSX spread attributes untuk menyebarkan `name`, handler, dan ref yang dikembalikan.

### Phase 3: TypeScript & Next.js

#### 3.1 TypeScript Dasar
- **Analogi:** Tipe TypeScript seperti label pada wadah yang menjelaskan isi yang diharapkan; label membantu menemukan kekeliruan saat menulis, tetapi tidak memeriksa paket dari luar ketika tiba saat runtime.
- `: number`, `: string`, `: boolean`, dan `: string[]` adalah anotasi tipe TypeScript, bukan operator runtime JavaScript. `:` memisahkan nama variable/parameter dari tipe.
- `interface` dan `type` adalah keyword TypeScript untuk mendeskripsikan tipe. `id: number` property wajib; `email?: string` property opsional.
- `"aktif" | "nonaktif"` memakai union operator tipe `|` (dibaca “atau”), bukan OR logis runtime.
- `function sapa(user: User, salam: string = "Halo"): string` berisi parameter bertipe, nilai default, dan anotasi tipe hasil setelah `)`.
- `<T>` pada `function ambilPertama<T>` adalah parameter tipe generic. `T[]` berarti array item bertipe T; `Promise<User>` berarti Promise yang hasilnya User.
- `any` melemahkan pemeriksaan tipe; `unknown` mewajibkan pemeriksaan/narrowing sebelum operasi. TypeScript menghapus tipe saat runtime sehingga data dari request tetap perlu validasi.
- `() => void` dalam tipe props menyatakan function tanpa parameter yang hasilnya tidak dipakai; `useState<number>(0)` memberikan argumen generic pada Hook.

#### 3.2 Next.js: File-based Routing
- **Analogi:** Struktur folder seperti peta alamat: folder menentukan jalur, file khusus menentukan apa yang ditemui di alamat itu, dan `[id]` adalah bagian alamat yang nilainya berubah-ubah.
- `app/`, `produk/`, `[id]/` adalah nama folder. `[id]` adalah pola route dinamis; bukan sintaks akses array JavaScript.
- `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, dan `route.ts` adalah nama file khusus Next.js, bukan keyword bahasa.
- `children` adalah prop yang memuat isi route; `React.ReactNode` adalah tipe React untuk konten yang dapat dirender.
- `<html lang="id">` memakai atribut HTML `lang`; `{children}` menyisipkan nilai JavaScript ke JSX.
- Pada route dinamis, `params` adalah nilai parameter route. Versi Next.js tertentu memberi `params` sebagai Promise, sehingga contoh memakai `await params`; ikuti tipe versi proyek.

#### 3.3 Server Component vs Client Component
- **Analogi:** Server Component seperti dapur belakang yang dapat memakai bahan rahasia; Client Component seperti meja layanan interaktif di depan pengguna. Informasi rahasia tidak boleh dibawa ke meja depan.
- `"use client"` adalah directive string di awal module yang menetapkan batas client; `"use server"` pada contoh Server Action adalah directive server. Keduanya bukan keyword JavaScript umum.
- `useState`, `useEffect`, dan `onClick` adalah Hook/prop React yang memerlukan kemampuan client. Component server dapat memakai `async`/`await` untuk data server sesuai kerangka Next.js.
- `prisma.produk.findMany()` membaca model `produk` melalui Prisma Client; `await` menunggu hasilnya.
- `.map((p) => <li key={p.id}>{p.nama}</li>)` menghasilkan list; `key` untuk identitas React, `p.id`/`p.nama` adalah field data.
- `params: Promise<{ id: string }>` adalah anotasi tipe TypeScript. `Number(id)` memanggil fungsi global untuk mengonversi teks URL menjadi angka; hasilnya perlu dipastikan valid.
- `if (!produk)` menguji nilai falsy/tidak ada. Nilai kosong array `[]` tetap truthy di JavaScript, jadi cek khusus bila ingin memperlakukan hasil kosong.

#### 3.4 SSR vs SSG
- **Analogi:** SSR seperti memasak pesanan saat pelanggan datang; SSG seperti menyiapkan hidangan lebih dulu; ISR seperti menyiapkan sebelumnya tetapi memperbarui persediaan secara berkala.
- `fetch(url, { ... })` memakai object options. `cache` adalah property opsi Fetch Next.js dengan nilai string `"force-cache"` atau `"no-store"`.
- `next` adalah property opsi khusus Next.js; `revalidate` menyatakan interval detik pada contoh. `{ next: { revalidate: 60 } }` adalah object bertingkat.
- `const res = await fetch(...)` menyimpan Response. Strategi caching memengaruhi kapan data diambil ulang; bukan operator JavaScript dan dapat bergantung versi/konfigurasi Next.js.

#### 3.5 Server Actions & API Routes
- **Analogi:** Server Action seperti loket internal aplikasi untuk mengirim form ke server; API Route seperti alamat layanan resmi yang dapat dipanggil lewat HTTP. Keduanya tetap harus memeriksa siapa peminta dan apa yang dikirim.
- `"use server"` adalah directive Next.js. `export async function` mengekspor function asynchronous yang dapat dipakai sebagai Server Action.
- `FormData` adalah API Web; `.get("nama")` mengambil nilai field dan hasilnya `FormDataEntryValue | null`, bukan otomatis string.
- `as string` adalah type assertion TypeScript. Ia tidak mengonversi atau memvalidasi nilai saat runtime; periksa `null`, jenis File/string, dan validasi isi.
- `formData.get("nama")` adalah pemanggilan method; `"nama"` cocok dengan atribut `name="nama"` pada input.
- `revalidatePath("/produk")` adalah function Next.js untuk meminta cache path diperbarui.
- `action={buatProduk}` menghubungkan form ke action; `{status: 201}` adalah object opsi response dengan property `status`.
- `export async function GET()`/`POST(request: Request)` menggunakan nama export yang dikenali Next.js sebagai HTTP method handler. `request.json()` membaca body; `NextResponse.json(data)` membentuk response JSON.
- `data: body` dan `where: ...` adalah property object argument Prisma, bukan operator. Validasi body dan otorisasi harus dilakukan sebelum operasi database.

#### 3.5b Fitur Next.js yang Sering Dipakai
- **Analogi:** `Image` dan `Link` seperti perlengkapan khusus yang membantu menangani gambar dan perpindahan halaman; metadata seperti label pada sampul; environment variable seperti konfigurasi yang disimpan terpisah dari isi aplikasi.
- `Image` dari `next/image` dan `Link` dari `next/link` adalah component yang diimport; `src`, `alt`, dan `href` adalah props yang diberikan.
- `export const metadata = { title: ... }` mengekspor konfigurasi metadata Next.js; `title` adalah property object.
- `process.env.NAMA` mengakses environment variable di sisi server. `NEXT_PUBLIC_` adalah konvensi prefix Next.js agar variable dapat diekspos ke client; jangan menyimpan credential/secret di dalamnya.

### Phase 4: Database, Backend & Keamanan

> Contoh di fase ini mencampur JavaScript/TypeScript dengan SQL dan Prisma Schema. Kata seperti `SELECT`, `WHERE`, `@id`, dan `@relation` bukan keyword JavaScript; penjelasannya di bawah menjaga konteks bahasanya.

#### 4.1 SQL Dasar
- **Analogi:** Query seperti instruksi mengolah lembar data: pilih sumber, cocokkan tabel, saring baris, kelompokkan, hitung, urutkan, lalu batasi hasil.
- `SELECT`, `FROM`, `JOIN`, `ON`, `WHERE`, `GROUP BY`, `ORDER BY`, `LIMIT`, `AS`, `COUNT`, dan `DESC` adalah keyword/fungsi SQL. `=` di kondisi SQL membandingkan nilai menurut aturan SQL; jangan samakan dengan assignment `=` JavaScript.
- `u` dan `p` adalah alias tabel; `u.nama` menunjuk kolom `nama` dari alias tabel `u`. `AS total_pesanan` memberi nama kolom hasil.
- `COUNT(p.id)` menghitung nilai `id` yang tidak null di tiap group. `GROUP BY u.nama` mengelompokkan semua baris dengan nama sama; tambahkan `u.id` untuk membedakan user bernama sama.
- String SQL ditulis dengan petik tunggal, misalnya `'selesai'`; `DESC` mengurutkan menurun; `LIMIT 5` membatasi hasil menjadi maksimal lima baris.

#### 4.2 PostgreSQL & Relasi
- **Analogi:** Relasi database seperti daftar rujukan antarlembar: foreign key menunjuk catatan induk, sementara tabel penghubung seperti daftar pasangan untuk menghubungkan banyak siswa dengan banyak kegiatan.
- `(1)`, `<`, dan `>` pada diagram adalah notasi cardinality: `1` berarti satu, kaki gagak menandai banyak. Dalam SQL nyata relasi diwujudkan melalui primary key, foreign key, constraint, dan tabel.
- `users`, `pesanan`, `siswa`, `ekskul`, `siswa_ekskul` adalah nama tabel ilustrasi, bukan variable JavaScript.
- `user_id`, `siswa_id`, dan `ekskul_id` lazim menjadi kolom foreign key. Tabel penghubung menyimpan pasangan key untuk relasi many-to-many.

#### 4.3 Prisma ORM
- **Analogi:** Prisma seperti penerjemah antara object JavaScript dan tabel database: schema menjelaskan bentuk data, sedangkan method seperti `findMany` menerjemahkan maksud baca data menjadi query.
- `model`, tipe field seperti `Int`, `String`, `DateTime`, dan tanda `?`/`[]` merupakan sintaks Prisma Schema: nullable dan relasi daftar. Bukan tipe atau operator JavaScript.
- `@id`, `@default(...)`, `@unique`, dan `@relation(...)` adalah attribute Prisma. `fields: [userId]` dan `references: [id]` adalah argumen bernama attribute; `@` bukan decorator JavaScript di sini.
- Dalam JavaScript/TypeScript, `new PrismaClient()` memakai `new` untuk membuat instance; `export const prisma` mengekspor satu client.
- `prisma.user.create({ data: {...} })`, `.findMany({ where, orderBy, include })`, `.update(...)`, dan `.delete(...)` adalah pemanggilan method Prisma. `data`, `where`, `orderBy`, dan `include` adalah property opsi.
- `contains` dan `mode` adalah property filter Prisma; `"insensitive"` memilih pencarian tanpa membedakan huruf besar/kecil. `orderBy: { id: "desc" }` mengurutkan ID menurun; `include: { pesanan: true }` meminta relasi ikut dimuat.
- `await` menunggu operasi database; `where: { id: 1 }` membatasi target. `delete` pada `prisma.user.delete(...)` adalah method, bukan operator JavaScript `delete`.
- `npx prisma ...` adalah perintah terminal. `migrate dev`, `generate`, dan `studio` adalah subperintah Prisma CLI.

#### 4.4 Supabase
- **Analogi:** Supabase menyediakan tempat database; `DATABASE_URL` seperti alamat dan kunci akses menuju tempat itu. Simpan kunci di konfigurasi rahasia, bukan ditempel di kode yang dibagikan.
- `DATABASE_URL` adalah nama environment variable. Teks connection string mengandung alamat/credential dan harus dirahasiakan.
- Pada Prisma Schema, `datasource`, `provider`, `url`, `env("DATABASE_URL")`, dan `"postgresql"` adalah sintaks/konfigurasi Prisma, bukan JavaScript. `env(...)` membaca environment variable untuk konfigurasi tool.
- Dalam kode server, `process.env.DATABASE_URL` adalah pola umum untuk membaca environment; pastikan nilai tersedia dan hanya digunakan pada server.

#### 4.5 Autentikasi & Otorisasi
- **Analogi:** Autentikasi seperti memeriksa kartu identitas; otorisasi seperti memeriksa apakah pemegang kartu boleh memasuki ruangan tertentu.
- `bcrypt.hash(password, 10)` dan `bcrypt.compare(...)` adalah method library. `10` adalah parameter cost factor sesuai API/library; ikuti panduan library dan kapasitas server.
- `passwordDariForm`, `hash`, `email`, dan `user.password` adalah variable/property data. Simpan hash, bukan password asli.
- `await` menunggu hash atau query; `prisma.user.create({ data: ... })` adalah operasi database.
- `const session = await auth()` memperoleh sesi dari helper auth. `if (!session) redirect("/login")` memakai `!` untuk memeriksa ketiadaan sesi dan memanggil helper redirect.
- `session.user?.name` memakai optional chaining. `role === "admin"` (contoh otorisasi) membandingkan role; pengecekan harus dilakukan server-side pada operasi yang dilindungi.

#### 4.6 Keamanan Dasar
- **Analogi:** Keamanan seperti menjaga gedung: validasi memeriksa barang yang dibawa, autentikasi memeriksa identitas, dan otorisasi memeriksa izin masuk ke ruangan/data tertentu.
- `where: { id: Number(id), userId: session.user.id }` adalah object filter Prisma; kedua kondisi pada object where secara default harus cocok (AND). `Number(id)` mengonversi teks, tetapi input tetap perlu divalidasi.
- `findFirst(...)` adalah method Prisma yang mencari record pertama yang memenuhi filter; `if (!pesanan)` menangani record yang tidak ditemukan.
- `notFound()` adalah helper Next.js untuk menampilkan status not-found/route not-found; bukan keyword JavaScript.
- SQL injection, XSS, CSRF, secret leakage, validasi, dan IDOR adalah kategori masalah keamanan, bukan operator. ORM, escaping React, atau middleware tidak menggantikan validasi input dan pemeriksaan izin yang sesuai.

### Phase 5: Capstone, Testing & Deployment

#### 5.1 Testing Dasar
- **Analogi:** Test seperti daftar pemeriksaan sebelum menyerahkan barang: siapkan kondisi, jalankan tindakan, lalu cocokkan hasil dengan standar yang diharapkan.
- `import { describe, it, expect } from "vitest"` mengimpor API test bernama. `describe`, `it`, dan `expect` adalah function framework test, bukan keyword JavaScript.
- Callback `() => { ... }` menjadi isi test. `expect(hasil).toBe(harapan)` memanggil matcher untuk membandingkan hasil.
- `expect(() => hitungDiskon(...)).toThrow()` memberikan function agar framework dapat menjalankannya dan memeriksa exception. Jika memanggil function sebelum `expect`, exception bisa terjadi di luar pemeriksaan.
- `10` pada `hitungDiskon(100000, 10)` adalah argument persentase; `.toBe(90000)` menguji nilai tepat. Arrange/Act/Assert adalah pola menyusun tes, bukan keyword.

#### 5.2 Capstone Project
- **Analogi:** Capstone seperti produk contoh di etalase: bukan hanya harus terlihat, tetapi juga perlu berfungsi, aman dicoba, memiliki petunjuk, dan bisa diperiksa orang lain.
- Checklist `- [ ]` adalah sintaks daftar tugas Markdown, bukan sintaks JavaScript. Isinya adalah kriteria aplikasi: auth/role, tabel relasional, validasi server, state UI, responsive, test, dokumentasi, demo, dan commit.
- Dalam implementasi, `loading`, `error`, dan data kosong biasanya direpresentasikan sebagai state/nilai dan ditampilkan secara kondisional; role/izin harus dicek di server.
- README, screenshot, link demo, dan riwayat commit adalah artefak proyek untuk membantu reviewer memeriksa aplikasi.

#### 5.3 Deployment
- **Analogi:** Deployment seperti memindahkan aplikasi dari meja kerja ke toko yang dibuka untuk umum; konfigurasi production adalah kunci toko, dan migration adalah perubahan tata ruang yang perlu dilakukan hati-hati.
- `git push` dan `npx prisma migrate deploy` adalah perintah terminal. Yang pertama mengirim commit; yang kedua menerapkan migration yang sudah disiapkan ke database target.
- `"scripts": { "build": "prisma generate && next build" }` adalah konfigurasi JSON `package.json`: `scripts` dan `build` adalah property; `"prisma generate && next build"` adalah string shell.
- `&&` pada string perintah shell menjalankan perintah kedua hanya jika perintah pertama sukses. Ini bukan evaluasi `&&` JavaScript, walau simbolnya sama.
- `DATABASE_URL` adalah environment variable rahasia; CI/CD dan dashboard hosting mengatur nilai production di luar source code.

### Phase 6: Persiapan Karier

#### 6.1 Dasar Algoritma & Struktur Data
- **Analogi:** Algoritma seperti petunjuk langkah demi langkah; struktur data seperti cara menata bahan agar cepat ditemukan dan dihitung.
- `for (const huruf of teks)` menggunakan keyword `for`, `const`, dan `of`: iterasi setiap karakter iterable `teks`, dengan variable baru `huruf` pada tiap langkah.
- `const hasil = {}` membuat object kosong. `hasil[huruf]` memakai bracket notation/computed property access: nilai `huruf` menjadi nama key, bukan teks literal `"huruf"`.
- `(hasil[huruf] || 0)` memakai OR logis sebagai fallback untuk nilai falsy. Karena jumlah yang tersimpan adalah angka positif atau belum ada, `0` adalah nilai awal yang sesuai.
- `(hasil[huruf] || 0) + 1` membaca hitungan sebelumnya lalu menambah satu; `hasil[huruf] = ...` menyimpan nilai baru pada property tersebut.
- `return hasil` mengembalikan object frekuensi. Pada sistem yang menerima key khusus/tidak tepercaya, gunakan `Map` atau object tanpa prototype untuk menghindari benturan key object.

#### 6.2 Bahasa Inggris Teknis
- **Analogi:** Membaca dokumentasi teknis seperti membaca peta: istilah kunci membantu menemukan bagian yang tepat, tetapi rute tetap perlu dicocokkan dengan versi dan kondisi proyek.
- `undefined`, `not found`, `unexpected token`, dan `unauthorized` adalah kata/teks yang mungkin muncul di error, bukan keyword yang harus ditulis di kode.
- Nama situs dokumentasi adalah sumber referensi. Saat membaca contoh kode, identifikasi syntax/API, versi library, dan pesan error lengkap sebelum menerapkan solusi.
- README dan pesan commit adalah dokumen/teks proyek; gunakan istilah yang akurat, singkat, dan mudah dicari.

#### 6.3 Profil Profesional
- **Analogi:** Profil profesional seperti etalase karya: susun contoh terbaik, beri label yang jujur, dan sediakan petunjuk agar orang lain dapat mencoba atau menilai hasilnya.
- GitHub profile README dan LinkedIn adalah halaman profil; headline, deskripsi, link repository/demo, serta CV adalah konten informasi, bukan konstruksi JavaScript.
- `Next.js` dan `TypeScript` pada headline adalah nama teknologi. Cantumkan hanya kemampuan yang dapat dibuktikan lewat proyek atau pengalaman.
- Saat meminta bantuan/review, sertakan tujuan, perilaku yang diharapkan, perilaku aktual, pesan error, dan langkah yang sudah dicoba; jangan mengirim secret seperti `.env`.

## Phase 0: Fondasi Lingkungan Kerja

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **0.1 Terminal / Command Line** | Terminal menerima perintah teks untuk berpindah folder, melihat file, membuat folder, dan menjalankan program. `pwd` menunjukkan lokasi saat ini; `ls` menampilkan isi folder; `cd` berpindah lokasi; `mkdir` membuat folder. Teks setelah `#` pada contoh adalah komentar untuk manusia. Perintah shell dapat berbeda antara macOS/Linux, PowerShell, dan Command Prompt, jadi gunakan padanan yang sesuai dengan terminalmu. | Bisa membuka folder proyek yang benar, menjalankan perintah di sana, dan memahami bahwa path relatif seperti `..` berarti folder induk. |
| **0.2 Node.js & npm** | Node.js adalah runtime untuk menjalankan JavaScript di luar browser. npm mengelola package dan script proyek. Di `package.json`, `name` adalah identitas proyek; `scripts` adalah perintah bernama yang dapat dijalankan lewat npm; `dependencies` adalah package yang dibutuhkan aplikasi saat berjalan. Versi seperti `^1.7.0` adalah rentang versi yang diizinkan npm, bukan operator JavaScript. `node_modules` adalah hasil instalasi package; jangan commit karena dapat dibuat ulang dari manifest dan lockfile. | Bisa membedakan memasang package (`npm install`) dari menjalankan script (`npm run ...`), serta mengetahui bahwa `package.json` dan lockfile perlu disimpan di Git. |
| **0.3 HTML, CSS & DOM Refresher** | HTML menyusun elemen dan makna halaman; CSS mengatur tampilannya; DOM adalah representasi elemen HTML sebagai pohon yang dapat dibaca atau diubah JavaScript. `getElementById` mencari satu elemen berdasarkan `id`; `addEventListener` memasang callback untuk event; `textContent` mengganti teks dengan aman sebagai teks biasa. Flexbox dan Grid mengatur tata letak, sedangkan margin, border, dan padding membentuk box model. Elemen semantik seperti `<main>` menjelaskan peran konten, bukan sekadar tampilannya. | Bisa menjelaskan hubungan HTML → DOM → JavaScript, membuat layout dasar, dan memilih elemen HTML berdasarkan maknanya. |
| **0.4 Debugging & Browser DevTools** | Debugging adalah proses menemukan penyebab kesalahan, bukan menebak lalu mengubah kode secara acak. Console memperlihatkan pesan dan error JavaScript; Network menunjukkan request, status, waktu, dan respons; Elements membantu memeriksa DOM/CSS; Sources menyediakan breakpoint untuk menghentikan eksekusi dan memeriksa nilai variable. `console.log` berguna untuk memeriksa input dan hasil antara, tetapi breakpoint lebih tepat bila perlu melihat urutan eksekusi dan scope. | Bisa mengulang masalah, membaca pesan error, memeriksa nilai aktual, lalu menunjukkan titik pertama nilai tersebut berbeda dari yang diharapkan. |
| **0.5 ESLint & Prettier** | Prettier merapikan bentuk kode secara konsisten, misalnya indentasi dan pemenggalan baris. ESLint memeriksa pola kode dan memberi peringatan/error untuk hal seperti variable tidak terpakai atau pola yang berisiko. Keduanya tidak menggantikan pemahaman kode dan tidak selalu mendeteksi bug logika. Format on save menjalankan formatter ketika file disimpan; aturan proyek sebaiknya diikuti bersama oleh seluruh tim. | Bisa membedakan masalah format dari masalah kualitas/pola kode dan menjalankan pemeriksaan proyek tanpa mengabaikan error yang bermakna. |

## Phase 1: JavaScript Modern & Asynchronous

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **1.1 `let` dan `const`** | Keduanya membuat binding variable dengan cakupan block. Gunakan `const` bila nama variable tidak perlu diberi nilai baru; gunakan `let` bila binding-nya memang akan diperbarui. `const` tidak membekukan object atau array: isinya masih bisa berubah, tetapi nama variable tidak dapat diarahkan ke object/array lain. Hindari `var` pada kode baru karena aturan scope dan hoisting-nya berbeda serta lebih mudah menimbulkan kebingungan. | Bisa memilih `const` atau `let` berdasarkan apakah binding akan di-assign ulang, bukan berdasarkan apakah nilai di dalam object bisa berubah. |
| **1.2 Scope & Closure** | Scope menentukan di bagian mana suatu nama variable dapat digunakan. `let` dan `const` mengikuti lexical scope: kode di dalam dapat membaca scope pembungkusnya, tetapi scope luar tidak dapat membaca variable yang hanya dibuat di dalam. Closure terjadi saat function tetap menyimpan akses ke variable lexical tempat function itu dibuat, walaupun function pembuatnya sudah selesai. Closure berguna untuk mempertahankan state privat, callback, dan memahami mengapa function React dapat mengakses state/props dari render tertentu. | Bisa menemukan mengapa suatu nama menghasilkan `ReferenceError`, serta menjelaskan bagaimana counter pada contoh mengingat nilai `hitung` di antara pemanggilan. |
| **1.3 Arrow Function & Shorthand** | Arrow function adalah cara menulis function sebagai expression. Bentuk `parameter => expression` otomatis mengembalikan hasil expression; bila memakai badan `{ ... }`, perlu `return` jika ingin mengembalikan nilai. Shorthand object `{ nama, umur }` setara dengan `{ nama: nama, umur: umur }` jika nama variable dan property sama. Arrow function juga memiliki aturan `this` yang berbeda dari function biasa; jangan menggantinya secara membabi buta ketika kode bergantung pada `this`. | Bisa membedakan badan expression dari badan blok, menambahkan `return` pada tempat yang tepat, dan membaca shorthand sebagai pasangan nama property/nilai. |
| **1.4 Destructuring** | Destructuring mengambil nilai dari object atau array lalu menempatkannya ke variable. Pada object, nama di pola biasanya harus sama dengan nama property; pada array, posisi yang menentukan nilai. `alamat: { kota }` mengambil property bertingkat `kota`, sedangkan `umur = 17` memberi default jika property `umur` bernilai `undefined` atau tidak ada—bukan jika nilainya `null`. | Bisa mengurai pola object dan array, mengetahui sumber setiap variable hasil, serta membedakan default dari validasi data. |
| **1.5 Spread & Rest** | Simbol `...` berarti spread saat menyebarkan isi array/object atau argument, dan rest saat mengumpulkan sisa nilai menjadi array/object. Urutan spread object penting: property yang ditulis belakangan menimpa property bernama sama. Salinan dengan spread bersifat **shallow** (dangkal): object di dalamnya masih dapat menunjuk ke object yang sama, sehingga perubahan data bertingkat perlu menyalin tiap tingkat yang diubah. | Bisa menjelaskan apakah `...` sedang menyebarkan atau mengumpulkan, memprediksi property mana yang menang, dan tidak menganggap spread membuat salinan mendalam. |
| **1.6 Template Literal, Optional Chaining, Nullish Coalescing** | Template literal memakai backtick dan `${...}` untuk menyisipkan hasil ekspresi ke string. Optional chaining `?.` menghentikan akses jika nilai tepat di kirinya `null` atau `undefined`, lalu menghasilkan `undefined`; ia tidak otomatis memvalidasi bahwa data wajib tersedia. Nullish coalescing `??` memilih nilai default hanya untuk `null`/`undefined`; berbeda dari `||`, yang juga mengganti `0`, `false`, dan string kosong. | Bisa memilih `??` ketika nilai falsy seperti `0` tetap sah, dan tahu kapan akses opsional harus diikuti pemeriksaan/penanganan nilai kosong. |
| **1.7 Modul `import` & `export`** | Module membagi kode ke beberapa file. `export` bernama mengeluarkan item dengan nama tertentu dan biasanya diambil memakai `{ nama }`; `export default` menyediakan satu ekspor utama yang dapat diimpor dengan nama pilihan. Path relatif seperti `./utils/harga.js` menunjuk file proyek, sedangkan nama package seperti `"axios"` dicari oleh resolver package. | Bisa mengekspor fungsi/data dari satu file, mengimpornya di file lain, dan mendiagnosis kesalahan path atau nama ekspor. |
| **1.8 Array Methods** | `map` mengubah tiap item dan menghasilkan array baru dengan panjang sama; `filter` mempertahankan item yang lolos kondisi; `find` mengembalikan item cocok pertama atau `undefined`; `reduce` menggabungkan item menjadi satu hasil dengan accumulator dan nilai awal. Callback menerima item saat ini; parameter tambahannya dapat berupa index dan array sumber. `map`/`filter` tidak mengubah array asal, tetapi callback tetap bisa mengubah object item jika sengaja melakukan mutasi. | Bisa memilih method berdasarkan bentuk hasil yang diperlukan dan menerangkan hasil tiap iterasi, khususnya accumulator pada `reduce`. |
| **1.9 HTTP Dasar & JSON** | HTTP mengatur pertukaran request/response. Method menyatakan maksud umum (`GET` baca, `POST` buat/kirim, `PUT` ganti, `PATCH` ubah sebagian, `DELETE` hapus), tetapi server yang menentukan perilaku endpoint sebenarnya. Status `2xx` sukses, `3xx` pengalihan, `4xx` masalah request/izin, dan `5xx` kegagalan server. Header membawa metadata; body membawa isi request/response. CORS adalah kebijakan browser untuk request lintas origin, bukan mekanisme autentikasi. JSON adalah format teks; `JSON.parse` mengurai teks, `JSON.stringify` mengubah data menjadi teks. | Bisa memeriksa method, URL, status, header, dan body sebuah request serta tidak menganggap JSON sebagai object sebelum di-parse. |
| **1.10 Asynchronous JavaScript** | Kode sinkron berjalan sesuai urutan; pekerjaan asynchronous memberi kesempatan program melanjutkan pekerjaan lain sebelum hasilnya tersedia. Event loop mengatur kapan callback yang siap dijalankan mendapat giliran. Promise merepresentasikan hasil yang mungkin tersedia nanti, dengan status pending/fulfilled/rejected. `async` membuat function selalu mengembalikan Promise; `await` menunggu Promise di dalam function tersebut dan melempar rejection sebagai error. `try/catch/finally` menangani jalur sukses, gagal, dan pekerjaan yang harus selalu dilakukan. `Promise.all` memulai pekerjaan dalam daftar secara bersamaan dan menghasilkan array hasil sesuai urutan input; ia reject jika salah satu Promise reject. | Bisa membedakan urutan baris dari waktu selesainya request, menangani rejection, dan tahu kapan pekerjaan independen layak dijalankan dengan `Promise.all`. |
| **1.11 Fetch API & Axios** | `fetch(url, options)` adalah API browser untuk membuat request; `method`, `headers`, dan `body` pada options mengatur request. Saat mengirim JSON, ubah object menjadi string dengan `JSON.stringify`; saat membaca response, panggil `res.json()`. `fetch` tidak otomatis melempar error untuk status HTTP seperti 404/500, jadi periksa `res.ok`. Axios menyederhanakan beberapa langkah, seperti serialisasi/parsing JSON dan pelaporan status non-sukses melalui rejection. Keduanya tetap memerlukan penanganan error jaringan dan validasi bentuk data. | Bisa mengirim request, membaca response, memeriksa status, dan membedakan error HTTP dari kegagalan jaringan atau parsing. |
| **1.12 Git & GitHub** | Git mencatat perubahan sebagai riwayat lokal; GitHub menyimpan repository jarak jauh dan menyediakan kerja kolaboratif. `add` memilih perubahan untuk snapshot berikutnya, `commit` menyimpan snapshot, `push` mengirim commit ke remote, dan branch memisahkan pekerjaan. Pull Request meminta review dan penggabungan perubahan; merge conflict berarti Git tidak bisa memilih perubahan secara otomatis. `.gitignore` mencegah file tertentu seperti `.env` dan `node_modules` masuk ke riwayat. | Bisa membuat branch, commit perubahan yang terpilih, push branch, membaca conflict, serta memastikan secret dan file hasil instalasi tidak ikut di-commit. |

## Phase 2: Tailwind & React

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **2.1 Tailwind CSS** | Class Tailwind adalah utility yang masing-masing menerapkan satu atau beberapa deklarasi CSS. `bg-blue-600` mengatur background; `px-4` dan `py-2` mengatur padding horizontal/vertikal; `hover:` memberi aturan saat hover; `md:` mengaktifkan aturan pada breakpoint medium ke atas. Tanpa prefix, aturan berlaku di semua ukuran. Skala angka Tailwind mengikuti konfigurasi/desain framework dan tidak selalu sebaiknya dianggap konversi universal yang tetap. Urutan class di teks tidak selalu menentukan CSS mana yang menang; konflik mengikuti aturan CSS dan generator Tailwind. | Bisa menerjemahkan class menjadi efek visual, membaca variant/prefix, dan membuat layout yang tetap nyaman pada layar kecil maupun besar. |
| **2.2 React: JSX** | JSX adalah sintaks untuk mendeskripsikan UI, lalu ditransformasikan menjadi pemanggilan React. Teks di antara tag tampil sebagai teks; `{...}` menyisipkan expression JavaScript. `className` digunakan untuk class CSS; elemen harus ditutup; hasil JSX umumnya perlu satu root (fragment `<>...</>` dapat menjadi root tanpa elemen tambahan). JSX bukan string HTML dan hanya menerima expression, bukan statement `if` langsung di dalam kurung kurawal. | Bisa membedakan teks dan expression, membuat elemen bersarang dengan tag tertutup, dan memilih conditional expression atau `if` di luar JSX sesuai kebutuhan. |
| **2.3 Komponen & Props** | Component adalah function yang menghasilkan UI. Nama component berhuruf besar agar React membedakannya dari tag HTML. Props adalah object input dari parent ke child; destructuring seperti `{ nama, harga, stok = 0 }` mengambil property, dan nilai default dipakai bila prop tidak diberikan/bernilai `undefined`. Sintaks `<KartuProduk nama="Kaos" harga={50000} />` mengirim string langsung dan expression JavaScript melalui `{}`. Props sebaiknya diperlakukan read-only; perubahan data dilakukan oleh pemilik state atau callback yang diberikan parent. | Bisa membuat component reusable dengan input yang jelas, mengirim prop bertipe sesuai maksudnya, dan tidak mengubah props langsung. |
| **2.4 Conditional Rendering & Rendering List** | `if` dan early return memilih tampilan untuk loading, data kosong, error, atau keadaan normal. `map` menghasilkan elemen untuk tiap item. `key` membantu React mencocokkan item antar-render; gunakan ID stabil dan unik dalam daftar tersebut, bukan nilai yang berubah atau index jika daftar dapat diurutkan/dihapus. `kondisi && elemen` cocok untuk tampilan opsional; ternary cocok untuk memilih satu dari dua hasil. | Bisa menangani keadaan UI yang berbeda dan memastikan setiap item list memiliki key stabil yang berasal dari identitas data. |
| **2.5 State: `useState`** | State adalah data component yang ketika diperbarui meminta React merender ulang UI terkait. `useState(initialValue)` mengembalikan pasangan `[nilai, setter]`; nama `setCount` hanya konvensi. Update state tidak sama dengan mengubah variable lokal, dan React dapat mengelompokkan update. Bila nilai baru dihitung dari nilai sebelumnya, bentuk updater `setCount((sebelumnya) => sebelumnya + 1)` lebih aman. Array/object state sebaiknya diperbarui dengan membuat salinan baru agar React dapat mengenali perubahan. | Bisa memperbarui state tanpa mutasi langsung, menggunakan updater untuk perubahan berdasarkan nilai sebelumnya, dan memahami bahwa pemanggilan setter tidak langsung mengubah variable pada baris yang sama. |
| **2.6 Side Effect: `useEffect`** | Effect menjalankan pekerjaan di luar perhitungan UI, misalnya mengambil data, memasang listener, atau sinkronisasi dengan sistem lain. Dependency array menentukan kapan effect dijalankan ulang: `[]` saat mount (dalam praktiknya perilaku development Strict Mode perlu dipahami), `[id]` saat mount dan saat `id` berubah, tanpa array setelah setiap render. Nilai yang dipakai effect dan dapat berubah umumnya perlu dicantumkan sebagai dependency. Effect dapat mengembalikan cleanup untuk melepas listener/timer atau membatalkan pekerjaan lama. Jangan jadikan callback effect `async`; buat dan panggil fungsi async di dalamnya. | Bisa menentukan dependency yang benar, mencegah loop akibat update yang memicu effect berulang, dan membersihkan pekerjaan saat dependency berubah atau component dilepas. |
| **2.7 `useRef`, Context & Custom Hook** | `useRef` memberi object stabil dengan property `.current`; mengubahnya tidak memicu render, sehingga cocok untuk referensi DOM atau nilai mutable yang tidak perlu tampil di UI. Context membagikan nilai kepada component di bawah Provider terdekat, berguna untuk data bersama dan bukan pengganti semua state lokal. Custom Hook mengekstrak logika React yang dapat dipakai ulang; namanya diawali `use` dan tetap mengikuti Rules of Hooks. | Bisa memilih state untuk data yang memengaruhi UI, ref untuk nilai/DOM yang tidak memicu render, Context untuk data lintas pohon, dan custom hook untuk logika bersama. |
| **2.8 Form Handling & Validasi** | Pada controlled input, `value` berasal dari state dan `onChange` memperbarui state; atribut `name` mengidentifikasi field yang diubah. `[name]` adalah computed property, sehingga field yang tepat diperbarui secara dinamis. `preventDefault` menghentikan submit bawaan browser. Validasi client membantu pengalaman pengguna, tetapi tidak dapat dipercaya sebagai batas keamanan karena request dapat dibuat tanpa UI; server wajib memvalidasi ulang. React Hook Form mengelola state/interaksi form, sedangkan Zod mendeskripsikan aturan dan memeriksa data; `z.infer` menghasilkan tipe statis dari schema tetapi bukan pengganti validasi runtime. | Bisa menjaga input dan state tetap sinkron, menampilkan error per field, serta memvalidasi payload lagi di server sebelum menyimpan atau memprosesnya. |

## Phase 3: TypeScript & Next.js

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **3.1 TypeScript Dasar** | Anotasi seperti `: number` memberi tahu pemeriksa tipe nilai yang diharapkan. `interface`/`type` mendeskripsikan bentuk data; `?` pada property berarti boleh tidak ada (`undefined`), sedangkan union dengan `null` menyatakan null sebagai nilai yang diizinkan. Union literal membatasi pilihan nilai. Tipe parameter dan tipe hasil function mendokumentasikan kontrak. Generic seperti `<T>` mempertahankan hubungan tipe antara input dan output. TypeScript memeriksa saat development/build; ia tidak otomatis memeriksa JSON/API saat runtime. `any` mematikan banyak pemeriksaan, sedangkan `unknown` mengharuskan pemeriksaan sebelum digunakan. | Bisa memberi tipe pada data/fungsi, membedakan property opsional dan nullable, serta memvalidasi data eksternal sebelum memperlakukannya sebagai tipe yang dipercaya. |
| **3.2 Next.js: File-based Routing** | App Router membentuk URL dari struktur folder. `page.tsx` menyediakan UI route; `layout.tsx` membungkus route anak dan mempertahankan bagian UI saat navigasi; `loading.tsx` memberi fallback loading; `error.tsx` menyediakan UI pemulihan error; `route.ts` mendefinisikan handler HTTP. Folder `[id]` menangkap segmen URL dinamis. `children` adalah konten route yang ditempatkan layout. | Bisa memetakan URL ke file yang sesuai, memilih file khusus sesuai fungsi, dan mengambil parameter route dinamis dengan benar menurut versi Next.js. |
| **3.3 Server Component vs Client Component** | Pada App Router, Server Component adalah default dan berjalan untuk menyiapkan UI di server; cocok untuk akses database/secret server serta pengambilan data tanpa mengirim logika interaktif ke browser. Client Component ditandai `"use client"` pada batas module yang membutuhkannya dan dapat memakai state, effect, serta event handler. `"use client"` bukan berarti hasilnya tidak pernah dirender di server; komponen tetap dapat diprerender. Jangan mengirim secret ke props/client bundle, dan pertahankan bagian client sekecil yang diperlukan. | Bisa menentukan bagian yang membutuhkan interaktivitas, menjaga akses database/secret di server, serta memahami batas server/client dan data yang melintasinya. |
| **3.4 SSR vs SSG** | SSR menghasilkan halaman dengan data saat request sesuai strategi runtime; SSG menyajikan hasil yang sudah dibuat/cache untuk digunakan kembali; ISR memperbarui hasil cache secara berkala atau saat di-revalidate. `force-cache`, `no-store`, dan `next.revalidate` pada contoh mengatur perilaku cache `fetch` Next.js. Caching dapat berubah menurut versi dan konfigurasi framework, jadi keputusan harus dicek pada dokumentasi versi proyek. | Bisa memilih strategi sesuai seberapa sering data berubah dan seberapa mutakhir data harus terlihat, bukan sekadar memilih mode karena dianggap selalu lebih cepat. |
| **3.5 Server Actions & API Routes** | Server Action menjalankan operasi server yang dapat dihubungkan ke form; `"use server"` menandai batas server. `FormData.get` mengembalikan nilai yang bisa berupa `string`, `File`, atau `null`; type assertion `as string` hanya memberi tahu TypeScript dan tidak memeriksa input sebenarnya. Validasi schema, otorisasi, dan penanganan error tetap diperlukan. `revalidatePath` meminta data/cache route diperbarui. API Route menggunakan nama export method seperti `GET`/`POST`; `request.json()` perlu divalidasi sebelum dipakai. Pilih Server Action untuk mutasi UI dalam aplikasi Next.js; API Route saat perlu endpoint HTTP yang dipanggil client atau sistem lain. Keduanya harus dianggap permukaan server yang perlu dilindungi. | Bisa memvalidasi input yang tidak tepercaya, memeriksa sesi/izin dalam operasi server, dan memilih mekanisme berdasarkan siapa yang akan memanggilnya. |
| **3.5b Fitur Next.js yang Sering Dipakai** | `next/image` membantu mengoptimalkan penyajian gambar; `next/link` melakukan navigasi internal melalui router Next.js; `metadata` mendeskripsikan judul/informasi halaman untuk browser dan mesin pencari. Environment variable biasa digunakan di server; prefix `NEXT_PUBLIC_` membuat nilainya dapat dikirim ke browser, sehingga tidak boleh berisi secret. Nilai environment produksi diatur pada platform hosting, bukan disimpan dalam repository. | Bisa memilih komponen/framework API yang sesuai dan membedakan konfigurasi publik dari credential rahasia. |

## Phase 4: Database, Backend & Keamanan

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **4.1 SQL Dasar** | `FROM` menentukan sumber baris; `JOIN ... ON` memasangkan baris berdasarkan kondisi relasi; `WHERE` menyaring baris sebelum agregasi; `GROUP BY` membuat kelompok; `COUNT` menghitung nilai/baris; `ORDER BY` mengurutkan; `LIMIT` membatasi jumlah hasil. `AS` memberi alias untuk kolom hasil. Dalam query contoh, pengelompokan berdasarkan nama saja dapat mencampur user berbeda yang kebetulan bernama sama; gunakan ID bersama nama untuk identitas kelompok yang benar. Index dapat mempercepat pencarian tertentu dengan biaya penyimpanan dan pekerjaan saat menulis data. Transaksi membuat beberapa operasi berhasil bersama atau dibatalkan bersama. | Bisa menelusuri query, menjelaskan akibat JOIN/filter/grouping, dan memahami bahwa index serta transaksi menyelesaikan kebutuhan berbeda. |
| **4.2 PostgreSQL & Relasi** | PostgreSQL adalah sistem database relasional. One-to-Many berarti satu baris induk berhubungan dengan banyak baris anak; foreign key biasanya berada di sisi “many”. Many-to-Many menghubungkan banyak baris pada kedua sisi dan biasanya memakai tabel penghubung dengan dua foreign key. Relasi database perlu constraint agar referensi tidak menunjuk data yang tidak ada; aturan hapus/perubahan relasi perlu dipilih sesuai kebutuhan. | Bisa menggambar cardinality relasi dan menentukan tabel/foreign key yang diperlukan, termasuk tabel penghubung many-to-many. |
| **4.3 Prisma ORM** | `model` mendefinisikan entitas; setiap field menyatakan nama, tipe, optionality, dan attribute. `@id` adalah primary key; `@default(autoincrement())` membuat ID bertambah otomatis; `@unique` melarang duplikasi; `String?` mengizinkan null; `Pesanan[]` menyatakan relasi banyak yang bukan kolom daftar fisik. Pada `@relation(fields: [userId], references: [id])`, `fields` menunjuk field foreign key lokal dan `references` menunjuk key pada model terkait. CRUD: `create` menambah, `findMany` membaca banyak, `where` menyaring, `orderBy` mengurutkan, `include` memuat relasi, `update` mengubah, dan `delete` menghapus. `migrate dev` membuat/menerapkan perubahan schema untuk development; `generate` membangun Prisma Client; Studio membantu melihat/mengelola data. | Bisa menghubungkan schema ke tabel/relasi, membatasi operasi dengan `where`, membaca tipe hasil, dan menjalankan migration/generate sesuai lingkungan. |
| **4.4 Supabase** | Supabase menyediakan layanan yang antara lain dapat menjadi hosting PostgreSQL. `DATABASE_URL` adalah connection string yang dipakai backend/ORM untuk terhubung; bagian-bagiannya mencakup host, port, database, user, dan credential. Simpan di environment variable, jangan di Git atau kode browser. `env("DATABASE_URL")` membuat schema mengambil nilai konfigurasi dari environment saat tool berjalan. Pisahkan credential lokal dan production serta batasi akses sesuai kebutuhan. | Bisa menghubungkan aplikasi server ke database tanpa menaruh password dalam source code dan tahu environment mana yang sedang digunakan. |
| **4.5 Autentikasi & Otorisasi** | Autentikasi memeriksa identitas; otorisasi memeriksa izin terhadap aksi/data tertentu. Password disimpan sebagai hash password yang memang dirancang lambat dan memakai salt—bukan disimpan sebagai teks asli atau enkripsi yang dapat dibalik. Session/token menghubungkan request berikutnya dengan identitas yang sudah diverifikasi; cookie perlu dikonfigurasi aman. Pemeriksaan login dan izin harus dilakukan di server pada setiap operasi yang dilindungi, termasuk mutasi data. Jangan mengandalkan menyembunyikan tombol atau route dari UI. | Bisa menjelaskan alur register/login, menyimpan password dengan library yang tepat, dan memastikan akses data/aksi diperiksa terhadap user/role pada server. |
| **4.6 Keamanan Dasar** | SQL injection terjadi saat input mengubah struktur query; gunakan parameterized query/ORM dan hindari merangkai SQL dari input mentah. XSS menjalankan konten tak tepercaya sebagai script; escaping membantu, sedangkan HTML mentah memerlukan sanitasi yang tepat. CSRF memalsukan request melalui sesi browser; gunakan perlindungan yang cocok dengan mekanisme cookie/framework. Secret yang bocor harus dianggap terkompromi dan dirotasi, bukan hanya dihapus dari versi terbaru. Validasi server memeriksa bentuk/nilai input, sedangkan otorisasi memeriksa hak akses. IDOR terjadi jika resource dicari hanya dari ID tanpa memeriksa kepemilikan/izin. | Bisa mengidentifikasi trust boundary, memvalidasi dan mengotorisasi setiap operasi server, serta tidak menganggap ORM/React/framework otomatis mengamankan seluruh aplikasi. |

## Phase 5: Capstone, Testing & Deployment

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **5.1 Testing Dasar** | Test menyatakan perilaku yang diharapkan dan memberi tahu jika perubahan merusaknya. `describe` mengelompokkan skenario; `it`/`test` menyebut perilaku yang diuji; `expect` membandingkan hasil aktual dengan harapan. Arrange menyiapkan input, Act menjalankan kode, Assert memeriksa hasil. Unit test menguji unit kecil; integration test menguji kerja sama bagian; E2E menjalankan alur mendekati penggunaan nyata. Pilih assertion yang benar-benar memeriksa nilai/efek yang penting—sekadar memastikan tidak error belum tentu membuktikan hasilnya benar. | Bisa menulis kasus normal, batas, dan gagal; menjalankan test; serta memahami bagian mana yang dijamin oleh tiap tingkat pengujian. |
| **5.2 Capstone Project** | Capstone menggabungkan kemampuan fase sebelumnya menjadi aplikasi yang dapat dicoba. Autentikasi dan minimal dua role membuktikan pembatasan akses; empat tabel berelasi menunjukkan pemodelan data; validasi server melindungi operasi; loading/error/empty state memberi umpan balik UI; tampilan responsif mendukung ponsel; test melindungi logika penting; README menjelaskan tujuan, teknologi, screenshot, dan cara menjalankan; demo live memudahkan reviewer mencoba; riwayat commit yang teratur memperlihatkan perubahan yang dapat ditelusuri. Checklist adalah kriteria mutu, bukan sekadar fitur untuk dicentang tanpa implementasi yang berfungsi. | Orang lain dapat memahami, menjalankan, dan mencoba aplikasi; alur penting berfungsi; akses dan data ditangani dengan benar; dan repository memberi bukti proses pengerjaan. |
| **5.3 Deployment** | Deployment menerbitkan aplikasi ke lingkungan yang dapat diakses pengguna. Repository GitHub menjadi sumber build; environment variables di dashboard hosting memasok konfigurasi dan secret; proses build memastikan aplikasi dapat dikompilasi untuk production. CI/CD otomatis menjalankan langkah deploy setelah perubahan dikirim. `prisma migrate deploy` menerapkan migration yang sudah dibuat ke database production dan tidak sama dengan alur development `migrate dev`. Script `"build": "prisma generate && next build"` menjalankan pembuatan Prisma Client sebelum Next.js membangun aplikasi. Rencana rollback/backup penting karena migration production memengaruhi data nyata. | Bisa memisahkan konfigurasi lokal/production, membaca log build/deploy, menerapkan migration yang benar, dan memastikan `.env` tidak masuk repository. |

## Phase 6: Persiapan Karier

| Poin | Penjelasan yang diperjelas | Tanda sudah dipahami |
|---|---|---|
| **6.1 Dasar Algoritma & Struktur Data** | Algoritma adalah langkah terstruktur untuk memecahkan masalah; struktur data adalah cara menyimpan/mengatur nilai agar operasi tertentu mudah dilakukan. Array cocok untuk urutan; object/`Map` dapat memetakan key ke nilai; loop menelusuri data; rekursi memecah masalah dengan pemanggilan diri dan wajib memiliki kondisi berhenti. Latihan sebaiknya mencakup memahami input/output, kasus batas, dan alasan solusi bekerja, bukan hanya menyalin jawaban. | Bisa menjelaskan pendekatan sebelum coding, menguji kasus sederhana dan batas, lalu menerangkan kompleksitas dasar secara intuitif. |
| **6.2 Bahasa Inggris Teknis** | Dokumentasi, API, error, dan diskusi teknis sering memakai istilah Inggris. Tujuannya bukan kefasihan percakapan sempurna, tetapi kemampuan menemukan informasi, memahami instruksi/error, dan menjelaskan perubahan secara singkat. Saat membaca pesan error, identifikasi kata inti, file/baris, dan konteks; verifikasi solusi pada dokumentasi resmi, bukan menerjemahkan pesan secara harfiah saja. | Bisa mencari dokumentasi dengan kata kunci yang tepat dan menulis README/commit sederhana yang dapat dimengerti orang lain. |
| **6.3 Profil Profesional** | GitHub profile README memperkenalkan fokus dan proyek terkuat; pin repository yang mudah dijalankan dan memiliki dokumentasi. LinkedIn menyajikan identitas profesional, headline spesifik, dan bukti proyek. CV satu halaman menonjolkan dampak/fitur yang dibuat, teknologi yang benar-benar dipakai, serta tautan demo/repository. Soft skill mencakup menyampaikan konteks saat meminta bantuan, merespons review dengan terbuka, dan memberi kabar progres/hambatan secara konsisten. | Reviewer dapat melihat kemampuan melalui proyek konkret, memahami kontribusimu, mengakses hasil kerja, dan berkomunikasi dengan jelas. |

---

# GLOSARIUM ISTILAH PEMROGRAMAN

Istilah di bawah tetap menggunakan nama globalnya dalam bahasa Inggris. Definisi dan contoh ditulis dalam bahasa Indonesia. Beberapa istilah punya arti yang lebih spesifik bergantung pada bahasa atau tool; gunakan contoh di roadmap ini sebagai konteks, lalu cek dokumentasi tool yang sedang dipakai.

## Istilah inti dengan penjelasan sederhana

Bagian ini menjelaskan istilah yang sering muncul dengan bahasa sehari-hari terlebih dahulu. Analogi membantu memahami gambaran awal, tetapi bukan definisi teknis yang sempurna. Setelah memahami gambaran sederhananya, lanjutkan ke penjelasan lebih lengkap pada kelompok istilah di bawah.

### Dasar membaca kode

| Istilah | Arti sederhananya | Contoh dan cara memahaminya |
|---|---|---|
| **Program / Code** | Serangkaian instruksi yang memberi tahu komputer apa yang harus dilakukan. | `console.log("Halo")` adalah instruksi untuk menampilkan teks `"Halo"` di console. Komputer menjalankan instruksi sesuai aturan bahasa pemrogramannya. |
| **Library / Framework** | `Library` adalah kumpulan kode siap pakai yang dipanggil oleh program kita. `Framework` menyediakan kerangka dan aturan kerja yang lebih besar; framework biasanya mengatur kapan kode kita dipanggil. | React sering disebut library UI; Next.js adalah framework yang menyediakan struktur aplikasi web di atas React. Keduanya membantu, tetapi tidak menggantikan pemahaman dasar JavaScript. |
| **Package / Dependency** | `Package` adalah unit kode yang dapat dipasang dan digunakan. `Dependency` adalah package atau tool lain yang dibutuhkan proyek agar dapat bekerja. | Jika proyek menggunakan Axios, Axios tercatat sebagai dependency dan dipasang ke proyek. Versi dependency penting karena versi berbeda dapat memiliki perilaku berbeda. |
| **Value** | Data atau nilai yang sedang dipakai program. | `"Budi"` adalah value berupa teks; `17` adalah value berupa angka; `true` adalah value boolean yang berarti benar. |
| **Variable** | Nama yang dipakai agar sebuah value mudah disimpan dan dipakai lagi. Bayangkan label pada kotak penyimpanan. | `const nama = "Budi"` membuat label `nama` yang merujuk ke teks `"Budi"`. `const` tidak berarti isi object/array di dalamnya pasti tidak dapat diubah. |
| **Function** | Sekumpulan instruksi bernama yang dapat dijalankan ketika dibutuhkan. Mirip resep: function menjelaskan langkah, pemanggilan function meminta langkah itu dijalankan. | `function tambah(a, b) { return a + b; }` mendefinisikan resep. `tambah(2, 3)` menjalankannya dan menghasilkan `5`. |
| **Parameter / Argument** | `Parameter` adalah nama tempat untuk menerima masukan; `argument` adalah nilai yang benar-benar dikirim. | Pada `function sapa(nama)`, `nama` adalah parameter. Pada `sapa("Budi")`, `"Budi"` adalah argument yang diberikan. |
| **Return value** | Hasil yang diberikan kembali oleh function setelah tugasnya selesai. | `return a + b` mengirim hasil penjumlahan keluar dari function supaya dapat disimpan atau dipakai oleh kode lain. `console.log(...)` hanya menampilkan nilai; itu tidak sama dengan `return`. |
| **Object / Property / Method** | `Object` mengelompokkan data yang saling berkaitan. `Property` adalah data di dalamnya; `method` adalah tindakan/function milik object. | Dalam `user.nama`, `nama` adalah property. Dalam `user.sapa()`, `sapa` adalah method yang dipanggil. |
| **Array** | Daftar berurutan yang menyimpan beberapa value dalam satu variable. | `const warna = ["merah", "biru"]`; `warna[0]` mengambil item pertama, yaitu `"merah"` (indeks array dimulai dari `0`). |
| **Scope** | Batas wilayah kode yang menentukan variable mana yang boleh digunakan di suatu tempat. Bayangkan setiap function/block sebagai ruangan: variable lokal tersedia di ruangnya, tidak otomatis di semua ruang lain. | `const pesan = "Hai"` di dalam function tidak dapat langsung dipakai di luar function tersebut. |
| **Callback** | Function yang diberikan kepada kode lain untuk dijalankan nanti atau pada saat tertentu. | `tombol.addEventListener("click", () => console.log("Diklik"))` memberikan function yang dijalankan ketika tombol diklik. |
| **Event** | Sesuatu yang terjadi dan dapat ditanggapi oleh program, misalnya klik, pengetikan, atau selesainya request. | `"click"` pada `addEventListener("click", ...)` adalah nama event; callback yang diberikan dijalankan saat event itu terjadi. |
| **Error / Exception** | Informasi bahwa suatu operasi gagal atau program menemui keadaan yang tidak dapat ditangani dengan cara biasa. | Jika kode mencoba membaca property dari `undefined`, JavaScript dapat menghasilkan `TypeError`. Pesan dan stack trace membantu mencari file/baris asal masalah. |

### Data, halaman web, dan komunikasi

| Istilah | Arti sederhananya | Contoh dan cara memahaminya |
|---|---|---|
| **Client / Server** | `Client` meminta sesuatu; `server` menerima permintaan itu, mengerjakan tugas, lalu memberi jawaban. Analogi: client seperti pelanggan dan server seperti dapur yang menyiapkan pesanan. | Browser meminta daftar produk ke server; server mengambil data lalu mengirimkannya kembali. Satu aplikasi dapat berperan sebagai client saat meminta data dan server saat melayani aplikasi lain. |
| **Request / Response** | `Request` adalah pesan permintaan dari client. `response` adalah balasan server. | Browser mengirim `GET /api/produk`; server membalas dengan status `200` dan data produk. |
| **API** | Cara yang disepakati agar dua program dapat saling meminta data atau menjalankan fungsi. Analogi: API seperti menu dan aturan pemesanan—client tahu apa yang bisa diminta tanpa perlu tahu cara dapur bekerja. | Aplikasi meminta `GET /api/produk` untuk membaca produk. API tidak selalu memakai HTTP, tetapi contoh di roadmap ini umumnya menggunakan HTTP. |
| **Endpoint** | Jalur operasi tertentu pada API—bayangkan alamat tujuan beserta jenis permintaannya. | `GET /api/produk` meminta daftar produk, sementara `POST /api/produk` biasanya mengirim data untuk membuat produk. Method dan alamat bersama-sama menjelaskan operasi yang dimaksud. |
| **HTTP Method** | Penanda jenis tindakan yang diminta dari server. | `GET` biasanya membaca, `POST` biasanya membuat/mengirim, `PATCH` biasanya mengubah sebagian, dan `DELETE` biasanya menghapus. Aturan tepatnya ditentukan oleh API. |
| **HTTP** | Aturan komunikasi yang umum dipakai browser dan server untuk bertukar request dan response. `HTTPS` adalah HTTP yang dilindungi enkripsi koneksi TLS. | Saat browser membuka halaman atau mengambil data API, ia biasanya berkomunikasi menggunakan HTTP atau HTTPS. |
| **URL / Origin** | `URL` adalah alamat lengkap resource di web. `Origin` adalah bagian yang menentukan asal sebuah halaman, yaitu gabungan protocol, hostname, dan port. | `https://contoh.com:443/produk` adalah URL. Untuk CORS, `https://contoh.com` berbeda origin dari `https://api.contoh.com` karena hostname berbeda. |
| **HTTP Status Code** | Angka ringkas yang memberi tahu bagaimana server menangani request. | `200` berarti berhasil; `201` berarti data berhasil dibuat; `404` berarti resource tidak ditemukan; `500` menandakan masalah di server. Status membantu kita mengetahui jalur penanganan berikutnya. |
| **Database / Table / Row / Column** | `Database` adalah tempat penyimpanan data terstruktur. `Table` seperti lembar data; `row` adalah satu catatan; `column` adalah satu jenis informasi pada tiap catatan. | Pada tabel `users`, satu row bisa mewakili satu user, sedangkan column `email` menyimpan alamat email user tersebut. |
| **Relation** | Hubungan antara data pada beberapa table, biasanya melalui key yang sama. | `pesanan.user_id` dapat menunjuk ke `users.id`; dari situ database mengetahui user mana yang memiliki pesanan tersebut. |
| **JSON** | Bentuk teks yang umum dipakai untuk mengirim data antarprogram. | `{"nama":"Budi","umur":17}` adalah teks JSON. Untuk menggunakannya sebagai object JavaScript, teks itu perlu diurai, misalnya dengan `JSON.parse()`. |
| **DOM** | Bentuk terstruktur dari halaman HTML yang dapat dibaca dan diubah oleh JavaScript di browser. Bayangkan halaman sebagai pohon elemen, dengan elemen induk dan anak. | Tombol dan paragraf HTML menjadi node di DOM; JavaScript dapat menemukan tombol lalu menanggapi klik. React membantu mengatur perubahan UI tanpa kita mengubah DOM satu per satu. |
| **Browser** | Aplikasi yang membuka dan menampilkan halaman web, seperti Chrome, Firefox, atau Edge. Browser juga menjalankan JavaScript halaman dan menyediakan alat pengembang. | Tab Console di browser DevTools menampilkan pesan `console.log` dan error dari halaman. |
| **Loading / Error State** | Kondisi UI yang menjelaskan status pekerjaan kepada user: data sedang dimuat atau terjadi kegagalan. | Saat request berjalan, tampilkan `"Memuat..."`; jika request gagal, tampilkan pesan error agar user tahu data belum berhasil dimuat. |
| **Responsive Design** | Cara membuat tampilan tetap mudah digunakan pada ukuran layar berbeda, seperti ponsel, tablet, dan desktop. | Layout dapat memakai satu kolom di layar kecil dan beberapa kolom di layar lebih lebar. |

### React, TypeScript, dan aplikasi

| Istilah | Arti sederhananya | Contoh dan cara memahaminya |
|---|---|---|
| **UI (User Interface)** | Bagian aplikasi yang dilihat atau digunakan orang, seperti halaman, tombol, menu, dan form. | Form login adalah UI: user mengisi email/password lalu menekan tombol masuk. |
| **Component** | Bagian UI yang dibuat sebagai unit tersendiri agar dapat dipahami dan digunakan kembali. Mirip potongan Lego yang dapat disusun menjadi halaman. | `KartuProduk` dapat menampilkan satu produk; daftar produk bisa memakai component itu berkali-kali dengan data berbeda. |
| **JSX** | Cara menulis gambaran UI React di dalam file JavaScript/TypeScript dengan bentuk yang mirip HTML. | `<h1>Halo</h1>` adalah JSX. JSX mirip HTML tetapi memiliki aturan JavaScript, misalnya memakai `className` alih-alih `class`. |
| **Props** | Data masukan yang dikirim dari component induk ke component anak—mirip informasi yang diberikan kepada sebuah cetakan. | `<KartuProduk nama="Kaos" />` mengirim prop `nama` bernilai `"Kaos"` kepada component `KartuProduk`. Component anak sebaiknya tidak mengubah props secara langsung. |
| **State** | Data yang dapat berubah selama aplikasi digunakan dan memengaruhi tampilan. | Nilai counter adalah state. Saat tombol menambah counter, React menerima nilai state baru lalu memperbarui tampilan yang berkaitan. |
| **Render** | Proses React menentukan tampilan yang sesuai dengan props dan state saat itu. Ini tidak sama dengan memuat ulang seluruh halaman. | Jika `count` berubah dari `0` menjadi `1`, component dapat dirender lagi agar teks counter menampilkan `1`. |
| **Hook** | Function React yang memberi component akses ke kemampuan seperti state dan effect. Namanya biasanya dimulai dengan `use`. | `useState(0)` menyediakan state awal; `useEffect(...)` menjalankan pekerjaan yang terhubung dengan perubahan/kemunculan component. Hook mengikuti aturan pemanggilan React. |
| **TypeScript Type** | Keterangan yang membantu memeriksa jenis data yang diharapkan saat menulis kode. Mirip label pada paket yang menyatakan isinya. | `let umur: number = 17` memberi tahu TypeScript bahwa `umur` seharusnya angka. TypeScript membantu menemukan sebagian kesalahan sebelum program dijalankan, tetapi tidak otomatis memvalidasi data dari API saat runtime. |
| **Route / Routing** | `Route` adalah alamat/pola alamat aplikasi; `routing` adalah proses memilih halaman atau handler yang cocok dengan alamat tersebut. | `/produk/5` dapat cocok dengan route dinamis `/produk/[id]`, dengan `id` bernilai `"5"`. |
| **Server Component / Client Component** | Di Next.js App Router, ini membedakan batas kemampuan component. Server Component dapat bekerja dengan sumber daya di server; Client Component dapat menggunakan interaksi React seperti state dan event handler. | Tombol yang berubah saat diklik memerlukan kemampuan client. `"use client"` menandai module client, tetapi tidak berarti component hanya dirender di browser. |
| **Build** | Langkah menyiapkan kode proyek agar dapat dijalankan atau diterbitkan. Tool dapat memeriksa kode, mengubah format tertentu, dan menghasilkan file siap deploy. | `next build` membuat hasil build Next.js; error saat build perlu diperbaiki sebelum aplikasi dapat dipublikasikan dengan benar. |
| **Cache / Caching** | Menyimpan salinan data atau hasil untuk sementara supaya dapat digunakan lagi tanpa mengerjakan atau mengambil ulang semuanya. Cache perlu aturan kapan data dianggap usang dan diperbarui. | Halaman artikel yang jarang berubah dapat di-cache; harga yang harus selalu terbaru mungkin perlu strategi cache yang berbeda. |

### Database, keamanan, dan kerja developer

| Istilah | Arti sederhananya | Contoh dan cara memahaminya |
|---|---|---|
| **ORM** | Alat yang membantu program berbicara dengan database menggunakan fungsi/object, sehingga banyak pekerjaan SQL dapat ditulis melalui API bahasa pemrograman. ORM tidak membuat database hilang dan tidak membuat semua query otomatis cepat. | Prisma dapat menulis `prisma.user.findMany()` untuk membaca user. Memahami SQL tetap berguna saat memeriksa hasil atau mencari query yang lambat. |
| **Schema / Migration** | `Schema` adalah rancangan bentuk data. `Migration` adalah catatan perubahan bertahap untuk membuat database mengikuti rancangan baru. | Menambahkan column `email` mengubah schema; migration mencatat perubahan yang perlu diterapkan pada database lokal atau production. |
| **Authentication / Authorization** | `Authentication` menjawab “siapa kamu?”; `authorization` menjawab “apa yang boleh kamu lakukan?”. | Login memeriksa identitas user. Setelah login, server tetap harus memastikan user tersebut memang boleh menghapus produk tertentu. |
| **Hashing** | Mengubah data menjadi bentuk ringkas satu arah untuk keperluan seperti menyimpan password dengan lebih aman. Hash password bukan password yang dienkripsi dan bisa dibalik. | Saat login, sistem membandingkan password yang dimasukkan dengan hash tersimpan menggunakan library password-hashing yang sesuai; password asli tidak perlu disimpan. |
| **Validation** | Memeriksa apakah data sesuai aturan sebelum dipakai atau disimpan. Mengirim form ke server bukan jaminan data benar. | Untuk field `umur`, server dapat menolak teks kosong atau nilai yang bukan angka. Validasi harus dilakukan di server meskipun form juga divalidasi di browser. |
| **Git Repository / Branch / Commit** | Repository menyimpan proyek dan riwayatnya; branch adalah jalur kerja terpisah; commit adalah satu catatan/snapshot perubahan. | Buat branch untuk fitur baru, simpan perubahan sebagai commit, lalu gabungkan setelah diperiksa. `commit` lokal belum sama dengan mengirim kode ke GitHub. |
| **Pull Request (PR) / Code Review** | PR adalah permintaan untuk memasukkan perubahan branch ke branch lain. Code review adalah proses orang lain membaca dan memberi masukan pada perubahan tersebut. | Sebelum fitur digabung ke branch utama, rekan tim dapat memeriksa logika, meminta perubahan, dan memastikan pemeriksaan otomatis lulus. |
| **Test / Testing** | Pemeriksaan untuk mengetahui apakah program berperilaku sesuai harapan. Test dapat menguji fungsi kecil atau alur aplikasi lengkap. | Test untuk `hitungDiskon(100000, 10)` bisa memeriksa apakah hasilnya `90000`. Jika hasil berbeda, test memberi tahu bahwa ada perilaku yang perlu diperiksa. |
| **Deployment** | Mengirim dan menjalankan aplikasi di environment yang dapat diakses pengguna, bukan hanya di komputer developer. | Setelah deployment, aplikasi dapat dibuka lewat URL publik. Environment production perlu konfigurasi secret dan database yang benar. |
| **CI/CD** | Otomatisasi yang memeriksa perubahan dan/atau merilis aplikasi saat kode diperbarui. | Setelah push, pipeline dapat menjalankan lint dan test; jika berhasil, sistem dapat melanjutkan deployment. CI/CD adalah rangkaian proses, bukan satu perintah tertentu. |
| **Algorithm / Data Structure** | `Algorithm` adalah langkah teratur untuk menyelesaikan masalah. `Data structure` adalah cara menyimpan dan mengatur data agar operasi tertentu lebih mudah atau cepat. | Menghitung frekuensi huruf adalah algorithm; object atau `Map` dapat dipakai sebagai data structure untuk menyimpan huruf dan jumlah kemunculannya. |
| **Production / Development** | `Development` adalah environment untuk membangun dan mencoba aplikasi. `Production` adalah environment yang melayani pengguna sungguhan. Keduanya dapat memiliki database, URL, dan konfigurasi berbeda. | Jangan menganggap data aman dihapus hanya karena perintah berhasil dijalankan; pastikan command ditujukan ke database development, bukan database production. |

Setelah memahami penjelasan sederhananya, gunakan definisi yang lebih lengkap berikut saat ingin mengetahui detail teknis atau perbedaan istilah yang mirip.

## JavaScript dan konsep umum

| Istilah | Penjelasan |
|---|---|
| **Runtime** | Lingkungan yang menjalankan program. Browser dan Node.js sama-sama dapat menjalankan JavaScript, tetapi menyediakan kemampuan berbeda: browser menyediakan DOM, sedangkan Node.js menyediakan akses ke file system dan proses server. |
| **Variable** | Nama yang merujuk ke sebuah nilai, misalnya `const harga = 50000`. `const` mencegah nama itu diisi ulang, tetapi tidak otomatis membuat isi object atau array menjadi immutable. |
| **Function** | Blok kode yang dapat dipanggil untuk menjalankan tugas. Function dapat menerima input lewat `parameter` dan mengirim hasil kembali lewat `return`. |
| **Parameter / Argument** | `Parameter` adalah nama penerima yang ditulis pada definisi function, misalnya `nama` di `function sapa(nama)`. `Argument` adalah nilai yang dikirim saat function dipanggil, misalnya `"Budi"` di `sapa("Budi")`. |
| **Return value** | Nilai yang dikirim keluar oleh function melalui `return`. Jika tidak ada `return` eksplisit, hasil pemanggilan function biasanya `undefined`. |
| **Expression / Statement** | `Expression` adalah potongan kode yang menghasilkan nilai, seperti `harga * jumlah`. `Statement` adalah instruksi yang menjalankan aksi, seperti `const total = harga * jumlah;` atau `if (...) { ... }`. |
| **Property / Method** | `Property` adalah data pada object (`user.nama`); `method` adalah function yang menjadi bagian object (`user.sapa()`). Tanda `()` memanggil method. |
| **Scope** | Aturan yang menentukan bagian kode mana yang dapat mengakses variable tertentu. `let` dan `const` mengikuti scope function atau block tempat keduanya dideklarasikan. |
| **Closure** | Function beserta aksesnya ke variable dari lexical scope tempat function itu dibuat. Karena itu, function dapat tetap memakai variable tersebut setelah function pembungkusnya selesai berjalan. |
| **Callback** | Function yang diberikan ke kode lain agar dapat dipanggil kemudian, misalnya ketika event terjadi atau operasi selesai. Contoh: function yang diberikan ke `addEventListener` atau `.map()`. |
| **Synchronous / Asynchronous** | Operasi `synchronous` berjalan berurutan dan menahan langkah berikutnya sampai selesai. Operasi `asynchronous` memungkinkan program melanjutkan pekerjaan lain sambil menunggu hasil, misalnya saat mengambil data lewat network. |
| **Promise** | Object yang mewakili hasil operasi asynchronous yang belum tentu selesai saat itu juga. Statusnya `pending` (belum selesai), `fulfilled` (berhasil), atau `rejected` (gagal). |
| **`async` / `await`** | `async` menandai function yang hasilnya berupa `Promise`. `await` menunggu hasil Promise di dalam function `async`, sehingga alur kode lebih mudah dibaca; ia tidak menghentikan seluruh aplikasi atau browser. |
| **Event Loop** | Mekanisme JavaScript yang mengatur kapan callback dari antrean asynchronous dapat dijalankan. Secara sederhana, callback dijalankan setelah pekerjaan synchronous yang sedang berada di `call stack` selesai. |
| **Immutable / Immutability** | Data disebut immutable jika tidak diubah langsung setelah dibuat. Dalam React, membuat array atau object baru saat memperbarui state membantu React mengenali perubahan. |
| **Destructuring** | Sintaks untuk mengambil nilai dari object atau array ke variable. Contoh: `const { nama } = user` mengambil property `nama` dari `user`. |
| **Spread / Rest** | Sintaks `...` punya arti sesuai posisinya. `Spread` membentangkan isi array/object, seperti `[...items]`; `rest` mengumpulkan beberapa nilai ke satu array, seperti `function jumlah(...angka)`. |
| **Module** | File JavaScript yang mengatur kode mana yang boleh digunakan file lain. `export` menyediakan nilai/function; `import` mengambilnya dari module lain. |
| **JSON** | Format teks untuk bertukar data, biasanya menggunakan object, array, string, number, boolean, dan `null`. `JSON.parse()` mengubah teks JSON menjadi nilai JavaScript; `JSON.stringify()` melakukan kebalikannya. |

## React dan Next.js

| Istilah | Penjelasan |
|---|---|
| **UI (User Interface)** | Bagian aplikasi yang dilihat dan digunakan orang, seperti tombol, form, menu, dan daftar data. |
| **Component** | Unit UI yang dapat digunakan kembali. Component React biasanya berupa function yang menghasilkan JSX. Component dapat menerima `props`, membaca `state`, lalu menghasilkan UI. |
| **JSX** | Sintaks mirip HTML yang ditulis di dalam JavaScript/TypeScript untuk mendeskripsikan UI React. JSX bukan HTML biasa; misalnya atribut `class` ditulis sebagai `className`. |
| **Props** | Input yang diberikan parent component kepada child component. Props diperlakukan sebagai read-only oleh component penerima; jika data perlu berubah, perubahan biasanya dikelola oleh state atau sumber data di parent. |
| **State** | Data yang dimiliki atau dikelola component. Saat state diperbarui dengan cara React yang sesuai, React menjadwalkan render baru agar UI mencerminkan data terbaru. |
| **Render** | Proses React memanggil component untuk mengetahui UI yang seharusnya ditampilkan. Render tidak selalu berarti seluruh halaman dimuat ulang; React membandingkan hasilnya dan memperbarui bagian DOM yang perlu. |
| **Effect / Side Effect** | Pekerjaan yang berinteraksi dengan sesuatu di luar proses menghasilkan UI, seperti network request, timer, atau subscription. `useEffect` dipakai untuk menghubungkan pekerjaan tersebut dengan siklus hidup component; tidak semua logika perlu diletakkan di effect. |
| **Hook** | Function React dengan aturan pemanggilan khusus yang memberi component akses ke fitur React, misalnya state dan effect. Hook bawaan seperti `useState` dan custom Hook seperti `useFetch` dipanggil di tingkat teratas component atau Hook lain. |
| **Controlled Component** | Form element yang nilainya disimpan di state React, lalu diperbarui melalui event handler. Pola ini membuat nilai input dan state tetap sinkron. |
| **Context** | Mekanisme React untuk menyediakan data kepada banyak component di bawah provider tanpa meneruskan props melalui setiap lapisan. Context cocok untuk data yang memang dibutuhkan lintas banyak bagian, bukan pengganti otomatis untuk semua state. |
| **Routing / Route** | `Routing` adalah pemetaan URL ke tampilan atau handler aplikasi. Satu `route` adalah satu alamat atau pola alamat, misalnya `/produk/[id]`. |
| **Server Component / Client Component** | Di Next.js App Router, Server Component dirender di server dan dapat mengakses resource server. Client Component mendukung interaksi browser seperti state dan event handler. Client Component tetap dapat ikut dirender di server pada proses awal; `"use client"` menandai batas module client, bukan berarti kodenya hanya pernah berjalan di browser. |
| **SSR (Server-Side Rendering)** | Pembuatan HTML di server saat request ditangani. Istilah ini menjelaskan kapan/di mana HTML dirender, bukan apakah halaman akan selalu memakai data terbaru atau tidak. |
| **SSG (Static Site Generation)** | Halaman dibuat sebagai output statis sebelum request pengguna, misalnya saat build. Hasilnya dapat disajikan tanpa merender ulang halaman untuk setiap request. |
| **ISR (Incremental Static Regeneration)** | Pendekatan Next.js untuk memperbarui hasil yang di-cache setelah jeda atau aturan tertentu tanpa harus membangun ulang seluruh situs. Detail konfigurasi mengikuti versi Next.js. |
| **Server Action** | Function server yang dapat dipanggil dari UI, termasuk melalui form. Input dari browser tetap harus divalidasi dan hak akses harus diperiksa di server; penanda server bukan pengganti keamanan. |
| **Middleware** | Kode yang dijalankan pada tahap awal penanganan request untuk kebutuhan seperti pemeriksaan atau pengalihan. Middleware bukan tempat yang tepat untuk semua pekerjaan server; batas runtime dan API yang tersedia bergantung pada platform/framework. |

## Web, HTTP, dan API

| Istilah | Penjelasan |
|---|---|
| **Client / Server** | `Client` adalah pihak yang meminta layanan, seperti browser atau aplikasi mobile. `Server` adalah program yang menerima request, menjalankan logika, lalu mengirim response. Satu sistem dapat bertindak sebagai client dalam satu komunikasi dan server dalam komunikasi lain. |
| **API (Application Programming Interface)** | Kontrak atau cara terstruktur agar satu software dapat meminta kemampuan/data dari software lain. API tidak selalu berbasis HTTP, tetapi roadmap ini terutama membahas HTTP API. |
| **Endpoint** | Alamat dan operasi spesifik yang bisa dipanggil pada API, misalnya `GET /api/produk`. URL saja belum selalu menjelaskan seluruh endpoint; HTTP method juga bagian dari konteksnya. |
| **Request / Response** | `Request` adalah pesan yang dikirim client ke server, termasuk method, URL, headers, dan terkadang body. `Response` adalah balasan server, termasuk status code, headers, dan terkadang body. |
| **HTTP Method** | Menjelaskan jenis operasi yang diminta. `GET` umumnya membaca data, `POST` umumnya mengirim atau membuat data, `PUT`/`PATCH` mengubah data, dan `DELETE` menghapus data. Arti tepatnya ditentukan oleh kontrak API. |
| **HTTP Status Code** | Angka yang memberi gambaran hasil request. `2xx` umumnya sukses, `3xx` berkaitan dengan pengalihan, `4xx` menunjukkan masalah pada request/izin client, dan `5xx` menunjukkan kegagalan server. Contoh: `201` dibuat, `401` belum terautentikasi, `403` tidak diizinkan, `404` tidak ditemukan. |
| **Header** | Metadata pada HTTP request/response, misalnya `Content-Type: application/json` yang menjelaskan format body atau `Authorization` yang membawa informasi autentikasi. |
| **CORS (Cross-Origin Resource Sharing)** | Aturan browser yang menentukan apakah JavaScript dari satu origin boleh membaca response dari origin lain. CORS bukan mekanisme autentikasi dan biasanya perlu dikonfigurasi pada server yang dituju. |
| **DOM (Document Object Model)** | Representasi dokumen HTML sebagai struktur object yang dapat dibaca atau diubah oleh JavaScript di browser. React mengelola pembaruan UI melalui DOM, sehingga aplikasi React biasanya tidak mengubah DOM secara manual. |
| **Environment Variable** | Nilai konfigurasi yang diberikan ke aplikasi dari environment saat dijalankan atau dibangun. Nilai server-only dapat berisi secret; variable dengan prefix `NEXT_PUBLIC_` di Next.js dapat masuk ke bundle browser dan tidak boleh berisi secret. |

## TypeScript, database, dan keamanan

| Istilah | Penjelasan |
|---|---|
| **Type / Type Annotation** | `Type` menjelaskan jenis nilai yang diharapkan. `Type annotation` adalah penulisan eksplisit seperti `nama: string`; TypeScript juga sering dapat menyimpulkan type dari nilai awal. |
| **Interface / Type Alias** | Keduanya dapat memberi nama pada bentuk data. `interface` sering dipakai untuk bentuk object yang dapat diperluas; `type` juga mendukung union dan bentuk type lainnya. Keduanya bukan validasi otomatis terhadap data saat aplikasi berjalan. |
| **Union Type** | Type yang mengizinkan salah satu dari beberapa pilihan, misalnya `"aktif" | "nonaktif"`. Nilai di luar pilihan tersebut akan ditolak oleh pemeriksaan TypeScript. |
| **Generic** | Parameter type yang membuat function atau struktur data dapat bekerja dengan beberapa type sambil mempertahankan informasi type. Pada `function ambil<T>(nilai: T): T`, type output mengikuti type input. |
| **Type Inference** | Kemampuan TypeScript menyimpulkan type dari konteks atau nilai yang tersedia, sehingga annotation tidak perlu ditulis di setiap variable. |
| **SQL Query** | Instruksi SQL untuk membaca atau mengubah data database. Dalam query, `FROM` menentukan sumber tabel, `JOIN` menggabungkan baris terkait, `WHERE` menyaring baris, dan `GROUP BY` mengelompokkan baris. |
| **Table / Row / Column** | `Table` menyimpan data sejenis; `row` adalah satu record/baris; `column` adalah satu field/atribut yang dimiliki setiap baris. |
| **Primary Key / Foreign Key** | `Primary key` mengidentifikasi satu row secara unik. `Foreign key` menghubungkan row ke row pada tabel lain dan dapat membantu database menjaga integritas relasi. |
| **Index** | Struktur tambahan yang membantu database menemukan atau mengurutkan data lebih cepat untuk pola query tertentu. Index memakai ruang penyimpanan dan dapat menambah biaya saat data ditulis, jadi tidak semua column perlu di-index. |
| **Transaction** | Sekumpulan operasi database yang diperlakukan sebagai satu unit: berhasil bersama atau dibatalkan sesuai aturan transaksi. Ini berguna untuk menjaga data tetap konsisten ketika beberapa perubahan saling bergantung. |
| **ORM (Object-Relational Mapper)** | Library yang menyediakan cara mengakses database melalui object/function dalam bahasa pemrograman. Prisma adalah ORM; memahami SQL tetap membantu saat menilai query, performa, dan hasilnya. |
| **Schema / Migration** | `Schema` adalah definisi struktur data, seperti model, column, dan relation. `Migration` adalah perubahan schema yang dicatat sebagai langkah berurutan agar database dapat diperbarui secara terkontrol. |
| **CRUD** | Singkatan `Create`, `Read`, `Update`, `Delete`: empat operasi dasar untuk membuat, membaca, memperbarui, dan menghapus data. |
| **Authentication / Authorization** | `Authentication` memeriksa identitas (siapa user ini?). `Authorization` memeriksa izin (apa yang boleh dilakukan user ini?). Login saja tidak otomatis memberi izin untuk membaca atau mengubah semua data. |
| **Session / Token** | `Session` menyimpan status login yang dapat dikenali server pada request berikutnya. `Token` adalah credential yang dibawa untuk membuktikan atau menyampaikan klaim tertentu; token yang dicuri dapat disalahgunakan, jadi penyimpanan dan masa berlakunya penting. |
| **Hashing** | Mengubah input menjadi nilai turunan dengan fungsi satu arah. Password harus disimpan memakai password-hashing algorithm khusus seperti bcrypt/Argon2, bukan enkripsi yang dapat dibalik atau hash cepat biasa. |
| **Validation / Sanitization** | `Validation` memeriksa apakah data memenuhi aturan yang diharapkan. `Sanitization` mengubah atau membatasi data untuk konteks penggunaannya. Keduanya berbeda dan tidak menggantikan encoding/output escaping yang sesuai. |
| **SQL Injection** | Kerentanan ketika input tidak tepercaya ikut ditafsirkan sebagai bagian dari perintah SQL. Gunakan parameterized query atau ORM dengan pola aman; hindari membangun query dengan menyambungkan input mentah. |
| **XSS (Cross-Site Scripting)** | Kerentanan ketika konten tidak tepercaya dijalankan sebagai script di browser pengguna lain. Hindari memasukkan HTML mentah tanpa sanitasi yang tepat; React escaping teks secara default, tetapi API seperti `dangerouslySetInnerHTML` mengubah risikonya. |
| **IDOR (Insecure Direct Object Reference)** | Masalah authorization ketika seseorang dapat melihat atau mengubah object milik pihak lain hanya dengan mengganti ID pada request. Server harus memeriksa izin dan kepemilikan data untuk setiap operasi. |

## Workflow dan kualitas kode

| Istilah | Penjelasan |
|---|---|
| **Git Repository** | Folder proyek yang dilacak Git, termasuk riwayat perubahan. Repository lokal dapat dihubungkan dengan remote repository seperti yang disimpan di GitHub. |
| **Branch** | Jalur kerja terpisah dalam repository. Branch membantu mengerjakan perubahan tanpa langsung mencampurnya ke branch utama. |
| **Commit** | Snapshot perubahan yang disimpan di riwayat Git, biasanya disertai pesan yang menjelaskan tujuan perubahan. Commit lokal belum otomatis terkirim ke GitHub. |
| **Pull Request (PR)** | Permintaan untuk meninjau dan menggabungkan perubahan dari satu branch ke branch lain. PR memfasilitasi code review, diskusi, dan pemeriksaan otomatis. |
| **Merge / Merge Conflict** | `Merge` menggabungkan riwayat perubahan branch. `Merge conflict` terjadi ketika Git tidak dapat menentukan cara menggabungkan perubahan secara otomatis; developer perlu memilih atau menyusun hasil yang benar. |
| **Code Review** | Pemeriksaan perubahan kode oleh developer lain untuk mengevaluasi ketepatan, keterbacaan, keamanan, dan kesesuaiannya dengan kebutuhan. Review bukan sekadar mencari kesalahan gaya. |
| **Testing** | Pemeriksaan otomatis atau manual untuk memastikan perilaku aplikasi sesuai harapan. `Unit test` menguji bagian kecil; `integration test` memeriksa beberapa bagian bekerja bersama; `E2E test` menjalankan alur aplikasi seperti yang dilakukan user. |
| **Linting / Formatting** | `Linting` memeriksa pola atau potensi masalah pada kode. `Formatting` merapikan tampilan kode secara konsisten. ESLint umumnya dipakai untuk linting; Prettier untuk formatting. |
| **CI/CD** | `Continuous Integration / Continuous Delivery (atau Deployment)` adalah rangkaian otomatis untuk memeriksa dan/atau merilis perubahan kode. Pipeline dapat menjalankan test, build, lalu deployment sesuai konfigurasi proyek. |
| **Deployment** | Proses menempatkan aplikasi/build ke environment yang dapat digunakan, misalnya server production. Deployment juga melibatkan konfigurasi environment, database, domain, dan pemantauan hasil. |
| **Sandbox** | Environment atau mode terisolasi untuk mencoba integrasi tanpa memengaruhi data/layanan production. Contohnya test mode penyedia pembayaran. Sandbox tetap perlu diperlakukan dengan hati-hati dan bukan jaminan keamanan mutlak. |

---

> *"Pahami tujuan kode, lalu telusuri aliran kontrol dan data dengan aturan bahasa yang digunakan."* 💪
