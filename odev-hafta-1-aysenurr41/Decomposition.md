# **Decomposition - Ayrıştırma**

Faktoring olarak da bilinen bilgisayar biliminde **decomposition**; karmaşık bir problemi veya sistemi, kavranması, anlaşılması, programlanması ve bakımı daha kolay parçalara bölmektir.

Bilgisayar bilimlerinde tanımlanan farklı ayrıştırma türleri vardır:

- Yapılandırılmış programlamada, algorithmic decomposition, bir süreci iyi tanımlanmış adımlara ayırır.
- Yapılandırılmış analiz, bir yazılım sistemini sistem bağlamı seviyesinden sistem işlevlerine ve Tom DeMarco tarafından açıklandığı gibi veri varlıklarına ayırır.
- Öte yandan, Object-oriented decomposition, büyük bir sistemi giderek daha küçük sınıflara veya problem alanının bir kısmından sorumlu olan nesnelere ayırır.
- Booch'a göre, algorithmic decomposition, nesne yönelimli analiz ve tasarımın gerekli bir parçasıdır, ancak nesne yönelimli sistemler, nesnelere ayrıştırma ile başlar ve vurgular.

Daha genel olarak, bilgisayar biliminde functional decomposition, bir modelin fonksiyonunun karmaşıklığına hakim olmak için bir tekniktir. Böylece bir sistemin işlevsel modeli, bir dizi işlevsel alt sistem modeliyle değiştirilir.

Ayrıştırma, büyük bir problemi daha yönetilebilir alt problemlere ayırma sürecidir. Motivating principle, büyük problemlerin çözülmesinin küçük problemlere göre orantısız bir şekilde daha zor olmasıdır.
İki adet 500 satırlık program yazmak, 1000 satırlık bir program yazmaktan çok daha kolaydır.

C'de ayrıştırma birimi function ve ADT'dir. C++ veya Java'da ise decomposition sınıftır. Ayrıştırmanın işe yaraması için, tüm problemin alt bölümlerinin mümkün olduğunca birbirinden bağımsız olmasıdır. Bu onların alt bölümlerinin olmayacağı anlamına gelmez. Tamamen birbirine bağlıdır. Sadece gereksiz yere birbirlerinin detaylarına bağlı kalmamalılar. Bağımsızlık, özellikle farklı alt problemlere karşı saldırıya uğrayan grup projelerinde önemlidir. Programcının endişelenmeden her soruna odaklanabilmesi gerekir.

## **Decomposition Amacı**

Ayrıştırmanın amacı, problemi bağımsız alt problemlere bölmektir. Kara kutular bu hedefin doğal uzantısıdır. Çoğunlukla bağımsız olarak yazılabilirler. Etkileşime girmeleri gerektiği ölçüde, iyi tanımlanmış ve nispeten basit mekanizmalar aracılığıyla olur. Bir işlev, herhangi bir koda kolayca sığdırılmaya hazır, düzgün bir pakete sarılmış muhtemelen kötü bir hesaplamadır.
Benzer şekilde, bir sınıf, düzenli bir soyutlamaya ve eksiksiz bir yöntem paketine sahip bir nesneyi temsil eder.

- Okuması ve anlaması daha kolay
- Test etmek daha kolay
- Hata ayıklamak daha kolay
- Yeniden kullanımı daha kolay

İyi ayrıştırılmış bir işlev veya iyi tasarlanmış bir sınıf bazen bir "kara kutuya" benzetilir. Bu kara kutunun amacı opak olmasıdır - iç işleyişi belirgin değildir. Bunun yerine kutu başardığıyla tanımlanır. Kutu, girdisi açısından iyi tanımlanmış bir davranışa sahiptir. Bu kara kutu, çıktının ne olacağını açıklamak için mümkün olan en basit soyutlamayı sunar ve gizler. Bir kara kutu bir yetki birimidir - onu ne yaptığınıza göre tanımlarsınız.
***"Bu veri yapısının bu dosyadan doldurulmasını istiyorum"***
 İstenen sonucun nasıl elde edildiğine dair tüm uygulama detayları güvenli bir şekilde içinde izole edilmiştir.

## **Avantajları**
- Farklı insanlar farklı alt problemler üzerinde çalışabilir.
- Paralelleştirme mümkün olabilir.
- Bakım daha kolaydır.

## **Dezavantajları**
- Alt problemlerin çözümleri orijinal problemi çözmek için bir araya gelmeyebilir.
- Yetersiz anlaşılan problemlerin ayrıştırılması zordur.

## **Decomposition paradigm**

