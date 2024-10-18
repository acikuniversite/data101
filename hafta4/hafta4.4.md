## **4. İleri NoSQL**
### 4.7 Veri Modelleme En İyi Uygulamaları
 Veri modelleme, bir veritabanının veriyi nasıl depolayacağını, ilişkilendireceğini ve sorgulayacağını belirleyen kritik bir adımdır. MongoDB gibi NoSQL veritabanlarında, esnek şema yapısı sayesinde veri modelleme stratejileri SQL tabanlı veritabanlarına göre farklılık gösterebilir. Bu bölümde, **gömme** ve **referanslama** yöntemlerini, şema tasarım desenlerini ve bu stratejilerin avantajlarını ve dezavantajlarını ele alacağız.

#### 4.7.1 Gömme ve Referanslama

MongoDB'de veri modelleme yaparken, ilişkili verileri **gömme (embedding)** veya **referanslama (referencing)** yöntemlerinden biriyle saklamayı seçebilirsiniz. Bu iki yaklaşım, veri yapınıza ve uygulamanızın gereksinimlerine bağlı olarak farklı avantajlar sunar.

##### **Gömme (Embedding)**
**Tanım:** Gömme, ilişkili verileri aynı belgede, iç içe yapılar olarak saklama yöntemidir. Bu yöntem, veriyi tek bir yerde toplar ve ilişkili bilgilerin bir arada bulunmasını sağlar.

**Avantajları:**
- **Hızlı Okuma:** İlişkili veriler aynı belgede bulunduğundan, tek bir sorguyla tüm gerekli verilere erişebilirsiniz.
- **Veri Bütünlüğü:** Verinin bütünlüğü korunur, çünkü ilişkili veriler tek bir belge içinde saklanır.
- **Az Sayıda Sorgu:** Daha az sayıda sorgu yapmanız gerekebilir, çünkü ilişkili veriler tek bir belgede bulunur.

**Dezavantajları:**
- **Belge Boyutu Sınırlamaları:** Çok fazla veri gömme, belgelerin boyutunu artırabilir ve MongoDB'nin belge boyutu sınırına (16 MB) yaklaşmanıza neden olabilir.
- **Veri Tekrarı:** Aynı veriyi birden fazla belgede tutmak gerektiğinde, veri tekrarına yol açabilir.
- **Güncelleme Karmaşıklığı:** Gömülü verilerin güncellenmesi daha karmaşık olabilir, özellikle gömülü yapılar derinleştikçe.

**Örnek:** Bir kullanıcı ve arkadaşlarını aynı belgede gömme:
```
{
  "isim": "Ahmet",
  "arkadaslar": [
    { "isim": "Mehmet", "yas": 30 },
    { "isim": "Ayşe", "yas": 25 }
  ]
}

```

**Kullanım Durumları:**
- **Sık Okunan ve Az Güncellenen Veriler:** İlişkili verilerin genellikle birlikte okunduğu ve nadiren güncellendiği durumlarda idealdir.
- **Bağımsız Veri Kümesi:** Arkadaşlar gibi, her bir arkadaşın bağımsız olarak kullanılmadığı durumlarda uygundur.

##### **Referanslama (Referencing)**
**Tanım:** Referanslama, ilişkili verileri ayrı belgelerde veya ayrı koleksiyonlarda tutma yöntemidir. Bu yöntem, belgeler arasında bağlantılar kurarak veri ilişkilerini yönetir.

**Avantajları:**
- **Veri Tekrarını Önler:** Aynı veriyi birden fazla yerde saklamaz, bu da veri tutarlılığını artırır.
- **Esneklik:** Büyük ve karmaşık veri ilişkilerini yönetmek için daha esnektir.
- **Belge Boyutu Yönetimi:** Büyük veri setlerini ayrı koleksiyonlarda tutarak belge boyutu sınırını aşmazsınız.

**Dezavantajları:**
- **Daha Fazla Sorgu Gerektirir:** İlişkili verilere erişmek için birden fazla sorgu yapmanız gerekebilir.
- **Veri Bütünlüğü:** Referanslar yönetilmediğinde veri bütünlüğü sorunları ortaya çıkabilir.
- **Performans:** Join benzeri işlemler MongoDB'de daha yavaştır, bu da performans düşüşüne neden olabilir.

**Örnek:** Bir kullanıcı ve arkadaşlarını referanslama:
```
// kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "arkadaslar": [
    ObjectId("60ad0cedf8d2e30d8c8b4568"),
    ObjectId("60ad0cedf8d2e30d8c8b4569")
  ]
}

// arkadas belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4568"),
  "isim": "Mehmet",
  "yas": 30
}

{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4569"),
  "isim": "Ayşe",
  "yas": 25
}

```
**Kullanım Durumları:**
- **Büyük ve Karmaşık Veri İlişkileri:** Birçok ilişkili veriyi yönetmek ve verilerin birbirleriyle ilişkili olduğu durumlarda uygundur.
- **Sık Güncellenen Veriler:** İlişkili verilerin sık sık güncellendiği durumlarda veri tekrarını önler.

#### 4.7.2 Gömme ve Referanslama Karşılaştırması**

| Özellik           | Gömme (Embedding)                                          | Referanslama (Referencing)                                    |
|-------------------|------------------------------------------------------------|---------------------------------------------------------------|
| Veri Yapısı       | İlişkili veriler aynı belgede iç içe gömülü olarak tutulur | İlişkili veriler ayrı belgelerde veya koleksiyonlarda tutulur |
| Okuma Performansı | Tek sorguyla tüm verilere erişim sağlar                    | Birden fazla sorgu gerekebilir                                |
| Yazma Performansı | İlişkili veriler tek bir belgede güncellenir               | İlişkili veriler ayrı belgelerde güncellenir                  |
| Veri Tekrarı      | Veri tekrarına yol açabilir                                | Veri tekrarı önlenir                                          |
| Veri Bütünlüğü    | Daha kolay korunur                                         | Referanslar yönetilmelidir, veri bütünlüğü karmaşık olabilir  |
| Esneklik          | Daha az esnek                                              | Daha esnek                                                    |
| Belge Boyutu      | Büyük veri setlerinde sorun yaratabilir                    | Büyük veri setleri için uygundur                              |
**4.7.2.1 Gömme ve Referanslama Kullanım Stratejileri**

