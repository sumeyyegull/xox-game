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

class Tahta : public OyunNesnesi {  // Oyun tahtası sınıfı
private:
    char tahta[SIZE][SIZE];  // 3x3'lük karakter dizisi (tahta)

public:
    Tahta() {  // Yapıcı fonksiyon, tahtayı boşluklarla başlatır
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                tahta[i][j] = ' ';
            }
        }
    }

    char getAlan(int satir, int sutun) { return tahta[satir][sutun]; }  // Belirli bir alandaki sembolü alma

    void setAlan(int satir, int sutun, char sembol) { tahta[satir][sutun] = sembol; }  // Alanı sembol ile güncelleme

    void display() const override {  // Tahtayı ekrana basma
        cout << "-------------" << endl;
        for (int i = 0; i < SIZE; i++) {
            cout << "| ";
            for (int j = 0; j < SIZE; j++) {
                cout << tahta[i][j] << " | ";
            }
            cout << endl;
        }
        cout << "-------------" << endl;
    }

    bool hamleYap(int satir, int sutun, char sembol) {  // Hamleyi tahtada yapma (geçerli bir hamle olup olmadığını kontrol eder)
        if (satir < 0 || satir >= SIZE || sutun < 0 || sutun >= SIZE || tahta[satir][sutun] != ' ') {
            return false;  // Geçersiz hamle
        }
        setAlan(satir, sutun, sembol);  // Hamleyi tahtada uygula
        return true;
    }

    bool alanDoluMu() {  // Tahtadaki tüm alanlar dolu mu kontrolü
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                if (tahta[i][j] == ' ')  // Boş alan varsa
                    return false;
            }
        }
        return true;  // Tüm alanlar dolu
    }

    char kazananiBelirle() {  // Kazananı belirleme (3'lü aynı sembol yatay, dikey ya da çapraz)
        for (int i = 0; i < SIZE; i++) {
            if (tahta[i][0] == tahta[i][1] && tahta[i][1] == tahta[i][2] && tahta[i][0] != ' ')
                return tahta[i][0];  // Yatay kazanan
            if (tahta[0][i] == tahta[1][i] && tahta[1][i] == tahta[2][i] && tahta[0][i] != ' ')
                return tahta[0][i];  // Dikey kazanan
        }
        if ((tahta[0][0] == tahta[1][1] && tahta[1][1] == tahta[2][2] && tahta[0][0] != ' '))
            return tahta[0][0];  // Çapraz kazanan
        if ((tahta[0][2] == tahta[1][1] && tahta[1][1] == tahta[2][0] && tahta[0][2] != ' '))
            return tahta[0][2];  // Diğer çapraz kazanan
        return ' ';  // Kazanan yok
    }
};
class Oyun {  // Oyun sınıfı
private:
    Tahta tahta;  // Tahta nesnesi
    Oyuncu* oyuncu1;  // 1. oyuncu
    Oyuncu* oyuncu2;  // 2. oyuncu
    Oyuncu* aktifOyuncu;  // Şu anki aktif oyuncu
public:
    Oyun(Oyuncu* o1, Oyuncu* o2) : oyuncu1(o1), oyuncu2(o2), aktifOyuncu(o1) {}  // Yapıcı

    void oynaOyun() {  // Oyunu oynama fonksiyonu
        int satir, sutun;
        char sembol;

        while (true) {  // Oyun devam ederken
            sembol = (aktifOyuncu == oyuncu1) ? 'X' : 'O';  // Aktif oyuncuya göre sembol belirleme

            aktifOyuncu->hamleYap(satir, sutun);  // Hamle yapma

            if (tahta.hamleYap(satir, sutun, sembol)) {  // Geçerli hamle ise
                tahta.display();  // Tahtayı görüntüle

                if (tahta.kazananiBelirle() == sembol) {  // Kazanan belirlendiyse
                    cout << aktifOyuncu->getAd() << " kazandi!" << endl;
                    aktifOyuncu->arttirSkor();  // Skor artır
                    aktifOyuncu->kaydetVeriTabani();  // Skoru kaydet
                    break;  // Oyunu bitir
                } else if (tahta.alanDoluMu()) {  // Tahta dolmuşsa
                    cout << "Beraberlik!" << endl;
                    break;  // Beraberlik
                }

                aktifOyuncu = (aktifOyuncu == oyuncu1) ? oyuncu2 : oyuncu1;  // Sıradaki oyuncuya geç
            } else {
                cout << "Gecersiz hamle, tekrar deneyin." << endl;  // Geçersiz hamle uyarısı
            }
        }
    }
};

int main(){






return 0;
}