Bilgisayar programlamasında bir decomposition paradigm, bir programı birkaç parça olarak düzenlemek için bir stratejidir ve genellikle bir program metnini organize etmenin belirli bir yolunu ifade eder.
Genellikle bir ayrıştırma paradigması kullanmanın amacı, örneğin programın modülerliği veya sürdürülebilirliği gibi program karmaşıklığı ile ilgili bazı ölçütleri optimize etmektir.
Çoğu ayrıştırma paradigması, bu parçalar arasındaki statik bağımlılıkları en aza indirmek ve her bir parçanın bütünlüğünü en üst düzeye çıkarmak için bir programı parçalara ayırmayı önerir. Bazı popüler ayrıştırma paradigmaları prosedürel, modüller, soyut veri tipi(abstract) ve nesne yönelimli olanlardır.

Ayrışma paradigması kavramı, tamamen bağımsızdır ve hesaplama modelinden farklıdır ancak ikisi genellikle karıştırılır, çoğu zaman işlevsel hesaplama modelinin prosedürel ayrıştırma ile karıştırıldığı ve hesaplamanın actor modelinin object oriented decomposition ile karıştırıldığı durumlarda.


## **Decomposition diagram**

Bir ayrıştırma diyagramı, karmaşık, süreç, organizasyon, veri konusu alanı veya daha düşük seviyeli, daha ayrıntılı bileşenlere ayrılmış başka türde bir nesneyi gösterir.
Örneğin, ayrıştırma diyagramları, organizasyon yapısını veya süreçlere işlevsel ayrıştırmayı temsil edebilir. Ayrışma diyagramları, bir sistemin mantıksal hiyerarşik bir ayrıştırmasını sağlar.

# **Functional Decomposition**

Adım adım programlama görevleriniz daha karmaşık hale geliyor, yöntemleriniz de öyle. Tek bir katı yönteme veya hatta ana yönteme sarılmış karmaşık bir program oluşturabilmenize rağmen, bir programı, okunması ve anlaşılması kolay birkaç daha spesifik yönteme bölmek daha iyidir. Karmaşık bir programı alt programlara bölme yaklaşımına **Functional Decomposition** denir.

Fonksiyonel ayrıştırma, basitçe bir problemi çeşitli fonksiyonlara veya yöntemlere ayırma sürecidir. İhtiyacımız olan sonuçları elde etmek için bu yöntemleri arka arkaya uygulayabilmemiz için her yöntem belirli bir görevi yerine getirir. Bir probleme baktığımızda, hangi eylemleri birden çok kez tekrarlamak isteyebileceğimizi veya alternatif olarak ayrı ayrı gerçekleştirmek isteyebileceğimizi düşünmemiz gerekir. İstediğimiz yöntemleri bu şekilde elde ediyoruz. Sonuç olarak, bu yöntemlerin okunması, anlaşılması, yeniden kullanılması, test edilmesi ve hata ayıklanması daha kolaydır.

```
function giveBonus(currentYear, price) {
   if ((currentYear % 4 === 0) && price > SUPER_THRESHOLD) {
      return SUPER_BONUS;
   }
   return price > BASIC_THRESHOLD ? NORMAL_BONUS : 0;
}
```

Yukarıdaki, bonus veren küçük bir fonksiyondur. Öyleyse neden daha fazla alt işleve ihtiyacım var?

```
function giveBonus(currentYear, price) {
   if (isLeapYear(currentYear) && 
         priceQualifiesForSuperBonus(price)) {
      return SUPER_BONUS;
   }
   if (qualifiesForNormalBonus(price)) {
      return NORMAL_BONUS;
   }
   return 0;
}
```
Yukarıdaki bazı şeylerin rastgele isimleri var, çünkü bu kurgusal bir örnek. Ancak, hesaplamaların küçük, tek amaçlı bir şey yapan işlevlere çıkarılmasına dikkat edin. Burada ki kullanım ilk kullanıma göre daha temiz ve düzenli. Aynı zamanda tek kullanımlık fonksiyonlar kullanarak ayrıştırma yapılmıştır. Böylece okunabilirlik daha kolay.

![function-decomposition-example](https://e5119252-a-62cb3a1a-s-sites.googlegroups.com/site/restaurantseproject/functional-decomposition/de.png?attachauth=ANoY7cpI8IgJnNevzCIBtR5zRB3ZPQN0zYkXsRqfN0XinbpB78yD6n7WuG46kiwVfOCv2aL5rn3Je3U60Y93sp_MIpIvWTkar5j4skzXNH7tneftciMgoJSGPemfJvObZPALAv1pPemGybFuB4bQQNCRfkztP_wyWHqFKODyKubHweKBW2VM77dEqY_ZduTFDk82Jj1XiiBYa19DYJbfPQo8wM7OLbooNPQoYfRKjfiZ-VDied9-65YuFbcOnS0ja4bJf6eMLvnq&attredirects=0)