MongoDB'de en iyi veri modelleme stratejisini belirlemek için, gömme ve referanslama yöntemlerini doğru şekilde kombinlemek önemlidir. Aşağıda, bu stratejilerin nasıl birleştirilebileceğine dair bazı ipuçları ve örnekler bulabilirsiniz.

 **1. İlişkilerin Doğasına Göre Seçim Yapın**
- **Birden Fazla Bir-çok İlişki:** Birçok arkadaş bir kullanıcıya aitken, bir arkadaş birden fazla kullanıcıya ait olabilir. Bu durumda, referanslama daha uygun olabilir.
- **Bire Bir İlişki:** Kullanıcı profil bilgileri gibi, her kullanıcının sadece bir profile sahip olduğu durumlarda gömme tercih edilebilir.

**2. Verilerin Sık Kullanım Şeklini Analiz Edin**
- **Sık Sorgulanan Alanlar:** Eğer ilişkili veriler sıkça birlikte sorgulanıyorsa, gömme daha iyi performans sağlayabilir.
- **Bağımsız Kullanım:** Eğer ilişkili veriler bağımsız olarak sıkça kullanılıyorsa, referanslama daha uygun olabilir.

**3. Veri Güncellemelerinin Frekansını Değerlendirin**
- **Sık Güncellenen Veriler:** İlişkili veriler sık sık güncelleniyorsa, referanslama veri tutarlılığını kolaylaştırır.
- **Nadiren Güncellenen Veriler:** İlişkili veriler nadiren güncelleniyorsa, gömme daha basit bir çözüm olabilir.

#### 4.7.3 Şema Tasarım Desenleri
MongoDB'de şema tasarımı yaparken, belirli desenler kullanmak veri organizasyonunu ve performansı optimize etmenize yardımcı olabilir. Bu bölümde, yaygın olarak kullanılan bazı şema tasarım desenlerini ve bunların ne zaman kullanılacağını inceleyeceğiz.

 **4.7.3.1. Öznitelik Deseni (Attribute Pattern)**
**Tanım:** Öznitelik deseni, dinamik ve esnek alanları saklamak için kullanılır. Bu desen, değişken sayıda özellik içerebilen belgeleri yönetmek için idealdir.

**Kullanım Amacı:**
- **Esnek Veri Yapıları:** Belirli bir alanda farklı sayıda ve türde özellikler saklanması gerektiğinde kullanılır.
- **Dinamik Özellikler:** Ürünler gibi, her bir ürünün farklı özelliklere sahip olabileceği durumlarda uygundur.

**Örnek:**
```
{
  "urunId": 1,
  "ozellikler": {
    "renk": "kırmızı",
    "boyut": "L",
    "agirlik": "200g"
  }
}
```

**Avantajları:**
- **Esneklik:** Belirli bir alanda dinamik veriler saklayabilirsiniz.
- **Sade Yapı:** Belgeler sade ve okunabilir olur.

**Dezavantajları:**
- **Sorgulama Karmaşıklığı:** Dinamik alanlar üzerinde sorgular yapmak daha zor olabilir.
- **Veri Tipi Tutarlılığı:** Farklı belgelerde aynı alanın farklı veri tiplerinde olması

**4.7.3.2. Bucket Deseni**
**Tanım:** Bucket deseni, özellikle zaman serisi verileri gibi büyük miktarda veriyi gruplamak için kullanılır. Bu desen, verileri belirli zaman aralıklarına (örneğin, günlük, haftalık) göre gruplandırır ve her grup için bir belge oluşturur.

**Kullanım Amacı:**
- **Zaman Serisi Verileri:** Sensör verileri, log kayıtları, finansal veriler gibi sürekli akan verilerin yönetimi.
- **Depolama ve Sorgulama Verimliliği:** Büyük veri setlerini daha yönetilebilir parçalara bölerek depolama ve sorgulama performansını artırmak.

**Örnek:**
```
{
  "sensorId": 1,
  "gun": "2023-10-15",
  "degerler": [
    { "saat": "10:00", "deger": 23.5 },
    { "saat": "11:00", "deger": 24.0 },
    // Daha fazla ölçüm değeri
  ]
}
```
**Avantajları:**
- **Veri Yoğunluğunu Azaltma:** Büyük miktarda veriyi yönetilebilir parçalara bölerek depolama alanını optimize eder.
- **Performans:** Belirli zaman aralıkları içinde sorgular yapmak daha hızlı olabilir.

**Dezavantajları:**

- **Veri Ekleme Karmaşıklığı:** Yeni verileri doğru "bucket" içine eklemek için ek mantık gerekebilir.
- **Sorgu Karmaşıklığı:** Belirli bir zaman aralığındaki verileri elde etmek için birden fazla belgeye sorgu yapılması gerekebilir.

**4.7.3.3. Referans Deseni (Reference Pattern)**

**Tanım:** Referans deseni, verileri ayrı belgelerde veya koleksiyonlarda tutarak ilişkili veriler arasında bağlantılar kurma yöntemidir. Bu desen, ilişkili verilerin bağımsız olarak yönetilmesini sağlar.

**Kullanım Amacı:**

- **Veri Tekrarını Önleme:** Aynı veriyi birden fazla yerde saklamamak.
- **Büyük ve Karmaşık Veri İlişkileri:** İlişkili verilerin yönetilmesinde esneklik sağlamak.

