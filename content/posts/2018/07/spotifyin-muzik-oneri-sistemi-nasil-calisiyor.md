---
title: "Spotify'ın Müzik Öneri Sistemi Nasıl Çalışıyor?"
date: '2018-07-14T09:50:00+00:00'
status: publish
images : ["/posts/uploads/2018/07/spotify.jpg"]
---
Spotify, 100 milyondan fazla kullanıcısının her birisi için her hafta 30 şarkılık yeni bir "Haftalık Keşfet" listesi hazırlıyor. Binlerce şarkı içerisinden sizin listenizde olmayan ama hoşunuza gidebileceğini düşündüğü bu şarkıları nasıl seçiyor peki? Bir algoritma nasıl oluyor da sizin müzik zevkinizi sizden daha iyi bilebiliyor?

![](../../../uploads/2018/07/spotify.jpg#mid#mid)

Şimdi bir adım geriye çekilip diğer müzik uygulamaları bu işin altından nasıl kalkmış bir bakalım. **Songza**, 2000’lerde ortaya çıkmış bir uygulama ve en ilkel tavsiye yöntemini uygulamakta. Songza’da, bir grup “müzik uzmanı” bir araya gelerek, kullanıcılar için listeler oluşturmakta. **Beat Music** de aynı yöntemi kullanan başka bir uygulama olarak karşımıza çıkmakta. Müziğin “uzmanları” tarafından gelen tavsiyeler belki arkadaş çevrenizden gelenlerden daha başarılı olabilir ama milyonlarca kullanıcı için kalıplaştırılmış bir kaç seçenek sunmak çok da yenilikçi bir yöntem değil.

![](../../../uploads/2018/07/all_apps.png#mid)

Öte taraftan **Pandora** adlı uygulama, biraz daha otomatize bir yaklaşım denedi. Bir grup müzik uzmanı, listeler oluşturmak yerine şarkıları etiketlediler. Sistemdeki tüm şarkılar bir kez etiketlendiğinde, geriye kullanıcının listesinde olan şarkılar ile aynı etikete sahip diğer şarkıları bulup ona önermek kalıyordu. Sorun şu ki sahnede hala kendini “müzik uzmanı” olarak tanımlayan insanlar vardı ve tüm iş gücü elle yapılıyordu.

Yaklaşık aynı zamanlarda, **MIT Media Lab**‘dan bir kaç uzman **The Echo Nest** adında bir şirket kurdular. Bu şirket müziğin “sesini” ve sözlerini analiz eden algoritmalar geliştirdi. Böylece bir müziği etiketlemeyi, özel listeler oluşturmayı ve analizi otomatize eden araçlara sahip olduk.

Bunların dışında pek çok öneri sisteminin temelini oluşturan ve **Last.fm** tarafından da kullanılan “**collaborative filtering**” tekniği var. Fakat buna birazdan değineceğim.

Peki tüm bu yaklaşımlar arasından Spotify hangisini kullanıyor? Spotfy’ın bu kadar güçlü bir öneri sistemine sahip olmasının arkasında sadece bir tane algoritma olduğunu düşünmek büyük bir hata olur. Bunun yerine üç farklı yaklaşımın iş birliği söz konusu.

1. Collaborative Filtering yaklaşımı: Sizin ve diğer kullanıcıların davranışlarının analizi
2. Natural Language Processing (NLP) (Doğal Dil İşleme) yaklaşımı: metin analizi
3. Ses analizi yaklaşımı: doğrudan müziğin kendisinin analizi

**Birinci Yaklaşım: Collaborative Filtering**

Pek çok öneri sisteminin temelini oluşturan bu yapıya çeşitli uygulamalarda denk gelmek mümkün. En bilinen örneklerden birisi **Netflix**. Bir film ya da dizi için verdiğiniz yıldızlar sizin zevkinize sahip diğer kullanıcıları bulmak ve o kullanıcıların oyladığı ama sizin izlemediğiniz içerikleri size önermek için kullanılıyor. Basit değil mi?  
Netflix’in aksine Spotify kullanıcılarından dinledikleri müzikleri oylamalarını istemiyor. Onun yerine sizin dinleme verilerinizi takip ediyor. Bir müziği kaç kez dinlediğiniz, kendi listelerinize ekleyip eklemediğiniz ya da dinledikten sonra sanatçının sayfasına gidip gitmediğiniz, sizin o parça için verdiğiniz “yıldız” oluyor aslında. Peki algoritmik olarak bu öneri sistemi nasıl çalışıyor?  
Algoritma kabaca kullanıcılardan beğendiği şarkılarda yüksek oranda kesişim gösterenlere bakıyor. Daha sonra bir kullanıcının bu kesişim dışında kalan şarkılarını diğer kullanıcılara öneriyor. Kısaca fark kümelerini karşılıklı olarak diğer kullanıcılara öneriyor diyebiliriz. Peki milyonlarca şarkı ve kullanıcı için bu “kesişim kümeleri” nasıl oluşturuluyor? Cevap: **Python** kütüphaneleri ile gerçekleştirilen **matris hesapları**.

![](../../../uploads/2018/07/user_song_matrix.png#mid)  
Kaynak: [From Idea to Execution: Spotify’s Discover Weekly](https://www.slideshare.net/MrChrisJohnson/from-idea-to-execution-spotifys-discover-weekly/31-1_0_0_0_1), by Chris Johnson, ex-Spotify

Spotify veri tabanını düşününce şekilde görülen matrisin ne kadar devasa olduğunu tahmin edebilirsiniz. Her bir satır yaklaşık olarak **140 milyon Spotify kullanıcısından** birini temsil ederken her bir sütun da **30 milyon şarkıdan** birini temsil etmekte. Detayına girmeyeceğim ama bu matris üzerinde yapılan işlemler ile hem kullanıcıları hem de şarkıları birer vektör (lise matematiğinden hatırlayacaksınızdır) olarak temsil edebiliyoruz. Daha sonra bu vektörlere bakarak bir birine benzeyen kullanıcıları ve şarkıları bulmamız mümkün.  
  
**İkinci Yaklaşım: Natural Language Processing (NLP) (Doğal Dil İşleme)**  

NLP bilgisayarın doğal dilleri anlayabilmek için yürüttüğü bir işlem. Bugün neredeyse hepimizin akıllı telefonlarında bulunan Text-To-Speech özelliği bu teknikten yararlanan uygulamalardan bir tanesi. Siri gibi dijital asistanların da köşe taşı bu teknolojidir diyebiliriz. Peki Spotify bunu nasıl kullanıyor?

Spotify tüm internette dolaşan “**web crawler**“lara sahip. Bu “gezginler” müzik üzerine yazılmış makaleleri tarayarak insanların hangi müziklerden hoşlandığını anlamaya çalışıyor. Dergilerdeki albüm değerlendirme köşelerini bilirsiniz. Bu gezginler sizin için internetteki tüm bu değerlendirmeleri okuyarak “iyi” müzikleri bulmaya çalışıyorlar. Bir albümden ya da şarkıdan bahsedilirken kullanılan kelimeler ve sıfatlar bu eserleri sınıflandırmakta kullanılabiliyor. Ayrıca şarkı sözleri de incelenebilmekte.

**Üçüncü Yaklaşım: Ham Ses Modelleri**  

Haftalık keşfetinizden daha önce hiç duymadığınız bir gruptan şarkı dinliyorsunuz. Sayfalarına baktığınızda dinlediğiniz şarkının daha dün yayınlanmış olduğunu ve grubun da ilk şarkısı olduğunu görüyorsunuz. Peki bu nasıl oldu? Daha önce bahsi geçen iki yaklaşım bu şarkıyı size sunamaz çünkü henüz hakkında ne bir yazı yazıldı ne de yeterli kullanıcı verisi oluştu. İşte üçüncü yaklaşımımız tam olarak burada devreye giriyor. “İyi de bu müzikler nasıl analiz ediliyor?” diye sorarsanız, karşımıza yeni bir kavram olarak **Convolutional Neural Networks (CNN)** çıkmakta. Görüntü tanıma gibi teknolojilerinde de kullanılan bir yöntem kendisi. Detaylarına girmeyeceğim ama kabaca pek çok katmandan oluşan ve bu katmanların da verinin farklı özellikleri üzerinde işlem yaparak o veriyi tanımlamaya çalıştığı yapılar olarak düşünebiliriz. Örneğin yüz tanıma için kullandığımızda bir katman gözleri tanımlarken bir diğeri çene yapısını tanımlamakla görevli olabilir. Tüm bu veriler işlendiğinde birbirine benzer insanları bulabilen bir sistem üretebiliriz.

![](../../../uploads/2018/07/sound_analyze.png#mid)  
Kaynak: [Tristan Jehan &amp; David DesRoches, The Echo Nest](http://docs.echonest.com.s3-website-us-east-1.amazonaws.com/_static/AnalyzeDocumentation.pdf)

Spotify ise CNN’leri kullanarak bir şarkının temposunu, ses şiddet seviyesini veya kullanılan perdeyi tanımlayabilmekte. Bu verilere bakarak da yeni eklenen şarkının daha önceden sisteme eklenmiş hangi şarkılar ile benzerlik gösterdiğini tespit edebiliyor. Böylece yeni eklenen bir şarkı, kendisini beğenebilecek bir kitleye ilk haftasında ulaşabiliyor.

![](../../../uploads/2018/07/backend.png#mid)  
Kaynak: [Ever Wonder How Spotify Discover Weekly Works? Data Science](http://blog.galvanize.com/spotify-discover-weekly-data-science/), via Galvanize.

Böylece “Haftalık Keşfet” listemizin sırrını biraz da olsa çözmüş oluyoruz. Tahmin edilebileceği gibi tüm bu yöntemlerin çalışabilmesi için arka planda çok güçlü bir sistemin çalışması gerekmekte. Böyle bir işin altından kalkmak herkesin harcı değil. Şöyle bir dönüp baktığımızda neden Spotify’ın en popüler müzik uygulaması olduğunu görmek zor olmasa gerek.

Umarım okurken keyif almışsınızdır. Bir sonraki yazıda görüşmek üzere.

Not: Bu yazının aslı [Sophia Ciocca](http://sophiaciocca.com/)‘ya ait olup, tarafımca izni alınarak Türkçe’ye çevrilmiş ve bu adres üzerinden yayınlanmıştır. Kendisine teşekkürü borç bilirim. Yazının aslına [buradan](https://medium.com/s/story/spotifys-discover-weekly-how-machine-learning-finds-your-new-music-19a41ab76efe) ulaşabilirsiniz.

Note: The original article was written by [Sophia Ciocca](http://sophiaciocca.com/). This translation was made by me with her permission. I thank her for her kindness and this inspiring article. The orginal article can be rached by clicking [here](https://medium.com/s/story/spotifys-discover-weekly-how-machine-learning-finds-your-new-music-19a41ab76efe).