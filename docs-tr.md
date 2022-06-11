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
