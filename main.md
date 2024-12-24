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



int main(){






return 0;
}
