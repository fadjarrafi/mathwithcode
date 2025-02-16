---
contributors:
  - name: "Fadjar"
    username: "fadjarrafi"
---
# Varians dan Standar Deviasi

Variansi adalah konsep dasar dalam statistika yang mengukur seberapa tersebar suatu kumpulan angka dari nilai rata-rata (mean)-nya. Bayangkan variansi sebagai ukuran jarak "rata-rata" antara titik data dan pusatnya, tetapi dengan sedikit perbedaan menarik - jarak ini dikuadratkan, yang memiliki implikasi matematis yang penting.

Bayangkan kamu sedang mengukur tinggi pohon di dua hutan yang berbeda. Di Hutan A, sebagian besar pohon memiliki tinggi sekitar 30 meter dengan sedikit variasi. Sementara itu, di Hutan B, tinggi pohonnya sangat beragam, mulai dari 10 meter hingga 50 meter. Meskipun rata-rata tinggi pohon di kedua hutan adalah 30 meter, jelas bahwa tingkat variasi tinggi pohon di kedua hutan berbeda. Variansi membantu kita menghitung perbedaan ini.

## Definisi Rumus

Mari kita uraikan rumus variansi secara bertahap:

1. Pertama, cari nilai rata-rata (μ) dari data.
2. Untuk setiap nilai dalam data:
    - Kurangkan dengan rata-rata (untuk mendapatkan jarak dari pusat).
    - Kuadratkan hasilnya (agar semua nilai positif dan menekankan perbedaan yang lebih besar).
3. Hitung rata-rata dari semua selisih yang telah dikuadratkan.

Rumusnya adalah:

$$
\sigma^2 = \frac{\sum (x - \mu)^2}{N}
$$

Di mana:  

| Simbol  | Pengertian |
|---------|------------|
| $\sigma^2$ | Varians |
| $x$ | Setiap nilai dalam kumpulan data |
| $\mu$ | Rata-rata dari kumpulan data, dihitung sebagai $\mu = \frac{\sum x}{N}$ |
| $N$ | Jumlah total nilai dalam kumpulan data |
| $\sum$ | Notasi sigma, berarti "jumlahkan semua yang mengikuti" |



## Implementasi dalam Pemrograman

Berikut adalah implementasi dalam JavaScript untuk menghitung variansi:

```javascript
// Fungsi untuk menghitung rata-rata dari sebuah array
const calculateMean = (numbers) => {
    return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
};

// Fungsi utama untuk menghitung variansi
const calculateVariance = (numbers) => {
    const mean = calculateMean(numbers);
    const squaredDifferences = numbers.map(num => Math.pow(num - mean, 2));
    return calculateMean(squaredDifferences);
};

// Fungsi untuk menghitung standar deviasi
const calculateStandardDeviation = (numbers) => {
    return Math.sqrt(calculateVariance(numbers));
};

// Contoh penggunaan
const exploreVariance = (datasetName, numbers) => {
    console.log(`\nAnalisis ${datasetName}:`);
    console.log(`Data: [${numbers.join(', ')}]`);
    console.log(`Mean: ${calculateMean(numbers).toFixed(2)}`);
    console.log(`Variansi: ${calculateVariance(numbers).toFixed(2)}`);
    console.log(`Standar Deviasi: ${calculateStandardDeviation(numbers).toFixed(2)}`);
};

// Contoh kumpulan data dengan variansi berbeda
const hutanA = [28, 29, 30, 31, 32];
const hutanB = [10, 20, 30, 40, 50];

exploreVariance('Hutan A (Tinggi Seragam)', hutanA);
exploreVariance('Hutan B (Tinggi Bervariasi)', hutanB);
// Ouput akan memunculkan kalau Hutan B memiliki nilai varians lebih besar dari Hutan A
```

## Mengapa Harus Dikuadratkan?

Mengkuadratkan selisih memiliki beberapa manfaat penting:

