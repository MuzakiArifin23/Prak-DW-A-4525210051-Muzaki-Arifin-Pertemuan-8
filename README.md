# Desain Web - Pertemuan 8: HTML Form Lanjutan

Form registrasi event **Workshop WebFest 2026** dengan radio button, checkbox, select, textarea, file upload, dan validasi HTML5.

## Identitas Penulis

| Keterangan | Data |
|---|---|
| Nama | Muzaki Arifin |
| NPM | 4525210051 |
| Program Studi | Teknik Informatika |
| Universitas | Universitas Pancasila |
| Mata Kuliah | Desain Web |
| Tugas | Tugas Individu Pertemuan 8 |

## Tujuan

1. Membuat form dengan radio button, checkbox, select, textarea, dan file upload.
2. Menerapkan minimal empat aturan validasi HTML5.
3. Menguji minimal lima skenario input salah dan menyusun test case validasi.
4. Membahas validasi yang tetap wajib dilakukan di server.

## Struktur Folder

```text
desain-web/
└── pertemuan-08/
    ├── index.html
    ├── README.md
    ├── css/
    │   └── style.css
    ├── images/
    │   └── logo-event.svg
    └── dokumentasi/
        ├── 4525210051_Muzaki Arifin_Tugas Pertemuan 8_Form Registrasi Event.docx
        ├── 01_form-kosong-desktop.png
        ├── 01_form-kosong-mobile.png
        ├── 02_input-salah-desktop.png
        ├── 02_input-salah-mobile.png
        ├── 03_form-valid-desktop.png
        └── 03_form-valid-mobile.png
```

## Tag dan Atribut HTML yang Digunakan

| Tag / Atribut | Fungsi |
|---|---|
| `<form action method enctype>` | Membungkus form. `method="post"` dan `enctype="multipart/form-data"` dibutuhkan karena ada upload file. |
| `<label for>` | Keterangan field yang terhubung ke `id` input. |
| `<input type="text">` | Isian teks (nama, NIM, telepon). |
| `<input type="email">` | Isian email dengan pengecekan format bawaan browser. |
| `<input type="radio">` | Pilihan tunggal (jenis peserta). Satu grup memakai `name` yang sama. |
| `<input type="checkbox">` | Pilihan jamak (topik minat) dan persetujuan. |
| `<select>` dan `<option>` | Dropdown program studi. |
| `<textarea>` | Isian teks panjang (alasan mengikuti kegiatan). |
| `<input type="file">` | Upload KTM dan surat pengantar. |
| `<fieldset>` dan `<legend>` | Mengelompokkan dan memberi judul pada radio dan checkbox. |
| `required` | Field wajib diisi atau dipilih. |
| `minlength` / `maxlength` | Batas minimal dan maksimal karakter. |
| `pattern` | Format input dengan regular expression. |
| `accept` | Menyarankan jenis file pada dialog pilih file. |
| `<button type="submit/reset">` | Tombol kirim dan reset. |

## Property CSS yang Digunakan

| Property | Fungsi |
|---|---|
| `:root` dan `var(--...)` | Menyimpan warna dan ukuran sebagai variabel. |
| `box-sizing: border-box` | Padding dan border ikut dihitung dalam lebar elemen. |
| `max-width`, `margin: auto` | Membuat kontainer berada di tengah dengan lebar terbatas. |
| `padding`, `border-radius`, `box-shadow` | Tampilan kartu form. |
| `display: flex`, `gap`, `align-items` | Tata letak opsi radio/checkbox dan grup tombol. |
| `width: 100%` | Input memenuhi lebar kolom. |
| `:focus` | Penanda saat field aktif. |
| `:user-invalid` / `:user-valid` | Border merah/hijau setelah pengguna berinteraksi dengan field. |
| `@media (max-width: 600px)` | Tampilan responsif untuk mobile (tombol menjadi satu kolom). |

## Style Guide

