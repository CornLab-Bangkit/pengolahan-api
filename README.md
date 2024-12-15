# pengolahan-jagung

PORT: 3000
HOST: 0.0.0.0

// Rute untuk melayani gambar
  server.route({
    method: 'GET',
    path: '/images/{filename}',
    handler: (request, h) => {
      const imagesPath = path.join(__dirname, '../images', request.params.filename);
      return h.file(imagesPath);
    },
  });

   // Rute untuk root URL
   server.route({
    method: 'GET',
    path: '/',
    handler: () => ({
      message: 'Selamat datang di Pengolahan Jagung! Gunakan /recoms untuk melihat rekomendasi.',
    }),
  });

  // Rute untuk mendapatkan detail rekomendasi berdasarkan ID
  server.route({
    method: 'GET',
    path: '/recoms/{id}',
    handler: (request, h) => {
      const { id } = request.params;
        const numericId = Number(id); // Konversi id dari string ke angka
        const recommendation = recoms.find(recom => recom.id === numericId);
      if (!recommendation) {
        return h.response({
          error: true,
          message: 'Recommendation not found',
        }).code(404);
      }
      return {
        error: false,
        message: 'Recommendation fetched successfully',
        recommendation: recommendation,
      };
    },
  });

  contoh output: 
  "recommendation": {
        "id": 23,
        "name": "Bunga dari Daun Jagung",
        "description": "Bunga daun jagung adalah kerajinan tangan yang menggunakan daun jagung sebagai bahan utama untuk membuat bunga hias yang unik dan ramah lingkungan. Bunga ini bisa digunakan sebagai dekorasi rumah, hadiah, atau bagian dari rangkaian bunga alami.",
        "steps": "<b>Langkah-langkah membuat bunga kreatif dari daun jagung</b><br><ol><li>Persiapkan Daun Jagung: Pilih daun jagung yang sudah kering dan cukup lentur. Jika daun jagung terlalu keras, rendam sebentar dalam air hangat untuk melenturkannya.</li><li>Memotong Daun Jagung: Potong daun jagung menjadi bagian-bagian kecil yang dapat digunakan untuk membuat kelopak bunga, sekitar 5-10 cm panjangnya, sesuai dengan ukuran bunga yang diinginkan.</li><li>Membuat Kelopak Bunga: Ambil selembar daun jagung dan gulung atau lipat untuk membentuk kelopak bunga. Anda bisa menggunakan beberapa lapisan daun jagung untuk menciptakan kelopak yang lebih tebal dan menarik.</li><li>Menyusun Kelopak: Gabungkan kelopak-kelopak daun jagung dengan menyusunnya dalam bentuk melingkar. Tempelkan bagian tengah kelopak dengan menggunakan lem atau kawat untuk menyatukan kelopak-kelopak tersebut.</li><li>Membuat Tangkai Bunga: Ambil sehelai daun jagung yang lebih panjang dan lentur, kemudian gulung atau anyam untuk membentuk tangkai bunga. Pastikan tangkai cukup panjang dan kuat untuk menopang bunga.</li><li>Menyatukan Tangkai dan Bunga: Pasang tangkai pada bagian bawah bunga dengan menggunakan benang, kawat, atau lem untuk memastikan bunga dan tangkai terhubung dengan kuat.</li><li>Menyelesaikan Bunga: Setelah bunga dan tangkai terpasang, rapikan bentuk bunga agar terlihat lebih indah. Anda juga bisa menambahkan daun jagung kecil sebagai pelengkap hiasan di sekitar bunga.</li><li>Menghias Bunga (Opsional): Untuk mempercantik bunga, Anda bisa menambahkan aksen seperti pita, manik-manik, atau cat untuk memberi warna pada kelopak bunga.</li></ol>",
        "imageCover": "https://storage.googleapis.com/cornlabs-cloud.appspot.com/images/corn-husk-flower.jpg",
        "category": "Husk"
