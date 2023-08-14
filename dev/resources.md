# All Development Resources

### Index

- [General](#general)
- [Linux](#linux)
  - [Daemons](#daemons)
    - [New Style Daemons](#new-style-daemons)
    - [Useful Stackexchange pages](#useful-stackexchange-pages)
    - [Signal Handling & Restart](#signal-handling-restart)
    - [Daemon Examples in Other Projects](#daemon-examples-in-other-projects)
  - [deb Packaging](#deb-packaging)
- [XMPP](#xmpp)
  - [XMPP Info](#xmpp-info)
  - [Security / Privacy / Encryption](#security-privacy-encryption)
  - [XMPP Servers&Clients written in Go](#xmpp-servers-clients-written-in-go)
- [GO](#go)
  - [External Git Repos](#external-git-repos)
  - [Useful Go Libraries](#useful-go-labraries)
  - [Plugin Logic](#plugin-logic)
  - [Missing Features](#missing-features-in-golang)
- [Agent Market Search](#agent-market-search)

<br>
<br>

---

<br>
<br>


# General
- https://liderahenk.
- https://docs.liderahenk.
- https://gonullu.pardus.org.tr/merkezi-yonetim-sistemi/

<br>

---

<br>

# Linux

## Daemons

- https://github.com/sevlyar/go-daemon | Ready-to-use Go Daemon
- https://www.makeuseof.com/create-daemons-on-linux/ | Step-by-Step Daemon Guideline
- [Wikipedia/init](https://en.wikipedia.org/wiki/Init)
- [FreeDesktop.org/man/systemd/daemon](https://www.freedesktop.org/software/systemd/man/daemon.html)
- [ArchWiki/SysVinit](https://wiki.archlinux.org/title/SysVinit)

### New Style Daemons / Systemd
- [superuser/systemd-forking-vs-simple](https://superuser.com/questions/1274901/systemd-forking-vs-simple)
- [ArchWiki/systemd](https://wiki.archlinux.org/title/Systemd)
- [FreeDesktop.org/man/systemd/systemd](https://www.freedesktop.org/software/systemd/man/systemd.html)
  - [#new-style](https://www.freedesktop.org/software/systemd/man/daemon.html#New-Style%20Daemons)
### Useful Stackexchange pages
- [stackoverflow/creating-a-daemon-in-linux](https://stackoverflow.com/questions/17954432/creating-a-daemon-in-linux)
- [unix.stackexchange/proper-way-to-run-shell-script-as-a-daemon](https://unix.stackexchange.com/questions/426862/proper-way-to-run-shell-script-as-a-daemon)
- [stackoverflow/how-to-start-a-go-program-as-a-daemon-in-ubuntu](https://stackoverflow.com/questions/10067295/how-to-start-a-go-program-as-a-daemon-in-ubuntu)
- [stackoverflow/how-to-create-a-daemon-process-in-golang](https://stackoverflow.com/questions/23736046/how-to-create-a-daemon-process-in-golang)
- [unix.stackexchange/creating-a-demon-using-systemd](https://unix.stackexchange.com/questions/377483/what-are-ways-of-creating-a-daemon-using-systemd#377498)
- [unix.stackexchange/sysv-upstart-systemd](https://unix.stackexchange.com/questions/196166/how-to-find-out-if-a-system-uses-sysv-upstart-or-systemd-initsystem)
### Old resources or references
- https://web.archive.org/web/20230630212904/http://www.enderunix.org/docs/eng/daemon.php (2001)
- https://ww2.cs.fsu.edu/~bogdanov/private/2013-LIS4488/agenda/week04/daemons-n-services.pdf (2013) | Overview - Daemons and Services
- https://flylib.com/books/en/1.393.1.20/1/ (2011) | BSD Sytle vs SysV daemon
- https://refspecs.linuxbase.org/LSB_3.1.1/LSB-Core-generic/LSB-Core-generic/tocsysinit.html | LSB System Init Scripts

### Signal Handling / Restart
- https://www.man7.org/linux/man-pages/man7/signal.7.html | Signals Manual Page
- https://www.developer.com/languages/os-signals-go/
- https://stackoverflow.com/questions/68201595/how-to-restart-itself-in-go-daemon-process
- https://github.com/kylelemons/daemon/blob/master/restart.go
- https://golang.howtos.io/managing-os-signals-in-go/
- https://golang.howtos.io/working-with-system-signals-in-go-using-the-os-signal-package/
### Daemon Examples in Other Projects
- SSH
  - [openssh/sshd.c](https://github.com/openssh/openssh-portable/blob/master/sshd.c)
  - [openssh/daemon.c](https://github.com/openssh/openssh-portable/blob/master/openbsd-compat/daemon.c#L52)
- Ahenk
  - [ahenk/ahenkd.py](https://github.com/Pardus-LiderAhenk/ahenk/blob/master/src/ahenkd.py)
  - [ahenk/base_daemon.py](https://github.com/Pardus-LiderAhenk/ahenk/blob/master/src/base/deamon/base_daemon.py)

## deb Packaging
- https://go-team.pages.debian.net/packaging.html
- https://wiki.debian.org/SimplePackagingTutorial
- https://people.debian.org/~stapelberg/2015/07/27/dh-make-golang.html

<br>

---

<br>

# XMPP
### XMPP Info
- https://xmpp.org/ | Official Page
- https://en.wikipedia.org/wiki/XMPP | Wiki
- https://xmpp.org/extensions/ | Specification List
- https://xmpp.org/about/technology-overview/ | Technology Overview and Basic Technical Info

### Security / Privacy / Encryption
- https://wiki.xmpp.org/web/XMPP_E2E_Security | OMEMO, OpenPGP comparison and Info

### XMPP servers/clients written in Go
- https://github.com/ortuman/jackal
- https://github.com/daneharrigan/hipchat

<br>

---

<br>

# Go
- https://github.com/golang/go | Go Source Code
- https://google.github.io/styleguide/go/ | Google, Go Style Guide
- https://go.dev/doc/effective_go | Official Effective Go (old doc)
### External Git Repos
- [asandikci/go-learning](https://git.aliberksandikci.com.tr/asandikci/go-learning) | Go Learning Resources
- [asandikci/go-organization](https://git.aliberksandikci.com.tr/asandikci/go-organization) | Project Structure Resources
- [asandikci/go-exercise](https://git.aliberksandikci.com.tr/asandikci/go-exercise) | Go Exercise Resources and Solutions
### Useful GO Labraries
- https://github.com/kirsle/configdir | Get User Config and Cache Directories
- https://github.com/shibukawa/configdir | Get User Config and Cache Directories
- https://github.com/sevlyar/go-daemon | Go Daemon
- **Look for more:** [github/list/go](https://github.com/stars/asandikci/lists/go-language)

### Plugin logic
- https://pkg.go.dev/plugin
- https://github.com/vladimirvivien/go-plugin-example
- https://eli.thegreenplace.net/2021/plugins-in-go/
- https://eli.thegreenplace.net/2023/rpc-based-plugins-in-go/
- https://appliedgo.net/plugins/

### Missing Features in Golang
- https://github.com/golang/go/issues/20461 | unload plugins
- https://github.com/golang/go/issues/19282 | Windows plugin support

<br>

---

<br>

# Agent Market Search
- [grafana/agent](https://github.com/grafana/agent) #golang
- [buildkite/agent](https://github.com/buildkite/agent) #golang
- [open-falcon-archive/agent](https://github.com/open-falcon-archive/agent) #golang
- [jenssegers/agent](https://github.com/jenssegers/agent) #php