**Örnek:**
```
// kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "arkadaslar": [ObjectId("60ad0cedf8d2e30d8c8b4568"), ObjectId("60ad0cedf8d2e30d8c8b4569")]
}

// arkadas belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4568"),
  "isim": "Mehmet",
  "yas": 30
}

{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4569"),
  "isim": "Ayşe",
  "yas": 25
}
```
**Avantajları:**

- **Veri Tutarlılığı:** Verilerin tek bir yerde saklanması, veri tutarlılığını sağlar.
- **Esneklik:** İlişkili verilerin bağımsız olarak yönetilmesine olanak tanır.

**Dezavantajları:**

- **Performans:** İlişkili verilere erişmek için ek sorgular gerekebilir.
- **Sorgu Karmaşıklığı:** İlişkili verilerin bir araya getirilmesi için join benzeri işlemler gerekebilir.

**4.7.3.4. Polymorphic Desen (Polymorphic Pattern)**

**Tanım:** Polymorphic desen, farklı türde belgeleri aynı koleksiyonda saklama yöntemidir. Bu desen, farklı veri türlerinin aynı koleksiyonda yönetilmesini sağlar.


**Kullanım Amacı:**

- **Çeşitli Türde Verileri Yönetme:** Aynı koleksiyon içinde farklı türde verileri saklamak.
- **Esnek Şema:** Belirli bir alanda farklı veri yapılarının bulunması gerektiğinde kullanılır.

**Örnek:**
```
// Kitap belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
  "tur": "kitap",
  "isim": "MongoDB Rehberi",
  "yazar": "Ahmet Yılmaz",
  "sayfaSayisi": 350
}

// Dergi belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456b"),
  "tur": "dergi",
  "isim": "Teknoloji Haftası",
  "yayinevi": "XYZ Yayıncılık",
  "baskiNo": 45
}
```

**Avantajları:**

- **Esneklik:** Farklı türde verileri aynı koleksiyonda yönetebilirsiniz.
- **Kolay Yönetim:** Tek bir koleksiyon üzerinden tüm veri türlerine erişim sağlanır.

**Dezavantajları:**

- **Sorgu Karmaşıklığı:** Belirli bir türdeki verileri sorgulamak için ek filtrelemeler gerekebilir.
- **Veri Tutarsızlığı:** Farklı veri türlerinin aynı koleksiyonda bulunması, veri bütünlüğü sorunlarına yol açabilir.

**4.7.3.5. Hybrid Desen (Hibrit Desen)**

**Tanım:** Hibrit desen, gömme ve referanslama yöntemlerini birleştirerek daha karmaşık veri ilişkilerini yönetme stratejisidir. Bu desen, hem veri bütünlüğünü hem de sorgu performansını optimize etmek için kullanılır.

**Kullanım Amacı:**

- **Karmaşık Veri İlişkileri:** İlişkili verilerin bir kısmını gömme, bir kısmını referanslama.
- **Veri Yönetimi ve Performans Optimizasyonu:** Hem veri bütünlüğünü sağlamak hem de performansı artırmak için kullanılır.

**Örnek:**
```
// Kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "profil": {
    "yas": 30,
    "cinsiyet": "Erkek"
  },
  "arkadaslar": [ObjectId("60ad0cedf8d2e30d8c8b4568"), ObjectId("60ad0cedf8d2e30d8c8b4569")]
}

// Arkadas belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4568"),
  "isim": "Mehmet",
  "yas": 30
}
```
**Avantajları:**

- **Esneklik:** Veri ilişkilerini daha esnek ve optimize bir şekilde yönetir.
- **Veri Bütünlüğü ve Performans:** Hem veri bütünlüğünü sağlar hem de sık kullanılan veriler üzerinde hızlı erişim sağlar.

**Dezavantajları:**

- **Karmaşıklık:** Veri modelinin karmaşıklaşmasına yol açabilir.
- **Yönetim Zorluğu:** Gömme ve referanslama yöntemlerini birlikte kullanmak, veri yönetimini zorlaştırabilir.

#### **4.7.4 Diğer Veri Modelleme En İyi Uygulamaları**

Bu alt bölümde, gömme ve referanslama dışında MongoDB'de etkili veri modelleme için kullanılabilecek diğer bazı en iyi uygulamaları ele alacağız.

**4.7.4.1. Bileşik Anahtarlar (Compound Keys)**

**Tanım:** Bileşik anahtarlar, birden fazla alanı içeren anahtarları ifade eder. Bu, daha karmaşık veri ilişkilerini yönetmek ve sorgu performansını artırmak için kullanılır.

**Kullanım Amacı:**

- **Çok Boyutlu Sorgular:** Birden fazla alana dayalı sorguların optimize edilmesi.
- **Veri Bütünlüğü:** Belirli kombinasyonların benzersiz olmasını sağlamak.

**Örnek:**
```
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456c"),
  "kullanici_id": 1,
  "urun_id": 1001,
  "siparis_tarihi": ISODate("2024-04-27T12:34:56Z"),
  "adet": 2
}
```
**Avantajları:**

- **Sorgu Performansı:** Çok boyutlu sorguların performansını artırır.
- **Benzersizlik:** Belirli alan kombinasyonlarının benzersiz olmasını sağlar.

**Dezavantajları:**

- **İndeks Yönetimi:** Daha fazla indeks oluşturmak, depolama alanını artırabilir ve indeks bakımını zorlaştırabilir.
- **Karmaşık Sorgular:** Bileşik anahtarlar, sorgu yazımını karmaşıklaştırabilir.

 **4.7.4.2. Denormalizasyon (Denormalization)**

