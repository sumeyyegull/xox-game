#include <iostream>
#include <vector>
#include <string>
#include <fstream>
#include <cstdlib>

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



int main(){






return 0;
}
