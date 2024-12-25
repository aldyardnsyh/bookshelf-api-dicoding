# Bookshelf API

Bookshelf API adalah proyek backend sederhana yang dibuat menggunakan Node.js dan Hapi.js. Proyek ini dibuat untuk memenuhi persyaratan submission **Belajar Back-End Pemula dengan JavaScript Dicoding**. API ini memungkinkan pengguna untuk menambahkan, melihat, memperbarui, dan menghapus data buku, serta memenuhi standar RESTful API.
## 📖 Fitur

 Fitur yang disediakan oleh API tersebut mencakup:

- Menyimpan data buku baru.
- Menampilkan seluruh buku atau detail spesifik berdasarkan ID.
- Memperbarui data buku.
- Menghapus data buku berdasarkan ID.

## 🛠️ Teknologi
Proyek ini dibangun menggunakan teknologi berikut:

- **Node.js** : Runtime JavaScript untuk server.
- **Hapi.js** : Framework server untuk membangun API yang kuat.
- **ESLint** : Untuk menjaga konsistensi gaya penulisan kode.
- **NanoID** : Untuk menghasilkan ID unik pada setiap buku.

## 🚀 Instalasi
Untuk menjalankan proyek ini, ikuti langkah-langkah berikut:
1. Persyaratan
Pastikan Anda telah menginstal:
  - Node.js (minimal versi 16.x)
  - npm (termasuk dalam instalasi Node.js)
  - Postman (untuk pengujian API)

2. Clone Repository 
Clone repository ini ke komputer Anda:

```bash
git clone https://github.com/aldyardnsyh/bookshelf-api-dicoding.git
cd bookshelf-api-dicoding
```

3. Install Dependencies
Instal semua dependencies yang diperlukan (ini sudah termasuk konfigurasi yang terdapat di dalam package.json):

```bash 
npm install
```

4. Menjalankan Server
Jalankan server API:
```bash 
npm run start
```
## 📚 API Response

Berikut adalah daftar fitur yang tersedia beserta contoh endpoint, request body, dan respons yang dihasilkan:

1. Menambahkan Buku
- Endpoint: POST /books
- Request Body:

```bash
  {
    "name": string,
    "year": number,
    "author": string,
    "summary": string,
    "publisher": string,
    "pageCount": number,
    "readPage": number,
    "reading": boolean
}
```
- Respons Sukses (201):
```bash
{
    "status": "success",
    "message": "Buku berhasil ditambahkan",
    "data": {
        "bookId": "wtLxqk3MKoAuzLQX"
    }
}
```
- Respons Gagal (400), Jika _**name**_ kosong:

```bash
{
    "status": "fail",
    "message": "Gagal menambahkan buku. Mohon isi nama buku"
}
```

- Respons Gagal (400), jika nilai properti _**readPage**_ yang lebih besar dari nilai properti _**pageCount**_
```bash
{
    "status": "fail",
    "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
}
```

2. Menampilkan Semua Buku
- Endpoint: GET /books
- Respons Sukses (200):
```bash
{
    "status": "success",
    "data": {
        "books": [
            {
                "id": "Qbax5Oy7L8WKf74l",
                "name": "Buku A",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "1L7ZtDUFeGs7VlEt",
                "name": "Buku B",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "K8DZbfI-t3LrY7lD",
                "name": "Buku C",
                "publisher": "Dicoding Indonesia"
            }
        ]
    }
```
Jika belum terdapat buku yang dimasukkan, server akan merespons dengan array books kosong seperti berikut:
- Respons Sukses(200):
```bash
{
    "status": "success",
    "data": {
        "books": []
    }
}
```
3. Menampilkan Detail Buku
- Endpoint: GET /books/{bookId}
- Respons Sukses (200):
```bash
{
    "status": "success",
    "data": {
        "book": {
            "id": "aWZBUW3JN_VBE-9I",
            "name": "Buku A Revisi",
            "year": 2011,
            "author": "Jane Doe",
            "summary": "Lorem Dolor sit Amet",
            "publisher": "Dicoding",
            "pageCount": 200,
            "readPage": 26,
            "finished": false,
            "reading": false,
            "insertedAt": "2021-03-05T06:14:28.930Z",
            "updatedAt": "2021-03-05T06:14:30.718Z"
        }
    }
}
```
Bila buku dengan id yang dilampirkan oleh client tidak ditemukan, maka server harus mengembalikan respons dengan:
- Respons Gagal (404):
```bash
{
    "status": "fail",
    "message": "Buku tidak ditemukan"
}
```

4. Memperbarui Buku
- Endpoint: PUT /books/{bookId}
- Request Body: Sama seperti POST /books.
- Respons Gagal (400):
Client tidak melampirkan properti _**name**_ pada request body. Bila hal ini terjadi, maka server akan merespons dengan:
```bash
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Mohon isi nama buku"
}
```
Client melampirkan nilai properti _**readPage**_ yang lebih besar dari nilai properti _**pageCount**_. Bila hal ini terjadi, maka server akan merespons dengan:
```bash
{
    "status": "fail",
    "message": "Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount"
}
```
_**Id**_ yang dilampirkan oleh client tidak ditemukkan oleh server. Bila hal ini terjadi, maka server akan merespons dengan:
```bash
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Id tidak ditemukan"
}
```
- Respons Sukses (200):
Bila buku berhasil diperbarui, server harus mengembalikan respons dengan,
```bash
{
    "status": "success",
    "message": "Buku berhasil diperbarui"
}
```

5. Menghapus Buku
- Endpoint: DELETE /books/{bookId}
- Respons Sukses (200):

Bila id **dimiliki** oleh salah satu buku, maka buku tersebut harus dihapus dan server mengembalikan respons berikut,
```bash
{
    "status": "success",
    "message": "Buku berhasil dihapus"
}
```

- Respons Gagal (400):

Bila id yang dilampirkan **tidak dimiliki** oleh buku manapun, maka server harus mengembalikan respons berikut:
```bash
{
    "status": "fail",
    "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```
