---
title: 'CUDA İçin Temel Bilgiler'
date: '2018-09-01T15:37:00+00:00'
status: publish
images : ["/posts/uploads/2018/09/thumbnail.jpg"]
---
Bu yazıda CUDA’ya ve GPU mimarisine göz atacağız. CUDA ile nasıl programlama yapılacağından değil temel kavramlardan bahsedeceğim. Oldukça seyreltilmiş bir yazı okuyacağınızı da belirteyim. Amacım tam bir CUDA rehberinden ziyade bir başlangıç noktası sunmak. Buradaki bazı başlıklar şöyle sıralanabilir:

- GPU mimarisi ve bellek yapısı
- Grid, block ve thread kavramı
- “Compute capability” kavramı
- Örnek bir program akışı

![](../../../uploads/2018/09/thumbnail.jpg)

GPU’lar ile CPU’ları ayıran en temel fark sahip oldukları işlem birimlerinin nitelik ve nicelikleri. CPU’lar daha yüksek hıza ve interrupt gibi mekanizmalara sahip işlem birimlerine sahip iken, GPU’lar daha düşük hızlarda ve interrupt gibi yeteneklerden yoksun olsa bile binlerce işlem birimine sahiptir. Daha yakından incelemek ve bu donanımların iç yapısını anlamak için Şekil 1’den yararlanılabilir.