| Elemen | Nilai |
|---|---|
| Warna utama | `#31598c` (hover `#203f65`) |
| Latar halaman | `#f4f6f8` |
| Latar kartu | `#ffffff` |
| Teks | `#252c35`, teks sekunder `#697585` |
| Border | `#d9dfe6` |
| Error | `#c62828` |
| Font | Arial, Helvetica, sans-serif |
| Judul (h1) | 30px |
| Teks input | 15px, petunjuk 13px |
| Radius | 8px (field), 14px (kartu) |
| Lebar maksimum | 780px |

## Aturan Validasi

| Field | Aturan |
|---|---|
| Nama | `required`, `minlength="3"`, `maxlength="60"` |
| Email | `required`, `type="email"` |
| NIM | `required`, `pattern="[0-9]{10}"`, `maxlength="10"` |
| Telepon | `required`, `pattern="[0-9]{10,13}"`, `minlength="10"`, `maxlength="13"` |
| Program Studi | `required` (opsi awal bernilai kosong) |
| Jenis Peserta | `required` pada grup radio |
| Alasan | `required`, `minlength="20"`, `maxlength="300"` |
| KTM | `required`, `accept=".pdf,.jpg,.jpeg,.png"` |
| Persetujuan | `required` |

## Source Code

### index.html

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Registrasi Event WebFest 2026</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>

    <main class="container">
        <section class="form-card">

            <header class="form-header">
                <img src="images/logo-event.svg" alt="Logo WebFest 2026" class="logo" width="56" height="56">
                <span class="label-top">EVENT TEKNOLOGI</span>
                <h1>Registrasi Workshop WebFest 2026</h1>
                <p>
                    Lengkapi data berikut untuk mendaftar sebagai peserta
                    dan unggah dokumen yang diperlukan.
                </p>
                <p class="required-info">* Wajib diisi</p>
            </header>

            <!--
                method POST + enctype multipart/form-data
                dibutuhkan karena form mengirim file (upload).
            -->
            <form action="/proses-registrasi" method="post" enctype="multipart/form-data">

                <!-- Nama (required, minlength, maxlength) -->
                <div class="form-group">
                    <label for="nama">Nama Lengkap *</label>
                    <input
                        type="text"
                        id="nama"
                        name="nama"
                        minlength="3"
                        maxlength="60"
                        placeholder="Contoh: Muzaki Arifin"
                        required>
                    <small>Tuliskan 3-60 karakter.</small>
                </div>

                <!-- Email -->
                <div class="form-group">
                    <label for="email">Email *</label>
                    <input
                        type="email"
                        id="email"
                        name="email"
                        placeholder="nama@email.com"
                        required>
                    <small>Gunakan alamat email yang masih aktif.</small>
                </div>

                <!-- NIM (pattern) -->
                <div class="form-group">
                    <label for="nim">NIM *</label>
                    <input
                        type="text"
                        id="nim"
                        name="nim"
                        pattern="[0-9]{10}"
                        maxlength="10"
                        placeholder="Contoh: 4525210051"
                        title="NIM harus berupa 10 digit angka"
                        required>
                    <small>Harus tepat 10 digit angka.</small>
                </div>

                <!-- Nomor Telepon (pattern) -->
                <div class="form-group">
                    <label for="telepon">Nomor Telepon *</label>
                    <input
                        type="text"
                        id="telepon"
                        name="telepon"
                        pattern="[0-9]{10,13}"
                        minlength="10"
                        maxlength="13"
                        placeholder="Contoh: 081234567890"
                        title="Nomor telepon berupa 10-13 digit angka tanpa spasi"
                        required>
                    <small>Masukkan 10-13 digit angka tanpa spasi.</small>
                </div>

                <!-- Select / Dropdown -->
                <div class="form-group">
                    <label for="program-studi">Program Studi *</label>
                    <select id="program-studi" name="program_studi" required>
                        <option value="">-- Pilih Program Studi --</option>
                        <option value="informatika">Teknik Informatika</option>
                        <option value="sistem-informasi">Sistem Informasi</option>
                        <option value="mesin">Teknik Mesin</option>
                        <option value="elektro">Teknik Elektro</option>
                        <option value="sipil">Teknik Sipil</option>
                    </select>
                </div>

                <!-- Radio Button -->
                <fieldset>
                    <legend>Jenis Peserta *</legend>

                    <div class="option">
                        <input type="radio" id="reguler" name="jenis_peserta" value="reguler" required>
                        <label for="reguler">Mahasiswa Reguler</label>
                    </div>

                    <div class="option">
                        <input type="radio" id="karyawan" name="jenis_peserta" value="karyawan">
                        <label for="karyawan">Mahasiswa Karyawan</label>
                    </div>

                    <div class="option">
                        <input type="radio" id="umum" name="jenis_peserta" value="umum">
                        <label for="umum">Peserta Umum</label>
                    </div>
                </fieldset>

                <!-- Checkbox -->
                <fieldset>
                    <legend>Topik yang Diminati</legend>
                    <p class="instruction">Anda boleh memilih lebih dari satu.</p>

                    <div class="option">
                        <input type="checkbox" id="web" name="minat[]" value="web">
                        <label for="web">Web Development</label>
                    </div>

                    <div class="option">
                        <input type="checkbox" id="uiux" name="minat[]" value="uiux">
                        <label for="uiux">UI/UX Design</label>
                    </div>

                    <div class="option">
                        <input type="checkbox" id="ai" name="minat[]" value="ai">
                        <label for="ai">Artificial Intelligence</label>
                    </div>

                    <div class="option">
                        <input type="checkbox" id="data" name="minat[]" value="data">
                        <label for="data">Data Science</label>
                    </div>

                    <div class="option">
                        <input type="checkbox" id="cyber" name="minat[]" value="cyber">
                        <label for="cyber">Cyber Security</label>
                    </div>
                </fieldset>

                <!-- Textarea -->
                <div class="form-group">
                    <label for="alasan">Alasan Mengikuti Kegiatan *</label>
                    <textarea
                        id="alasan"
                        name="alasan"
                        rows="5"
                        minlength="20"
                        maxlength="300"
                        placeholder="Jelaskan alasan Anda mengikuti kegiatan ini..."
                        required></textarea>
                    <small>Tuliskan antara 20-300 karakter.</small>
                </div>

                <!-- Upload KTM -->
                <div class="form-group">
                    <label for="ktm">Upload KTM / Kartu Identitas *</label>
                    <input
                        type="file"
                        id="ktm"
                        name="ktm"
                        accept=".pdf,.jpg,.jpeg,.png"
                        required>
                    <small>Format yang disarankan: PDF, JPG, atau PNG. Ukuran maksimum ditentukan oleh server.</small>
                </div>

                <!-- Upload Surat Pengantar -->
                <div class="form-group">
                    <label for="surat">Upload Surat Pengantar</label>
                    <input
                        type="file"
                        id="surat"
                        name="surat"
                        accept=".pdf">
                    <small>Opsional. Format PDF.</small>
                </div>

                <!-- Persetujuan -->
                <div class="agreement">
                    <input type="checkbox" id="persetujuan" name="persetujuan" value="setuju" required>
                    <label for="persetujuan">Saya menyatakan data yang diisi sudah benar. *</label>
                </div>

                <!-- Tombol -->
                <div class="button-group">
                    <button type="submit" class="btn btn-primary">Kirim Pendaftaran</button>
                    <button type="reset" class="btn btn-secondary">Reset</button>
                </div>

            </form>

        </section>
    </main>

