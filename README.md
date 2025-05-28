# ❌⭕ XOX Game (Tic Tac Toe) - C++ Konsol Uygulaması

Bu proje, **C++** dilinde **Nesne Yönelimli Programlama (OOP)** prensiplerine uygun olarak geliştirilmiş klasik bir **XOX (Tic Tac Toe)** oyunudur. Oyuncular 3x3'lük bir tahtada sırayla hamle yaparak kazanmayı hedefler. Oyun, hem **İnsan vs İnsan** hem de **İnsan vs Bilgisayar** modlarını destekler.

## 🚀 Kullanılan Teknolojiler

- C++
- Nesne Yönelimli Programlama (OOP)
- Konsol uygulaması (Terminal tabanlı)

## 🎮 Oyun Özellikleri

- OOP prensiplerine uygun sınıf yapısı
- 3x3 oyun tahtası
- Oyuncu adı girişi
- Bilgisayara karşı oynama seçeneği (rastgele hamle yapar)
- Yatay, dikey ve çapraz kazanma kontrolü
- Beraberlik durumu tespiti
- Geçersiz hamle kontrolü
- Kazananın adı ve skoru `oyuncu_skorları.txt` dosyasına kaydedilir

## 🧱 Sınıf Yapısı

- `OyunNesnesi` (Soyut Sınıf): Görsel oyun nesneleri buradan türetilir.
- `Oyuncu`: Oyuncu bilgilerini ve hamlelerini yönetir.
- `BilgisayarOyuncu`: Rastgele hamle yapan bilgisayar oyuncusu.
- `Tahta`: Oyun tahtasını ve oyun kurallarını yönetir.
- `Oyun`: Oyun akışını, oyuncu sırasını ve skor kayıtlarını kontrol eder.

## 🎯 Oyun Kuralları

- Oyuncular sırayla hamle yapar (X ve O sembolleri).
- Aynı satır, sütun veya çaprazda üçlü yapan oyuncu kazanır.
- Tüm hücreler dolarsa ve kazanan yoksa oyun berabere biter.
- Bilgisayar, hamlelerini rastgele seçer.
- Geçersiz hamlelerde uyarı verilir ve tekrar istenir.

## 🛠️ Derleme ve Çalıştırma

Aşağıdaki komutları kullanarak projeyi derleyip çalıştırabilirsiniz:

```bash
g++ main.cpp -o xox
./xox
