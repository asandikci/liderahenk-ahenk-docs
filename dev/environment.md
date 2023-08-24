## Development Environment - Geliştirici Ortamı

Geliştirme sürecinin sürekliliği ve bütünlüğü için:
- Önerilen IDE'ler:
  - VSCode
  - VSCodium
- Önerilen VSCode/Codium Eklentileri:
  - Comment Anchors (`exodiusstudios.comment-anchors`)
    - `TODO` ▶ Future Tasks
    - `NEXT` ▶ High Priority Tasks
      - settings.json dosyasına ekleyiniz (default, #12449f, file)
    - `FILLME` ▶ Reusable code block
      - settings.json dosyasına ekleyiniz (default, #A8C993, file)
    - `FIXME` ▶ Bug or error
    - `NOTE` ▶ Extra note
    - `REVIEW` ▶ This code block needs a review
    - `LINK` ▶ Link to documentation/forum/information
  - Go (`golang.go`)
- Önerilen Makine Düzeni:
  - 1 adet Liderahenk sunucusu (Sanal)
  - 1 adet Pardus + ahenk-go (Sanal/Fiziksel/Docker)
  - 1 adet Windows + ahenk-go (Sanal/Fiziksel)
  - 1 adet Debian + ahenk-go (Docker, .deb build için)
  - 1 adet Pardus + [ahenk](https://github.com/pardus-liderahenk/ahenk) (python) (Sanal, `opsiyonel`)

### Creating Docker Development Environment
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