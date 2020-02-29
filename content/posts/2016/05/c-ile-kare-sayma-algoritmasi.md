---
title: 'C++ ile Kare Sayma Algoritması'
date: '2016-05-26T12:45:00+00:00'
status: publish
---
Bir proje ödevini daha bitirmiş bulunmaktayım ve kodları paylaşacağım. Başlık tuhaf gelebilir. Fakat daha doğru nasıl ifade edilir bilmiyorum. Öncelikle ödevin ne olduğundan bahsedeyim. Proje raporunda yaptığım tanımı doğrudan buraya aktarıyorum.

Hazırlanılan projede, verilen nokta koordinatlarına göre, noktalar dikey veya düşey çizgiler ile birleştirilmekte; son koordinat bilgisi de alındıktan sonra oluşan karelerin büyüklükleri de göz önüne alınarak kaç adet oldukları bilgisi kullanıcıya verilmektedir. Kaç nokta olacağı, kaç çizgi çizileceği ve koordinat bilgileri “input.txt” dosyası ile kullanıcıdan alınıp işlemler yapıldıktan sonra, sonuçlar “output.txt” dosyasına yazılmaktadır. Kare sayılarının yanında verilen koordinatlar doğrultusunda oluşan şekli de yazdırarak kullanıcıya tam bir geri dönüş sağlanmaktadır.

“Dots and Boxes” adlı oyunun sadece kare sayma kısmı gibi düşünebilirsiniz. Örnek bir girdi ve çıktı dosyası görüntüsü paylaşırsam daha iyi anlaşılacaktır galiba.

[![](https://2.bp.blogspot.com/-fvKXM8vgPRo/V0bqSnXJUtI/AAAAAAAAANQ/8iYKt8u11bQj9ZV8a5p5aH5Zk8xusF_-wCLcB/s320/input.PNG#float)](https://2.bp.blogspot.com/-fvKXM8vgPRo/V0bqSnXJUtI/AAAAAAAAANQ/8iYKt8u11bQj9ZV8a5p5aH5Zk8xusF_-wCLcB/s1600/input.PNG)  
[![](https://3.bp.blogspot.com/-Ux3PHlJkRiY/V0bqSgEs9QI/AAAAAAAAANM/ZZRhfL-P8ZYTA-5lJb_l_896wTIP6TefwCLcB/s320/output.PNG#float)](https://3.bp.blogspot.com/-Ux3PHlJkRiY/V0bqSgEs9QI/AAAAAAAAANM/ZZRhfL-P8ZYTA-5lJb_l_896wTIP6TefwCLcB/s1600/output.PNG)  



**Önemli Not:** 

Yatay çizgi koordinatlarında 1. sayı satır numarası, 2. sayı sütün numarasını temsil ederken; dikey çizgiler için tam tersi geçerli. Koordinat ‘H’ ile başlıyorsa bu yatay olacağı anlamına gelir. Noktaya gidilir ve sağındaki nokta ile birleştirilen yatay bir çizgi çizilir. ‘V’ ile başlıyorsa ilgili nokta ile altındaki nokta dik bir çizgi ile birleştirilir. Asıl kritik nokta tüm büyüklükteki kareler için çalışabilecek bir sayma algoritması oluşturmak. Artık kodu ve akış diagramlarını paylaşıp burada bitireyim.  

Kaynak kod: [https://drive.google.com/file/d/0B01T\_59j7QNeNGJWQVE4UVFqa28/view?usp=sharing](https://drive.google.com/file/d/0B01T_59j7QNeNGJWQVE4UVFqa28/view?usp=sharing)  
Akış Diagramları: <https://goo.gl/photos/8YBj1fUrvUZVEsi17>