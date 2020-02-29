---
title: 'Sanal Makine ile Windows Üzerinde Mac OS X Yosemite Çalıştırmak'
date: '2016-05-23T19:01:00+00:00'
status: publish
---
Normal şartlarda Mac OS deneyimi yaşamak için Apple markalı bir ürüne sahip olmalısınız. Apple, Intel işlemcileri kullanmaya başladıktan sonra bu cümlenin son kelimesi “olmalıydınız” halini aldı. Artık PC’ler üzerinde de Mac işletim sistemleri çalışabiliyor. Hatta bu cihazların “Hacintosh” gibi gayet karizmatik bir de isimleri var. Ayrıca, bu işlem için illaki Mac sisteminizin korsan olmasına gerek yok. Parasını verip almış olduğunuz bir işletim sistemiyle de bu “Hacintosh”lardan bir tane yaratabilirsiniz. İşte bu yaratma işlemi için başlıkta göreceğiniz olay mükemmel bir pratik. Herhangi bir veri kaybı olmadan kendi PC’niz üzerinde Mac çalıştırmayı deneyebilir, sonuçtan memnun kalırsanız gerçek bir kurulum yapabilir ya da bir Apple cihaz edinmek isteyebilirsiniz. Zorlama giriş yazımızdan sonra bu işlemin nasıl yapılacağına geçelim.

Not: Bu rehber Virtualbox Üzerine, OS X Yosemite kurulumunun adımlarını içermektedir.

**1. Hazırlık**

Her şeyden önce kullandığınız Windows sürümünün 64-bit olduğundan emin olun. Çünkü Yosemite 64-bit’lik bir işletim sistemi. Bunun dışında en az 4GB RAM ve çift çekirdekli bir Intel(\*) işlemciye ihtiyacınız var. Eğer sisteminiz bu yeterlilikleri sağlıyor ise devam edebiliriz. AMD işlemcilerle ve Haswell mimarisine sahip Intel işlemciler ile de bu kurulumu gerçekleştirmek mümkün fakat onlar için bazı ek ayarlamalar yapmak gerekmekte.