**Tanım:** Denormalizasyon, veriyi normalleştirilmiş yapısında gereksiz kopyalar oluşturarak sorgu performansını artırma yöntemidir. Bu, veriyi belirli durumlarda tekrar etmeyi kabul eder.

**Kullanım Amacı:**

- **Okuma Performansını Artırma:** Sıkça yapılan sorgular için veriyi tekrarlayarak sorgu süresini kısaltmak.
- **Sorgu Kolaylığı:** Daha basit ve hızlı sorgular yazmak.

**Örnek:** Bir sipariş belgesinde, kullanıcının ismini ve adresini gömme:
```
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4570"),
  "siparis_id": 5001,
  "kullanici_id": 1,
  "kullanici_isim": "Ahmet",
  "kullanici_adres": "İstanbul",
  "urunler": [
    { "urun_id": 1001, "isim": "Laptop", "adet": 1 },
    { "urun_id": 1002, "isim": "Mouse", "adet": 2 }
  ],
  "siparis_tarihi": ISODate("2024-04-27T12:34:56Z")
}
```
**Avantajları:**

- **Hızlı Okuma:** Sıkça erişilen veriler daha hızlı okunur.
- **Az Sorgu:** Tek bir belgeye erişerek tüm gerekli verilere ulaşabilirsiniz.

**Dezavantajları:**

- **Veri Tutarsızlığı:** Veri tekrar ettiğinden, güncellemeler sırasında tutarsızlık riski artar.
- **Depolama Alanı:** Veriyi tekrar etmek, depolama alanını artırır.

**4.7.4.3. Indexed Lookup ve Join Deseni**

**Tanım:** MongoDB'de veriyi join'lemek için `$lookup` operatörünü kullanarak farklı koleksiyonlardaki verileri ilişkilendirme yöntemidir. Bu desen, ilişkili verilerin birbirine bağlanmasını sağlar.

**Kullanım Amacı:**

- **İlişkili Verilerin Birleştirilmesi:** Farklı koleksiyonlarda bulunan ilişkili verilerin bir araya getirilmesi.
- **Sorgu Esnekliği:** İlişkili veriler üzerinde daha karmaşık sorgular yapma imkanı.

**Örnek:** Bir kullanıcı ve siparişlerini birleştirme:
```
db.kullanicilar.aggregate([
  {
    $lookup: {
      from: "siparisler",
      localField: "_id",
      foreignField: "kullanici_id",
      as: "kullanici_siparisleri"
    }
  }
])
```
**Avantajları:**
- **Esneklik:** Farklı koleksiyonlardaki verileri kolayca birleştirebilirsiniz.
- **Veri Bütünlüğü:** Veriler ayrı koleksiyonlarda tutulduğundan, veri bütünlüğü korunur.

**Dezavantajları:**
- **Performans:** Büyük veri setlerinde performans sorunlarına yol açabilir.
- **Karmaşık Sorgular:** Join işlemleri daha karmaşık ve yavaş olabilir.

#### **4.7.5 Veri Modelleme Stratejilerini Belirleme**

Etkili veri modelleme, uygulamanızın performansını, ölçeklenebilirliğini ve bakım kolaylığını doğrudan etkiler. Aşağıda, veri modelleme stratejilerinizi belirlerken dikkate almanız gereken bazı önemli faktörler bulunmaktadır.

#### **1. Sorgu Analizi Yapın**

- **Sık Kullanılan Sorgular:** Uygulamanızın en sık yaptığı sorguları analiz edin. Hangi alanlar üzerinde sorgular yapılıyor? Sorguların performansını artırmak için hangi veri modelleme stratejisi uygun olabilir?
- **Sorgu Türleri:** Sıkça yapılan sorguların doğası nedir? Örneğin, aralık sorguları mı, yoksa belirli bir kullanıcıya ait verileri mi sorguluyorsunuz?

#### **2. Veri İlişkilerini Anlayın**

- **Bir-çok İlişkiler:** Bir belge ile birden çok başka belge arasındaki ilişkiler nasıl yönetilecek?
- **Çok-çok İlişkiler:** Birçok belge ile birçok başka belge arasındaki ilişkiler nasıl yönetilecek?

#### **3. Veri Büyüklüğünü ve Büyüme Hızını Değerlendirin**

- **Veri Miktarı:** Büyük veri setleri mi yönetiyorsunuz? Bu durumda sharding ve indexing stratejileri nasıl olmalı?
- **Veri Büyüme Hızı:** Verileriniz hızlı bir şekilde mi artıyor? Bu durumda veri modelleme stratejilerinizin esnek ve ölçeklenebilir olması gerekir.

#### **4. Performans Gereksinimlerini Belirleyin**

- **Okuma ve Yazma İhtiyaçları:** Uygulamanız daha çok okuma mı yapıyor yoksa yazma mı? Hangi işlemler daha kritik?
- **Yanıt Süresi:** Hangi sorguların hızlı yanıt vermesi gerekiyor?

#### **5. Veri Bütünlüğü ve Tutarlılığını Sağlayın**

- **Veri Bütünlüğü:** Veri modelleme stratejinizin veri bütünlüğünü nasıl koruyacağını düşünün. Gömme ve referanslama yöntemlerinin veri bütünlüğüne etkisini değerlendirin.
- **Tutarlılık Seviyeleri:** Uygulamanızın veri tutarlılığı gereksinimleri nelerdir?

---

#### **4.7.6 İleri Düzey Veri Modelleme Teknikleri**

Bu alt bölümde, MongoDB'de veri modelleme konusunda daha ileri düzey teknikleri ve stratejileri inceleyeceğiz. Bu teknikler, büyük ve karmaşık veri setlerini yönetirken performansı ve ölçeklenebilirliği optimize etmenize yardımcı olur.

 **4.7.6.1. Materialized Views (Materyalize Görünümler)**

