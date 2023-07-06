
# WORD SEGEMENTATION
def detect_letters(image_path):
# Baca gambar menggunakan scikit-image
    image = io.imread(image_path)
    
# Ubah gambar ke skala keabuan
    gray = color.rgb2gray(image)
    
# Lakukan thresholding untuk mengubah gambar ke binary
    threshold = gray < 0.5
    
# Terapkan operasi morfologi untuk membersihkan gambar
    clean_image = measure.label(threshold)
    
# Temukan kontur huruf
    contours = measure.find_contours(clean_image, 0.8)
    
 # Deteksi huruf berdasarkan area dan aspek rasio
    detected_letters = []
    for contour in contours:
        y, x = contour[:, 0], contour[:, 1]
        ymin, ymax = int(min(x)), int(max(x))
        xmin, xmax = int(min(y)), int(max(y))
        width = xmax - xmin
        height = ymax - ymin
        area = width * height
        aspect_ratio = width / height
        if area > 100 and aspect_ratio > 0.2:
            detected_letters.append((xmin, ymin, width, height))
    
    return detected_letters

# Path file gambar
image_path = 'gamal.jpg'

# Buka gambar menggunakan scikit-image
image = io.imread(image_path)

# Tampilkan gambar awal
plt.subplot(1, 2, 1)
plt.imshow(image)
plt.axis('off')
plt.title('GAMBAR ASLI')

# Panggil fungsi deteksi huruf
detected_letters = detect_letters(image_path)

# Tampilan gambar dengan persegi panjang yang mengelilingi huruf yang terdeteksi
plt.subplot(1, 2, 2)
plt.imshow(image)
plt.axis('off')
plt.title('GAMBAR SETELAH DETEKSI TEXT')

# Tampilan persegi panjang yang mengelilingi huruf yang terdeteksi
for (x, y, width, height) in detected_letters:
    rect = plt.Rectangle((y, x), height, width, edgecolor='r', linewidth=0.5, fill=False)
    plt.gca().add_patch(rect)
    
# muhammadgamal_202131035
plt.show()

##  TEORI WORD SEGEMENTATION 
Word segmentation dalam pengolahan citra adalah proses untuk memisahkan kata-kata dalam citra yang berisi teks menjadi unit-unit kata yang terpisah. Tujuan utama dari word segmentation adalah untuk mengidentifikasi batas antara setiap kata dalam citra teks sehingga teks tersebut dapat diproses lebih lanjut, seperti pengenalan karakter atau analisis teks.

Word segmentation merupakan tantangan dalam pengolahan citra karena teks dalam citra bisa memiliki variasi bentuk, ukuran, orientasi, dan tingkat kompleksitas yang tinggi. Dalam word segmentation, pendekatan yang umum digunakan adalah dengan memanfaatkan informasi visual dalam citra, seperti kontras, bentuk, tekstur, dan distribusi piksel, untuk memisahkan kata-kata.

Berikut adalah beberapa metode dan teknik yang umum digunakan dalam word segmentation dalam pengolahan citra:

1. Metode berbasis pemrosesan intensitas: Metode ini menggunakan informasi intensitas piksel dalam citra untuk mengidentifikasi batas antara kata-kata. Metode ini dapat melibatkan pendekatan seperti analisis tepi, analisis proyeksi, analisis profil, atau metode pemrosesan intensitas lainnya.

2. Metode berbasis pemrosesan tekstur: Metode ini memanfaatkan informasi tekstur citra untuk memisahkan kata-kata. Teknik seperti ekstraksi fitur tekstur (misalnya, GLCM, LBP, atau Haralick) atau pemrosesan menggunakan filter tekstur (misalnya, Gabor filter) dapat digunakan dalam metode ini.

3. Metode berbasis pemrosesan bentuk: Metode ini menggunakan informasi bentuk dan struktur kata-kata dalam citra untuk memisahkan kata-kata. Metode ini bisa melibatkan deteksi bentuk atau objek (misalnya, elips, lingkaran) atau analisis struktur hierarki dalam citra.

