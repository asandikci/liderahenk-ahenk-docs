# Ahenk Go Changelog
newest from bottom to top

## NEXT
- plugin/resources: Implement ResourceUsage()

### Geliştirme Sürümü 0.0.1 (Dev-0.0.1-1)

- plugin/resources: get memory usage

#### Initial Development Tree:
- main executable file: ahenk-go/cmd/ahenk-go/
  - main.go: arguman handling, starting daemon, calling PluginManager
  - plugin-manager.go: running plugins, handling plugin outputs and sending Lider (TODO)
  - plugin-opener.go: connecting plugins to main program with looking for public symbols
- debian
  - ahenk-go.service: Systemd service file
  - changelog: debian release changelog
  - control/copyright/rules: for deb packaging
- pkg
  - osinfo: fetch information about os. Disks, memory etc. Frequently using in plugin/resources
  - utils: variety of utilities
- plugins
  - resources: returns resource usage and machine information to plugin manager
  - this plugin can be seen as *plugin/resources*, *plugins/resources* or *resource usage plugin*