</body>
</html>
```

### css/style.css

```css
:root {
    --primary: #31598c;
    --primary-dark: #203f65;
    --background: #f4f6f8;
    --surface: #ffffff;
    --text: #252c35;
    --muted: #697585;
    --border: #d9dfe6;
    --danger: #c62828;
    --radius: 8px;
}

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    background-color: var(--background);
    color: var(--text);
    line-height: 1.6;
}

.container {
    width: 90%;
    max-width: 780px;
    margin: 50px auto;
}

.form-card {
    background-color: var(--surface);
    padding: 40px;
    border-radius: 14px;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
}

.form-header {
    margin-bottom: 30px;
}

.logo {
    display: block;
    margin-bottom: 14px;
    border-radius: 12px;
}

.label-top {
    color: var(--primary);
    font-size: 12px;
    font-weight: bold;
    letter-spacing: 1.5px;
}

.form-header h1 {
    margin: 8px 0 10px;
    font-size: 30px;
}

.form-header p {
    margin: 0 0 5px;
    color: var(--muted);
}

.form-header .required-info {
    color: var(--danger);
    font-size: 13px;
}

.form-group {
    margin-bottom: 22px;
}

.form-group label {
    display: block;
    margin-bottom: 7px;
    font-weight: bold;
}

input[type="text"],
input[type="email"],
input[type="file"],
select,
textarea {
    width: 100%;
    padding: 12px;
    border: 1px solid var(--border);
    border-radius: var(--radius);
    font-family: inherit;
    font-size: 15px;
    background-color: white;
}

