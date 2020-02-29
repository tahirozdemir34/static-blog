---
title: 'VLC Player ile Twitch Yayınlarını İzlemek'
date: '2014-09-14T21:48:00+00:00'
status: publish
---
[![](https://2.bp.blogspot.com/-vyzriaxCA1k/VBYMZxuq6VI/AAAAAAAAADQ/lUoTwoxGhnA/s1600/Ads%C4%B1z2.jpg)](http://2.bp.blogspot.com/-vyzriaxCA1k/VBYMZxuq6VI/AAAAAAAAADQ/lUoTwoxGhnA/s1600/Ads%C4%B1z2.jpg)

Selam, umarım keyfiniz yerindedir. Başlıkta da gördüğünüz gibi bu yazıda Twitch yayınlarını VLC Player üzerinden nasıl izleyebileceğinizi anlatacağım.

İsterseniz öncelikle neden Twitch’in kendi oynatıcısı yerine VLC Player’ı tercih ettiğimi anlatıyım. Ben oldukça eski bir notebooka sahibim. Flash performansı zaten düşük olan bu notebookta, Twtich gibi ağır bir oynatıcıya sahip bir sistem üzerinden yayınları izlemek tam bir işkence haline geliyor. Zaten izleyeceğim pek çok videoyu önceden indiriyorum ki bir sorun yaşamayım. Eğer siz de benimki kadar eski bir bilgisayar sahibiyseniz, kesinlikle yayınları VLC Player üzerinden izlemenizi öneririm. Gelelim ikinci sebebe. Hepimizin malumu üzere Twitch zaten sorunlu bir platformdu. Amazon’un satın almasıyla birlikte bu sorunlar daha da arttı. Bu sorunları bir nebze de olsa bertaraf etmek için yine bu yönteme başvurabilirsiniz. Sebeplerimizden bahsettiğimize göre bu işi nasıl yapacağımıza geçelim.

Öncelikle tabiki VLC Player’ı edinmeliyiz: [www.videolan.org/vlc/](http://www.videolan.org/vlc/)  
Ardından ihtiyacımız olan eklentiyi (livestreamer.exe): [github.com/chrippa/livestreamer/releases](http://github.com/chrippa/livestreamer/releases) (Yeşil butona tıklayarak 🙂

[![](https://4.bp.blogspot.com/-FINOeXSfuvg/VBYDbUyEgLI/AAAAAAAAACg/v-tz_551-To/s1600/Ads%C4%B1z.jpg)](http://4.bp.blogspot.com/-FINOeXSfuvg/VBYDbUyEgLI/AAAAAAAAACg/v-tz_551-To/s1600/Ads%C4%B1z.jpg)

Her iki programı da indirip kurduktan sonra şimdi işin en cafcaflı kısmına geliyoruz. Livestreamer.exe kurulduktan sonra ilgili yerdeki “tik”i kaldırmadıysanız karşınıza bir notdefteri ve “#” ile başlayan satırlar çıkacak. Eğer “tik”i kaldırdıysanız dosyaya ulaşmak için Windows 7’de başlat menüsünün arama kısmına %appdata% yazıp entera basıyoruz. Açılan klasörde “livestreamer” klasörünü buluyoruz ve onun içindeki “livestreamerrc” adlı dosyayı not defteri ile açıyoruz. Şimdi bu notdefteri içinde… ehm… ııı. yok böyle olmayacak resim atıyorum…

[![](https://2.bp.blogspot.com/-tOMWjLBQYPQ/VBYF0Z4Q5gI/AAAAAAAAACs/YC3U8oa_oHY/s1600/Ads%C4%B1z3.jpg)](http://2.bp.blogspot.com/-tOMWjLBQYPQ/VBYF0Z4Q5gI/AAAAAAAAACs/YC3U8oa_oHY/s1600/Ads%C4%B1z3.jpg)

Ok ile göstermiş olduğum satırın başındaki #’i kaldırıyoruz. Tabi 32 bit işletim sistemi kullanıyorsanız ve yükleme sırasında değişiklik yapmadıysanız. Eğer işletim sisteminiz 64 bit ise bir üstteki satırın başındaki # i kaldırın. Yok derseniz ben farklı bir yere yükledim, tırnaklar arasındaki yolu yüklediğiniz yol ile değiştirin ve kaydedin.

Gelelim yayınları nasıl açacağımıza. Bunun için BaşlatTuşu + R kombinasyonu ile “çalıştırı” açıyoruz (başlat menüsünden de “çalıştır”ı açabilirsiniz). Ardından satıra şunu yazıyoruz: livestreamer.exe twitch.com/yayıncıadı kalite. Örneğin:

[![](https://1.bp.blogspot.com/-EvhXeXYlMm4/VBYIhaXQrCI/AAAAAAAAAC4/DeD5vUn_DR8/s1600/Ads%C4%B1z4.jpg#mid)](http://1.bp.blogspot.com/-EvhXeXYlMm4/VBYIhaXQrCI/AAAAAAAAAC4/DeD5vUn_DR8/s1600/Ads%C4%B1z4.jpg)

“Kalite” kısmını biraz açmam gerekiyor. Bu kısma “audio” yazarsanız yayının sadece sesini dinleyebilirsiniz. “Bunu neden yapıyım?” sorusu aklınıza geliyorsa şöyle bir senaryo yazabiliriz. Diyelim ki AKK’yi doldurdunuz ve internetiniz çok yavaşladı. Bu da yetmezmiş gibi interneti komşularınızla paylaşıyorsunuz. Yayında dönen geyiği de merak ediyorsunuz. Hemen kaliteyi audio olarak ayarlayıp en azından muhabbeti dinleyebiliyoruz. Ben mi? Yok canım ben fiber internet kullanıyorum…

Bunların dışında “source” kalitesi için “best”, mobil kalite için “worst” yazıyoruz. Diğer kalite değerleri için herhangi bir değişiklik yok.
---------------------------------------------------------------------------------------------------------------------------------------------

Bundan sonraki kısımda ek olarak yayınlar için kısayol oluşturmayı anlatacağım. Bunun için öncelikle not defterini açıyoruz ve içine şunu kopyala-yapıştır yapıyoruz:
```
@echo

cd C:Program FilesLivestreamer

livestreamer.exe www.twitch.tv/yayıncıadı kalite

@echo off
```

Daha sonra Dosya-> Farklı Kaydet dedikten sonra kayıt türünü “tüm dosyalar” olarak seçip isminin sonuna “.bat” ekliyoruz.

[![](https://1.bp.blogspot.com/-40My11fCjbI/VBYMZ_cC6qI/AAAAAAAAADE/2Hdc8U5vuvY/s1600/Ads%C4%B1z5.jpg#mid)](http://1.bp.blogspot.com/-40My11fCjbI/VBYMZ_cC6qI/AAAAAAAAADE/2Hdc8U5vuvY/s1600/Ads%C4%B1z5.jpg)

Burada önemli nokta ikinci satırdaki yolun bizim livestreamer’ı yüklediğimiz yol ile aynı olması. 64 bit işletim sistemi ve yükleme sırasında seçilen farklı yükleme yerleri hakkında söylediklerimi hatırlıyorsunuzdur…