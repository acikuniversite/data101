## **4. İleri NoSQL**

Bu bölümde, NoSQL veritabanlarının gelişmiş özelliklerini ve MongoDB gibi popüler bir NoSQL veritabanında bu özelliklerin nasıl kullanıldığını inceleyeceğiz. Ele alacağımız konular şunlardır:
- İleri Düzey Sorgulama İşlemleri
- Agregasyon Çerçevesi
- İndeksleme Stratejileri ve Performans Optimizasyonu
- NoSQL Veritabanlarında İşlemler (Transactions)
- Sharding ve Replikasyon
- Güvenlik ve Yetkilendirme
- Veri Modelleme En İyi Uygulamaları
- MapReduce ve Büyük Veri İşleme

### 4.1 İleri Düzey Sorgulama İşlemleri**

NoSQL veritabanları, temel CRUD işlemlerinin ötesinde güçlü sorgulama yetenekleri sunar.

#### 4.1.1 Sorgu Operatörleri**
**Karşılaştırma Operatörleri:** $eq, $ne, $gt, $gte, $lt, $lte

| Operator | Açıklama                |
| -------- | ----------------------- |
| eq       | _equal_                 |
| ne       | _not equal_             |
| gt       | _greater than_          |
| gte      | _greater than_ or equal |
| lt       | _lower then_            |
| lte      | _lower than or equal_   |
```
db.kullanicilar.find({ yas: { $gte: 18 } })
```
**Mantıksal Operatörler:** $and, $or, $not, $nor

| Operator | Açıklama     |
| -------- | ------------ |
| and      | 1 and 1 => 1 |
| or       | 1 or 0 => 1  |
| not      | 1 not => 0   |
| nor      | 1 nor 0 => 1 |

```
db.gonderiler.find({
  $or: [
    { begeni_sayisi: { $gt: 100 } },
    { yorum_sayisi: { $gt: 50 } }
  ]
})
```

 **Eleman Operatörleri:** $exists, $type

| Operator | Açıklama                                                 |
| -------- | -------------------------------------------------------- |
| exists   | `db.gonderiler.find({ resim_url: { $exists: true } })`   |
| type     | `db.collection.find({ "field": { "$type": "string" } })` |
|          | `db.students.find({ "age": { "$type": "int" } })`        |

**Dizi Operatörleri:** $all, $elemMatch, $size

| Operator                | Açıklama                                                                                                                                                                                                                                    |                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| all                     | `$all` operatörü, belirtilen değerlerin **hepsini** içermesi gerektiğini belirtir. Bu sorgu, `courses` dizisinde hem "Mathematics" hem de "Physics" derslerini içeren tüm öğrencileri döndürür.                                             | `db.students.find({ "courses": { "$all": ["Mathematics", "Physics"] } })`                                                  |
| elemMatch               | `$elemMatch` operatörü, dizideki **tek bir** elemanın tüm belirtilen koşulları karşılamasını sağlar. Bir öğrencinin aldıkları dersler arasında, ders adı "Matematik" olan ve kredisi 4 olan bir dersin bulunup bulunmadığını kontrol edelim | `db.students.find({"courses": { "$elemMatch": { "name": "Mathematics", "credits": 4 } }})`                                 |
| size                    | `$size` operatörü, dizinin eleman sayısını kontrol eder ve tam olarak belirtilen sayıya eşit olup olmadığını belirler. Bu sorgu, `courses` dizisinde tam olarak 5 ders bulunan tüm öğrencileri döndürür.                                    | db.students.find({<br>  "courses": { "$size": 5 }<br>})<br>                                                                |
| `$elemMatch` ve `$size` | Bir ürünün varyasyonlarından en az bir tanesinin fiyatı 100'den fazla ve stoğu en az 50 iken, varyasyon sayısının 3 olduğunu kontrol edelim.                                                                                                | ```db.products.find({ "variants": { "$elemMatch": { "price": { "$gt": 100 }, "stock": { "$gte": 50 } }, "$size": 3 } })``` |
| `$all` ve `$size`       | Bir öğrencinin aldığı derslerin hem "Matematik" hem de "Fizik" olduğunu ve toplamda 5 ders aldığını kontrol edelim.                                                                                                                         | ````db.students.find({   "courses": {      "$all": ["Mathematics", "Physics"],     "$size": 5   } })````                   |

#### 4.1.2 Projeksiyon
Sorgu sonuçlarında hangi alanların döndürüleceğini kontrol etmek için kullanılır.
```
db.kullanicilar.find(
  { durum: "aktif" },
  { _id: 0, isim: 1, email: 1 }
)
```