textarea {
    resize: vertical;
}

input:focus,
select:focus,
textarea:focus {
    outline: 2px solid rgba(49, 89, 140, 0.20);
    border-color: var(--primary);
}

/* Umpan balik visual setelah pengguna berinteraksi dengan field */
input:user-invalid,
select:user-invalid,
textarea:user-invalid {
    border-color: var(--danger);
    background-color: #fff6f6;
}

input:user-valid:not([type="file"]),
select:user-valid,
textarea:user-valid {
    border-color: #2e7d32;
}

small,
.instruction {
    display: block;
    margin-top: 6px;
    color: var(--muted);
    font-size: 13px;
}

fieldset {
    margin: 0 0 22px;
    padding: 20px;
    border: 1px solid var(--border);
    border-radius: var(--radius);
}

legend {
    padding: 0 8px;
    font-weight: bold;
}

.option {
    display: flex;
    align-items: center;
    gap: 9px;
    margin: 10px 0;
}

.option label {
    font-weight: normal;
}

.agreement {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 15px;
    margin-bottom: 25px;
    background-color: #f7f9fc;
    border-radius: var(--radius);
}

.agreement label {
    font-weight: normal;
}

.button-group {
    display: flex;
    gap: 12px;
}

.btn {
    padding: 12px 22px;
    border: none;
    border-radius: var(--radius);
    font-size: 15px;
    font-weight: bold;
    cursor: pointer;
}

.btn-primary {
    background-color: var(--primary);
    color: white;
}

.btn-primary:hover {
    background-color: var(--primary-dark);
}

.btn-secondary {
    background-color: #e7ebf0;
    color: var(--text);
}