1. **Mengatasi Nilai Negatif**: Selisih bisa bernilai negatif atau positif, tetapi dengan mengkuadratkannya, semua nilai menjadi positif.
2. **Menekankan Outlier**: Nilai yang jauh dari rata-rata akan menghasilkan selisih yang lebih besar setelah dikuadratkan, sehingga variansi lebih sensitif terhadap outlier.
3. **Manfaat Matematis**: Kuadrat menciptakan fungsi yang lebih halus dan dapat diturunkan, yang bermanfaat dalam berbagai optimasi.

## Interpretasi Varians dan Standar Deviasi dalam Statistik

Varians dan standar deviasi tidak hanya angka matematis, tetapi juga memiliki makna penting dalam memahami distribusi data. Berikut adalah beberapa cara menginterpretasikan kedua metrik ini dalam analisis statistik:

1. **Varians dan Standar Deviasi Kecil**
    
    - Jika varians dan standar deviasi suatu dataset kecil, ini berarti nilai-nilai data cenderung berkumpul di sekitar rata-rata.
    - Contoh: Dalam produksi suku cadang mobil, standar deviasi kecil menunjukkan bahwa ukuran suku cadang yang dihasilkan sangat konsisten.
2. **Varians dan Standar Deviasi Besar**
    
    - Jika varians dan standar deviasi besar, ini berarti data tersebar jauh dari rata-rata, menunjukkan adanya variabilitas tinggi.
    - Contoh: Dalam investasi saham, standar deviasi besar menunjukkan volatilitas tinggi, yang berarti harga saham dapat berfluktuasi secara signifikan.
3. **Perbandingan antara Dataset**
    
    - Dua dataset dapat memiliki **rata-rata yang sama tetapi varians berbeda**, yang mengindikasikan tingkat penyebaran data yang berbeda.
    - Contoh: Jika dua sekolah memiliki rata-rata nilai ujian yang sama, tetapi satu sekolah memiliki standar deviasi lebih tinggi, maka siswa di sekolah tersebut memiliki perbedaan nilai yang lebih ekstrem dibandingkan sekolah lainnya.
4. **Kaitan dengan Distribusi Normal**
    
    - Dalam distribusi normal, **sekitar 68% data berada dalam satu standar deviasi dari rata-rata**, **95% dalam dua standar deviasi**, dan **99.7% dalam tiga standar deviasi**.
    - Ini sangat berguna dalam analisis data untuk menentukan apakah suatu data adalah outlier atau tidak.

## Jenis-jenis Varians

Ada dua jenis utama varians dalam statistik, tergantung pada apakah kita menganalisis seluruh populasi atau hanya sampel dari populasi tersebut:

1. **Varians Populasi (Population Variance, σ²)**
    
    - Digunakan ketika kita memiliki **seluruh data dalam populasi**.
    - Rumus: $s^2 = \frac{\sum (x - \bar{x})^2}{n - 1}$  
    - Contoh: Jika kita memiliki data berat badan **seluruh** penduduk suatu kota, kita menggunakan varians populasi.
2. **Varians Sampel (Sample Variance, s²)**
    
    - Digunakan ketika kita hanya memiliki **sebagian data dari populasi** (sampel).
    - Rumus: $s2=∑(x−xˉ)2n−1s^2 = \frac{\sum (x - \bar{x})^2}{n - 1}$
    - Perbedaan utama dari varians populasi adalah **menggunakan pembagian dengan (n - 1) daripada N**. Ini disebut **derajat kebebasan (degrees of freedom)** dan digunakan untuk menghindari bias dalam estimasi varians populasi.
    - Contoh: Jika kita hanya memiliki data berat badan dari **100 orang** di kota (bukan seluruh populasi), kita menggunakan varians sampel.

## Kapan Menggunakan Varians Populasi vs. Sampel?

- Gunakan **varians populasi** jika Anda memiliki **seluruh data** dari populasi yang ingin dianalisis.
- Gunakan **varians sampel** jika Anda hanya memiliki **sebagian data**, dan ingin mengestimasi varians untuk seluruh populasi.

## Hubungan dengan Standar Deviasi

Standar deviasi (σ) adalah akar kuadrat dari variansi. Meskipun variansi berguna dalam perhitungan matematis, standar deviasi lebih intuitif karena memiliki satuan yang sama dengan data aslinya.