4. Metode berbasis pemrosesan konteks: Metode ini memanfaatkan konteks global dalam citra atau konteks lokal di sekitar kata-kata untuk memisahkan kata-kata. Metode ini bisa melibatkan penggunaan model bahasa atau aturan bahasa untuk mengidentifikasi batas kata-kata.

5. Metode berbasis pembelajaran mesin: Metode ini melibatkan penggunaan algoritma pembelajaran mesin untuk mempelajari pola segmentasi kata-kata dari data latih. Metode ini bisa melibatkan penggunaan fitur-fitur visual dan teks untuk melatih model yang dapat memisahkan kata-kata dalam citra.

Setiap metode dan teknik dalam word segmentation memiliki kelebihan dan keterbatasan sendiri tergantung pada karakteristik teks dalam citra dan tujuan pengolahan yang diinginkan. Pemilihan metode yang tepat dan pengaturan parameter yang sesuai sangat penting untuk mencapai hasil word segmentation yang akurat dalam pengolahan citra.




teori tentang tahapan-tahapan dalam word segmentation pada pengolahan citra:

1. Pra-pemrosesan citra:
   Pra-pemrosesan citra melibatkan langkah-langkah awal untuk mempersiapkan citra sebelum melakukan word segmentation. Tahap ini mencakup impor citra ke dalam format yang sesuai, konversi ke skala abu-abu, dan normalisasi intensitas. Konversi ke skala abu-abu dilakukan untuk menghilangkan informasi warna yang tidak diperlukan dalam word segmentation, sedangkan normalisasi intensitas dilakukan untuk memastikan tingkat keabuan citra berada dalam rentang yang tepat untuk analisis lebih lanjut.

2. Deteksi teks:
   Deteksi teks adalah langkah penting dalam word segmentation. Pada tahap ini, dilakukan upaya untuk mendeteksi lokasi teks dalam citra. Beberapa metode yang umum digunakan dalam deteksi teks meliputi filter citra, analisis tepi, deteksi komponen terhubung, dan segmentasi teks. Filter citra seperti filter Sobel atau filter Laplacian dapat digunakan untuk meningkatkan deteksi tepi teks. Selanjutnya, analisis tepi digunakan untuk mengidentifikasi garis atau tepi teks dalam citra. Deteksi komponen terhubung dilakukan untuk mengenali komponen dalam citra yang mungkin merupakan teks berdasarkan informasi tepi. Setelah itu, segmentasi teks dilakukan untuk memisahkan teks dari latar belakangnya.

3. Segmentasi kata:
   Setelah teks berhasil dideteksi, langkah selanjutnya adalah segmentasi kata. Pada tahap ini, dilakukan upaya untuk memisahkan kata-kata dalam teks menjadi unit-unit terpisah. Metode yang umum digunakan dalam segmentasi kata meliputi analisis profil horizontal, analisis proyeksi, dan deteksi spasi antara kata. Analisis profil horizontal melibatkan analisis pola kecerahan pada setiap baris teks untuk mengidentifikasi garis pemisah antara kata-kata. Analisis proyeksi melibatkan analisis pola proyeksi piksel vertikal pada citra teks untuk mengidentifikasi batas antara kata-kata. Deteksi spasi antara kata dilakukan dengan mengidentifikasi jarak atau ruang kosong antara komponen terhubung yang mewakili kata-kata.

4. Pembersihan dan penyempurnaan:
   Setelah kata-kata tersegmentasi, tahap terakhir adalah pembersihan dan penyempurnaan

Tahapan-tahapan tersebut dapat disesuaikan tergantung pada metode dan algoritma yang digunakan dalam implementasi spesifik. Namun, secara umum, text segmentation bertujuan untuk memisahkan teks dari gambar melalui serangkaian proses pra-pemrosesan, pemisahan teks dari latar belakang, dan pengolahan lebih lanjut untuk mendapatkan hasil teks yang diinginkan.


 implementasi word segmentation untuk mendeteksi huruf-huruf dalam sebuah gambar menggunakan Python dengan menggunakan library scikit-image. Berikut penjelasan dari setiap bagian codingan tersebut:

