# Development Environment - Geliştirici Ortamı
Bu dosyada geliştirme sürecinin sürekliliği ve bütünlüğü için geliştiricilerin ilk başta kurması gereken ortam anlatılmaktadır.

---
## IDE/Eklentiler
### Önerilen IDE'ler
  - VSCode
  - VSCodium
### Önerilen VSCode/Codium Eklentileri
#### Comment Anchors (`exodiusstudios.comment-anchors`)
  - `TODO` » Future Tasks
  - `NEXT` » High Priority Tasks
  - `FILLME` » Reusable code block
    - use epic anchors for improve reachability
  - `FIXME` » Bug or error
  - `NOTE` » Extra note
  - `REVIEW` » This code block needs a review
  - `LINK` » Link to code block with line number/id
    - see https://github.com/StarlaneStudios/vscode-comment-anchors#link-anchors
  - see https://github.com/StarlaneStudios/vscode-comment-anchors for more information
#### Go (`golang.go`)
  - 
##### FIXME build flag issues
- package_linux.go ve package_windows.go kodlarındaki aynı fonksiyonlar sorun yaratmakta. Örnek için ahenk-go/pkg/osinfo/os_windows.go ve os_linux.go dosyalarını IDE'nizde birlikte açınız
- see these [t](https://github.com/microsoft/vscode-go/issues/2672)w[o](https://github.com/golang/go/issues/29202) issues or [workaround](#workaround) to resolve problem

###### Workaround
- `.vscode/settings.json` içinde `go.buildFlags` ayarı linux/windows için çalışırken manuel olarak değiştirilmeli. 
- `package_linux.go` dosyalarında, `//go:build linux` yerine `//go:build linux && !windows` kullanılmalı (ki go.buildFlags -tags=windows'a ayarlı iken bu paketleri dahil etmesin)
- **Windows** üzerine bir özellik geliştirirken `.vscode/settings.json` dosyasına ekleyiniz: `"go.buildFlags": ["-tags=windows"],`
- **Linux** üzerine bir özellik geliştirirken `.vscode/settings.json` dosyasına ekleyiniz: `"go.buildFlags": ["-tags=linux"],`
- Sorunlar
  - Her seferinde manuel olarak ayarın değiştirilmesi lazım
  - herhangi bir sistem için çalışırken diğer sistemin kodu içinde diagnotics çalışmamakta. Örneğin `tags=windows` etkinken eğer package_linux.go dosyasına gidersek go eklentisinin çoğu yapılandırma özellikleri çalışmamakta ve uyarı vermekte
  - Nedenini tam olarak bilmiyorum ama bazen bu geçici çözüm işe yaramamakta ¿
    - go build satırını yorum işaretine bitişik yaz!, `// go:build linux && !windows` değil, `//go:build linux && !windows`
    - go build satırından sonra bir satır boşluk bırak ?

### Otomatik Eklenti Ayarları
- Eklentileri Manuel olarak yüklemeniz gerekmektedir. Konfigrasyonlarını ise VSCode/Codium üzerinden kendiniz yapabilirsiniz veya `.vscode/settings.json` dosyasını direkt kullanabilirsiniz.
  - Not: Eğer workspace içerisinde ahenk-go haricinde başka dosya veya klasörler varsa bazı ayarlar geçersiz olabilir, `.vscode/settings.json` içerisindeki tüm ayarları kopyalayıp vscode ayarlarındaki setting.json dosyasına yapıştırabilirsiniz. (tabii ki ilk ve son süslü parantez hariç)
---

## Önerilen Makine Düzeni
### Geliştirme
  - 1 adet Liderahenk sunucusu (Fiziksel/Sanal)
    - veya herhangi bir yerel/diğer XMPP sunucusu
  - 1 adet GNU/Linux Dağıtımı (Fiziksel/WSL)
    - Wine yüklü
      - [bakınız](#wine-geliştirme-ortamının-oluşturulması)
    - Docker [godeb](#creating-docker-development-environment)
      - Paket buildlemek ve mini testler için
    - içinde Pardus sanal makine
      - Ekstra testler ve [ahenk python implementasyonu](https://github.com/pardus-liderahenk/ahenk)nu anlamak için ahenk yüklenmiş şekilde
### Test
  - Pardus sürümleri (Sanal/Fiziksel)
  - Windows 10, 11 (Sanal/Fiziksel)

## Creating Docker Development Environment
> For testing and building .deb package
1. Install and Create docker environment, [Quick Start](https://sulincix.github.io/sayfalar/html/docker-kullanimi.html)
2. Pull docker image
```sh
docker pull asandikci/godeb
```
> Or alternatively build Dockerfile with `docker build -t godeb:latest` code for lower data usage

3. Create container from image and attach to container, an example:
```sh
docker run -it -d --name build1 asandikci/godeb:latest "bin/bash"
docker attach build1 --detach-keys "ctrl-k"
```

<br>
<details>
<summary>-- wine --</summary>

### Wine Geliştirme Ortamının oluşturulması
> Daha önce hiç Wine kullanmadıysanız **ve** bilgisayarınız sanal makinede windows çalıştırabilecek güçte ise bu başlığı atlamanız önerilir.
> adımlar wine8.15(staging) ve go1.21.0 sürümleri kullanılarak yapılmıştır
- paket yöneticinizden `wine` veya `wine-staging` paketini indiriniz ve `wineboot -u` komutunu çalıştırınız
- https://go.dev/dl/ adersinden en son yayınlanan .msi dosyasını indiriniz.
- terminal üzerinde `wine control` komutunu çalıştırınız ve kontrol panelini açınız
  - Add/Remove Program
  - bir önceki adımda indirdiğiniz .msi dosyasını yükleyiniz
    - yükleme konumu olarak `C:\users\KullanıcıAdınız\go\` dizinini seçiniz
- terminal üzerinde `wine regedit` komutunu çalıştırınız ve kontrol panelini açınız
  - **HKEY_CURRENT_USER** > **Environment** dosyasına geliniz.
  - GOPATH'i `C:\users\KullanıcıAdınız\go` şeklinde düzenleyiniz (kurulumda kurduğunuz path)
  - PATH'i `C:\users\KullanıcıAdınız\go\bin` şeklinde düzenleyiniz
- https://github.com/eh-steve/goloader#build adresinde yer alan ayarları yapınız, GOROOT değişkenini kullanmak yerine işlemi manuel olarak yapmanız önerilir.
- Artık `make local_wine` komutu ile go dosyasını buildleyip, `wine /usr/bin/ahenk-go` komutu ile çalıştırabilirsiniz. (sisteminiz sadece `ahenk-go` yazınca da wine ile çalıştıracağını anlayabilir)

#### Wine ile ilgili ek bilgiler
- eğer halihazırda bir wine kurulumunuz varsa ve farklı bir dizin kullanmak istiyorsanız `winetricks` uygulamasını yükleyerek yeni bir prefix oluşturabilirsiniz.
  - sonrasında çalıştıracağınız tüm komutları `env WINEPREFIX=~/.local/share/wineprefixes/PREFIX_ISMI wine KOMUT` öneki ile çalıştırınız. ([yukarı](#wine-geliştirme-ortamının-oluşturulması)daki komutların tümünü ve sonrasında çalıştıracağınız ahenk-go)
    - bazı kabuklarda tilde ~ sembolü çalışmayabiliyor, full dizini yazının.
  - eğer yeni bir prefix oluşturduysanız Makefile dosyasını gözden geçiriniz ve **özellikle** `WINE_C` değişkenini değiştiriniz !
- Herhangi bir sorun olduğunda ve çözüm bulamadığınızda winetricks uygulamasından ilgili prefix'i seçip herşeyi sil seçeneğini seçip, tüm adımları baştan yapabilirsiniz.
- eğer wine konsolu üzerinde sürekli fixme hataları çıkıyorsa kodu `env WINEDEBUG=fixme-all wine KOMUT` ile çalıştırınız
- goloader, jit, kernel veya pluginlerin yüklenmesi ile ilgili sorun/panic oluşuyorsa `make local_wine_safeplugins` komutunu deneyiniz
  - bu komut pluginleri paket olarak içeri import eder ve hangi pluginde sorun olduğunu daha anlaşılabilir bir şekilde gösterir.
    - dolayısı ile unload vb. diğer plugin özellikleri çalışmaz, sadece debugging amaçlı kullanınız ! 
- FIXME `panic: Failed to find GetStdHandle procedure in kernel32.dll: Path not found.`  ve `panic: Failed to load kernel32.dll: Path not found.` hatalarının çözümü bulunamadı! Eğer siz de bu hatayı alırsanız wine yerine windows kullanmayı deneyiniz veya sorunu çözerseniz bu dökümantasyona ekleyiniz.
</details>