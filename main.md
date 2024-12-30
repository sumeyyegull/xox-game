#include <iostream>
#include <vector>
#include <string>
#include <fstream>
#include <cstdlib>
#include <limits>
#include <ctime> // Rastgele sayı üretimi için

using namespace std;
#define SIZE 3 // Tahtanın boyutu (3x3)

class OyunNesnesi {  // Oyun nesnesi olarak temel sınıf oluşturduk
public:
    virtual void display() const = 0;  // Tahtayı ekrana basma işlevi. Oyun nesneleri tahtada nasıl görünecekse bu fonksiyon ile ekrana basılacaktır.
    virtual ~OyunNesnesi() = default;  // Sanal yıkıcı (virtual), temizleme için. Bu yıkıcı, polymorfizm kullanırken doğru kaynak yönetimini sağlamak için gereklidir.
    /*Sanal yıkıcı, sınıfın alt sınıflarından türetilmiş nesneler silindiğinde,
     doğru şekilde temizlenmesini sağlar. Default derleyicinin
     yıkıcıyı otomatik olarak oluşturmasını sağlar.*/
};
class Oyuncu {  // Oyuncu sınıfı temel sınıf
protected:  //public de olur ama private olamaz turetilmiş sınıfımızdan cekemeyiz cunku
    string ad;  // Oyuncunun adı
    int skor;  // Oyuncunun skoru

public:
    Oyuncu(string oyuncuAd) : ad(oyuncuAd), skor(0) {}  // Yapıcı fonksiyon (başlangıçta skor 0)

    virtual void setAd(string oyuncuAd) { ad = oyuncuAd; }  // Oyuncunun adını ayarlama
    virtual string getAd() { return ad; }  // Oyuncunun adını alma

    virtual void setSkor(int yeniSkor) { skor = yeniSkor; }  // Skoru ayarlama
    virtual int getSkor() { return skor; }  // Skoru alma

    virtual void arttirSkor() { skor += 1; }  // Skoru artırma (her kazançta)

virtual void hamleYap(int& satir, int& sutun) {  // Oyuncunun hamlesini alma
        cout << ad << ", Satir ve Sutun girin (0, 1, 2): ";
        while (!(cin >> satir >> sutun)) {  // Geçerli sayılar girilene kadar devam et
            cout << "Lütfen iki tam sayı girin: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }

    virtual void kaydetVeriTabani() {  // Oyuncu skorunu bir dosyaya kaydetme
        ofstream dosya("oyuncu_skorları.txt", ios::app);  // Dosyaya ekleme modunda aç
        if (dosya.is_open()) {
            dosya << ad << "- Skor: " << skor << endl;
            dosya.close();  // Dosyayı kapat
        } else {
            cout << "Dosya acilamadi!" << endl;  // Dosya açılamazsa hata mesajı
        }
    }

    virtual ~Oyuncu() = default;  // Sanal yıkıcı (temizleme işlemi için)
};
class BilgisayarOyuncu : public Oyuncu {  // Bilgisayar oyuncusu sınıfı (Oyuncu sınıfından türetilmiş)
public:
    BilgisayarOyuncu(string oyuncuAd) : Oyuncu(oyuncuAd) {}  // Yapıcı

    void hamleYap(int& satir, int& sutun) override {  // Bilgisayarın hamlesini yapma (rastgele)
        satir = rand() % SIZE;
        sutun = rand() % SIZE;
        cout << ad << " hamle yapti: (" << satir << ", " << sutun << ")" << endl;
    }
};

int main(){






return 0;
}