1. Fungsi `detect_letters(image_path)`:
   - Fungsi ini menerima path file gambar sebagai parameter.
   - Fungsi ini membaca gambar menggunakan scikit-image dan mengubahnya menjadi skala keabuan.
   - Dilakukan thresholding pada gambar untuk mengubahnya menjadi gambar biner, di mana nilai pixel yang lebih rendah dari 0.5 dianggap sebagai foreground (huruf) dan yang lebih tinggi sebagai background.
   - Dilakukan operasi morfologi untuk membersihkan gambar dari noise dan menghubungkan bagian-bagian huruf yang terputus.
   - Menggunakan fungsi `find_contours` untuk menemukan kontur huruf pada gambar biner yang telah dibersihkan.
   - Kontur huruf yang terdeteksi kemudian diambil berdasarkan ukuran area dan aspek rasio. Jika area huruf lebih besar dari 100 piksel dan aspek rasio huruf lebih besar dari 0.2, maka huruf tersebut dianggap terdeteksi.
   - Fungsi ini mengembalikan daftar persegi panjang yang mengelilingi huruf-huruf yang terdeteksi.

2. Inisialisasi path file gambar:
   - Variabel `image_path` berisi path file gambar yang ingin diproses untuk deteksi huruf.

3. Membuka dan menampilkan gambar asli:
   - Menggunakan fungsi `io.imread` dari scikit-image untuk membaca gambar dari path file yang telah ditentukan.
   - Menampilkan gambar asli menggunakan `plt.imshow` dan memberi judul "GAMBAR ASLI".

4. Panggil fungsi `detect_letters` untuk deteksi huruf:
   - Variabel `detected_letters` akan menyimpan persegi panjang yang mengelilingi huruf-huruf yang terdeteksi di gambar.
   - Fungsi `detect_letters` dipanggil dengan menggunakan path file gambar sebagai argumen.

5. Menampilkan gambar setelah deteksi huruf:
   - Menggunakan `plt.subplot` untuk membagi area plot menjadi 1 baris dan 2 kolom.
   - Menampilkan gambar asli di subplot pertama dengan menggunakan `plt.imshow` dan memberi judul "GAMBAR ASLI".
   - Menampilkan gambar setelah deteksi huruf di subplot kedua dengan menggunakan `plt.imshow` dan memberi judul "GAMBAR SETELAH DETEKSI TEXT".
   - Menggunakan `plt.gca().add_patch` untuk menambahkan persegi panjang dengan warna merah yang mengelilingi setiap huruf yang terdeteksi.

6. Menampilkan persegi panjang yang mengelilingi huruf:
   - Menggunakan loop untuk mengiterasi setiap persegi panjang yang terdeteksi dalam `detected_letters`.
   - Membuat objek `plt.Rectangle` dengan koordinat dan ukuran yang sesuai dari persegi panjang yang terdeteksi.
   - Menambahkan objek `rect` ke plot menggunakan `plt.gca().add_patch` untuk menampilkan persegi panjang di atas gambar.

7. Menampilkan gambar:
   - Menggunakan `plt.show()` untuk menampilkan plot yang telah    dibuat.

Dengan menjalankan codingan di atas, Anda akan mendapatkan tampilan gambar asli dan gambar setelah deteksi huruf. Pada gambar setelah deteksi huruf, persegi panjang dengan warna merah akan mengelilingi huruf-huruf yang terdeteksi. Ini memberikan visualisasi yang jelas dan mempermudah dalam memahami hasil deteksi huruf.

Tujuan dari codingan ini adalah untuk menunjukkan implementasi deteksi huruf dalam sebuah gambar menggunakan pendekatan word segmentation. Melalui langkah-langkah yang tertera, gambar awal diproses untuk mengidentifikasi dan memisahkan huruf-huruf yang ada dalam gambar tersebut.

link jurnal https://drive.google.com/drive/folders/1Wg5vcRJ1WmBJw3aQJkR53mGk1cMPuyOT?usp=sharing
