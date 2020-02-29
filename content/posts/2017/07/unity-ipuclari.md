---
title: 'Unity İpuçları'
date: '2017-07-02T11:34:00+00:00'
status: publish
images : ["/posts/uploads/2017/07/unity.jpg"]
---
![](../../../uploads/2017/07/unity.jpg)

Bu yazıda, işinize yarayabilecek bir kaç Unity ipucu göstermeyi düşünüyorum. Basit bir tane ile başlayalım…

1- Bir klasörü tüm alt klasörleri ile beraber açmak için ALT + Sol Tık kombinasyonunu kullanın. Aynı kısayolu hiyerarşide de kullanıp bir objenin tüm “child” objelerine bakabilirsiniz.

{{< tweet 877146090352635904 >}}

2- Çarpışma modeli için mesh collider kullanmaktan olabildiğince kaçının. Detaylı çarpışma modelleri ile en gerçekçi deneyimi elde etseniz de sahneniz kalabalıklaştıkça işlem yükü çok artacaktır. Eğer tek bir basit collider sizin ihtiyacınızı karşılamıyorsa, ana objenize bir kaç boş obje ekleyip çarpışma olaylarını onlar üzerinden yönetebilirsiniz.

{{< tweet 864865224880533504 >}}

3- Biraz matematik ve özenle hazırlanmış görseller, performans açısından harikalar yaratan sonuçlar doğurabilir. Oyununuz 3 boyutlu olsa bile yer yer ikinci boyuttan yardım almaktan korkmayın.

{{< tweet 804947515237810176 >}}

{{< tweet 857935959572201472 >}}

4- Eğer legolar ile aranız iyiyse [MagicaVoxel](http://ephtracy.github.io/index.html?page=mv_main) ile harika modeller yaratabilirsiniz. Birim küpler ile modelleme yapmanıza olanak sağlayan programdan Unity’e çıktı almak da oldukça kolay.

{{< tweet 785070463924011008 >}}

5- Yazdığınız koda yapacağınız bir satırlık bir eklenti, kodunuzun editör penceresinde de çalışmasını sağlayacaktır. Detaylı bilgi için [buraya tıklayın](https://docs.unity3d.com/ScriptReference/ExecuteInEditMode.html).

{{< tweet 774746351204610049 >}}

6- Eğer belirli objeleri sürekli seçiyorsanız, bu seçiminizi kaydedebilir ve sonradan seçiminize tek tıkla erişebilirsiniz.

{{< tweet 765580941976711168 >}}

7- Bir enum için switch-case yazacaksanız, MonoDevelop sizin için işleri biraz kolaylaştırabilir. VisualStudio için ise switch satırını tamamladıktan sonra, ALT + Enter kombinasyonu ile açılan menüden ya da ampul ikonundan bu işlemi gerçekleştirmeniz mümkün.

{{< tweet 760395329745383424 >}}

8- Karakteriniz için birden fazla “idle” animasyonunuz varsa aralarında geçiş yapmak için Blend Tree aracını kullanabilirsiniz. Ayrıntılı bilgi için [buraya tıklayın](https://docs.unity3d.com/Manual/class-BlendTree.html).

{{< tweet 864421865103740928 >}}

9- Kodlarınıza “TODO”lar eklemek kendinize hatırlatıcılar oluşturmanın bir yolu elbette; fakat bu ufak araç sayesinde editör arayüzüne de notlar bırakabilirsiniz. İndirmek için [GitHub sayfası](https://github.com/charblar/stickies)nı ziyaret edin.

{{< tweet 864413157363789824 >}}

10- Sadece geliştirme sürecinde ihtiyaç duyduğunuz objeleri “EditorOnly” olarak etiketleyin. Build aldığınızda o objeler çıkarılacaktır. Böylece, kendiniz için bölümü geçmeye yarayan ya da karakterinizin canını dolduran butonlar oluşturup hile yapabilirsiniz.

{{< tweet 867000960622759938 >}}

Belki ileride yeni bir derleme hazırlayabilirim. O zamana kadar, eğer Twitter kullanıcısı iseniz, [\#unitytips](https://twitter.com/search?q=%23unitytips&src=tyah) etiketini arada bir kontrol etmeyi unutmayın.