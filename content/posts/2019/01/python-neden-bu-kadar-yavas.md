---
title: 'Python Neden Bu Kadar Yavaş?'
date: '2019-01-16T20:31:00+00:00'
status: publish
images : ["/posts/uploads/2019/01/python-logo-master-v3-TM-flattened.png"]
---
Tekrardan merhabalar. Bu yazıda Python'ın neden yavaş olduğu ve bu yavaşlığa rağmen nasıl bu kadar popüler olabildiği üzerine bazı bilgiler paylaşacağım. Python'ın ne kadar yavaş olduğuna dair şüpheleriniz varsa [The Computer Language Benchmarks Game](https://benchmarksgame-team.pages.debian.net/benchmarksgame/)‘i ziyaret etmenizi şiddetle öneririm. Sadece Python değil C, C++, Java, Go vb. pek çok dil için karşılaştırmalar mevcut. Farklı testler yapılmış ve sonuçlara göre Python rakiplerine nazaran 2-10 kata kadar yavaş çalışıyor. Bunun temelde 3 sebebi var:

- GIL (Global Interpreter Lock)
- Derlenen (compiled) değil "yorumlanan" (interpreted) bir dil olması
- Dinamik tipli bir dil olması

Şimdi bu üç sebebin performansa nasıl etki ettiğine bakalım.

![](../../../uploads/2019/01/python-logo-master-v3-TM-flattened.png)

**GIL (Global Interpreter Lock)**
---------------------------------

Bildiğimiz üzere CPU'lar pek çok çekirdek barındırıyorlar. İşletim sistemleri tüm CPU gücünü kullanabilmek için "thread" adını verdiğimiz yapıları kullanıyor. Burada bu kavramların detayına girmeyeceğim ama özellikle CPU'nun etkin kullanılması gerektiği durumlarda thread'ler vasıtasıyla iş yükünü CPU çekirdeklerine dağıtabiliyoruz ya da I/O işlemlerini bekleyerek kaybedilecek zamandan kaçınabiliyoruz.  
Eğer daha önce multi-thread çalışacak programlar yazdıysanız "lock" kavramını biliyorsunuzdur. Bu yapılar birden fazla thread'in aynı bellek adresi üzerinde aynı anda değişiklik yapmasını önlemek için kullanılıyor. Python yorumlayıcısı (interpreter) da bu işlem için "reference counting" dediğimiz bir yöntemden faydalanıyor. Birden fazla thread eğer ortak bir değişkeni kullanıyorsa bu değişkenin erişim kontrolü Global Interpreter Lock ile sağlanıyor. GIL, ne kadar thread olursa olsun herhangi bir zamanda sadece birinin çalışmasına sebep oluyor. Eğer tek çekirdek üzerinde çalışan bir uygulamanız varsa bu madde sizin için bir anlam ifade etmeyecektir.

**"Python yorumlanan bir dil"**
-------------------------------
Bu ifadeyi çok sık duyduğunuza eminim. Bu ifadenin doğruluğu-yanlışlığı üzerene yeterince konuşulduğunu düşündüğüm için bu konuya girmiyorum ama dilerseniz [şuradaki ](https://stackoverflow.com/questions/2998215/if-python-is-interpreted-what-are-pyc-files)tartışmayı inceleyebilirsiniz. Eğer terminali açar ve "python script.py" yazarsanız Python okuma, ayrıştırma, derleme, yorumlama ve çalıştırma gibi pek çok adım içeren bir işlem yürütmeye başlar. Sizin Python ile yazdığınız kodunuz öncelikle "bytecode" adını verdiğimiz bir yapıya çevrilir ve aslında "yorumlanan" şey bu bytecode'dur. Java ve C#.NET de benzer şekilde yazdığınız kodu önce bir "aracı dile" çevirir ve ihtiyaç anında bu dilden makine koduna derleme/dönüştürme işlemi yapılarak istenen kod bloğu çalıştırılır.

### Java, C# ve Python'ın üçü de bir aracı dil (bytecode) ve bir çeşit sanal makine kullanıyorsa, Python neden bu ikisinden daha yavaş?

C# ve Java [JIT-Compiled ](https://hacks.mozilla.org/2017/02/a-crash-course-in-just-in-time-jit-compilers/)(just-in-time) diller ve bir JIT derleyici kullanıyorlar. Öte taraftan AOT (Ahead of Time) derleyiciler kodu çalıştırmadan önce her bir satırın CPU tarafından anlaşılabileceğine ve çalıştırılabileceğine emin oluyorlar. Ama şimdi konumuz onlar değil. JIT yapısı aslında çalışmayı daha hızlı hale getirmiyor zira hala bytecode'dan yorumlama/derleme işlemi yapılması gerekmekte. Ancak, JIT çalışma anında optimizasyon yapmaya imkan sağlıyor. İyi bir JIT derleyicisi, çalışma anında hangi kod bloklarının daha sık kullanıldığını tespit edebilir ve bu kod bloklarının daha efektif çalışması için düzenlemeler yapabilir. Bu da demek oluyor ki, sizin uygulamanız aynı işlemi tekrar tekrar yaptığında, JIT o işlemi analiz ederek daha hızlı tamamlanmasını sağlayabilir. Ayrıca Java ve C# statik tipli diller bu da optimizasyon ile ilgilenen yazılımın daha verimli çalışabilmesine olanak sağlıyor. Varsayılan Python yorumlayıcısında ise optimizasyon sağlayan bir JIT mekanizması bulunmuyor. Öte taraftan, başka bir Python yorumlayıcısı olan PyPy JIT yapısına sahip ve varsayılan Python yorumlayıcısına kıyasla daha hızlı olduğu [yapılan testlerde](https://hackernoon.com/which-is-the-fastest-version-of-python-2ae7c61a6b2b) ortaya çıkmış.

### JIT yapısı bu tarz dilleri hızlandırabiliyorsa neden varsayılan yorumlayıcıda bu yapı yok?

JIT başlangıç süresini oldukça uzatıyor. PyPy, varsayılan yorumlayıcıya kıyasla 2-3 kat daha yavaş başlıyor. Benzer şekilde Java Virtual Machine'in de başlangıç süresi uzun. .Net'de başlangıç için gerekli olan işlemler Windows işletim sistemi tarafından halledildiği için etkisi bu kadar hissedilmiyor.

Eğer uzun süre çalışmasını ön gördüğünüz bir Python kodunuz varsa ve bu kodunuz tekrar tekrar çağrılan bloklar içerecekse, JIT işinize oldukça yarayabilir. Ancak Python'ın varsayılan derleyicisi genel amaçlı bir yazılım. Eğer Python ile tek bir işe yönelik basit CLI uygulamar geliştiriyorsanız her seferinde JIT'in ilk çalışma süresini beklemek biraz can sıkıcı olabilir.

**"Python dinamik tipli bir dil"**
----------------------------------

Statik tipli dillerde bir değişken tanımlarken onun tipini belirtmek zorundasınızdır. Bu dillere örnek olarak C, C++, Java ve C# verilebilir. Dinamik tipli dillerde ise tip kavramı mevcuttur ama bir değişkenin tipi dinamik olarak değişebilir. Bir örnek verelim:
```python {linenos=table}
a = 1  
a = "test"
```

Bu kod parçası için Python aynı isimde ve "str" tipinde ikinci bir değişken yaratır ve ilk "a" değişkenini bellekten siler. Diğer dillerde bu işlemleri kendiniz halletmeniz gerekirken Python bunu sizin yerinize yapıyor, siz sadece görmüyorsunuz. Aslında Python'ı yavaşlatan şey tiplerin belirtilmemesi değil, Python'ın tasarımının neredeyse her şeyi dinamik yapmaya imkan sağlaması. Örneğin herhangi bir nesnenin bir methodunu çalışma zamanında değiştirebilirsiniz. Bu ve benzeri tasarımsal sebeplerle Python'ı optimize etmek çok zor. Yani kısaca:

- Tipleri karşılaştırmak ve dönüştürmek maliyetli. Ne zaman bir değişkene erişilse tipi kontrol edilir ve eğer gerekliyse bir takım düzenlemeler yapılır.
- Bu kadar dinamik bir dili optimize etmek oldukça zor. Python'ın rakiplerinden daha yavaş olamasının sebeplerinden biri Python'ın esnekliği ve dinamikliği performansa tercih etmiş olmasıdır.

**Bu kadar yavaşsa nasıl bu kadar popüler?**
--------------------------------------------

Aslında burada bir ikilemden söz etmek mümkün. Python, kullanımının bu kadar kolay olmasının bedelini yavaş çalışarak ödüyor. Her ne kadar yavaş çalışsa da aynı işi yapan bir yazılımı Python ile geliştirmek genelde daha az zaman, iş gücü ve kod gerektiriyor. Kolay öğrenilebilir olması da programlamaya yeni başlayanları cezbediyor. Ayrıca Python için yazması kadar okuması da kolay diyebiliriz. Az ve kolay okunabilir bir kodun bakımı ve geliştirmesi ise daha az insan gücü ve zaman ile sağlanabiliyor; bu da az kişi ile proje geliştiren ekiplerde oldukça hayati bir rol oynuyor. Bu özellikleri onu nihai ürün için kullanmak istemeseniz bile prototipleme için oldukça kullanışlı bir araç haline geliyor. Öte taraftan Python her ne kadar yavaş bir dil olsa da bir betik dili olmasının verdiği avantajla C ve C++ gibi daha performanslı diller ile geliştirilmiş kütüphaneleri ve uygulamaları çağırmak için kullanılabiliyor. Örneğin en popüler Python paketlerinden birisi olan NumPy, Python'da oldukça yavaş gerçekleşen dizi/matris işlemlerini C/C++ ile yazılmış backend'de (arka uç) yürüterek ciddi anlamda hız kazandırabiliyor. Tensorflow, Pandas gibi performans ağırlıklı işleri yapmak üzere tasarlanmış diğer pek çok Python paketi de benzer bir yaklaşımı kullanıyor. Bu özellikleri ile Python uzun bir süre daha popülaritesini koruyacak gibi.

Buraya kadar okuyan herkese teşekkürler. Aşağıda da belirttiğim üzere bu yazıdaki bilgiler Antony Shaw'ın "Why is Python so slow?" başlıklı yazısından derlendi. Akıcılığı artırmak adına bazı küçük düzenlemeler yaptım ve son paragrafı naçizane ben ekledim. Umarım keyif almışsınızdır.

Not: Bu yazının aslı [Antony Shaw](https://tonybaloney.github.io/)'a ait olup, tarafımca izni alınarak Türkçe'ye çevrilmiş ve bu adres üzerinden yayınlanmıştır. Kendisine teşekkürü borç bilirim. Yazının aslına [buradan](https://hackernoon.com/why-is-python-so-slow-e5074b6fe55b) ulaşabilirsiniz

Note: The original article was written by [Antony Shaw](https://tonybaloney.github.io/). This translation was made by me with his permission. I thank him for his kindness and this informative article. The orginal article can be rached by clicking [here](https://hackernoon.com/why-is-python-so-slow-e5074b6fe55b).