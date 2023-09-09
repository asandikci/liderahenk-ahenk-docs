# Yeni Geliştiriciler için Açıklamalar
Bu projede devam edecek olan geliştiriciler, stajyerler veya katkı sağlamak isteyen harici *contributor*lar için başlangıç kılavuzu, açıklamalar ve öneriler. Bu dosyayı, hâlihazırda olan dökümantasyonların sırasıyla daha iyi anlaşılması için oluşturulmuş bir roadmap gibi düşünebilirsiniz.

SON UPDATE: howto.md ve changelog.md dosyalarını güncellemeye ve dev-notes/asandikci.md dosyasındaki son hafta için yazdıklarımı (commit=316ef3713e9119b0869baea40406fcf5482faf10) yapmaya vaktim yetmedi, bu dosyadan ana mantığı anlamaya çalışın ama goloader kullandıktan beri güncellemediğim için plugin mantığı çok eksik kalacak... goloader-changes branchına ve son commit'e bakınız ve anlamaya çalışınız!

## Gereklilikler
### Geliştirme Ortamının kurulması
- Geliştirme ortamı için go dilini paket yöneticinizden veya resmi sitesinden kurunuz (>=1.21.0) 
- [environment.md](environment.md) dosyasındaki adımları izleyiniz. VSCode/Codium + Eklentilerini kullanmanız kolaylık ve geliştirme sürecinin bütünlüğünü sağlayacağı için *önerilmektedir*
- Eğer .deb paketi buildleyecek iseniz veya harici testler gerçekleştirmek istiyorsanız [docker geliştirici ortamı kurmanız](environment.md#creating-docker-development-environment) *önerilmektedir* ~~*yeni başlayan stajyerler bunu daha sonra halledebilirler*~~
- Ayrıca kullanılan dinamik plugin yapısı nedeniyle kodun düzgün çalışması ve buildlenmesi için [şu](https://github.com/eh-steve/goloader#build) adımları sırasıyla yapınız. (**önemli**)

### Golang
- Ahenk-go, Go dili ile yazılmıştır. Dolayısı ile go dilinin synatxini, modül ve proje yapısını, concurrent programlamayı ve plugin mantığını bilmeniz önerilmektedir.
- Kaynaklar için [resources.md](resources.md#go) dosyasındaki ilgili linkleri veya [asandikci/go-learning](https://git.aliberksandikci.com.tr/asandikci/go-learning) deposunu kullanabilirsiniz

### Diğer
Go dili ve ortamın kurulması haricinde bunlar hakkında bilgi sahibi olmanız da işinize yarayabilir:
- Git versiyon kontrol kullanımı 
- Shell kullanımı, Genel Linux bilgisi
- Linux Daemon - Windows Service çalışma mantıkları
- Sanal makine çalıştırma
- XMPP (bu dosya yazıldığı an itibarı için projenin ilerisi için)
- LDAP (bu dosya yazıldığı an itibarı için projenin ilerisi için)
- PAM modülleri (bu dosya yazıldığı an itibarı için projenin ilerisi için)
- ...

## Projenin çalışma mantığının anlaşılması
- Projenin mantığının anlaşılması için sırasıyla ilk önce [howto.md](howto.md) dosyasına göz gezdirmeniz sonrasında [changelog.md](changelog.md) dosyasını en alttan en üste doğru okumanız önerilmektedir. (daha kısa versiyonları için [admin](../admin/) dizinine göz gezdirebilirsiniz)
- Özetlemek gerekirse ahenk basitçe sistem başladığında daemon olarak çalışan, Lider'den gelen komutları uygulayan ve sonuçlarını geri Lider'e ileten bir istemci uygulamasıdır. Gerekli komutları yapmak için ilgili pluginleri kullanır. Son kullanıcı [Ahenkdesk](https://github.com/Pardus-LiderAhenk/ahenkdesk) uygulaması ile aynı zamanda Lider ile iletişime de geçebilir ve ilgili bilgileri öğrenebilir. 
- İlgili dökümantasyonları okuduktan sonra projedeki [cmd/ahenk-go/main.go](https://git.aliberksandikci.com.tr/Liderahenk/ahenk-go/src/branch/main/cmd/ahenk-go/main.go) koduna gidip sırasıyla pluginleri vb. incelemeniz *önerilmektedir*

## Geliştirme Sürecinin devamlılığı
- Geliştirme sürecinin devamlılığını sağlamak için [environment.md](./environment.md) dosyasındaki anchor'ları kullanmanız önerilmektedir. Kod editörünüz içinde NEXT, TODO, FIXME ... kelimelerini aratıp eksik/hatalı kod öbeklerini doldurabilrsirsiniz. Siz de kendi anchorlarınızı eklemekten çekinmeyin.
- ahenk-docs dökümanlarında veya ahenk-go projesinde herhangi bir dosyayı, fonksiyonu vb. yeniden isimlendirirken,oluştururken veya silerken hâlihazırdaki dökümantasyon/kod içersinde aratıp başka bir soruna yol açmayacağından emin olunuz. (örneğin bu dosyanın isminin newdew2.md olması durumunda README.md dosyasının da update edilmesi veya pluginlerden birindeki bir fonksiyonun isminin değiştirilmesi durumunda plugin-manager'de de fonksiyon isminin değiştilmesi vb.)
- Dökümantasyona özen gösteriniz, özellikle hem [admin](../admin/) hem de [dev](../dev) klasöründeki howto.md ve changelog.md dosyalarını olabildiğince sık güncellemeye çalışınız. Anlaşılırlığı arttırmak için harici veya dahili bağlantılar da kullanabilirsiniz.
- [Kaynakları](./resources.md) olabildiğince sık güncellemeye çalışınız. Gereksiz bağlantıları silip daha yeni veya daha iyi bağlantıları tutunuz. Olabildiğince kısa, öz ama bir o kadar da bilgilendirici kaynakları toplayınız *ki herhangi bir noktada eksiği olan geliştirici/stajyerler hızlıca bilgilere erişebilsin*
- Kod içinde fonksiyonlardan, methodlardan ve diğer uzun kod bloklarından önce; ne işe yaradığı, nasıl çalıştığı ve neden öyle olduğunu açıklayan anlaşılır yorumlar koyunuz. Aynı zamanda diğer gerek duyduğunuz yerlere kısa yorum satırları eklemekten çekinmeyiniz. Açıklayıcı ve anlaşılabilir yorumlar yazmak ve bir dökümana dönüştürmek için [go yorum rehberini](https://go.dev/doc/comment) takip ediniz.
- Kodun anlaşılabilirliğini sağlamak için [Go stil rehberini](https://google.github.io/styleguide/go/) takip ediniz.<!-- TODO Dev-0.0.1-1 sürümünde yorum ve stil rehberlerine dikkat edilmemiştir, sonraki sürümlerde zamanla daha açıklayıcı ve anlaşılır şekilde devam etmeye ve hâlıhazırdaki yerleri düzeltmeye çalışınız -->
- Git commitlerini olabildiğince açıklayıcı bir şekilde yazınız, [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) şeklini veya geliştirici ekibin kullandığı şekli kullanabilirsiniz. Her şekilde en önemlisinin commitlerin birbirleri ile uyumlu olmasının olduğunu unutmayınız.

### Proje Yapısı
> Go dili hızla gelişen bir dil olduğu için bazı yapılar değişebilmektedir, dolayısı ile bu başlık altında yazılanlar ileride geçerli olmayabilir. Ek bilgi için resmi **olmayan** [şu dokümantasyona](https://github.com/golang-standards/project-layout) bakabilirsiniz

- `.vscode/` içerisinde VSCode/Codium için yer alan ilgili ayarlar bulunmaktadır
- `cmd/` dizininde çalıştırılacak asıl komutlar yer almaktadır.
  - örneğin ahenk-go programı `cmd/ahenk-go/` dizininden başlar (daha doğrusu bu dizin compile edilip /usr/bin/ahenk-go olarak taşınır)
  - kendi başına program olarak çalışan birbirlerinden bağımsız kodları buraya ekleyiniz
    - örneğin ileride geliştirilecek olan ahenk-register
  - aynı zamanda sadece yine `cmd/` dizini içindeki ana programlar tarafından kullanılan ana paketler de buraya yerleştirilmiştir.
    - örneğin `plugin` paketi. Tek başına bir işlevi yok ama projedeki diğer plugin veya paketler tarafından kullanılmamakta, sadece `cmd/ahenk-go/` dizininde bulunan ana programdan çağırılmakta
- `debian/` içerisinde .deb paketi oluşturmak için gerekli olan bilgiler bulunmaktadır. Ayrıca paket oluşturma *tool*ları tarafından oluşturulan otomatik dosyalar için `debian` *branch*ına göz gezdirebilirziniz. NEXT
- `pkg/` dizininde projenin herhangi bir yerinde kullanılabilecek paketler yer alır
  - bu paketlerin kodun diğer kısımlarından bağımsız olması gerekir (kendileri arasında bağlantılı olabilirler ¿)
  - pluginler gibi dinamik bir şekilde load/unload edilmezler. Kod dosyaları başında import edilirler (ve compile edilirken direkt kullanılırlar)
- `plugins/` içinde plugin paketi tarafından load/unload edilebilecek plugin paketleri yer alır
  - pluginler hakkında daha fazla bilgi için [newplugin.md](./newplugin.md)
### Yeni Plugin Geliştirme
- Geliştirme sürecini basit ve anlaşılır tutmak ayrıca dinamik bir yapı oluşturmak için ahenk-go plugin yapısını kullanır. Plugin yapısı ile daha fazla bilgi edinmek için [newplugin.md](./newplugin.md) dosyasını inceleyiniz.

## Geliştirme Süreci
- Kod içlerindeki anchor'lardan ilerleyiniz. (NEXT, TODO, FIXME, REVIEW, FILLME)
- Git adresindeki Issue'lerden ilerleyiniz.
- Mattermost (veya kullanılan diğer adres)teki roadmap'ten ilerleyiniz.
- [Python implementasyonundaki](https://github.com/Pardus-LiderAhenk/ahenk) özelliklerden/pluginlerden devam ediniz.
- [bakınız](#neler-yarım-bırakıldı-veya-planlanmıştı-ama-başlanmadı)

### Genel Taslak
- [x] Linux Daemon
- [ ] Windows Service
- [x] Debian,  .deb packaging
- [ ] Windows, .msi packaging
- [x] Docker Dev Environment 
- [x] Plugin Manager
- [x] plugins/resources
- [x] Dynamic Plugin Manager (with unload, reload features)
- [ ] Connection to Lider with XMPP
- [ ] Connect with Ahenkdesk
- [ ] ...
- [ ] plugins/usb
- [ ] ...
- [ ] plugins/LDAP
- [ ] ...
- [ ] plugins/... (Look more in [python implementation](https://github.com/Pardus-LiderAhenk/ahenk/tree/master/src/plugins))
- [ ] ...
- [ ] a running Docker Ahenk-go container
- [ ] Testing with different operating systems, distributions
...

### Neler Yarım Bırakıldı (Veya planlanmıştı ama başlanmadı)
- osinfo'yu gopsutil gibi organize etmek, alt dosyalara ayırmak ve windows/linux varyantlarını ayırmak
- plugin implementasyonunun iyileştirilmesi, https://github.com/eh-steve/goloader'in daha detaylı incelenmesi ve https://github.com/pkujhd/goloader ile farkının anlaşılması
  - jit'in anlaşılması, go üzerinde ne gibi bir patch uygulandığının belirlenmesi
  - olası hataların ve bugların yakalanması, güvenlik açısından bu plugin implementasyonunu değerlendirme
  - her seferinde build ile kodun yavaşlamaması için precompiled dosyaların da çalıştırılabilmesi özelliğinin eklenmesi, [bakınız](https://github.com/eh-steve/goloader/issues/18)
- resources pluginini daha işlevsel hâle getirmek (python implementasyonundaki tüm işlevlere sahip değil)
- Windows üzerinde çalışan daemon(servis) yapılması, windows için logların, dosyaların ve configlerin ayarlanması
- Windows yüklemesi için .exe kurulum dosyası oluşturulması
- Lider ile iletişim / XMPP
- daha düzenli loglar, debug logları
- cli flag, argument management (cobra) (gerekli mi?)
- daha iyi versiyon yönetimi, deb/exe ve version dosyası için senkronizasyon
- otomatik versiyon güncellemesi
- go kodları için otomatik testler (package_test.go ve makefile içinde)
- daha fazlası için [buraya](./changelog.md#next) bakınız

<br><br>

---

<br>

#### Ekstra
- commitlerinizi GPG ile şifreleyebileceğinizi biliyor muydunuz?
- geliştirme sürecini yönetmeniz için (~~*eğer liderahenk ekibi proje üzerinde çalışmaya başladıysa ve sizin için bir mattermost hesabı açıldıysa*~~) bir mattermost hesabı talep edip roadmap üzerinden ilerleyebilirsiniz. Veya GitHub/Forgejo üzerindeki Issue/Proje sayfası üzerinden kendinize bir roadmap oluşturabilirsiniz. Veya en basitinden bir txt dosyası ile kendinize bir roadmap oluşturabilirsiniz.
- eğer projede hangi görevde çalıştığınız, notlarınızı ve düşüncelerinizi paylaşmak istersiniz [dev-notes](./dev-notes/) dizine isminizi (*veya isterseniz gizlilik nedeni ile nickinizi*) ekleyip yeni bir markdown dosyası oluşturabilirsiniz.