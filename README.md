# Docker-HelloWorld-With-PHP
# Docker Hakkında Araştırmalarım Doğrultusunda Almış Olduğum Notlar

- 1.0-Container Nedir?  
      - 1.1-Container Mimarisi Nasıl Çalışır?
- 2.0-Docker Nedir?
     - 2.1-Docker Mimarisi Nasıl Çalışır?
     - 2.2-Docker İle İlgili Temel Kavramlar
               <br> * 2.2.0-İmage Nedir?
               <br> * 2.2.1-Dockerfile Nedir?
               <br> * 2.2.2-Docker Network Nedir?
               <br> * 2.2.3-Docker Compose Nedir?
- 3.0-Docker Komutlarından Bazıları ve İşlevleri
- 4.0-Nginx Nedir?
- 5.0-Docker ve Php Temel Kod Örnekleri
- 6.0-Karşılaştığım Hatalar ve Çözüm Önerileri
        <br> * 6.1-Windows 10 Home Docker Kurulumu
        <br> * 6.2-Yazım Hataları Kaynaklı Hatalar
        <br> * 6.3-Projeyi Ayağa Kaldırırken Kullanılan Komut Dolayısıyla Yanlış Yükleme






# 1.0-Container Nedir?
- Container (konteyner) denince aklımıza ilk olarak gemilerde taşımacılığı yapılan her biri birbirinden bağımsız ve aynı boyutlarda olan yani belirli standartlara sahip bulundukları yerden başka bir tarafa rahat bir şekilde taşınabilen kapalı kutular gelir. Üzerinde konuştuğumuz teknoloji bu temel taşımacılık kavramı ele alınarak oluşturulmuştur.
- Container kısa ve net tanımıyla, bir uygulamanın ihtiyaç duyulan tüm bağımlılıklar, kütüphaneler ve diğer tüm nesneler ile birlikte paketlenerek standart hale getirilmesidir.
- Oluşturulan bu kutular bir işletim sisteminden diğerine , bir bilgisayardan başka bir bilgisayara kolaylıkla ve güvenli bir şekilde taşınabilmektedir.Taşıma işleminde uygulama ile birlikte uygulamanın yaşamsal döngüsü için gerekli olan bütün nesneler aktarıldığı için uygulama herhangi bir problem olmadan çalışmaya devam edecektir.


## 1.1-Container Mimarisi Nasıl Çalışır?
- Container mimarisinde en alt katmandan en üst katmana şu şekilde sıralanabilir;
            <br>     - İşletim sistemi 
            <br>   - Container Engine ( Konteyner yöneticisi) (Docker vb.)
            <br>   - Container Engine üzerinde birbirinden bağımsız olarak çalışan konteynerler


- Her konteyner birbirinden bağımsız ve habersiz bir şekilde çalışmaktadır biz bu konteynerleri oluşturmak, yönetmek veya çalıştırmak istersek orta katmanda bulunan container engine araçlarından birini kullanmak zorundayız. 


# 2.0-Docker Nedir?
- Docker kısa ve net bir şekilde tanımlanması gerekirse, container teknolojisi kullanılarak uygulama geliştirmeyi ve çalıştırmayı kolaylaştıran açık kaynak kodlu bir platformdur.
- İşletim sisteminden bağımsız olarak uygulamalarımızı derlememize , test etmemize ve dağıtmamıza imkan sağlayan bir yazılım çözümüdür. 
- Docker uygulamamız için gerekli olan tüm dosyaları (kütüphaneler,bağımlılıklar vb) paketleyip bir container haline getirmektedir.Her container alt katmandaki işletim sistemine göre servisleri paylaştırmaktadır.


## 2.1-Docker Mimarisi Nasıl Çalışır?
- Docker aşağıda adı geçen bölümlerden oluşmaktadır.
      <br> - Docker Host
      <br> - Docker Client
      <br> - Registry
      <br> - Docker Object (İmage,Volume,Container ,Plugin)