**Tanım:** Materialized Views, sıkça kullanılan ve hesaplanması zor sorguların sonuçlarını önceden hesaplayarak saklama yöntemidir. Bu, sorgu performansını artırmak için kullanılır.

**Kullanım Amacı:**

- **Sık Kullanılan Sorguların Hızlandırılması:** Büyük ve karmaşık sorguların sonuçlarını önceden hesaplayarak hızlı erişim sağlamak.
- **Yük Dağılımı:** Hesaplamaları sorgu sırasında değil, veri ekleme veya güncelleme sırasında yaparak sorgu yükünü azaltmak.

**Örnek:** Satış verilerinin aylık toplamını materialized view olarak saklamak:
```
db.sales.aggregate([
  { $group: { _id: { ay: { $month: "$satis_tarihi" }, yil: { $year: "$satis_tarihi" } }, toplam_satis: { $sum: "$tutar" } } },
  { $out: "monthly_sales_summary" }
])
```
**Avantajları:**

- **Hızlı Sorgular:** Önceden hesaplanmış veriler sayesinde sorgu süresi azalır.
- **Azalan Sunucu Yükü:** Karmaşık hesaplamalar sunucu üzerinde daha az yük oluşturur.

**Dezavantajları:**

- **Veri Güncelliği:** Materialized view'lar veri ekleme veya güncellemeler sırasında güncellenmelidir, bu da ek işlem gerektirir.
- **Depolama Maliyeti:** Ek veri saklama gereksinimi doğurur.

 **4.7.6.2. Sharded Cluster'da Index Yönetimi**

**Tanım:** Sharded cluster'larda, indekslerin doğru yönetimi veri erişimini optimize etmek için kritik öneme sahiptir. Shard anahtarına uygun indeksler oluşturmak, performansı artırır.

**Kullanım Amacı:**

- **Hızlı Erişim:** Shard anahtarına dayalı sorguların hızlı bir şekilde gerçekleştirilmesini sağlamak.
- **Veri Dağılımını Optimize Etmek:** Shard anahtarının kendisi dışında sık kullanılan alanlara göre indeksler oluşturarak veri erişimini hızlandırmak.

**Örnek:** Shard anahtarı `kullanici_id` olan bir koleksiyonda, `created_at` alanına göre indeks oluşturma:
```
db.gonderiler.createIndex({ created_at: 1 })
```
**Avantajları:**

- **Performans Artışı:** Sık kullanılan alanlara dayalı indeksler sorgu performansını artırır.
- **Denge:** İndeksler shard'lar arasında dengeli veri dağılımını destekler.

**Dezavantajları:**

- **İndeks Bakımı:** Sharded cluster'larda indekslerin bakımı daha karmaşık olabilir.
- **Ek Depolama Alanı:** İndeksler ek depolama alanı gerektirir.

**4.7.6.3. Lookup ve Aggregation Kullanarak Veri İlişkilerini Yönetme**

**Tanım:** MongoDB'de `$lookup` operatörü, farklı koleksiyonlardaki verileri birleştirerek ilişkili verilerin bir araya getirilmesini sağlar. Bu, SQL'deki JOIN işlemlerine benzer şekilde çalışır.

**Kullanım Amacı:**

- **İlişkili Verilerin Birleştirilmesi:** Farklı koleksiyonlardaki verileri tek bir sonuç setinde birleştirmek.
- **Veri Bütünlüğü:** İlişkili verilerin mantıksal olarak bir araya getirilmesi.

**Örnek:** Bir kullanıcı ve siparişlerini birleştirme:
```
db.kullanicilar.aggregate([
  {
    $lookup: {
      from: "siparisler",
      localField: "_id",
      foreignField: "kullanici_id",
      as: "kullanici_siparisleri"
    }
  },
  {
    $project: {
      isim: 1,
      "kullanici_siparisleri.siparis_id": 1,
      "kullanici_siparisleri.tutar": 1
    }
  }
])
```
**Avantajları:**

- **Veri Birleştirme:** Farklı koleksiyonlardaki verileri kolayca birleştirir.
- **Esneklik:** Karmaşık veri ilişkilerini yönetmek için esnek bir yöntemdir.

**Dezavantajları:**

- **Performans:** Büyük veri setlerinde performans sorunlarına yol açabilir.
- **Sorgu Karmaşıklığı:** Karmaşık sorguların yazılması ve yönetilmesi zor olabilir.

#### **4.7.7 Denormalizasyon ve Normalizasyon Stratejileri**

MongoDB'de veri modelleme yaparken, veriyi normalize etmek veya denormalize etmek arasındaki dengeyi doğru kurmak önemlidir. Bu stratejiler, veri bütünlüğü, performans ve esneklik açısından farklı avantajlar sunar.

**4.7.7.1. Normalizasyon (Normalization)**
**Tanım:** Normalizasyon, veriyi mantıksal olarak organize etme ve tekrar eden verileri en aza indirgeyerek veri tutarlılığını sağlama yöntemidir. Bu, ilişkili verilerin ayrı belgelerde veya koleksiyonlarda saklanmasını içerir.

**Kullanım Amacı:**

- **Veri Tutarlılığı:** Veri tekrarını önleyerek veri tutarlılığını sağlar.
- **Veri Yönetimi:** Büyük ve karmaşık veri setlerini yönetmek için idealdir.

**Avantajları:**

- **Veri Bütünlüğü:** Tek bir kaynakta veriyi saklayarak tutarlılığı sağlar.
- **Depolama Verimliliği:** Veri tekrarını önler, depolama alanından tasarruf sağlar.

**Dezavantajları:**

- **Daha Fazla Sorgu:** İlişkili verilere erişmek için daha fazla sorgu gerekebilir.
- **Performans:** Join benzeri işlemler nedeniyle sorgu performansı düşebilir.