#### 4.1.3 Metin Arama
Tam metin aramaları yapmak için kullanılır.
```
// Index Oluşturma Kısmı
db.gonderiler.createIndex({ icerik: "text" })
// Metin Arama Kısmı
db.gonderiler.find({ $text: { $search: "NoSQL veritabanları" } })
```
#### 4.1.4 Coğrafi Sorgular
Konum tabanlı sorgular için kullanılır.
```
db.mekanlar.createIndex({ konum: "2dsphere" })
db.mekanlar.find({
  konum: {
    $near: {
      $geometry: {
        type: "Point",
        coordinates: [29.012345, 41.012345]
      },
      $maxDistance: 5000
    }
  }
})
```
### 4.2 Agregasyon Çerçevesi
Agregasyon çerçevesi, verileri işlemeye ve hesaplanmış sonuçlar döndürmeye olanak tanır.

**4.2.1 Agregasyon Pipeline**
Bir dizi aşamadan oluşur; her aşama veriyi dönüştürür.
- **Temel Aşamalar:**
	- $match: Verileri filtreler.
	- $group: Verileri belirli bir anahtara göre gruplar.
	- $sort: Verileri sıralar.
	- $project: Her belgeyi yeniden şekillendirir.
**Örnek:**
```
db.gonderiler.aggregate([
  { $match: { begeni_sayisi: { $gt: 50 } } },
  {
    $group: {
      _id: "$kullanici_id",
      toplamBegeni: { $sum: "$begeni_sayisi" },
      gonderiSayisi: { $sum: 1 }
    }
  },
  { $sort: { toplamBegeni: -1 } }
])
```

Bu sorgu ile:
- **50'den fazla beğeni almış gönderileri** bulursunuz.
- Her kullanıcının bu tür gönderilerinden **toplam kaç beğeni aldığını** ve **kaç gönderi yaptığını** öğrenirsiniz.
- Son olarak, **en çok beğeni toplayan kullanıcıları** en üstte olacak şekilde sıralarsınız.

**Adım Adım Açıklama**:
1. **`$match` Aşaması: Filtreleme**
2. **`$group`**: Belirli bir alana göre gruplar ve gruplar üzerinde hesaplamalar yapar.
3. **`$sort`**: Sonuçları belirli bir alana göre sıralar.
4.  **`$project`** operatörü, dökümanların hangi alanlarının dahil edileceğini, hangi alanların dışlanacağını ve yeni alanların nasıl oluşturulacağını belirlemek için kullanılır.
   ```
   db.kullanicilar.aggregate([ { $project: { isim: 1, email: 1, _id: 0 // _id alanını dışla } } ])
   ```
 5. **`$limit`** operatörü, bir bütünleştirme boru hattından sonraki aşamalara gönderilecek doküman sayısını sınırlandırmak için kullanılır. Belirli sayıda dokümanla çalışmak istediğinizde idealdir.
```
const sayfaNumarası = 2;
const sayfaBaşına = 10;

db.kullanicilar.aggregate([
  { $skip: (sayfaNumarası - 1) * sayfaBaşına },  // İlk sayfa için atla
  { $limit: sayfaBaşına }                        // Sayfa başına 10 doküman getir
])
```
6. **`$lookup`** operatörü, bir bütünleştirme boru hattı içinde başka bir koleksiyondan verileri **left outer join** şeklinde birleştirmek için kullanılır. Bu, SQL'deki JOIN işlemine benzer şekilde çalışır ve ilişkili verileri tek bir dokümanda birleştirmenizi sağlar
```
db.calisanlar.aggregate([
  {
    $lookup: {
      from: "departmanlar",
      localField: "departman_id",
      foreignField: "_id",
      as: "calisanDepartmani"
    }
  },
  {
    $unwind: "$calisanDepartmani"  // Tekil departman bilgisi için diziyi aç
  },
  {
    $project: {
      isim: 1,
      departmanAdı: "$calisanDepartmani.ad"
    }
  }
])

```
İki koleksiyonunuz var: `calisanlar` ve `departmanlar`. Her çalışanın bir `departman_id` alanı var. Bu sorgu, her çalışanın departman adını içeren bir `departmanAdı` alanı ekler.

#### Notlar
- `$lookup` operatörü, birleşim yapılacak koleksiyonun büyük olması durumunda performans sorunlarına yol açabilir. Bu nedenle, uygun indekslerin oluşturulduğundan emin olun.
- MongoDB 3.6 ve üzeri sürümlerde, daha gelişmiş `$lookup` özellikleri sunar, örneğin, boru hattı kullanarak daha karmaşık birleşimler yapmak.
### 4.3 İndeksleme Stratejileri ve Performans Optimizasyonu
İndeksler, sorgu performansını artırmak için kritik öneme sahiptir.
**Index Tipleri:**
- **İkincil İndeksler:**
	- Belirli alanlara göre sorgulama yapmak için
