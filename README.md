# SubdomainTakeover
Subdomain Takeover için gerekli araçkların kurulumu ve kullanımı.

Go Kurulum (Kali Linux)

Ubuntu’da en son güvenlik güncellemelerini uygulamak için yükseltme kodu;

sudo apt-get update
sudo apt-get -y upgrade

Go ikili dosyasını indirmeniz gerekir. İşletim sistemlerine ve mimariye göre indirme bağlantılarının listesini resmi paketlerinden bulabilirsiniz. Ubuntu 64-bit işletim sistemine kurmak için aşağıdaki komutlara basın:

cd /tmp
wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz

Şimdi, indirilen arşivi çıkartın ve sistemde istediğiniz yere kurun. Genellikle, standartların önerdiği şekilde /usr/local dizini altında tutulur.

komutumuz;

sudo tar -xvf go1.11.linux-amd64.tar.gz

sudo mv go /usr/local


Go Ortamını Ayarlama

Şimdi, Go dil ortamı değişkenlerini ayarlayalım. GOROOT , GOPATH ve PATH.

GOPATH : Go çalışma dizininizin konumu işaret eder.
GOROOT : Go paketinin sisteminize kurulu olduğu konumdur.

.profile dosyanızı açın ve dosyanın sonuna bir genel değişken ekleyin. Bunu, kabuk yapılandırmanıza göre bir .zshrc veya .bashrc dosyasına eklemek isteyebilirsiniz.

export GOROOT=/usr/local
export GOPATH=/home/kamilkaplan/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH


Mevcut kabuk Oturumunu Güncelle

$ source ~/.profile

Bu, terminalinizi yeniden başlatmadan go komutlarını kullanmanıza izin verecektir.


Kurulumu Doğrulama

Go dilini sisteminize başarıyla yüklediniz ve yapılandırdınız. Go versiyonunu kontrol etmek için:

$ go version// go version go1.10.3 gccgo (Ubuntu 8.3.0-6ubuntu1~18.04.1) 8.3.0 linux/amd64

Şimdi, aşağıdaki komutu kullanarak yapılandırılmış tüm ortam değişkenlerini de doğrulayın:

go envGOARCH=”amd64"
GOBIN=””
GOCACHE=”/home/kali/.cache/go-build”
GOEXE=””
GOHOSTARCH=”amd64"
GOHOSTOS=”linux”
GOOS=”linux”
GOPATH=”/home/kali/go”
GORACE=””
GOROOT=”/usr”
GOTMPDIR=””
GOTOOLDIR=”/usr/lib/gcc/x86_64-linux-gnu/8"
GCCGO=”/usr/bin/x86_64-linux-gnu-gccgo-8"
CC=”x86_64-linux-gnu-gcc-8"
CXX=”x86_64-linux-gnu-g++-8"
CGO_ENABLED=”1"
CGO_CFLAGS=”-g -O2"
CGO_CPPFLAGS=””
CGO_CXXFLAGS=”-g -O2"
CGO_FFLAGS=”-g -O2"
CGO_LDFLAGS=”-g -O2"
PKG_CONFIG=”pkg-config”
GOGCCFLAGS=”-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build059483897=/tmp/go-build -gno-record-gcc-switches -funwind-tables”

Go 1.10.3’ü başarıyla yükledik.


Gerekli Toolların Kurulumu ve Kullanımı

1-) Assetfiner
2-) Subzy
3-) Subjack

ASSETFINDER

+ Hedef domainin subdomainlerini çekmemize ve liste halinde txt'ye kaydetmemize yarar.

Github reposu

https://github.com/tomnomnom/assetfinder

Kurulum

go get -u github.com/tomnomnom/assetfinder

Örnek Kullanım

assetfinder hedefdomain.com (hedef domainin subdomainlerini çıkarır.)
assetfinder hedefdomain.com | tee subdomainlist.txt (hedef domainin subdomainlerini çıkarır ve belirttiğimiz şekilde kaydeder.)

SUBZY 

+ Belirttiğimiz subdomain listesinde tarama yapar zafiyetli subdomainleri bildirir.

Github reposu 

https://github.com/LukaSikic/subzy

Kurulum

go get -u -v github.com/lukasikic/subzy
go install -v github.com/lukasikic/subzy@latest

Örnek kullanım

subzy --targets subdomainlist.txt (belirttiğimiz listedeki subdomainleri tarar)
subzy --targets subdomainlist.txt --hide_fails (belirttiğimiz listedeki subdomainleri tarar ve zafiyetli olmayanları ekrana vermez sadece zafiyetli olanları çıkartır.)

SUBJACK

+ Belirttiğimiz subdomain listesinde tarama yapar zafiyetli subdomainleri bildirir.

Github reposu

https://github.com/haccer/subjack

Kurulum

go get github.com/haccer/subjack

Kullanım

subjack -w subdomainlist.txt -v -ssl (belirttiğimiz subdomain listesinde daha doğru, ayrıntılı bir şekilde tarama yapmamızı sağlar)