![](../../../uploads/2018/09/CPU-2Bvs-2BGPU.png#mid)  
Şekil 1: CPU ve GPU iç yapısı \[1\]

Bir GPU, Streaming Multiprocessor (SM) dizisidir. SM’ler içerisinde CUDA çekirdekleri barındırır ve çalıştırılacak olan kod bu çekirdekler üzerinde çalıştırılır. Bir GPU’da bulunan SM sayısı ve SM’lerin barındıracağı çekirdek sayısı o GPU’nun mimarisine göre değişiklik gösterir.

![](../../../uploads/2018/09/SM.png#mid)  
Şekil 2: Streaming Multiprocessor yapısı \[1\]

Programlamak için grid, blok ve thread yapıları kullanılır. Gridler bloklardan; bir blok ise thread’lerden oluşur. Grid, blok ve threadler üzerinde nasıl çalıştırılacağı programlanan kod GPU’ya aktarıldığında SM’ler üzerine dağıtılır ve işletilir.

![](https://3.bp.blogspot.com/-iRE0_MuY-kE/W4qrWnIGDvI/AAAAAAAAAuE/Ihm2mvKvOdwpmkH3hvOnf7wWbywhF_SfACLcBGAs/s400/GBT.png#mid)  
Şekil 3: Grid, block ve thread yapısı \[1\]

Bir problemin kaç blok ve thread üzerinde çalıştırılacağının hesabı problemin büyüklüğüne ve problemin özelliklerine göre hesaplanmalıdır. Bu bağlamda en yüksek performansı elde etmek için genel bir çözümden ziyade, probleme özel yazılım geliştirilmesi gereklidir. Bu temel mimari farkın yanına GPU’nun bellek birimlerinin ayrıca ele alınması mücbirdir. Birbirinden farklı yeteneklere ve amaçlara sahip bellek birimlerinin kullanımının doğru şekilde planlanması pek çok problemde performans artışına imkan sağlamaktadır.

![](../../../uploads/2018/09/Bellekler.png#mid)  
Şekil 4: Bellek hiyerarşisi (Nobile et al. 2014)

GPU’larda her thread’in kendine ait bir yerel belleği (local memory) bulunur. Ayrıca Bir blok içerisinde çalışan tüm blokların erişebileceği, o bloğa atanmış bir paylaşımlı bellek (shared memory) ve tüm birimlerin erişebileceği global bellek (global memory) de GPU içerisinde yer alır. Bu belleklere hem okuma hem de yazma yapılabilmektedir. Erişim hızları açısından hızlıdan yavaşa: threadlere ait yerel bellek, bloklara ait paylaşımlı bellek, hepsine ait global bellek şeklinde sıralanabilir. Erişilecek verilerin bu bellekler üzerinde dağıtımı hız açısından ciddi farklar doğurmaktadır. Bu üç bellek dışında sadece okuma yapılabilen (read-only) belleklerde vardır. Bunlar şekilde de görülen constant memory ve texture memory’dir. Farklı amaçlar için özelleşmiş bu bellek tiplerinin hesap işlemlerinde kullanıldığı bir örneğe rastlamadım. Bir problemde algoritmanın nasıl paralelleştirilebileceğinin yanı sıra o problem için bellek yönetiminin nasıl yapılacağının planlanması da nihai performans kazancı için önemlidir.

CUDA yeteneğine sahip ekran kartları, yeteneklerine göre bir “compute capability” derecesine sahip olurlar. Compute capability değeri kabaca o GPU’nun desteklediği yazılımsal ve donanımsal yeteneklere göre belirlenir. Örneğin derin öğrenme için özel olarak tasarlanan Tensor Core işlem birimleri compute capability’si 7 olan Tesla V100 ve Titan V ekran kartlarında bulunmaktadır. Compute capability sayısal değerini X.Y şeklinde düşünecek olursak X, doğrudan GPU’nun mimarisini gösterir. Örneğin Volta mimarisine sahip kartlarının X değeri 7 iken Pascal mimarisine sahip olanlarınki 6’dır. Y ise aynı mimarideki küçük gelişmelere göre çeşitlilik gösterir. Örneğin Pascal mimarisine sahip olan ve bellek boyutlarında baz sürümden bazı farklara sahip olan Quadro P5000 için bu değer 6.1’dir. \[2\] Ancak unutulmamalıdır ki minör değerin yüksek olması her kalemde bir iyileşme olduğu anlamına gelmez. Yazılım geliştirilirken üzerinde çalışacağı donanımın özellikleri dikkate alınarak geliştirilmelidir. Daha yüksek işlem kapasitesine sahip bir cihazda gerekli iyileştirmelerin yapılmadığı bir yazılım beklenen performans artışını gösteremeyecektir.

CUDA-enabled bir GPU’yu programlamak için birden çok seçeneğe sahibiz. Pek çok alternatifin arasında Nvidia’nın kendi çözümü olan ve C/C++ desteği bulunan Cuda Toolkit öne çıkmaktadır. Donanım geliştiricisinin ürünü olması sebebiyle en yüksek verim bu araç ile elde edilmekte ve yenilikler önce ona gelmektedir. CUDA, daha önceden bahsi geçen birimlerden her birimin (grid, blok, thread ve bellek birimleri) yönetimi için kullanılabilir. Yazılan kod CPU tarafından yönetilir ve gerekli fonksiyonlar GPU üzerinde çalıştırılır. Burada en yüksek maliyet verinin host yani ana bilgisayar belleğinden device yani GPU belleğine kopyalanmasıdır.

![](../../../uploads/2018/09/Ak-25C4-25B1-25C5-259F.png#mid)   
Şekil 5: CPU ve GPU’da program akışı \[3\]

Şekil 5’de de görüldüğü üzere program CPU üzerinde çalışmaya başlar. GPU ana belleğe doğrudan erişemediği için gerekli veriler GPU’nun belleklerine aktarılır. Daha sonra GPU üzerinde çalıştırılacak fonksiyon (bu fonksiyonlar “kernel” olarak isimlendirilmekte) çağrılır. GPU hesabını yaparken CPU’da farklı komutlar çalıştırılmaya devam edebilir ya da GPU’nun işini bitirmesini bekleyebilir. İşlem sonlandığında, CPU doğrudan GPU belleğine erişemediği için, GPU belleğinde bulunan sonuçlar ana belleğe taşınır ve program akışına devam edilir.

CUDA’nın da her yazılımda olduğu gibi farklı sürümleri mevcuttur. Nasıl ki daha yüksek performans elde etmek için kullanılan GPU’nun compute capability’si göz önüne alınıyorsa, kullanılan CUDA sürümünün yetenekleri de irdelenmelidir. Örneğin CUDA 8.0 ile birlikte Unified Memory kavramı ortaya çıkmıştır. Bu bellek modeli CPU ile GPU arasında veri taşıma ve bu taşıma işleminin optimize edilmesi yükünü ortadan kaldırır. Ayrıca, bu teknolojiye compute capability’si 6.0 ve üstü olan GPU’larda donanım seviyesinde de destek sunulmaktadır. Bu bağlamda Pascal mimarisine sahip bir cihaz üzerinde Cuda 8.0 ile geliştirilmiş bir yazılımın bellek erişim performansı düşük versiyonlara nazaran oldukça iyi olacağını söyleyebiliriz \[4\].

Bunun dışında GPU üzerinde yapılacak bazı işlemleri hızlandıran optimize edilmiş kütüphaneler de bulunmaktadır. Bu kütüphaneler derin öğrenme (cuDNN vb.); lineer cebir ve matematik (cuBLAS, cuRAND vb.); sinyal, görüntü ve video (cuFFT vb.) ve paralel algoritma (Thrust, NCLL vb.) gibi temel başlıklar altında toplanabilir \[5\]. Temel işlemler için özelleşmiş ve optimize edilmiş bu kütüphaneler doğru noktalarda kullanıldığında hem geliştirme süresini kısaltmakta hem de performans kazancı sağlamaktadır.

\[1\] <https://docs.nvidia.com/cuda/cuda-c-programming-guide>  
\[2\] <https://developer.nvidia.com/cuda-gpus>  
\[3\] Luong, Thé Van. (2016). Parallel Metaheuristics on GPU. 10.13140/RG.2.1.4017.5127.  
\[4\] <https://devblogs.nvidia.com/unified-memory-cuda-beginners/>  
\[5\] <https://developer.nvidia.com/gpu-accelerated-libraries>

