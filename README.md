# xox-game
XOX Game - C++
Bu proje, C++ dili kullanılarak Nesne Yönelimli Programlama (OOP) prensiplerine uygun şekilde geliştirilmiş klasik bir Tic Tac Toe (XOX) oyunudur. Oyuncular sırayla X ve O sembollerini 3x3’lük bir tahtaya yerleştirerek oyunu kazanmaya çalışır. Oyun, İnsan vs İnsan ve İnsan vs Bilgisayar modlarını destekler. Bilgisayar rastgele hamleler yapar.

Kullanılan Teknolojiler
-C++
-Nesne Yönelimli Programlama (OOP)
-Konsol (Terminal) Uygulaması

Proje Özellikleri
-OOP temelli sınıf yapısı
-3x3 oyun tahtası
-Oyuncu adı girişi
-Bilgisayara karşı oynama modu (rastgele hamle yapar)
-Kazanma kontrolü (yatay, dikey, çapraz)
-Beraberlik tespiti
-Geçersiz hamle kontrolü
-Skorların oyuncu_skorları.txt dosyasına kaydedilmesi

Sınıf Yapısı
-OyunNesnesi: Tüm görsel oyun nesneleri için soyut sınıf (draw(), erase() metodları).
-Oyuncu: İnsan oyuncunun adını ve hamlelerini yönetir.
-BilgisayarOyuncu: Rastgele hamle yapan bilgisayar oyuncusu.
-Tahta: Oyun tahtasını ve kuralları yönetir.
-Oyun: Oyun akışını, oyuncu sırasını ve skor işlemlerini kontrol eder.

Oyun Kuralları
-Oyuncular sırayla hamle yapar (X ve O).
-Aynı satır, sütun veya çaprazda 3 sembolü olan oyuncu oyunu kazanır.
-Tüm hücreler dolduğunda kazanan yoksa oyun berabere biter.
-Bilgisayar oyuncusu rastgele hamle yapar.
-Geçersiz girişler reddedilir ve tekrar istenir.