@media (max-width: 600px) {
    .container {
        margin: 20px auto;
    }

    .form-card {
        padding: 24px;
    }

    .button-group {
        flex-direction: column;
    }

    .btn {
        width: 100%;
    }
}
```

## Screenshot

### Desktop (1280 px)

![Form kosong desktop](dokumentasi/01_form-kosong-desktop.png)

![Input salah desktop](dokumentasi/02_input-salah-desktop.png)

### Mobile (390 px)

![Form kosong mobile](dokumentasi/01_form-kosong-mobile.png)

![Input salah mobile](dokumentasi/02_input-salah-mobile.png)

## Test Case Validasi

Diuji di browser Chromium dengan membaca status validitas bawaan browser. Skenario bertanda **Perlu server** lolos di browser padahal seharusnya ditolak.

| No | Field | Input Uji | Hasil yang Diharapkan | Hasil Aktual | Status |
|---|---|---|---|---|---|
| 1 | nama | (dikosongkan) | Ditolak: field wajib diisi | Ditolak: wajib diisi | Sesuai |
| 2 | nama | Al (2 karakter) | Ditolak: kurang dari 3 karakter | Ditolak: terlalu pendek (2 dari min. 3) | Sesuai |
| 3 | nama | 70 karakter diketik | Input dibatasi maksimal 60 karakter | Terpotong otomatis di 60 karakter | Sesuai |
| 4 | email | muzaki@ | Ditolak: format email tidak valid | Ditolak: email tidak lengkap | Sesuai |
| 5 | nim | 12345# | Ditolak: tidak sesuai pola 10 digit angka | Ditolak: tidak sesuai pola | Sesuai |
| 6 | nim | 123456789A | Ditolak: mengandung huruf | Ditolak: ada huruf | Sesuai |
| 7 | nim | 123456789 (9 digit) | Ditolak: kurang dari 10 digit | Ditolak: hanya 9 digit | Sesuai |
| 8 | nim | 45252100511 diketik (11 digit) | Input dibatasi maksimal 10 karakter | Terpotong otomatis di 10 karakter | Sesuai |
| 9 | telepon | 08123abc456 | Ditolak: mengandung huruf | Ditolak: ada huruf | Sesuai |
| 10 | telepon | 0812345 (7 digit) | Ditolak: kurang dari 10 digit | Ditolak: pola salah dan terlalu pendek | Sesuai |
| 11 | program-studi | -- Pilih Program Studi -- | Ditolak: belum memilih program studi | Ditolak: belum memilih | Sesuai |
| 12 | jenis_peserta | (tidak ada yang dipilih) | Ditolak: jenis peserta wajib dipilih | Ditolak: belum memilih | Sesuai |
| 13 | alasan | Mau belajar (11 karakter) | Ditolak: kurang dari 20 karakter | Ditolak: terlalu pendek (11 dari min. 20) | Sesuai |
| 14 | alasan | 350 karakter diketik | Input dibatasi maksimal 300 karakter | Terpotong otomatis di 300 karakter | Sesuai |
| 15 | ktm | (tidak ada file dipilih) | Ditolak: file wajib dipilih | Ditolak: file belum dipilih | Sesuai |
| 16 | ktm | malware.exe | Seharusnya ditolak: bukan PDF/JPG/PNG | File .exe diterima browser | **Perlu server** |
| 17 | persetujuan | (tidak dicentang) | Ditolak: persetujuan wajib dicentang | Ditolak: belum dicentang | Sesuai |
| 18 | nim + nama | Atribut validasi dihapus lewat DevTools, NIM 'abc', nama kosong | Server tetap harus menolak | Form diterima browser walau atribut validasi dihapus | **Perlu server** |

Hasil: 16 dari 18 skenario sesuai harapan, 2 skenario menunjukkan celah validasi browser.

## Validasi yang Tetap Wajib di Server

Validasi HTML5 hanya untuk kenyamanan pengguna. Atribut dapat dihapus lewat DevTools atau request dikirim langsung (misalnya dengan curl), sehingga server wajib memeriksa ulang:

1. **Tipe dan isi file upload**: ekstensi, MIME type sebenarnya, ukuran maksimum, dan penggantian nama file (skenario 16 membuktikan `accept` tidak menolak `.exe`).
2. **Kelengkapan field wajib**: semua field `required` harus dicek ulang.
3. **Format dan panjang data**: pola NIM, telepon, email, serta batas panjang nama dan alasan.
4. **Nilai yang diizinkan**: `program_studi`, `jenis_peserta`, dan `minat[]` harus sesuai daftar pilihan.
5. **Keunikan dan keamanan**: cek NIM/email ganda, sanitasi input (cegah XSS), dan prepared statement (cegah SQL injection).

## Cara Menjalankan

1. Buka folder `pertemuan-08`.
2. Buka `index.html` di browser.
3. Isi form lalu klik **Kirim Pendaftaran**. Form mengirim ke `/proses-registrasi` yang belum memiliki backend, sehingga yang diuji hanyalah validasi di sisi browser.

## Kesimpulan

Form registrasi berhasil dibuat dengan seluruh komponen yang diminta dan sembilan jenis aturan validasi HTML5. Validasi browser efektif untuk input kosong, terlalu pendek, dan format salah, tetapi tidak cukup sebagai satu-satunya pengaman karena file yang tidak sesuai dan atribut yang dimanipulasi tetap lolos. Karena itu, validasi di server tetap wajib sebagai lapisan pertahanan utama.