- Docker istemci-sunucu (client-host) mimarisine dayanmaktadır.
       <br>  -Docker Client: Hizmet alan taraf (komut satırı , arayüz vb.)
       <br>  -Docker Host: Client tarafından gelen isteklerin dinlendiği, container işlemlerinin yapılıp takip edildiği Docker Engine ‘in yürütüldüğü taraftır.


!! Docker Host üzerinde Docker daemon çalışmaktadır ve tüm docker işlemlerini Docker daemon servisi geliştirmektedir.


- Docker Registry:Bir kayıt defteridir. Docker üzerinde çalıştırılacak imagelar burada saklanır.
(hub.docker.com)
- Docker Objects: Docker kullanımı esnasında oluşturulan ve işlem yapılan nesnelerdir.


- Çalışma Sistemi: Docker Client komut satırı veya arayüz üzerinden gelen istekleri docker API üzerinden docker host’a yani docker daemon’a iletir.Örneğin bir image dosyası eklenirken (ör:nginx) komut satırına girilen komut öncelikle docker daemon’a iletilir.Docker daemon image dosyasının daha önce indirilip indirilmediğini kontrol eder.İmage dosyası sistemde bulunmaz ise daemon registry (hub.docker.com) adresinde image dosyasını sorgulatır ve bu adreste ilgili image dosyası bulunursa host üzerine indirilir..   




(Ek bilgi-Benzer Bilgi)
Docker Engine Nedir?
        Docker Engine server client mimarisinde bir uygulamadır. 3 temel katmanı vardır.
               <br>  -Docker Daemon:İmage ,Container , Volume gibi docker objelerini yaratmamıza ve kontrol etmemize olanak sağlar. 
               <br>  -Docker Rest API:Daemon ile iletişim kurmamızı sağlayan yapı
               <br>  -Docker CLI: docker komut satırı ile rest apı kullanarak daemon ile iletişim kurmamızı sağlar.


# 2.2-Temel Kavramalar
## 2.2.0-Docker İmage Nedir?
- Birden çok katmandan oluşan ve docker container da işlem yapmak için oluşturulmuş dosyalardır.
- Konteynerlerin çalışması için gerekli önceden tanımlanmış kalıplar da diyebiliriz.
- Dockerfile kullanarak oluşturulurlar.
## 2.2.1-Dockerfile Nedir?
- İmage dosyası oluşturulurken var olan katmanların ve tüm işlemlerin detaylıca belirtildiği ve açıklandığı text dosyalarıdır.        
- Bunu hazır kurulu gelmeyen bir eşyayı kurarken kullandığımız, nasıl kurulum yapacağımızı adım adım anlatan bir kurulum kılavuzuna benzetebiliriz.
- .yaml veya .yml uzantılı dosyalar ile oluşturulur.
- Varsayılan olarak Dockerfile şeklinde oluşturulur.


Dockerfile Komutlarından Bazıları
- FROM → image dosyasını ifade eder.
- RUN →Çalıştırılacak komutları ifade eder örneğin (RUN apt-get update)
- COPY →İmage’ kopyalanmasını istediğimiz dosyaları ifade eder.
- WORKDIR→Çalışma dizinini ifade eder
- VOLUME→İmage a geçirilecek dosyaları ifade eder.




## 2.2.2 Docker Network Nedir? 
- Docker evreninde container sistemlerinin birbirleri ve dış dünya ile konuşmalarını ,dış dünyadan container’ lara erişimi yani tüm iletişim alt yapılarını docker network objelerini kullanarak sağlıyoruz. 
- Varsayılan docker network objesi Bridge network’üdür. Eğer yeni bir container network oluşturmak istersek ve sürücü belirtmez isek otomatik olarak Bridge Driver kullanılacaktır.


## 2.2.3 Docker Compose Nedir?
- Çoklu docker uygulamalarını tanımlamak ve çalıştırmak için bir araçtır.
- Bir diğer tabirle sistemimizde çalıştırdığımız container, network ve volume konfigürasyonlarını tek bir text dosyası ile yönetmenize olanak sağlayan bir araçtır.
- .yaml veya .yml uzantılı dosyalar ile oluşturulur. varsayılan şekli docker-compose.yml ‘dir.
- Komut satırında docker compose veya docker-compose kullanarak


