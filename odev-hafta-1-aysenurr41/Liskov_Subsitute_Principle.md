# **Liskov Substitution Principle (LSP) – Liskov’un Yerine Geçme Prensibi**

## **Liskov Substitution Principle Nedir ?** 

Barbara Liskov tarafından geliştirilen bu prensip kısaca şöyle açıklanabilir:
Alt sınıflardan oluşturulan nesneler üst sınıfların nesneleriyle yer değiştirdiklerinde aynı davranışı göstermek zorundadırlar.

LSP’ye göre herhangi bir sınıf kullanıcısı, bu sınıfın alt sınıfları kullanmak için özel bir efor sarf etmek zorunda kalmamalıdır. Onun bakış açısından üst sınıf ve alt sınıf arasında farklılık yoktur. Üst sınıf nesnelerinin kullanıldığı metotlar içinde alt sınıftan olan nesneler aynı davranışı sergilemek zorundadır, çünkü oluşturulan metotlar üst sınıf davranışları örnek alınarak programlanmıştır. Alt sınıflarda meydana gelen davranış değişiklikleri, bu metotların hatalı çalışmasına sebep verebilir. Özellikte bu metotlarda instanceof gibi nesnelerin tipleri arasında kıyaslama yapılmak zorunda kalındığı zaman, LSP prensibi çiğnenmiş olur ki, bu alt sınıfların varlığından haberdar olunduğu anlamına gelir. Kullanıcı sınıflar ideal durumda alt sınıfların varlığından haberdar bile olmamalıdır.


## **Neden İhtiyaç Duyarız ?**

Kodlarımızda herhangi bir değişiklik yapmaya gerek duymadan alt sınıfları, türedikleri(üst) sınıfların yerine kullanabilmeliyiz. Hem kod  tekrarını önlemek, daha uzun  kod satırlarından  kurtulmak ve  daha anlaşılır olması  için hem de daha temiz bir kod mimarisi oluşturmak için ihtiyaç duyarız. Diyelim ki bir sınıftan iki alt sınıf oluşturmak istedik. Bu sınıflar birbiriyle aynı özelliklere ve birbirinden farklı özelliklere sahiptirler. İşte burada OOP devreye girer. Liskov’un yerine geçme prensibi aslında OOP prensiplerinden Polymorphism (Çok biçimlilik) ile yakından ilgilidir. Buna göre türetilmiş sınıflar, alt sınıflarıyla yer değiştirebilmeli ve türetilmiş sınıf ile aynı davranışı sergilemelidir.
Temelde şu kontrolleri sağlamamız  ile yerine geçme prensibine uygun bir kodumuz olduğunu teyit edebiliriz; türetilmiş sınıfta yeni istisnalar oluşmamalıdır, giriş ve dönüş parametreleri değişmemelidir {tip, sıralama ya da sayı olarak} (hatta mümkünse interface ile sınırlandırılmalıdır), sabitler (constants) mümkün mertebe korunmalı ve mümkünse miras alınmalıdır, üst sınıfta yapılan önemli eylemler sürdürülmelidir (örn: db bağlantısı kapatma vs.), üst sınıf içerisinde private tanımlanmış varlıkların değerleri reflection vs. yöntemler ile değiştirilmemeli gerekiyorsa yeni varlıklar oluşturulmalıdır.


## **Liskov Substitution Principle Nasıl Uygulanır ?**

LSP’nin nasıl uygulanabileceğini bir örnekte görelim :
Örneğimizde soyut(abstract) olarak bir **Car** sınıfı tanımlıyoruz. İçerisine **Run** ve **OpenAirConditioning** metotlarını ekliyoruz.

```
namespace LiskovSubstitutionPrinciple {

    public abstract class Car
    {
        public string Run(){
             return "Araba çalıştırıldı.";
        }
        public absract string OpenAirConditioning();
    }
}
```
Kalıtım alınacak **Run** metotu ile araba çalıştırılacak, soyut(abstract) olarak tanımlanmış **OpenAirConditioning** metotu ile de kalıtım alan türe göre klima açılacak.
Ardından **Ferrari** ile **Murat131** somut sınıflarını (concreate) **Car** soyut sınıfından kalıtım yoluyla oluşturuyoruz. Burada dikkatin çekilmesi gereken nokta: **Murat131**’in klima özelliğinin olmamasından dolayı ve soyut(abstract) olarak tanımlanmış metotu override etmek zorunda olduğumuz için ya **NotImplementedException** hatası fırlatılacak yada null geçerek hatanın üzerini örtmüş olacağız.

```
  public class Ferrari : Car{
         public override string OpenAirConditioning(){
             return " Klima açıldı.";
         }
  }
   public class Murat131 : Car{
         public override string OpenAirConditioning(){
             throw new NotImplementedException();
            // return null;
         }
  }

```

Buraya kadar her şey güzel. Murat131’in kliması olsun olmasın ben null geçtim ve hataya engel oldum diye düşünüyoruz. Ne olabilir ki? Evet çok şey olabilir! Eğer büyük bir proje ekibi ile aynı proje üzerinde çalışıyorsak ve günlerden bir gün bir kodu başka bir yazılımcı ihtiyaç duyuyorsa ve şöyle bir şeyler kodlamaya başlarsa:

```
  static void Main(string[] args) {

      Car car = new Ferrari();

      car.Run();
      car.OpenAirConditioning();
      //Sıkıntı yok her şey yolunda.

      car = new Murat131();

      car.Run();
      car.OpenAirConditioning(); // ? problem..   
  }
```
LSP’ye girişteki ilk sözü hemen hatırlayalım tekrar: ***alt sınıflardan oluşan nesnelerin üst sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesini beklemektir.***

Bu durumda Murat131 aynı davranışı sergilememesinden dolayı LSP’ye **uymadığını** söyleyebiliriz. Ayrıca, **OpenAirConditioning** özelliğini temel sınıfımız olan Car sınıfından bir **Interface(arayüz)** aracılığı ile ayırabilir ve ilgili somut sınıfa (concreate class) **implemente** ederek bu problemin önüne geçmiş olabiliriz.  Hemen klima için olan **IAirConditionable** arayüzünü(interface) oluşturalım ve ilgili sınıfa implemente edelim.

```
using System;

namespace LiskovSubstitutionPrinciple {

    public interface IAirConditionable {
        
        string OpenAirConditioning();
    }
     public abstract class Car
    {
        public string Run(){
             return "Araba çalıştırıldı.";
        }
    }
     public class Ferrari : Car, IAirConditionable {
         public string OpenAirConditioning() {
             return " Klima açıldı.";
         }
    }
     public class Murat131 : Car {
     }
}
```
Klima özelliğini sadece Ferrari için implemente ettiğimizden dolayı, hiç kimse Murat131 için **OpenAirConditioning** metoduna erişemeyecek ve herhangi bir problem ile karşılaşılmayacaktır.



