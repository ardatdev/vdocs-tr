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