- **TTL İndeksleri:**
	- Zaman aşımına uğrayan veriler için (örneğin, oturum verileri)
#### 4.3.1 Tek Alanlı İndeksler
```
db.kullanicilar.createIndex({ email: 1 }, { unique: true })
```
**4.3.2 Bileşik İndeksler**
```
db.gonderiler.createIndex({ kullanici_id: 1, tarih: -1 })
```
**4.3.3 Çoklu Anahtar İndeksleri (Multikey Indexes)**
Dizi alanları üzerinde indeksleme yapar.
```
db.gonderiler.createIndex({ etiketler: 1 })
```
**4.3.4 Metin İndeksleri**
Tam metin aramalarını optimize eder.
```
db.gonderiler.createIndex({ icerik: "text", baslik: "text" })
```
**4.3.5 Geospatial İndeksler**
Konum tabanlı sorguları hızlandırır.
```
db.mekanlar.createIndex({ konum: "2dsphere" })
```
**4.3.6 Seyrek ve Kısmi İndeksler**
• **Seyrek İndeks:**
```
db.users.createIndex(
  { email: 1 },
  { sparse: true }
)
```
Seyrek indeksler, yalnızca belirli bir alana sahip olan dokümanları indeksleyen özel indekslerdir. Yani, indeksin oluşturulduğu alan mevcut olmayan (null veya undefined) dokümanlar bu indekste yer almaz. Bu sayede, indeks boyutu küçülür ve sorgu performansı artar.
- **Kullanım Amacı**
	- **Boş Alanları Dışlamak:** Belirli bir alanın çoğu dokümanda mevcut olmadığı durumlarda, boş (null veya undefined) değerleri indeks dışında bırakarak indeks boyutunu küçültmek.
	- **Performans Artışı:** Daha küçük indeksler, daha hızlı arama ve daha az bellek kullanımı sağlar.
	- **Depolama Alanı Optimizasyonu:** Boş alanların indeks boyutunu artırmasını önler.
-  **Örnek Kullanım**
	- **Senaryo:** `users` koleksiyonunda, bazı kullanıcıların `email` alanına sahip olduğunu, bazılarının ise bu alana sahip olmadığını varsayalım. Sadece `email` alanına sahip olan dokümanları indekslemek istiyorsunuz.
- **Kısmi Indeks:**
```
db.orders.createIndex(
  { orderDate: 1 },
  {
    partialFilterExpression: { status: "active" }
  }
)  
```
  Kısmi indeksler, belirli bir filtre kriterine uyan dokümanları indeksleyen özel indekslerdir. Yani, indeks sadece belirli koşulları sağlayan dokümanları içerir. Bu, daha hedefli ve optimize edilmiş indeksler oluşturmanıza olanak tanır.
-  **Kullanım Amacı**
	- **Hedefli İndeksleme:** Belirli bir koşula uyan dokümanları indeksleyerek, indeks boyutunu küçültmek ve performansı artırmak.
	- **Karmaşık Filtreler:** Daha karmaşık filtreleme koşullarını destekler, bu sayede belirli sorgular için optimize edilmiş indeksler oluşturabilirsiniz.
	- **Depolama Alanı Optimizasyonu:** İndeksin sadece belirli bir alt kümesini içererek depolama alanını verimli kullanır.
- **Örnek Kullanım**
	- **Senaryo:** `orders` koleksiyonunda, sadece `status` alanı "active" olan siparişleri indekslemek istiyorsunuz.

| Özellik                       | Seyrek (Sparse) İndeksler                      | Kısmi (Partial) İndeksler                                            |
|-------------------------------|------------------------------------------------|----------------------------------------------------------------------|
| İndeksleme Kriteri            | Alanın varlığı (null olmayan)                  | Belirli bir filtre koşulu                                            |
| Kullanım Durumu               | Alanın çoğu dokümanda mevcut olmadığı durumlar | Belirli bir koşula uyan dokümanları indekslemek istediğiniz durumlar |
| İndeks Boyutu                 | Daha küçük (boş alanlar indeks dışında)        | Daha küçük (belirli koşula uyan dokümanlar indekslenir)              |
| Filtreleme Esnekliği          | Sadece alanın varlığına göre                   | Karmaşık ve özelleştirilmiş filtre koşulları destekler               |
| Sorgu Uyumu                   | Alanın mevcut olduğu sorgular için uygundur    | Belirli koşullara uyan sorgular için uygundur                        |
| Desteklenen MongoDB Sürümleri | MongoDB 2.6 ve üzeri                           | MongoDB 3.2 ve üzeri                                                 |