**Örnek:** Bir kullanıcı ve onun siparişlerini ayrı koleksiyonlarda saklama:
```
// kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet"
}

// siparis belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
  "kullanici_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "siparis_tarihi": ISODate("2024-04-27T12:34:56Z"),
  "tutar": 150.00
}
```

**4.7.7.2. Denormalizasyon (Denormalization)**
**Tanım:** Denormalizasyon, veriyi gereksiz kopyalar oluşturarak sorgu performansını artırma yöntemidir. Bu, veri tekrarını kabul eder ve veriyi daha hızlı erişilebilir hale getirir.

**Kullanım Amacı:**

- **Sorgu Performansını Artırma:** Sıkça yapılan ve karmaşık sorgular için veriyi kopyalayarak hızlı erişim sağlamak.
- **Az Sayıda Sorgu:** Veriyi birden fazla yerde saklayarak tek sorguyla tüm verilere ulaşmak.

**Avantajları:**

- **Hızlı Okuma:** Sıkça erişilen veriler tek bir yerde bulunduğundan hızlı okunur.
- **Az Sorgu:** Veri erişiminde daha az sayıda sorgu yapılmasını sağlar.

**Dezavantajları:**

- **Veri Tutarsızlığı Riski:** Veri tekrar ettiğinden, güncellemelerde tutarsızlık oluşabilir.
- **Depolama Maliyeti:** Veri tekrar ettiğinden, depolama alanı artar.

**Örnek:** Bir kullanıcı belgesinde onun en son sipariş bilgisini gömme:
```
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "son_siparis": {
    "siparis_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
    "siparis_tarihi": ISODate("2024-04-27T12:34:56Z"),
    "tutar": 150.00
  }
}
```
#### **4.7.8 Veri Modelleme ve Sharding Stratejileri**

Veri modelleme stratejileri, sharding stratejileri ile birlikte düşünülmelidir. Veri modellemenin doğru yapılması, sharding'in verimli çalışmasını sağlar. Aşağıda, veri modelleme ve sharding stratejilerini uyumlu hale getirmenin bazı yollarını inceleyeceğiz.

**4.7.8.1. Shard Anahtarının Veri Modeli ile Uyumlu Olması**

Shard anahtarınızın, veri modelinizle uyumlu olması, shard'lar arasında dengeli bir veri dağılımı sağlar ve performansı artırır.

**Örnek:**

- **Kullanıcı Bazlı Veriler:** `kullanici_id` shard anahtarı, kullanıcı bazlı verilerin dengeli dağıtılmasını sağlar.
- **Zaman Bazlı Veriler:** `created_at` shard anahtarı, zaman serisi verilerini yönetmek için kullanılabilir, ancak dikkatlice seçilmelidir.

**4.7.8.2. İndekslerin Shard Anahtarı ile Uyumlu Olması**

Shard anahtarı, verilerin nasıl bölündüğünü belirlediğinden, indekslerin de bu anahtarla uyumlu olması önemlidir.

**Örnek:**
```
db.gonderiler.createIndex({ kullanici_id: 1, created_at: -1 })
```
- Bu indeks, hem shard anahtarı (`kullanici_id`) hem de zaman bilgisi (`created_at`) ile sorguları optimize eder.

**4.7.8.3. Sık Kullanılan Sorgulara Göre Veri Modelleme**

Veri modelleme stratejilerinizi, en sık kullanılan sorgularınıza göre belirleyin. Bu, hem veri modellemede hem de sharding stratejisinde doğru seçim yapmanıza yardımcı olur.

**Örnek:**

- **Sıkça Kullanılan Sorgu:** Kullanıcının tüm gönderilerini almak.
- **Veri Modelleme:** Gönderileri gömme veya shard anahtarı olarak `kullanici_id` kullanma.
- **Sharding Stratejisi:** `kullanici_id` shard anahtarı ile shard etme.

**4.7.8.4. Veri Güncellemelerinin Sharding ve Modelleme ile Entegrasyonu**

Veri güncellemelerinin nasıl yapılacağını ve shard'lar arasındaki etkileşimi planlayın. Gömme ve referanslama stratejilerinin veri güncellemelerine etkisini değerlendirin.

**Örnek:**

- **Gömme Stratejisi:** Gömülü veriler güncellenirken tüm belgeyi yeniden yazmak gerekebilir.
- **Referanslama Stratejisi:** Referans edilen veriler güncellenirken, referansların doğru şekilde yönetilmesi gerekir.

#### **4.7.9 Veri Modelleme İpuçları ve En İyi Uygulamalar**

MongoDB'de etkili veri modelleme için bazı ipuçları ve en iyi uygulamalar şunlardır:

**4.7.9.1. Sorgu Performansını Önceliklendirin**

- **Sıkça Kullanılan Sorgular:** En sık yapılan sorguları belirleyin ve veri modelinizi bu sorgulara göre optimize edin.
- **İndeksleme:** Sık kullanılan alanlara uygun indeksler oluşturun. Shard anahtarını içeren indeksler, shard'lar arasında dengeli veri dağılımını destekler.

**4.7.9.2. Shard Anahtarını Dikkatlice Seçin**

- **Yüksek Kardinalite:** Shard anahtarınızın yüksek kardinaliteye sahip olması, verilerin shard'lar arasında dengeli bir şekilde dağıtılmasını sağlar.
- **Sık Kullanılan Sorgularla Uyumluluk:** Shard anahtarınız, en sık yapılan sorgularla uyumlu olmalıdır.

**4.7.9.3. Sharded ve Replika Set Yapılandırmalarını Optimize Edin**

- **Shard'lar İçin Replika Setleri:** Her shard'ı bir replika seti olarak yapılandırın. Bu, yüksek erişilebilirlik ve veri güvenliği sağlar.
- **Config Servers ve Query Routers:** Config servers ve mongos query routers'ın düzgün çalıştığından emin olun. Bu bileşenler, sharded cluster'ın doğru şekilde çalışmasını sağlar.

