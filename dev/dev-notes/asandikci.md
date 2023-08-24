# Kişisel Notlarım - Aliberk Sandıkçı
> Go dilini öğrenme ve ahenk-go geliştirme sürecine dair kişisel notlarım, düşüncelerim ve yaptıklarım ile ilgili güncellemeler

> iletişim: https://asandikci.com/link

## Önemli NOT
Bu dosya içerisinde yazılan tüm yazılar şahsın kendisini (Aliberk Sandıkçı) ilgilendirmekte olup TÜBİTAK, Pardus veya Liderahenk Kurum/Kuruluş veya ekiplerini ilgilendirmemektedir. Yazılanlardan sadece kişinin kendisi sorumludur!

---


## Genel Deneyimim
Yazılım geliştirme konusunda uzman olmadığımdan, go dilini daha önce kullanmadığımdan, docker ile daha önce uğraşmadığımdan ve daha önce deb paketi paketlemediğimden dolayı bu staj benim için daha çok öğrenme ve deneyim edinme üzerine oldu. Liderahenk ve Pardus ekibine soru sorma ve onların deneyimlerinden faydalanma imkanı buldum. 

- Neler Öğrendim/Geliştirdim:
  - Go dilini
    - Basit Syntax
    - Modul mantığı ve proje yapısı
    - Plugin mantığı
  - Linux Daemon 
    - Daemon mantığı (forking)
    - Iki farklı dilde daemon implementationu
    - Systemd service file oluşturma
    - Signal and command handling
  - Docker
    - Basit docker komutları
    - dockerfile
  - Deb packaging
    - Deb dosyasının temel bileşenleri
    - Deb dosyası oluşturmak için kullanılan komutlar (dh-make, dh-make-golang, gbp, dpkg-buildpackage)
    - Makefile
  - Diğer
    - Süreç içerisinde sürekli git repoları ile uğraştığım için git versiyon kontrol yapısında kendimi geliştirdim
    - Aynı zamanda bazı processleri otomatikleştirmek için hazırladığım bash scriptleri sayesinde bash dilinde de gelişme katettim.

---

## Hafta Bazında 

#### İlk Hafta (10-16 Temmuz 2023)
- Gönüllü staj için kabul aldım, Liderahenk ekibi ile çalışmam kararlaştırıldı.
- Aynı zamanda YKS de çalışacağım için 2 gün yüz yüze olmak üzere haftada yaklaşık 20 saat çalışmam kararlaştırıldı
- Ahenk Istemcisini Go dili ile baştan implemente etmem söylendi, iki nedeni var:
  - Go, pythona göre daha hızlı ve compile edilebilir bir dil
  - Go için .deb ve .exe çıktısı almak, dependency'leri yönetmek daha kolay
    - Windows için python sürümleri sıkıntı çıkartıyormuş, aslında go da düşünüldüğü gibi sıkıntılı değil ve bir yandan da Windows kullanmayan ve Microsoft'u sevmeyen biri olarak Ahenkin Windows'ta çalışması için çalışmak da çok istediğim bir şey değil. Ama go dilini öğrenmek ve bir proje implemente etmek ilgimi çekti. Bu yüzden severek kabul ettim. 
- İlk defa resmi bir yerde çalışmanın verdiği heyecan ile projeyi daha iyi yönetebilmek adına Mattermost ve Forgejo sunucusu kurdum. (Tavsiye etmiyorum, gerekli değil)
- Go öğrenmeye başladım, kullandığım kaynaklar ve notlar için [/asandikci/go-learning](/asandikci/go-learning) reposuna bakabilirsiniz.

#### İkinci Hafta (17-23 Temmuz 2023)
- Go öğrenmeye devam ettim
- Go dilinin proje yapısını ve module mantığını kavramaya çalıştım, ilgili notlarım için [/asandikci/go-organization](/asandikci/go-organization) reposuna bakabilirsiniz.
- Daemon mantığını anlamak için C dili üzerinde linux makinelerde çalışacak bir daemon yazdım

#### Üçüncü Hafta (24-30 Temmuz 2023)
- Go üzerinde çalışan bir daemon yazdım
- ahenk-docs dökümantasyonuna başladım

#### Dördüncü Hafta (31 Temmuz - 6 Ağustos 2023)
- Go daemon üzerinde çalışmaya devam edildi
- ahenk-go reposu açılıp artık bu repo üzerinden çalışılmaya başlandı

#### Beşinci Hafta (7-13 Ağustos 2023)
- Basit docker komutları öğrenildi ve docker ile çalışılmaya başlandı
- deb dosyası paketleme ile ilgili uğraşıldı, araştırıldı. dh-make-golang paketi kullanılarak docker üstünde .deb dosyası oluşturuldu

#### Altıncı Hafta (14-20 Ağustos 2023)
- Bu dizini ve dosyayı oluşturdum
- Go Plugin yapısını araştırdım
- Memlekete gittiğimiz için çalışmalara biraz ara vermek zorunda kaldım

#### Yedinci Hafta (21-27 Ağustos 2023)
- Makefile yapısını anladım ve daha kolay kurulum/build/silme işlemleri için oluşturdum
- Dökümantasyonları güncelledim
- Go Plugin yapısını implemente etmeye başladım
- Resource Usage plugin'ini kodladım


