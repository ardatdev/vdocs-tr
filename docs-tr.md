# V Dokümantasyonu

(V'nin standart kütüphanelerinin dokümantasyonu için bu adresi ziyaret edin https://modules.vlang.io/)

## Giriş

V, sürdürülebilir yazılımlar için tasarlanmış, statik olarak yazılan, derlenmiş bir programlama dilidir.

Go dili ile benzerlikler içerir ve tasarım açısından Oberon, Rust, Swift,
Kotlin ve Python'dan etkilenmiştir.

V çok basit bir programlama dilidir. Bu dokümantasyonu bitirmeniz 1 saat civarı sürecek ve
dokümantasyonu bitirdiğinizde V programlama dilinin büyük bir kısmını öğrenmiş olacaksınız.

V programlama dili minimum soyutlama ile basit ve temiz kod yazmayı sağlar.

Basit olmasının yanında, V geliştiriciye çok fazla güç verir.
Diğer dillerde yapabileceğiniz her şeyi V ile de yapabilirsiniz.

## Kaynak kodundan indirmek
V'nin en son ve en iyi sürümünü indirmenin ana yolu __kaynak kodunu indirmektir__.
Kaynak kodunu indirmek, __kolay__ bir seçenektir ve genelde sadece __bir kaç dakikanızı alır__.

### Linux, macOS, FreeBSD, vb. için:

Kaynak kodunu indirmek için `git`'e ve `tcc`, `gcc`, `clang` veya `msvc` gibi bir C compiler'a ihtiyacınız var.
```bash
git clone https://github.com/vlang/v
cd v
make
```
Geliştirme araçlarını nasıl indireceğinizi görmek için 
[buraya](https://github.com/vlang/v/wiki/Installing-a-C-compiler-on-Linux-and-macOS) bakabilirsiniz.

### Windows:
Kaynak kodunu indirmek için `git`'e ve `tcc`, `gcc`, `clang` veya `msvc` 
gibi bir C compiler'a ihtiyacınız var.
```bash
git clone https://github.com/vlang/v
cd v
make.bat -tcc
```
Not: `-tcc` yerine `-gcc`, `-msvc`, `-clang` gibi başka bir C compiler'da kullanabilirsiniz.
Fakat `-tcc` küçük, hızlı ve indirmesi kolaydır. 
(V önceden oluşturulmuş binary'yi otomatik olarak indirecektir.)

C compiler'ı yüklemeyi ve daha fazla bilgiyi 
[burada](https://github.com/vlang/v/wiki/Installing-a-C-compiler-on-Windows) bulabilirsiniz.

Bu klasörü "Ortam Değişkenleri" yoluna eklemeniz önerilir.
Bu işlem `v.exe symlink` komutuyla yapılabilir.

Not: Bazı antivirüs programları(Symantec gibi) tek karakterli(`v.exe` gibi) 
çalıştırılabilir dosyalara karşı paranoyaktır. Bu durumda geçici bir çözüm
`v.exe` programını `vlang.exe` ye kopyalamaktır (kopya daha yeni olsun diye)
ya da antivirüs programınızdan V dosyasını beyaz listeye alabilirsiniz.

### Android
Android cihazlarda V grafik uygulamalarını çalıştırmak [vab](https://github.com/vlang/vab) sayesinde mümkündür.

V Android bağımlılıkları: **V**, **Java JDK** >= 8, Android **SDK + NDK**.

  1. Bağımlılıkları indirin ([vab](https://github.com/vlang/vab))
  2. Android cihazınızı bağlayın
  3. Run:
 ```bash
  git clone https://github.com/vlang/vab && cd vab && v vab.v
  ./vab --device auto run /path/to/v/examples/sokol/particles
  ```
Daha fazla detay ve sorun giderme için, lütfen [vab GitHub deposunu](https://github.com/vlang/vab) ziyaret edin.

## İçerik Tablosu

<table>
    <tr><td width=33% valign=top>

* [Merhaba Dünya](#hello-world)
* [Proje dosyasını çalıştırma](#running-a-project-folder-with-several-files)
* [Yorumlar](#comments)
* [Fonksiyonlar](#functions)
    * [Birden çok değer döndürme](#returning-multiple-values)
    * [Hoistingler](#hoistings)
* [Sembol görünürlüğü](#symbol-visibility)
* [Değişkenler](#variables)
* [V tipleri](#v-types)
    * [Stringler](#strings)
    * [Sayılar](#numbers)
    * [Arrayler](#arrays)
        * [Çok boyutlu arrayler](#multidimensional-arrays)
        * [Array methodları](#array-methods)
        * [Array sliceları](#array-slices)
    * [Sabit boyutlu arrayler](#fixed-size-arrays)
    * [Haritalar](#maps)
* [Modül içe aktarma](#module-imports)
* [Açıklamalar & ifadeler](#statements--expressions)
    * [If](#if)
    * [In operatorü](#in-operator)
    * [For döngüsü](#for-loop)
    * [Match](#match)
    * [Defer](#defer)
* [Yapılar](#structs)
    * [Varsayılan alan değerleri](#default-field-values)
    * [KIsa yapı sabit syntax](#short-struct-literal-syntax)
    * [Erişim değiştiriciler](#access-modifiers)
    * [Methodlar](#methods)
    * [Gömülü yapılar](#embedded-structs)
* [Unionlar](#unions)

</td><td width=33% valign=top>

* [Fonksiyonlar 2](#functions-2)
    * [Varsayılan saf fonksiyonlar](#pure-functions-by-default)
    * [Değişebilir argümanlar](#mutable-arguments)
    * [Değişken sayıda argüman](#variable-number-of-arguments)
    * [Anonim ve üst düzey fonksiyonlar](#anonymous--higher-order-functions)
    * [Closurelar](#closures)
* [Referanslar](#references)
* [Constantlar](#constants)
* [Yerleşik fonksiyonlar](#builtin-functions)
    * [println](#println)
    * [Çalışma zamanında ifadeleri boşaltma](#dumping-expressions-at-runtime)
* [Moduller](#modules)
* [Tip Bildirimleri](#type-declarations)
    * [Arayüzler](#interfaces)
    * [Numaralar](#enums)
    * [Toplam türleri](#sum-types)
    * [Takma adlar](#type-aliases)
    * [Seçenek/Sonuç türleri ve hata işleme](#optionresult-types-and-error-handling)
* [Özel hata türleri](#custom-error-types)
* [Genericler](#generics)
* [Eşzamanlılık](#concurrency)
    * [Eşzamanlı Görevleri Oluşturma](#spawning-concurrent-tasks)
    * [Kanallar](#channels)
    * [Paylaşılan Nesneler](#shared-objects)
* [JSON](#json)
	* [Decoding JSON](#decoding-json)
	* [Encoding JSON](#encoding-json)
* [Testing](#testing)
* [Hafıza yönetimi](#memory-management)
    * [Stack ve Heap](#stack-and-heap)
* [ORM](#orm)

</td><td valign=top>

* [Doküman yazma](#writing-documentation)
* [Araçlar](#tools)
    * [v fmt](#v-fmt)
    * [v shader](#v-shader)
    * [Profiling](#profiling)
* [Paket Yönetimi](#package-management)
	* [Paket yayınlama](#publish-package)
* [İleri seviye konular](#advanced-topics)
    * [Güvenli olmayan kodlar](#memory-unsafe-code)
    * [Referans alanları olan yapılar](#structs-with-reference-fields)
    * [sizeof ve __offsetof](#sizeof-and-__offsetof)
    * [C ile V'yi çağırma](#calling-c-from-v)
    * [V ile C'yi çağırma](#calling-v-from-c)
	* [Atomics](#atomics)
	* [Global Değişkenler](#global-variables)
    * [Debugging](#debugging)
    * [Koşullu derleme](#conditional-compilation)
    * [Derleme zamanı sahte değişkenleri](#compile-time-pseudo-variables)
    * [Derleme zamanı yansıması](#compile-time-reflection)
    * [Sınırlı operatörü aşırı yükleme](#limited-operator-overloading)
    * [Satır içi assembly](#inline-assembly)
    * [C dilinden, V diline çevirme](#translating-c-to-v)
    * [Hot code yeniden yükleme](#hot-code-reloading)
    * [Çapraz Derleme](#cross-compilation)
    * [V ile cross-platform shell scriptleri](#cross-platform-shell-scripts-in-v)
    * [Attribute](#attributes)
    * [Goto](#goto)
* [Ekler](#appendices)
    * [Anahtar kelimeler](#appendix-i-keywords)
    * [Operatörler](#appendix-ii-operators)

</td></tr>
</table>

<!--
Not: v:compile, cgen, live, görmezden, failcompile, oksyntax, badsyntax, wip, nofmt 
için kod çerçevelerinden sonra koyabileceğiniz birkaç özel anahtar kelime vardır.
Daha fazla ayrıntı için: `v check-md

NB: there are several special keywords, which you can put after the code fences for v:
compile, cgen, live, ignore, failcompile, oksyntax, badsyntax, wip, nofmt
For more details, do: `v check-md
-->

## Hello World


```v
fn main() {
	println('merhaba dünya')
}
```
`hello.v` adlı bir dosya oluşturun ve bu kod parçasını dosyaya yapıştırın. Sonra bunu yapın: `v run hello.v`.

> Burada V'yi [burada](https://github.com/vlang/v/blob/master/README.md#symlinking) anlatıldığını gibi 
> `v symlink` ile symlinklediğini varsayıyorum. Eğer yapmadıysan manuel olarak V'nin konumunu yazman gerekiyor.

Tebrikler, az önce ilk V programını yazdın!

`v hello.v` komutunu çalıştırmadan da programını derleyebilirsin.
`v help` yazarak desteklenen tüm komutları görebilirsin.

Yukarıdaki örnekteki gibi, fonksiyonlar `fn` kelimesi ile belirtiliyor.
Dönüş tipi fonksiyon isminden sonra belirtilir.
Bu durumda `main` hiç bir şey döndürmüyor.

Diğer bir çok programlama dilleri(C, Go ve Rust vb.) `main` programının giriş noktası. 
Yani program çalıştığında ilk önce `main` içindeki kodlar çalışmakta.

[`println`](#println) bir kaç [yerleşik fonksiyondan](#builtin-functions) bir tanesi.
Kendisine iletilen değeri çıktıya yazdırır.

Tek dosyalı programlarda `fn main()` belirtmenize gerek yoktur.
`fn main()` küçük programlar, "scriptler" ve öğrenme sırasında daha kullanışlıdır.
Kısa olması için bu tutorialda `fn main()` geçeceğiz.

Bu demek oluyor ki V dilinde "merhaba dünya" yazdırmak şu kadar kolay:

```v
println('merhaba dünya')
```

## Birden fazla dosyası olan projeleri çalıştırma

Birden fazla ".v" dosyalı bir klasörün olduğunu varsayalım, o dosyaların biri `main()` fonksiyonunu içeriyor, 
diğerleri ise yardımcı fonksiyonları. Konuya göre düzenlenmiş olabilirler 
fakat hala yeniden kullanılabilir modüller olarak yapılandırılmamışlar ve 
sen onları tek bir program olarak derlemek istiyorsun.

Diğer dillerde "include"lar veya tüm dosyaları numaralandırmak için 
bir derleme sistemi kullanmanız, bunları nesne dosyalarına ayrı ayrı derlemeniz 
ve ardından bunları son bir yürütülebilir dosyaya bağlamanız gerekir.

V'de ise, tüm ".v" dosyalarının tüm klasörünü sadece `v run .` yazarak
derleyebilirsin. Geçiş parametrelerini de aynı zamanda çalıştırabilirsin.
Sadece şunu yapman gerekli: `v run . --yourparam some_other_stuff`

Yukardaki yöntem ilk önce tüm dosyaları tek program altında(senin dosya/klasörünün adıyla) derleyecek, sonra programı CLI parametreleri olarak
belirtilen `--yourparam some_other_stuff` ile birlikte çalıştıracaktır.

Programın daha sonra aşağıdaki CLI parametrelerini kullanabilir:
```v
import os

println(os.args)
```
Not: Başarılı bir çalıştırmadan sonra, V tüm çalıştırılabilir dosyaları silecektir. Eğer dosyaların silinmemesini istiyorsanız `v -keepc run .` komutunu kullanın veya `v .` komutu ile manuel olarak kopyalayın.

Not: Herhangi bir V derleyici etiketi, `run` komutundan önce belirtilmelidir.
Kaynak dosyası/klasöründen sonra olan her şey, direkt olarak programa geçirilecektir.
V tarafından işlenmeyecektir.

## Yorum satırları

```v
// Tek satırlık yorum.
/*
Çok satırlı yorum.
   /* İç içe geçmiş olabilir. */
*/
```

## Fonksiyonlar

```v
fn main() {
	println(add(77, 33))
	println(sub(100, 50))
}

fn add(x int, y int) int {
	return x + y
}

fn sub(x int, y int) int {
	return x - y
}
```

Yine, tür argümanın adından sonra gelir.

Go ve C dilindeki gibi fonksiyonlar aşırı yüklenemez.
Böylece kod daha sade olur ve okunulabilirliği artırır.

### Hoistingler

Fonksiyonlar, oluşturuldukları yerden önce kullanılabilir:
Yani fonksiyonu satır 200'de oluşturduysanız, satır 100'de
bu fonksiyonu çağırabilirsiniz. Mesela yukardaki örnekte
`add` ve `sub`, `main`'den sonra belirtilmiş ama yine de
`add` ve `sub` fonksiyonunu `main` fonksiyonunda çağırabilirseniz.
Bu V'deki tüm fonksiyon bildirmelerinde geçerlidir ve "header" dosyalarına
olan ihtiyacı ortadan kaldırır.

### Birden fazla değer döndürme

```v
fn foo() (int, int) {
	return 2, 3
}

a, b := foo()
println(a) // 2
println(b) // 3
c, _ := foo() // `_` kullanan değerleri görmezden gelin
```

## Sembol görünürlüğü

```v
pub fn public_function() {
}

fn private_function() {
}
```

Fonksiyonlar varsayılan olarak "private"dır(dışarıdan erişelemez).
Diğer modüllerde fonksiyonu kullanmak için fonksiyonu belirtirken başına
`pub` eklemeniz gerekmektedir. Aynı olay sabit değerler(constants) ve türler içinde 
geçerlidir.

Not: `pub` sadece adlandırılmış bir modülden kullananılabilir.
Modüller hakkında daha fazla bilgi için [Modüller](#modules)
bölümüne bakın.

## Değişkenler

```v
name := 'Bob'
age := 20
large_number := i64(9999999999)
println(name)
println(age)
println(large_number)
```
Değişkenler `:=` ile bildirilir. V'de sadece bu yolla değişkenleri belirtebilirsiniz.
Bu yüzden her değişkenin bir başlangıç değeri olur. 

Değişkenin türü sağ taraftaki değerden çıkarılır, yani `:=` sonrasına göre belirlenir.
Farklı bir tür seçmek için, tür dönüştürmeyi kullanın: T(v) ifadesi, v değerini 
T tipine dönüştürür. 


