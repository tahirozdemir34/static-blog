---
title: 'Unity Geliştirici Günlüğü #2'
date: '2016-07-07T16:28:00+00:00'
status: publish

---
Öncelikle herkese iyi bayramlar. İlk günlükte projeye tekrar ne zaman dönerim bilmem diyordum ama aradan geçen 4 gün sonrası kendimi tekrar Unity’nin başında buldum. Umarım bu istek devam eder. Geçen yazının sonunda “farkında olduğum sıkıntılar” kısmı vardı hatırlarsanız. Bugün biraz onlarla uğraşayım dedim. Aslında Unity’i ilk açtığımda amacım, kafamdaki yetenek sistemi için biraz giriş yapmaktı lakin nasıl olduğunun farkına varamadan, kendimi oyunu Android için düzenlerken buldum. Neler yaptığıma şöyle bir göz atalım.

Bugünün çözülmüş sıkıntısı, mermilerin zor fark edilmesi oldu. Kendimce ikinci bir obje daha oluşturup bunu parlak bir materyal ile kaplamayı ve asıl merminin “child” objesi yapmayı düşündüm. Fakat ileride oyunu mobil platforma geçirmeyi düşündüğüm için ekstra bir obje eklemenin doğurabileceği performans sıkıntılarından korkarak araştırmaya koyuldum ve Unity’nin **“Trail Renderer”** adında bir bileşeni olduğunu öğrendim. Üstelik tam da istediğim işi yapıyordu. Ayarları ile biraz oynayarak istediğim şekle sokabildim.

Android için dokunmatik ekran ile kamerayı yönlendirmeyi sağladım. Fakat geliştirilmesi gerek. Küçük hareketlerde sıkıntı çıkarıyor. Kodun şimdiki halini paylaşayım. Zaten oldukça basit.

```csharp {linenos=table}
int ScrollTouchID = -1; 

void Update(){

  foreach(Touch T in Input.touches) {
  
    if (T.phase == TouchPhase.Began) {                                    
    
      if (ScrollTouchID == -1) {
   
        ScrollTouchID = T.fingerId;    
        ScrollTouchOrigin = T.position;    
       }
    }

    //Dokunma bitince değişkeni eski haline getiriyoruz.
    if ((T.phase == TouchPhase.Ended) || (T.phase == TouchPhase.Canceled)) {                                    
               
      ScrollTouchID = -1;    
    }

    if (T.phase == TouchPhase.Moved) {
                 
    //Eğer parmak hareket ederse, x eksenindeki hareketini 
    //döndüreceğim cismin "z" açısına ekliyorum
    //Sizin uzayınız için döndürme ekseni farklı olabilir.
    //İstenirse ufak düzenlemelerle kameranın pozisyonu, uzaklığı gibi 
    //ayarların dokunmatik ekran ile yapılması sağlanabilir.

      if (T.fingerId == ScrollTouchID) {
        float turz = turret.transform.rotation.z;
        turret.transform.Rotate (new Vector3(0, 0, turz + T.deltaPosition.x));
      }
    }
  }
}
```

 Ayrıca oyun bittikten sonra tekrar oynamak için bir buton da ekledim. Tıklandığında bütün oyun sahasını temizleyip, puan ve zamanı ilk haline getiriyor. Aklınızda olsun, eğer bir buton ile bir scriptteki fonksiyonu çağırmak istiyorsanız, fonksiyonun “public” olduğundan ve scriptin hali hazırda bir objeye ekli olduğundan emin olun. Sonra tek yapmanız gereken “Button” bileşinin “On Click()” kısmını düzenlemek

 Bu süreçte bulduğum bir siteden bahsederek bu günü de tamamlayayım. Geliştirmekte olduğunuz projelerin WebGl buildlerini yükleyebileceğiniz [CheeseGames.net](http://cheesegames.net/) adında bir site mevcut. Şu an için oldukça çiğ durduğunu kabul ediyorum. Fakat doğru reklamı yapmayı başarabilirse ve daha güzel bir arayüze geçerse, başarılı bir girişim olabilir. Siz de isterseniz oyununuzun test sürüşlerini bu site üzerinden yapabilirsiniz.

 Oyunun şu anki halini de yine CheeseGames üzerinden deneyebilirsiniz: [TIKLA ](http://www.cheesegames.net/games/490/index.php?gameDataId=490)

 Edit(15.07.2016): Son sürümü denemek için [TIKLA](http://www.cheesegames.net/games/507/index.php?gameDataId=507)

 Yeni çıkan sorunlar ve yeni fikirler:  
* Mermiler nadiren aynı hizada oluşmuyor.  
* Dokunmatik sıkıntılı çalışıyor.  
* Tekrar başlatılan oyunda bulutlar oluşmaya devam etmiyor. Halletmesi çok kolay 🙂  
* Küpler çeşitlendirilebilir. Daha çok puan veren, vurulmaması gereken, zaman bonusu veren gibi çeşitler türetilebilir.