İhtiyacımız olan Virtualbox programını şu adresten indirebilirsiniz: [Virtualbox](https://www.virtualbox.org/)  
Daha sonra OS X Yosemite’in bizim kullanacağımız kırılmış versiyonu olan “Yosemite Zone” un iso dosyasını edinmelisiniz. Google’da yapacağınız ufak bir arama ile bulabilirsiniz. Maalesef , sanal makine kurulumu için korsan versiyonu kullanmak zorundayız.

**2. Sanal Bir Makine Oluşturmak**  
  
 Daha önce sanal bir makine oluşturmuş olanlar sonraki adıma geçebilir. İlk adım için anlatacak bir şey yok. Sol üstten “Yeni” butonuna bastıktan sonra. Açılan pencerede “Türü” kısmına Mac OS X’i seçiyoruz. “Sürüm” için de Mac OS X (64-bit)’i seçiyoruz. “Ad” kısmına canınız ne isterse yazın. İleri dediğimizde bizi bellek ekranı karşılıyor. Düz bir mantıkla “ne kadar ekmek o kadar köfte” prensibine sahip Virtualbox. Ben 4GB ayırdım, size de en az 2GB ayırmanızı öneririm. Sonraki adımda bu sanal makinemize bir de depolama birimi vereceğiz. Bu yazıyı yazdığım tarih itibari ile varsayılan değerleri kullandım. Ekran görüntülerinden bakarak kontrol edebilirsiniz. Disk boyutu olarak 20GB seçtim bu da size kalmış ama bu noktada çok büyük alanlar ayırmanın anlamı yok.

[![](https://4.bp.blogspot.com/-pP88-ZDR0-I/V0NLrm9YIdI/AAAAAAAAAMg/jmjjkfV5gxwp7dUvdioSyCVrLh1HEkcBwCLcB/s320/1.PNG#mid)](https://4.bp.blogspot.com/-pP88-ZDR0-I/V0NLrm9YIdI/AAAAAAAAAMg/jmjjkfV5gxwp7dUvdioSyCVrLh1HEkcBwCLcB/s1600/1.PNG)  
[![](https://4.bp.blogspot.com/-rGl0_LS84gI/V0NLsO3GX1I/AAAAAAAAAMo/gIwj1y4saNQbR-rySCvhvgyiaQXzZx4bACKgB/s320/2.PNG#mid)](https://4.bp.blogspot.com/-rGl0_LS84gI/V0NLsO3GX1I/AAAAAAAAAMo/gIwj1y4saNQbR-rySCvhvgyiaQXzZx4bACKgB/s1600/2.PNG)  
[![](https://4.bp.blogspot.com/-TuPUzXMNDto/V0NLsD3GHGI/AAAAAAAAAMk/q4EFwWgJCRc-RGxhzp9cwM4oRkhGQ1VdwCKgB/s320/3.PNG#mid)](https://4.bp.blogspot.com/-TuPUzXMNDto/V0NLsD3GHGI/AAAAAAAAAMk/q4EFwWgJCRc-RGxhzp9cwM4oRkhGQ1VdwCKgB/s1600/3.PNG)  
[![](https://4.bp.blogspot.com/-Gxvs4Y-vsCU/V0NLsWrM1UI/AAAAAAAAAMs/-1vAk1KQxSYpNmaX3YpJ1dvbsrwwBgHowCKgB/s320/4.PNG#mid)](https://4.bp.blogspot.com/-Gxvs4Y-vsCU/V0NLsWrM1UI/AAAAAAAAAMs/-1vAk1KQxSYpNmaX3YpJ1dvbsrwwBgHowCKgB/s1600/4.PNG)  
[![](https://2.bp.blogspot.com/-_8B9I3VRqbA/V0NLs4A7rFI/AAAAAAAAAM0/Oly3W0ZRfEkKzcAjyuBtvRUOh4GKIuMlACKgB/s320/5.PNG#mid)](https://2.bp.blogspot.com/-_8B9I3VRqbA/V0NLs4A7rFI/AAAAAAAAAM0/Oly3W0ZRfEkKzcAjyuBtvRUOh4GKIuMlACKgB/s1600/5.PNG)  
[![](https://4.bp.blogspot.com/-C1FR4UQhZDI/V0NLsySQukI/AAAAAAAAAMw/UhgZr-Dfj8IK6hqn1M1GbSJigXIhOlKFwCKgB/s320/6.PNG#mid)](https://4.bp.blogspot.com/-C1FR4UQhZDI/V0NLsySQukI/AAAAAAAAAMw/UhgZr-Dfj8IK6hqn1M1GbSJigXIhOlKFwCKgB/s1600/6.PNG)

**3. Kuruluma Geçmeden Son Ayarlar**

 Sanal makinemizi oluşturduk ama işimiz daha bitmedi. Sol taraftaki listeden oluşturduğumuz sanal makineye tıklıyor ve ayarlar diyoruz. “Sistem” menüsünün altındaki gösterdiğim “EFI etkinleştir” ayarını seçimini kaldırıyoruz. Mac’in kendine özgü bir EFI’si var. Bu adım önemli.

[![](https://1.bp.blogspot.com/-EMyWy9H3KFc/V0NLtOBTKeI/AAAAAAAAAM4/R5CJsmYJti4dMoVzET8qFRG_IClQdONfwCKgB/s320/7.PNG#mid)](https://1.bp.blogspot.com/-EMyWy9H3KFc/V0NLtOBTKeI/AAAAAAAAAM4/R5CJsmYJti4dMoVzET8qFRG_IClQdONfwCKgB/s1600/7.PNG)  

Daha sonra “Depolama” menüsü altından gösterdiğim ayarları yaparak daha önce edindiğimiz “Yosemite-Zone.iso” dosyasını makinemize yerleştiriyoruz. Böylece makine başladığından doğrudan kuruluma geçecek.

[![](https://4.bp.blogspot.com/-teWvhYckI6E/V0NLta-KsDI/AAAAAAAAAM8/P3_pCHb4jT0BYL-tJsQPyYa5zC6geqNBwCKgB/s320/8.PNG#mid)](https://4.bp.blogspot.com/-teWvhYckI6E/V0NLta-KsDI/AAAAAAAAAM8/P3_pCHb4jT0BYL-tJsQPyYa5zC6geqNBwCKgB/s1600/8.PNG)  

**4. OS X Yosemite Kurulum**  
  
Cihazımızı çalıştırdıktan sonra kurulumu başlatmak için bir kez enter tuşuna basıyoruz. Sisteminizin gücüne göre 30 saniye ile 15 dakika arasında kurulum başlayacaktır. Dil ayarlarımızı yaptıktan ve kullanıcı sözleşmemizi kabul ettikten sonra sıra geldi diskimizi Mac için uygun hale getirmeye. Bundan sonraki kısımlar için kendi kullandığım kaynaktaki görsellerden yararlanacağım. Fotoğrafta görünen “Disk Aracı” nı açıyoruz. Soldaki kısmın en tepesinde bizim sanal makinemizin diski var. Onu seçip sağ bölmeden “Sil” menüsüne geliyoruz. Hiç bir değişiklik yapmadan (isterseniz isim verebilirsiniz) sağ alttan “Sil” butonuna basıp işlemimizi tamamlıyoruz. Korkmayın sizin verileriniz herhangi bir zarara uğramaz. Daha sonra kurulum için diskimizi seçip sağ alttan özelleştir diyoruz. Açılan pencereden “Drivers” altındaki Install Audio Drivers ve Install Network Drivers’ın; “Graphics” altındaki Graphics Enabler=YES’in seçimlerini kaldırıyoruz.

[![](https://2.bp.blogspot.com/-p3HKq07YeJk/VLm4QSOd2iI/AAAAAAAAF-A/AFk2ZqKQKMc/s1600/Screenshot_13.png#mid)](http://2.bp.blogspot.com/-p3HKq07YeJk/VLm4QSOd2iI/AAAAAAAAF-A/AFk2ZqKQKMc/s1600/Screenshot_13.png)  
[![](https://4.bp.blogspot.com/-r2LOwERyVLw/VLm4s6yxi2I/AAAAAAAAF-I/YMkuSmjFiZk/s1600/Screenshot_14.png#mid)](http://4.bp.blogspot.com/-r2LOwERyVLw/VLm4s6yxi2I/AAAAAAAAF-I/YMkuSmjFiZk/s1600/Screenshot_14.png)  
[![](https://4.bp.blogspot.com/-eZtwTgThoDk/VLm5CIGaV5I/AAAAAAAAF-Q/xpI0NnPtPy4/s1600/Screenshot_17.png#mid)](http://4.bp.blogspot.com/-eZtwTgThoDk/VLm5CIGaV5I/AAAAAAAAF-Q/xpI0NnPtPy4/s1600/Screenshot_17.png)  

**Önemli Not:** Bu seçimleri kaldırmamızın sebebi kurulumu sanal makine üzerine yapıyor olmamız. Normal Kurulum için bu adımı atlayabilirsiniz.

Bu işlemleri tamamladıktan sonra geriye “Yükle”ye tıklayıp beklemek kalıyor.

Bütün işlem bittikten sonra kalıbı çıkarmayı unutmayın. Bunun için sağ alt kısımdaki CD simgesine sağ tıklayıp yanında ✓ olan kalıba tıklamanız yeterli.

**2 Dakika Kaldı” deyip ilerlemiyorsa:**

Bu benim de başıma gelen bir durum ve pek çok kişi de bu sorundan muzdarip. Neyse ki üstesinden gelmesi çok kolay.

- Diski seçtiğimiz ekranda “**-s -v -x**” yazıyoruz. Biraz bekledikten sonra “bash” e ulaşmış olacaksınız.
- İlk olarak “**/sbin/fsck -fy**” komutunu giriyoruz. İşlem bittikten sonra “**/sbin/mount -uw** “.
- Bu da bittikten sonra konumumuzu şu kod ile değiştiriyoruz “**cd /.OSInstallSandboxPath/Scripts/**” ve konumdaki içeriği görmek için “ls” komutunu çalıştırıyoruz.
- Listede “**Hackintosh.Zone.Post-Script.xxxxxx**” dosyasını arıyoruz. Herkes için dosyanın son kısmı farklı olur.
- Sonra tekrar konum değiştirerek oraya giriyoruz “**cd Hackintosh.Zone.Post-Script.sizeözelkısım**“.
- Sonra da “**./postinstall**” komutunu çalıştırıyoruz. Bu işlemde bittikten sonra “**exit**” yazarak çıkıyoruz. Kısa bir süre içinde giriş ekranını görmeniz lazım.

Kaynak: <http://www.macbreaker.com/2015/01/virtualbox-yosemite-zone.html>