**4.7.9.4. Veri Güncellemelerini Optimize Edin**

- **Güncellemelerde Atomic Operasyonlar:** MongoDB, tek bir belgede atomic güncellemeleri destekler. Gömme stratejisinde, bir belgedeki tüm verileri tek bir güncellemeyle değiştirebilirsiniz.
- **Referanslı Verilerde Tutarlılık:** Referanslama stratejisinde, veriler arasında tutarlılığı sağlamak için transaction kullanabilirsiniz (MongoDB 4.0 ve üzeri sürümlerde desteklenir).

**4.7.9.5. Shard Balancer'ı İzleyin ve Optimize Edin**

- **Dengeyi Sağlama:** Shard balancer'ın shard'lar arasında dengeli bir veri dağılımı sağladığından emin olun.
- **Hotspot'ları Önleme:** Balancer, veri yoğunluğunu shard'lar arasında dengeler. Ancak, shard anahtarının yanlış seçilmesi hotspot'lara yol açabilir. Shard anahtarınızı dikkatlice seçerek bu durumu önleyin.

**4.7.9.6. Veri Modelinizi Düzenli Olarak Gözden Geçirin**

- **Performans Analizi:** Veri modelinizi düzenli olarak gözden geçirin ve performans analizleri yapın. Gerekirse, veri modelinizi optimize edin.
- **İndeks Yönetimi:** İndekslerinizi düzenli olarak gözden geçirin ve gereksiz indeksleri kaldırın.

#### **4.7.10 Örnek Senaryolar ve Uygulamalar**

Bu alt bölümde, yukarıda ele alınan veri modelleme stratejilerini gerçek dünya senaryolarında nasıl uygulayabileceğinizi göstermek için bazı örnekler sunacağız.

**Örnek 1: E-Ticaret Uygulaması**

**Senaryo:** Bir e-ticaret platformunda kullanıcılar, ürünler ve siparişler arasında ilişkiler bulunmaktadır. Kullanıcıların siparişleri, ürünlerin kategorilere ait olduğu ve her ürünün birden fazla yorumu olduğu bir yapıya sahiptir.

**Veri Modelleme Stratejisi:**

- **Kullanıcı ve Siparişler:** Kullanıcı belgelerinde siparişleri referanslamak.
- **Ürün ve Yorumlar:** Ürün belgelerinde yorumları gömme.
- **Shard Anahtarı:** Kullanıcı bazlı shard anahtarı (`kullanici_id`).

**Örnek Belgeler:**
```
// Kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "email": "ahmet@example.com",
  "siparisler": [ObjectId("60ad0cedf8d2e30d8c8b456a"), ObjectId("60ad0cedf8d2e30d8c8b456b")]
}

// Siparis belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
  "kullanici_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "urun_id": ObjectId("60ad0cedf8d2e30d8c8b456c"),
  "siparis_tarihi": ISODate("2024-04-27T12:34:56Z"),
  "tutar": 150.00
}

// Urun belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456c"),
  "isim": "Laptop",
  "kategori": "Elektronik",
  "yorumlar": [
    { "isim": "Mehmet", "yorum": "Çok iyi!", "puan": 5 },
    { "isim": "Ayşe", "yorum": "Fiyatı makul.", "puan": 4 }
  ]
}
```
**Sharding ve Replication:**

- **Shard Anahtarı:** `kullanici_id`
- **Replica Set:** Her shard kendi replika setine sahiptir.

**Sorgu Örnekleri:**

1. **Kullanıcının Siparişlerini Getirme:**`
   `db.kullanicilar.find({ "_id": ObjectId("60ad0cedf8d2e30d8c8b4567") }, { "siparisler": 1 })`
2. **Ürünün Yorumlarını Getirme:**
   `db.urunler.find({ "_id": ObjectId("60ad0cedf8d2e30d8c8b456c") }, { "yorumlar": 1 })` 
**Avantajları:**
- **Sıkça Kullanılan Sorguların Optimize Edilmesi:** Kullanıcı bazlı sorgular hızlı bir şekilde gerçekleştirilir.
- **Veri Bütünlüğü:** Yorumlar ürün belgelerinde gömülü olduğundan, yorumlara erişim hızlı ve tutarlıdır.

**Dezavantajları:**

- **Büyük Sipariş Verileri:** Kullanıcıların çok sayıda siparişi olduğunda, sipariş listeleri büyük belgeler oluşturabilir.
- **Yorumların Büyümesi:** Ürün yorumları sürekli arttığında, ürün belgeleri aşırı büyük hale gelebilir.

**Örnek 2: Sosyal Medya Uygulaması**

**Senaryo:** Bir sosyal medya platformunda kullanıcılar, gönderiler, beğeniler ve yorumlar arasında ilişkiler bulunmaktadır. Kullanıcıların gönderileri, beğeniler ve yorumlar ayrı koleksiyonlarda tutulmaktadır.

**Veri Modelleme Stratejisi:**

- **Kullanıcı ve Gönderiler:** Kullanıcı belgelerinde gönderileri referanslamak.
- **Gönderiler ve Beğeniler:** Beğenileri gömmek.
- **Gönderiler ve Yorumlar:** Yorumları referanslamak.
- **Shard Anahtarı:** Gönderi bazlı shard anahtarı (`gonderi_id`).

**Örnek Belgeler:**
```
// Kullanici belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "isim": "Ahmet",
  "email": "ahmet@example.com",
  "gonderiler": [ObjectId("60ad0cedf8d2e30d8c8b456a"), ObjectId("60ad0cedf8d2e30d8c8b456b")]
}

