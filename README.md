
# Word Segementation

Segmentasi pada citra adalah proses membagi citra menjadi beberapa segmen atau wilayah yang saling terpisah. Tujuan dari segmentasi citra adalah untuk mengidentifikasi dan memisahkan objek atau bagian yang penting dalam citra. Dengan melakukan segmentasi, kita dapat mengisolasi objek, mengenali kontur atau bentuk, menghitung fitur-fitur seperti warna atau tekstur, dan menerapkan analisis atau pengolahan lebih lanjut pada setiap segmen secara terpisah.

Segmentasi citra dapat dilakukan dengan berbagai metode, termasuk:

- Metode berbasis intensitas: Metode ini memanfaatkan informasi intensitas piksel dalam citra untuk memisahkan objek. Contoh metode ini adalah metode ambang (thresholding), pemrosesan histogram, dan pemisahan berdasarkan algoritma deteksi tepi (edge detection).

- Metode berbasis wilayah: Metode ini memisahkan citra berdasarkan kesamaan atribut antara piksel-piksel yang berdekatan. Pada metode ini, piksel-piksel yang memiliki atribut yang serupa (misalnya, warna atau tekstur) dikelompokkan menjadi wilayah-wilayah yang homogen.

- Metode berbasis kontur: Metode ini mencari garis-garis kontur yang memisahkan objek dalam citra. Kontur bisa didapatkan dengan menggunakan teknik-teknik seperti deteksi tepi, transformasi Hough, atau algoritma berbasis kurva.

- Metode berbasis pengelompokan (clustering): Metode ini mengelompokkan piksel-piksel dalam citra menjadi beberapa kelompok berdasarkan kesamaan atribut. Contoh metode ini adalah K-means clustering atau algoritma pengelompokan berbasis kepadatan seperti Mean Shift.

- Pemilihan metode segmentasi yang tepat tergantung pada karakteristik citra dan tujuan aplikasi yang diinginkan. Segmentasi citra merupakan tahap awal yang penting dalam banyak aplikasi pengolahan citra, seperti pengenalan pola, deteksi objek, analisis medis, dan pengolahan gambar digital secara umum.




## Codingan

berikut adalah library yang digunakan pada project yang saya gunakan pada bahasa python

```bash
import cv2 as cv
import numpy as np
import matplotlib.pyplot as plt
```

Dengan menggunakan kodingan di atas, kita dapat menggunakan fungsi dan fitur dari library-library tersebut untuk melakukan berbagai operasi pada citra, seperti membaca citra, melakukan segmentasi, menerapkan filter, dan menampilkan hasilnya dalam bentuk grafik atau gambar. Namun, dalam kodingan yang Anda berikan, tidak ada contoh penggunaan fungsi-fungsi tersebut.

Dibawah digunakan untuk menginport

```bash
gambar = cv.imread('azminih.jpg')
tinggi, lebar, _ = gambar.shape

if lebar > 1000:
    rasio_skala = lebar / 1000
    lebar = 1000
    tinggi = int(tinggi / rasio_skala)

gambar = cv.resize(gambar, (lebar, tinggi))
plt.imshow(gambar)
```

Dilanjutkan dengan Convert to Binary

```bash
def thresholding(img):
    img_gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
    ret, thresh = cv.threshold(img_gray, 80, 255, cv.THRESH_BINARY_INV)
    plt.imshow(thresh, cmap='gray')
    return thresh

thresh_img = thresholding(gambar)

kernel = np.ones((3,85), np.uint8)
dilated = cv.dilate(thresh_img, kernel, iterations = 1)
plt.imshow(dilated, cmap = 'gray')
```
Fungsi thresholding yang diberikan menerima citra img sebagai argumen dan melakukan proses thresholding pada citra tersebut

Setelah itu kita mencari kontur pada gambar

```bash
(contours, hirarki) = cv.findContours(dilated.copy(), cv.RETR_EXTERNAL, cv.CHAIN_APPROX_NONE)
sorted_contours_line = sorted(contours, key = lambda ctr : cv.boundingRect(ctr)[1])

gambar2 = gambar.copy()

for ctr in sorted_contours_line:
    
    x,y,w,h = cv.boundingRect(ctr)
    cv.rectangle(gambar2, (x,y), (x+w, y+h), (4, 100, 250), 2)
    
plt.imshow(gambar2)

kernel = np.ones((3,5), np.uint8)
dilated2 = cv.dilate(thresh_img, kernel, iterations = 1)
plt.imshow(dilated, cmap = 'gray')
```
Fungsi thresholding yang diberikan menerima citra img sebagai argumen dan melakukan proses thresholding pada citra tersebut.

Berikut adalah Segmentasi Kata nya

```bash
gambar3 = gambar.copy()

for line in sorted_contours_line:
    x, y, w, h = cv.boundingRect(line)
    roi_line = dilated2[y:y+h, x:x+w]
    
    (cnt, _) = cv.findContours(roi_line.copy(), cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE)
    sorted_contours_word = sorted(cnt, key=lambda ctr2: cv.boundingRect(ctr2)[0])
    
    for word in sorted_contours_word:
        x2, y2, w2, h2 = cv.boundingRect(word)
        
        # Memotong gambar huruf dari gambar asli
        huruf = roi_line[y2:y2+h2, x2:x2+w2]
        
        # Menggambar persegi panjang pada gambar asli
        cv.rectangle(gambar3, (x+x2, y+y2), (x+x2+w2, y+y2+h2), (255, 255, 100), 2)
        
plt.imshow(gambar3)

```



## Social Media
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/azmiazis/)

[![instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/crophx/)

[![twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://www.twitter.com/kubukandilanmu)

