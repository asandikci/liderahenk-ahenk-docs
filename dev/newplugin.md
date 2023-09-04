# Yeni Plugin Oluşturma
> Her ne kadar ilk başlarda [resmi plugin yapısı](https://pkg.go.dev/plugin) kullanılmış olsa da windows üzerinde çalışmadığından ve unload özelliği olmadığından dolayı [dinamik plugin yapısı](./resources.md#dynamic-plugin-logic)(goloader) kullanılmaya başlanmıştır.

## Plugin Oluşturma
- plugin ismi belirleyin, küçük harflerler ve tek kelime olması önerilmektedir. Bu dokümanın devamında plugin isminin **myplugin** olduğu varsayılacaktır.
- `plugins/` dizininde plugin isminiz için bir dizin oluşturun, örneğin `plugins/myplugin/`
- ilgili dizin içinde `main.go` ve `info.go` dosyalarını oluşturun
- plugin içindeki oluşturucağımız fonksiyonların plugin manager ve ana program tarafından anlaşılması için ilk önce bir bağlantı kurmamız gerekmektedir. Plugin manager bu bağlantıyı kurmak için dosyada bir sembol arar. Bunun için `main.go` dosyası içinde ilgili sembolleri oluşturunuz. Sembol isminin `Pluginismi + Connect` olmasına ve ilk harfin büyük olmasına dikkat ediniz, örnek:
```go
package myplugin

type plug string

// exported plugin Symbol
var MypluginConnect plug
```
- Sonrasında oluşturacağınız tüm fonksiyonların (aslında plugin içinde method olarak kullanıyoruz, plugin manager import ettikten sonra fonksiyonmuş gibi kullanıyoruz) sembol türünü alan bir method olduğuna ve büyük harfle başladığına emin olunuz. Aksi taktirde plugininizde oluşturduğunuz bu fonksiyon plugin manager tarafından algılanamaz (interface içinde kullanılamaz) ve ana program tarafından kullanılamaz, örnek:
```go
func (p plug) MyFunction1() { // ÇALIŞIR
  fmt.Println(1)
}
func (p plug) myFunction2() { // ÇALIŞMAZ !
  fmt.Println(2)
}
func MyFunction3() { // ÇALIŞMAZ !
  fmt.Println(3)
}
func myFunction4() { // ÇALIŞMAZ !
  fmt.Println(4)
}
```
- `info.go` dosyası içerisinde pluginler yüklenirken kontrol edilecek olan Info() methodunu implemente ediniz. Bir üst adımdaki uyarılara dikkat ediniz. Ayrıca Info() methodunuzun `map[string]interface{}` türünde bir veri döndürdüğünden emin olunuz. `support` kısmı "any", string slice olarak sıralanmış sistemleri (`[]string{"sistem1", "sistem2"}`) veya `map[string]interface` tipinde kategorize edilmiş sistemleri içerebilir, örnek:
```go
func (p plug) Info() map[string]interface{} {
	return map[string]interface{}{
		"name":    "myplugin",
		"version": "2.6.3",
		"support": map[string]interface{}{
			"linux":   []string{"debian", "ubuntu", "pardus21", "pardus23"}, 
			"windows": []string{"10", "11"},
		},
		"description": "My Plugin",
		"developer":   "mail@domain.tld",
	}
```
- Tebrikler, başarıyla bir plugin oluşturdunuz, daha fazla örnek için [plugins/](https://git.aliberksandikci.com.tr/Liderahenk/ahenk-go/plugins/) dizinindeki diğer pluginleri inceleyebilirsiniz. Şimdi sıra bu pluginleri ana koda içe aktarmakta, sıradaki başlığı takip ediniz.

## Plugini İçe Aktarma
- NEXT



