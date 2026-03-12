# HyperLogLog Cardinality Estimation

## 📌 Proje Özeti
Bu proje, **HyperLogLog (HLL)** algoritmasının C++ dili ile sıfırdan implementasyonunu içerir.  
Amaç, büyük veri analitiğinde **Cardinality Estimation (küme büyüklüğü tahmini)** problemini çözmek ve teorik hata sınırlarını analiz etmektir.

---

## 🔑 Algoritma Bileşenleri
- **Hash Fonksiyonu**: MurmurHash64 kullanıldı. Yüksek kaliteli, uniform dağılım sağlar.  
- **Bucketing Mekanizması**: Hash çıktısının ilk `p` biti ile kova seçimi yapılır.  
- **Register Yapısı**: Kovada ardışık sıfır sayısı (leading zeros) takip edilir.  
- **Tahmin Hesabı**: Harmonik ortalama formülü kullanıldı.  
- **Düzeltmeler**:  
  - Küçük cardinality → Linear Counting  
  - Büyük cardinality → Logaritmik düzeltme  
- **Birleştirilebilirlik**: İki HLL yapısı register bazında maksimum alınarak birleştirilebilir.

---

## 📊 Teorik Analiz
Tahmin hatası yaklaşık olarak:
\[
\text{Std Error} \approx \frac{1.04}{\sqrt{m}}
\]
- \( m = 1024 \) için hata ≈ %3.2  
- Kova sayısı arttıkça hata oranı azalır.

---

## ⚙️ Kullanım
### Derleme
```bash
g++ -std=c++11 main.cpp -o hll
./hll
