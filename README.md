# Web Cari Film - Latihan Callback

Ini adalah proyek latihan untuk memahami konsep callback di JavaScript dengan membangun aplikasi pencarian film sederhana. Aplikasi ini menggunakan jQuery, Bootstrap, dan JavaScript.

## Fitur Utama

- Pencarian film berdasarkan judul.
- Menampilkan informasi film seperti poster, judul, dan sinopsis.
- Implementasi callback untuk pengelolaan data hasil pencarian.

## Teknologi yang Digunakan

- **HTML5**: Untuk struktur halaman.
- **CSS3**: Styling halaman.
- **Bootstrap**: Untuk membuat desain responsif dan komponen UI yang cepat.
- **JavaScript**: Untuk logika aplikasi.
- **jQuery**: Untuk manipulasi DOM dan AJAX.

## Cara Kerja Callback

Callback digunakan untuk:

1. Mengambil data dari API menggunakan AJAX.
2. Menampilkan hasil ke halaman setelah data berhasil diambil.

## Langkah Instalasi

1. Clone repository:
   ```bash
   git clone https://github.com/Ramdhik/latihan-callback.git
   ```
2. Buka folder proyek:
   ```bash
   cd latihan-callback
   ```
3. Buka file `index.html` di browser.

## Struktur Proyek

```
web-cari-film/
├── index.html       # Halaman utama
├── style.css        # Styling tambahan
├── app.js           # Logika aplikasi
├── README.md        # Dokumentasi proyek
└── assets/          # Folder untuk gambar dan file lain
```

## Contoh Callback di app.js

```javascript
// Fungsi untuk mengambil data dari API
$('.search-button').on('click', function () {
  $.ajax({
    url: 'http://www.omdbapi.com/?apikey=5910effc&s=' + $('.input-keyword').val(),
    success: (result) => {
      const movies = result.Search;
      let cards = '';
      movies.forEach((m) => {
        cards += showCards(m);
      });
      $('.movie-container').html(cards);

      $('.modal-detail-button').on('click', function () {
        $.ajax({
          url: `http://www.omdbapi.com/?apikey=5910effc&i=${$(this).data('imdbid')}`,
          success: (m) => {
            const movieDetails = showMovieDetails(m);
            $('.modal-body').html(movieDetails);
          },
        });
      });
    },
    error: (error) => {
      console.log(error);
    },
  });
});
```
## Contoh Fungsi untuk menampilkan hasil pencarian
```javascript
function showCards(m) {
  return `<div class="col md-4 my-5">
          <div class="card" style="width: 18rem">
            <img src=${m.Poster} class="card-img-top" alt=${m.Title}>
            <div class="card-body">
              <h5 class="card-title">${m.Title}</h5>
              <h6 class="card-subtitle mb-2 text-muted">${m.Year}</h6>
              <a href="#" class="btn btn-primary modal-detail-button" data-toggle="modal" data-target="#movieDetailModal" data-imdbid=${m.imdbID}>Show Details</a>
            </div>
          </div>
        </div>`;
}

function showMovieDetails(m) {
  return `           
            <div class="container-fluid">
              <div class="row">
                <div class="col-md-3">
                  <img src="${m.Poster}" class="img-fluid" alt="${m.Title}" />
                </div>
                <div class="col-md">
                  <ul class="list-group">
                    <li class="list-group-item"><h4>Title</h4></li>
                    <li class="list-group-item"><strong>Director : </strong> ${m.Director}</li>
                    <li class="list-group-item"><strong>Actors : </strong> ${m.Actors}</li>
                    <li class="list-group-item"><strong>Writer : </strong> ${m.Writer}</li>
                    <li class="list-group-item"><strong>Plot : </strong> ${m.Plot}</li>
                  </ul>
                </div>
              </div>
            </div>`;
};


```
## Cara Menggunakan

1. Masukkan judul film pada kolom pencarian.
2. Klik tombol "Cari".
3. Daftar film yang relevan akan muncul di halaman.

## Catatan Penting

- Ganti `YOUR_API_KEY` dengan API key dari [OMDb API](https://www.omdbapi.com/).
- Pastikan Anda memiliki koneksi internet saat menjalankan aplikasi.

## Referensi

- [Dokumentasi jQuery](https://api.jquery.com/)
- [Bootstrap](https://getbootstrap.com/)
- [OMDb API](https://www.omdbapi.com/)







