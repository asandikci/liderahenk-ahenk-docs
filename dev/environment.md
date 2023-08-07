### Development Environment - Geliştirici Ortamı

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
- Önerilen Sanal Makine Düzeni:
  - 1 adet Liderahenk sunucusu (Sanal)
  - 1 adet Pardus + [ahenk](https://github.com/pardus-liderahenk/ahenk) (python) (Sanal, `opsiyonel`)
  - 1 adet Pardus + ahenk-go (Sanal/Fiziksel)
  - 1 adet Windows + ahenk-go (Sanal/Fiziksel)
  - 1 adet GNU/Linux + ahenk-go (Fiziksel, `opsiyonel`)