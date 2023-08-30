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
    - settings.json dosyasına ekleyiniz (default, #12449f, file)
  - `FILLME` » Reusable code block
    - settings.json dosyasına ekleyiniz (default, #A8C993, file)
  - `FIXME` » Bug or error
  - `NOTE` » Extra note
  - `REVIEW` » This code block needs a review
  - `LINK` » Link to documentation/forum/information
#### Go (`golang.go`)
  - package_linux.go ve package_windows.go kodlarındaki aynı fonksiyonların çakışmaması için gerekli ayarları yapınız. (FIXME)

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