// Gonderi belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
  "kullanici_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "icerik": "Merhaba Dünya!",
  "begeni_sayisi": 120,
  "yorumlar": [ObjectId("60ad0cedf8d2e30d8c8b456c"), ObjectId("60ad0cedf8d2e30d8c8b456d")]
}

// Yorum belgesi
{
  "_id": ObjectId("60ad0cedf8d2e30d8c8b456c"),
  "gonderi_id": ObjectId("60ad0cedf8d2e30d8c8b456a"),
  "kullanici_id": ObjectId("60ad0cedf8d2e30d8c8b4567"),
  "yorum": "Çok güzel bir gönderi!",
  "yorum_tarihi": ISODate("2024-04-27T12:34:56Z")
}
```
**Sharding ve Replication:**

- **Shard Anahtarı:** `gonderi_id`
- **Replica Set:** Her shard kendi replika setine sahiptir.

**Sorgu Örnekleri:**

1. **Gönderinin Yorumlarını Getirme:**
```
db.gonderiler.aggregate([
	{ $match: { "_id": ObjectId("60ad0cedf8d2e30d8c8b456a") } },
	{ $lookup: { from: "yorumlar", localField: "_id", foreignField: "gonderi_id", as: "yorumlar_detay" } },
	{ $project: { "icerik": 1, "yorumlar_detay.yorum": 1 } }
])
```
2. **Bir Kullanıcının Gönderilerini Getirme:**
```
db.kullanicilar.find({ "_id": ObjectId("60ad0cedf8d2e30d8c8b4567") }, { "gonderiler": 1 })   
```

**Avantajları:**

- **Bölümlendirilmiş Veri Yönetimi:** Gönderiler shard anahtarına göre bölündüğü için, veriler dengeli bir şekilde dağıtılır.
- **Yüksek Okuma Performansı:** Beğeniler gömülü olduğu için, beğeni sayısını hızlıca okuyabilirsiniz.

**Dezavantajları:**

- **Yorumların Dağıtımı:** Yorumlar ayrı koleksiyonlarda olduğu için, yorumlara erişim ek sorgular gerektirir.
- **Shard Anahtarının Etkisi:** Shard anahtarı olarak seçilen `gonderi_id`, verilerin shard'lar arasında dengeli dağıtılmasını sağlamalıdır. Aksi takdirde, bazı shard'lar aşırı yüklenebilir.
#### **4.7.11 Veri Modelleme Hataları ve Kaçınma Yolları**

Veri modelleme sürecinde yapılan hatalar, veritabanı performansını, ölçeklenebilirliğini ve bakımını olumsuz etkileyebilir. Aşağıda, MongoDB'de sıkça yapılan veri modelleme hatalarını ve bu hatalardan kaçınma yollarını inceleyeceğiz.

**4.7.11.1. Yanlış Shard Anahtarı Seçimi**

**Hata:** Shard anahtarını yanlış seçmek, verilerin shard'lar arasında dengesiz dağıtılmasına ve hotspot'ların oluşmasına yol açar.

**Kaçınma Yolları:**

- **Yüksek Kardinalite:** Shard anahtarının yüksek kardinaliteye sahip olmasına özen gösterin.
- **Sık Kullanılan Sorgularla Uyumluluk:** Shard anahtarı, en sık yapılan sorgularla uyumlu olmalıdır.
- **Dengeli Veri Dağılımı:** Shard anahtarı, verilerin shard'lar arasında dengeli bir şekilde dağıtılmasını sağlamalıdır.

**4.7.11.2. Aşırı Gömme veya Aşırı Referanslama**

**Hata:**

- **Aşırı Gömme:** Çok fazla veri gömme, belgelerin çok büyük olmasına ve performans sorunlarına yol açabilir.
- **Aşırı Referanslama:** Çok fazla referanslama, veri erişimini yavaşlatabilir ve sorgu karmaşıklığını artırabilir.

**Kaçınma Yolları:**

- **Orta Düzeyde Gömme:** İlişkili verileri gömmeyi gerektiren durumları dikkatlice değerlendirin ve gerektiğinde referanslama kullanın.
- **Optimize Edilmiş Referanslama:** Sadece gerçekten bağımsız olarak kullanılan veriler için referanslama kullanın.

**4.7.11.3. İndekslerin Yanlış Kullanımı**

**Hata:** Yanlış veya eksik indeksler, sorgu performansını olumsuz etkiler ve gereksiz depolama alanı kullanımına yol açar.

**Kaçınma Yolları:**

- **Sık Kullanılan Alanları İndeksleyin:** En sık sorgulanan alanlara uygun indeksler oluşturun.
- **İndekslerin Bakımını Yapın:** Gereksiz indeksleri kaldırın ve mevcut indekslerin optimize edildiğinden emin olun.

**4.7.11.4. Denormalizasyonun Aşırı Kullanımı**

**Hata:** Denormalizasyonu aşırı kullanmak, veri tutarlılığı sorunlarına ve depolama alanı artışına yol açar.

**Kaçınma Yolları:**

- **Sadece Gerektiğinde Denormalize Edin:** Denormalizasyonu sadece performans gereksinimlerini karşılamak için kullanın.
- **Veri Tutarlılığını Sağlayın:** Denormalize edilen verilerin güncellenmesini yönetmek için uygun mekanizmalar kullanın (örneğin, transaction).

**4.7.11.5. Sharded Cluster'ın Yanlış Yapılandırılması**

**Hata:** Shard'ların yanlış yapılandırılması, veri dağılımında dengesizliklere ve performans sorunlarına neden olabilir.

**Kaçınma Yolları:**

- **Doğru Yapılandırma:** Sharded cluster'ınızı doğru bir şekilde yapılandırın ve shard anahtarınızı dikkatlice seçin.
- **Monitor ve Optimize Edin:** Sharded cluster'ınızı sürekli izleyin ve veri dağılımını optimize edin.