# 3.0-Docker Komutlarından Bazıları ve İşlevleri


- Docker kurulumunu yaptıktan sonra kontrol amacıyla (CMD,Powershell) üzerine ;
```
docker version 
```
komutu yazılarak docker sürümü kontrol edilebilir.


- Sistemde yer alan image container, çalışan container sayısı ile ilgili bilgileri öğrenmek istiyorsak
```
docker info
```
komutu çalıştırılır.


- İmage dosyalarını aramak için search komutu kullanılabilir.
```
docker search image-adı 
```
şeklinde kullanılır.


- İmage dosyası indirmek için 
```
docker pull image-adı
```

- İmageları listelemek için images komutu kullanılır.
```
docker images
```

- İmage silmek için rmi komutu
```
docker rmi image-adı
```

- İmage çalıştırmak için 
```
docker run image-adı
```
- Docker komutları çalıştırılırken arka planda çalışmasını istiyorsak sonuna -d koymamız gerekir.
```
docker-compose up -d
```
böylelikle yeni bir komut girmek için önceki komutu durdurmamız gerekmez.


- Bir container'ı başlatmak ve durdurmak için
```
docker start container-id        →Başlatmak için
docker stop container-id        →Durdurmak için
docker kill container-id          →Zorla Durdurmak için
```

- Bir container silmek için
```
docker rm container-id
```

# 4.0 Nginx Nedir?
- Nginx yaygın olarak kullanılan açık kaynak bir web sunucusudur. Apache’nin bir alternatifi olarak düşünebiliriz.


# 5.0-Docker ve Php Temel Kod Örnekleri

- [Ngix kullanarak php ile hello-world yazdırma](https://github.com/hamdihacihaliloglu/Docker101-With-PHP/tree/main/ngix-helloworld-docker-php)
- [Php Apache kullanarak hello-world yazıdırma](https://github.com/hamdihacihaliloglu/Docker101-With-PHP/tree/main/php-helloworld-docker)



# 6.0-Karşılaştığım Hatalar ve Çözüm Önerileri
## 6.1-Windows 10 Home Docker Kurulumu
- Docker Desktop kurulumunu yapıp bilgisayarınızı yeniden başlattığınızda muhtemelen wsl ile ilgili bir hata alıcaksınızdır aşağıda linkini verdiğim dökümandaki işlemleri adım adım takip ederek ve  komutları powershell i yönetici olarak çalıştırarak yazdığınızda sorununuz çözülmüş olacaktır. [Windows WSL Döküman Link:](https://learn.microsoft.com/tr-tr/windows/wsl/install-manual#step-1---enable-the-windows-subsystem-for-linux)


- Daha detaylı anlatım için aşağıdaki youtube videosunu da izleyebilirsiniz.
[Windows 10 Home edition üstünde WSL 2, Docker, Windows Terminal, VS Code, Git kurulumu ve ayarları](https://www.youtube.com/watch?v=t4ZS9rTtbOk)




## 6.2-Yazım Hataları Kaynaklı Hatalar
- docker-compose up komutunu çalıştırdığınız zaman “…. Additional property .... is not allowed “ gibi bir hata alırsanız muhtemelen docker-compose.yml dosyanızda bir kelimeyi yanlış yazmış olabilirsiniz. 
- Örneğin:” ` Services.db Additional property enviroment is not allowed `” şeklinde bir hata almış iseniz docker-compose.yml dosyanızda enviroment yerine environment yazmanız durumunda muhtemelen hata ortadan kalkacaktır.


## 6.3-Projeyi Ayağa Kaldırırken Kullanılan Komut Dolayısıyla Yanlış Yükleme
- Kodunuzu yazdınız ve komut satırına docker-compose up komutunu girdiniz , yükleme tamamlandıktan sonra docker da container a baktığınızda örneğin php imajında “ ` php-fpm error failed to post process the configuration ` ” şeklinde bir hata görebilirsiniz. Bu durumda öncelikle  ` docker-compose build  ` komutunu çalıştırıp ardından  ` docker-compose up ` komutu girilmesi durumunda hata ortadan kalkabilir.
