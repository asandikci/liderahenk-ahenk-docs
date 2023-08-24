# Ahenk Çalışma Mekaniği ve Süreçleri - DEV

Henüz ilk kurulum, kullanıcı ilk girişi, normal giriş ve politika değişikliği için ayrı çalışma mekanikleri implemente edilmemiştir. Edildikten sonra bu mekaniklerin de çalışma şekillerini buraya ekle. TODO

Latest Update: with Version Dev-0.0.1-1

- **Sistem Ile Başlama, Süreç:**
  - Ahenk daemon olarak sistem ile başlar (sadece systemd ile uyumlu)
    - /usr/bin/ahenk-go (ahenk-go/cmd/ahenk-go)
  - ana kod bloğu (ahenk-go/cmd/ahenk-go/main.go) Plugin Manager'i başlatır (./plugin-manager.go)
  - plugin-manager.go, plugin-opener.go'yu çağırır ve tek tek pluginleri ana koda bağlar, sonrasında bunları kullanır ve gerekli çıktılarını handle eder. (ve Lider'e gönderir TODO)
  - Şu anki implementasyonda her 30 saniyede bir log dosyasına plugin/resources > AhenkInfo() yazdırır.

- **Argümanlar:**
  - nodaemon ve tmptest argümanları ile test amaçlı çağırılabilir. nodaemon ile çağrıldığı zaman log file'ı yine bağlar. Tmptest log file'ı bağlamaz, kodun geri kalanını çalıştırır (veya test amaçlı geçici olarak belirli kod parçalarına atlayabilir).
  - start: daemon'u başlatır, kendini forklayıp ana process'ten çıkış yapar. (systemd > forking). forklana process parent process'i olmadığı için init sistemin altına atılır ve grup lideri olur. Pid file ve log file'ı otomatik olarak bağlar. Pid file kullandığı için hâlihazırda arkada çalışan bir daemon varken bu argümanın çağrılması kodu çalıştırmayacaktır. error verip çıkacaktır (yeni process, hâlihazırdaki çalışmaya devam eder)
  - stop, restart: şu anda ikisi de aynı işlevi görmekte. Çünkü systemd, harici durdurma işlemlerinde daemon'u otomatik olarak geri başlatır. Dolayısı ile iki argüman da restart etmek için kullanılır. Harici bir kod bloğu başlatıp pid file'a bakarak çalışan daemon'u signal ile kill eder (15=SIGTERM) 