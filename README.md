# P1_Probstat_C_5025201087

### Daniel Hermawan - 5025201087  

## Soal No 1  
A. Berapa peluang penyurvei bertemu x = 3 orang yang tidak menghadiri acara vaksinasi sebelum keberhasilan pertama ketika p = 0,20 dari populasi menghadiri acara vaksinasi ? (distribusi Geometrik)  
```r
p = 0.20  # Peluang  
n = 3     # Jumlah Sampel  
dgeom(x = n, prob = p)  
```  
  
Output :  
```r
[1] 0.1024  
```  
  
B. Mean Distribusi Geometrik dengan 10000 data random , prob = 0,20 dimana distribusi
geometrik acak tersebut X = 3 ( distribusi geometrik acak () == 3 )  
```r
# Mean dengan 1000 data random, peluang 20%
p = 0.20
mean(rgeom(n = 10000, prob = p) == 3) 
```  
  
Output :  
```r
[1] 0.1035
```  
  
C. Bandingkan Hasil poin a dan b , apa kesimpulan yang bisa didapatkan?  
- Nilai terlihat memiliki perbedaan 0.0011 (Tidak signifikan), perbedaan nilai ditentukan oleh variable distribusi geometrik acak (X).  
  
D. Histogram Distribusi Geometrik , Peluang X = 3 gagal Sebelum Sukses Pertama.  
```r
data.frame(x = 0:10, prob = dgeom(x = 0:10, prob = p)) %>%
  mutate(Failures = ifelse(x == n, n, "other")) %>%
ggplot(aes(x = factor(x), y = prob, fill = Failures)) +
  geom_col() +
  geom_text(
    aes(label = round(prob,2), y = prob + 0.01),
    position = position_dodge(0.9),
    size = 3,
    vjust = 0
  ) +
  labs(title = "Histogram Distribusi Gemoetrik dengan peluang X = 3 akan gagal sebelum yang pertama sukses",
       subtitle = "Geometric(.2)",
       x = "Gagal sebelum sukses pertama (x)",
       y = "Peluang")
```  
  
E. Nilai Rataan (μ) dan Varian (σ²) dari Distribusi Geometrik.  
```r  
rataan = 1/peluang
paste ("Nilai rataan adalah ",rataan)
varian = (1-p) / p^2
paste ("Nilai Varian adalah ",varian)
```  
  
Output :
```r
[1] "Nilai Varian adalah 20"
```  
  
  
## Soal No 2  
Terdapat 20 pasien menderita Covid19 dengan peluang sembuh sebesar 0.2. Tentukan :  
  
A. Peluang terdapat 4 pasien yang sembuh  
```r  
n = 20
p = 0.2
x = 4
peluang = dbinom(x, n, prob = p, log = FALSE)
peluang
```  
  
Output :  
```r
[1] 0.2181994
```  
  
B. Gambarkan grafik histogram berdasarkan kasus tersebut.  
```r
hist(rbinom(x, n, prob = p), xlab = "X", ylab = "Frekuensi", main = "Histogram bilangan binomial")
```  
  
<img width="257" alt="image" src="https://user-images.githubusercontent.com/82170943/162623541-31619baa-0746-4366-9569-3bf7477a529c.png">
  
  
C. Nilai Rataan (μ) dan Varian (σ²) dari DistribusiBinomial.  
```r
rataan = n * (prob = p)
variansi = n * (prob = p) * (1 - (prob = p))
rataan
variansi 
```  
  
Output :  
```r
[1] 4  
[1] 3.2  
```  
  
  
## Soal No 3  
Diketahui data dari sebuah tempat bersalin di rumah sakit tertentu menunjukkan rata-rata historis 4,5 bayi lahir di rumah sakit ini setiap hari. (gunakan Distribusi Poisson)  
  
A. Berapa peluang bahwa 6 bayi akan lahir di rumah sakit ini besok?  
```r
lahir = 6
lahir_avg = 4.5
dpois(lahir, lahir_avg)
```  
  
Output :  
```r
[1] 0.1281201  
```  
  
B. simulasikan dan buatlah histogram kelahiran 6 bayi akan lahir di rumah sakit ini selama setahun (n = 365)  
```r
n = 365
lahir_avg = 4.5
set.seed(2)
baby <- data.frame('data' = rpois(n, lahir_avg))

baby %>% ggplot() +
  geom_histogram(aes(x = data, y = stat(count / sum(count)), fill = data == 6), binwidth = 1, color = 'black',) +
  scale_fill_manual(values = c("#6BCB77", "#FF6B6B")) +
  scale_x_continuous(breaks = 0:10) +
  labs(x = 'Kelahiran per periode', y = 'Proporsi', title = 'Simulasi kelahiran satu tahun (n = 365)') +
  theme_bw()
```  
  
C. dan bandingkan hasil poin a dan b , Apa kesimpulan yang bisa didapatkan  
- A merupakan hasil perhitungan eksak sedangkan poin B melalui proses simulasi, didapatkan hasil keduanya tidak jauh berbeda.  
  
D. Nilai Rataan (μ) dan Varian (σ²) dari Distribusi Poisson  
```r
lahir = 6
l <- lahir
rataan<- l
rataan
variansi <- l
variansi
```  
  
Output :  
```r
[1] 6  
[1] 6  
```  
  
  
## Soal no 4  
Diketahui nilai x = 2 dan v = 10. Tentukan:  
  
