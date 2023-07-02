## WORD SEGEMENTATION 

Text segmentation adalah proses memisahkan teks dari gambar atau dokumen visual. Tujuan utama dari text segmentation adalah untuk mengidentifikasi dan mengisolasi wilayah-wilayah yang berisi teks sehingga dapat dianalisis lebih lanjut. 

Tahapan-tahapan dalam text segmentation secara umum meliputi:

1. **Preprocessing**: Tahap ini melibatkan persiapan gambar sebelum dilakukan segmentasi. Langkah-langkah preprocessing yang umum dilakukan meliputi konversi gambar ke skala keabuan (grayscale), normalisasi intensitas piksel, peningkatan kontras, serta penghapusan noise atau gangguan yang tidak diinginkan.

2. **Thresholding**: Pada tahap ini, gambar diubah menjadi gambar biner dengan membagi piksel-piksel gambar menjadi dua kelompok berdasarkan ambang batas tertentu. Piksel-piksel dengan intensitas di atas ambang batas akan dianggap sebagai piksel teks, sedangkan piksel-piksel dengan intensitas di bawah ambang batas akan dianggap sebagai latar belakang.

3. **Operasi Morfologi**: Operasi morfologi seperti dilasi, erosi, pembukaan, dan penutupan dapat digunakan untuk membersihkan gambar dan menghilangkan noise serta menghubungkan komponen teks yang terputus.

4. **Segmentasi Kontur**: Pada tahap ini, kontur-kontur pada gambar hasil thresholding ditemukan. Kontur-kontur ini merepresentasikan batas-batas dari objek atau komponen pada gambar.

5. **Seleksi Kontur**: Kontur-kontur yang ditemukan kemudian dianalisis dan diseleksi berdasarkan kriteria tertentu untuk memilih komponen-komponen teks yang relevan. Kriteria yang umum digunakan meliputi ukuran area, aspek rasio, dan bentuk geometris.

6. **Deteksi Teks**: Setelah seleksi kontur, komponen-komponen teks yang terdeteksi dapat diekstraksi dan diolah lebih lanjut. Langkah ini dapat mencakup ekstraksi fitur teks, pengenalan karakter, atau penggunaan metode optical character recognition (OCR) untuk mengubah teks visual menjadi teks yang dapat dipahami oleh komputer.

Tahapan-tahapan tersebut dapat disesuaikan tergantung pada metode dan algoritma yang digunakan dalam implementasi spesifik. Namun, secara umum, text segmentation bertujuan untuk memisahkan teks dari gambar melalui serangkaian proses pra-pemrosesan, pemisahan teks dari latar belakang, dan pengolahan lebih lanjut untuk mendapatkan hasil teks yang diinginkan.