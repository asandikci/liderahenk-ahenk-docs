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
  - Neden bilmiyorum ama bazen bu geçici çözüm işe yaramamakta ¿

### Otomatik Eklenti Ayarları
- Eklentileri Manuel olarak yüklemeniz gerekmektedir. Konfigrasyonlarını ise VSCode/Codium üzerinden kendiniz yapabilirsiniz veya `.vscode/settings.json` dosyasını direkt kullanabilirsiniz.
  - Not: Eğer workspace içerisinde ahenk-go haricinde başka dosya veya klasörler varsa bazı ayarlar geçersiz olabilir, `.vscode/settings.json` içerisindeki tüm ayarları kopyalayıp vscode ayarlarındaki setting.json dosyasına yapıştırabilirsiniz. (tabii ki ilk ve son süslü parantez hariç)
---

## Önerilen Makine Düzeni
### Geliştirme
  - 1 adet Liderahenk sunucusu (Fiziksel/Sanal)
    - veya herhangi bir yerel/diğer XMPP sunucusu
  - 1 adet GNU/Linux Dağıtımı (Fiziksel/WSL)
    - Wine yüklenmiş
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