
import matplotlib.pyplot as plt
from skimage import io, color, measure
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

# Tampilkan gambar dengan persegi panjang yang mengelilingi huruf yang terdeteksi
plt.subplot(1, 2, 2)
plt.imshow(image)
plt.axis('off')
plt.title('GAMBAR SETELAH DITEKSI TEXT')

# Tampilkan persegi panjang yang mengelilingi huruf yang terdeteksi
for (x, y, width, height) in detected_letters:
    rect = plt.Rectangle((y, x), height, width, edgecolor='g', linewidth=2, fill=False)
    plt.gca().add_patch(rect)

# Tampilkan gambar yang telah dideteksi hurufnya
# MUHAMMADGAMAL-202131035
plt.show()

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