A. Fungsi Probabilitas dari Distribusi Chi-Square.  
```r
x = 2
v = 10
dchisq(x, v, ncp = 0, log = FALSE)
```  
  
Output :  
```r
[1] 0.007664155  
```  
  
B. Histogram dari Distribusi Chi-Square dengan 100 data random
```r
n=100
set.seed(1)
hist(rchisq(n,v),
     main="Histogram poison kelahiran bayi",
     col="Hijau",)
```  
  
Output :
```r

```  
  
C.  Nilai Rataan (μ) dan Varian (σ²) dari DistribusiChi-Square.  
```r
rataan = v
rataan
variansi = 2*v
variansi
```  
  
Output :  
```r
[1] 10  
[1] 20  
```  
  
  
## Soal No 5  
Diketahui bilangan acak (random variable) berdistribusi exponential (λ = 3). Tentukan:  
A. Fungsi Probabilitas dari Distribusi Exponensial  
```r
lamda = 3
dexp(x = seq(1, 10, by = 0.1) , rate = lamda)  
```  
  
  Output :  
  ```r
  [1] 1.493612e-01 1.106495e-01 8.197117e-02 6.072573e-02
 [5] 4.498673e-02 3.332699e-02 2.468924e-02 1.829024e-02
 [9] 1.354974e-02 1.003790e-02 7.436257e-03 5.508914e-03
[13] 4.081104e-03 3.023356e-03 2.239757e-03 1.659253e-03
[17] 1.229205e-03 9.106174e-04 6.746020e-04 4.997574e-04
[21] 3.702294e-04 2.742727e-04 2.031862e-04 1.505240e-04
[25] 1.115110e-04 8.260935e-05 6.119851e-05 4.533697e-05
[29] 3.358645e-05 2.488146e-05 1.843264e-05 1.365523e-05
[33] 1.011605e-05 7.494151e-06 5.551804e-06 4.112877e-06
[37] 3.046894e-06 2.257195e-06 1.672171e-06 1.238775e-06
[41] 9.177070e-07 6.798540e-07 5.036483e-07 3.731118e-07
[45] 2.764080e-07 2.047681e-07 1.516959e-07 1.123791e-07
[49] 8.325250e-08 6.167497e-08 4.568994e-08 3.384794e-08
[53] 2.507517e-08 1.857614e-08 1.376155e-08 1.019480e-08
[57] 7.552496e-09 5.595027e-09 4.144898e-09 3.070616e-09
[61] 2.274768e-09 1.685190e-09 1.248419e-09 9.248517e-10
[65] 6.851470e-10 5.075694e-10 3.760166e-10 2.785600e-10
[69] 2.063623e-10 1.528770e-10 1.132540e-10 8.390065e-11
[73] 6.215513e-11 4.604566e-11 3.411146e-11 2.527039e-11
[77] 1.872077e-11 1.386868e-11 1.027417e-11 7.611296e-12
[81] 5.638586e-12 4.177168e-12 3.094522e-12 2.292478e-12
[85] 1.698310e-12 1.258139e-12 9.320521e-13 6.904812e-13
[89] 5.115210e-13 3.789441e-13 2.807287e-13  
```    
  
B. Histogram dari Distribusi Exponensial untuk 10, 100, 1000 dan 10000 bilangan random  
```r
set.seed(1)
hist(rexp(n = 10, rate = lamda))
set.seed(1)
hist(rexp(n = 100, rate = lamda))
set.seed(1)
hist(rexp(n = 1000, rate = lamda))
set.seed(1)
hist(rexp(n = 10000, rate = lamda))
```  
  
Output :  

<img width="327" alt="image" src="https://user-images.githubusercontent.com/82170943/162624191-e52d693d-d6c7-4f7f-a565-5eec78c26c49.png">

  
C. Nilai Rataan (μ) dan Varian (σ²) dari Distribusi Exponensial untuk n = 100 dan λ = 3
  
```r
n = 100
mean(rexp(n = n, rate = lamda))
var(rexp(n = n, rate = lamda))
```  
  
Output :  
```r
[1] 0.3358927  
[1] 0.07642556  
```  
  
  
## Soal No 6  
Diketahui generate random nilai sebanyak 100 data, mean = 50, sd = 8. Tentukan  
  
A. Fungsi Probabilitas dari Distribusi Normal P(X1 ≤ x ≤ X2), hitung Z-Score Nya dan plot data generate randomnya dalam bentuk grafik. Petunjuk(gunakan fungsi plot()).  
```r
norm_dist_i <- rnorm(N,Mean,Std_dev_i)
x1 <- floor(mean(norm_dist_i))
x2 <- ceiling(mean(norm_dist_i))
z_score <- ((norm_dist_i - mean(norm_dist_i))/ (sd(norm_dist_i)))
plot(z_score, type = 'p', col='blue') 
```  
  
B. Generate Histogram dari Distribusi Normal dengan breaks 50 dan format penamaan:  
```r
hist(norm_dist_i,50,main = "5025201087_Daniel Hermawan_Probstat_C_DNhistogram ")  
```  
  
C. Nilai Varian (σ²) dari hasil generate random nilai Distribusi Normal.  
```r
 std_dev_ii <- sd(norm_dist_i)
  variansi <- std_dev_ii * std_dev_ii
  variansi 
```  
  
Output :
```r
[1] 20  
```  
  
  
# Terima Kasih.


