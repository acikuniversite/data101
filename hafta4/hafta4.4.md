## **4. İleri NoSQL**
### 4.7 Veri Modelleme En İyi Uygulamaları
NoSQL veritabanları, şemasız yapısıyla esneklik sunsa da veri modelleme stratejileri performans, ölçeklenebilirlik ve bakım kolaylığı açısından büyük önem taşır.

#### 4.7.1 Gömme ve Referans
- **Gömme (Embedding)**: Veriler arasında bir birlikte kullanım ilişkisi varsa ve veriler çoğunlukla birlikte sorgulanacaksa gömme kullanımı tercih edilir.
  - Örnekler:
    - E-ticaret Senaryosu: Bir sipariş verisi ve bu siparişe ait ürünlerin listesi. Her sipariş, içindeki ürünlerle birlikte tek bir belge olarak saklanabilir. 
    - Blog Yazısı ve Yorumlar: Bir blog yazısı ve altındaki yorumlar, aynı anda sorgulanacak ve güncellenecekse, yorumlar blog yazısının içine gömülebilir.
  - Avantaj: Tüm veriye tek sorguda erişim sağlanır, özellikle okuma ağırlıklı operasyonlarda performansı artırır. Veri tek bir belge içinde olduğu için veriler arasında güçlü bir tutarlılık vardır.
  - Dezavantaj: Belge boyutu artabilir, bu da maksimum belge boyutunu (MongoDB için 16MB) aşma riski yaratabilir. Sık güncellenen veya büyük hacimli alt veriler olduğunda, belgeyi güncellemek daha maliyetli olabilir.
  - Ne zaman Kullanılmalı:
    - Alt veri nadiren güncelleniyorsa veya sadece ana belgeyle birlikte güncelleniyorsa (örneğin, blog yazısı ve yorumları).
    - Veriler sıkça birlikte sorgulanıyorsa (örneğin, sipariş ve siparişe ait ürünler)
    - Veri bağlantı tipi 1:1 veya 1:N ise ve bir veri diğerinin bir parçasıysa, gömme kullanılabilir.

```
db.blogYazilari.insertOne({
    baslik: "Embedding Post",
    icerik: "This is a post with embedded comments.",
    yorumlar: [
      { yazar: "Mehmet", icerik: "Nice post!" },
      { yazar: "Ayşe", icerik: "Great post!" }
    ]
})
```

- **Referans (Referencing)**: İki veri arasında bir ilişki varsa ve bir veri diğerinin bir parçası değilse, bu verileri referans kullanarak birleştirebiliriz. Örneğin, bir blog yazısı ve yorumları arasında bir ilişki varsa, yorumları blog yazısının referansı olarak tutabiliriz. Bu durumda, blog yazısı ve yorumları farklı belgelerde tutulur.
  - Örnekler:
    - Sosyal Ağ Uygulaması: Bir kullanıcı profili ve kullanıcının arkadaş listesi. Kullanıcı profili ile arkadaş listesi ayrı tutulabilir çünkü arkadaş bilgisi genellikle ayrı bir şekilde sorgulanabilir.
    - E-ticaret Senaryosu: Ürünler birden fazla siparişte yer alıyorsa, ürünler ayrı belgeler olarak saklanabilir ve sipariş belgeleri, bu ürünlere referans içerebilir.
  - Avantaj: Belge boyutları küçük tutulur, böylece depolama ve bellek kullanımı daha verimli hale gelir. Tekrarlanan verilerden kaçınılır, bu da veri tutarlılığı sorunlarını azaltır.
  - Dezavantaj: Ek sorgular gerekebilir, bu da karmaşıklığı ve sorgu gecikmesini artırabilir. Büyük veri kümelerinde ilişkisel bütünlüğü sağlamak için uygulama düzeyinde ek iş yükü gerekebilir.
  - Ne zaman Kullanılmalı:
    - Veriler sıkça ayrı sorgulanıyorsa (örneğin, kullanıcı profili ve arkadaş listesi).
    - Veri bağlantı tipi N:M ise ve bir veri diğerinin bir parçası değilse, referans kullanılabilir.
    - Alt veri boyutu büyükse ve sık güncelleniyorsa, referans kullanılabilir.

```
db.sosyalAgKullanicilar.insertOne({
    ad: "Mehmet",
    arkadaslar: [
      ObjectId("5f7b1b3b9b3b3d1b3b3b3b3b"),
      ObjectId("5f7b1b3b9b3b3d1b3b3b3b3c")
    ]
})

db.sosyalAgKullanicilar.insertOne({
    ad: "Ayşe",
    arkadaslar: [
      ObjectId("5f7b1b3b9b3b3d1b3b3b3b3a"),
      ObjectId("5f7b1b3b9b3b3d1b3b3b3b3b")
    ]
})
```

#### 4.7.2 Şema Tasarım Desenleri
MongoDB veri modellemesinde yaygın olarak kullanılan bazı desenler vardır. Her desen, belirli bir kullanım senaryosuna hitap eder.

##### 4.7.3.1 Attribute Pattern
**Tanım**: Esnek sayıda özelliği tek bir belge içinde yönetmek için kullanılır.
**Kullanım**: Ürün özellikleri, kullanıcı tercihlerinin dinamik olarak değişebildiği durumlar.

```
{
  "_id": 1,
  "urunAdi": "Akıllı Telefon",
  "ozellikler": {
    "renk": "kırmızı",
    "bellek": "8GB",
    "kamera": "108MP"
  }
}
```
Avantaj: Şema değişikliklerine karşı esneklik.
Dezavantaj: Sorgularda dinamik alan isimleri kullanımı karmaşıklık yaratabilir.

##### 4.7.3.2 Bucket Pattern
**Tanım**: Zaman serisi veya benzer nitelikteki verileri mantıksal gruplar halinde saklamak.
**Kullanım**: Sensör verileri, log kayıtları, metrikler.


```
{
  "sensorId": 42,
  "gun": "2024-04-10",
  "degerler": [
    { "saat": "10:00", "sicaklik": 23.5 },
    { "saat": "11:00", "sicaklik": 24.0 }
  ]
}
```

**Avantaj:** Büyük veri setlerinde toplu sorguların hızlanması.  
**Dezavantaj:** Güncellemeler ve eklemeler daha karmaşık hale gelebilir.

#### 4.7.3.3 Polymorphic Pattern
**Tanım:** Aynı koleksiyonda farklı yapıda belgeleri saklama.  
**Kullanım Durumu:** Farklı tipte içerik öğeleri (kitap, dergi, blog yazısı) tek bir `icerikler` koleksiyonunda tutulabilir.  
**Avantaj:** Tüm içerik tiplerine tek bir uç noktadan erişim.  
**Dezavantaj:** Sorgularda tip filtrelemesi gerekebilir, veri bütünlüğü kontrolü zorlaşabilir.

#### 4.7.3.4 Referans Pattern
**Tanım:** Verileri ayrı koleksiyonlarda tutup referanslar kullanarak bağlama.  
**Kullanım Durumu:** Çok-çok ilişkiler, büyük boyutlu ilişkili veriler, kullanıcı - yorum, ürün - kategori ilişkileri.  
**Avantaj:** Depolama tasarrufu, veri tekrarının önlenmesi.  
**Dezavantaj:** İlişkili verilere erişirken ek sorgu masrafı.

#### 4.7.3.5 Hybrid Pattern (Hibrit Yapı)
**Tanım:** Hem gömme hem de referanslamayı bir arada kullanmak.  
**Kullanım Durumu:** En sık erişilen verileri göm, geri kalanını referansla. Örneğin bir forum sisteminde, son 5 mesajı konu belgesine göm, daha eski mesajları ayrı bir koleksiyonda tut.  
**Avantaj:** Sık erişilen verilere hızlı erişim, veri artarken sürdürülebilirlik.  
**Dezavantaj:** Karmaşıklık artar, güncellemeler dikkat ister.

### 4.7.4 Denormalizasyon ve Normalizasyon Dengesi
**Normalizasyon:** Geleneksel veri tabanlarından aşina olduğumuz, veri tekrarını en aza indirme yaklaşımıdır.
- Avantaj: Veri bütünlüğü, daha az depolama.
- Dezavantaj: İlişkisel sorgularda performans düşüşü (ek sorgu gerekmesi).
**Denormalizasyon:** Okuma performansını artırmak için veriyi kopyalama ve bir arada tutma stratejisidir.
- Avantaj: Tek sorguyla gereken veriye erişim, hızlı okuma.
- Dezavantaj: Veri tekrarları nedeni ile güncelleme zorluğu, tutarlılığı sağlamak için ek mantık.
**Örnek Senaryo:**
- E-ticaret uygulamasında, sipariş belgesi içerisine müşteri adını ve adresini gömmek (denormalize) sorgu performansını artırır. Ancak müşteri adresi değiştiğinde tüm ilgili sipariş belgelerini güncellemek gerekir. Bunu önlemek için müşteriyi ayrı bir koleksiyonda tutup siparişlere referans vermek (normalize) gerekir; ancak bu kez sorgular `$lookup` ile yavaşlar. En iyi strateji, uygulama gereksinimlerinize göre seçtiğiniz dengedir.

### 4.7.5 Sharding ile Uyumlu Modelleme

Eğer veriniz büyüdükçe sharding kullanacaksanız, veri modelinizin shard anahtarını desteklemesi gerekir.

- Shard anahtarınızı sık sorgulanan ve yüksek kardinaliteye sahip bir alan seçin.
- Veri modelinizi shard anahtarına göre şekillendirin, böylece istenen belgelere tek bir shard üzerinden erişilebilir.

Örneğin, kullanıcı bazlı bir sosyal medya uygulamasında `kullanici_id` shard anahtarı seçilmişse, gönderileri de `kullanici_id` alanıyla partition etmek mantıklıdır. Böylece belirli bir kullanıcının gönderilerini sorgularken tüm shard’ları gezmek yerine tek bir shard üzerinde çalışabilirsiniz.
### 4.7.7 Örnek Senaryolar
1. **Blog Uygulaması:**
    - Yazı ve yorumlar ilişkiniz var. Yorum sayısı çok fazla ve sürekli artıyor.
    - Strateji: Yazı belgesine en son 3 yorumu gömün, tüm yorumları ayrı bir koleksiyonda tutun. Bu sayede yazıya hızlı erişim ve sınırlı yer tutan gömülmüş yorumlar elde ederken, eski yorumlara `$lookup` ile ulaşırsınız.
    - Avantaj: Hızlı okuma, esnek sorgu.
2. **E-Ticaret Ürün Kataloğu:**
    - Her ürünün binlerce özelliği (renk, ebat, marka, vb.) olabilir.
    - Strateji: Attribute pattern kullanarak değişken özellikleri bir `ozellikler` alanında saklayın. Bu sayede yeni özellik eklemek kolaylaşır. Sık sorgulanan kategoriler için ise ayrı bir koleksiyon tutup ürün belgelerinden referans verin.
    - Avantaj: Esnek yapı, kategoriler değiştikçe ürün verisini minimal güncellemeyle yönetme.
3. **Log Analizi ve Zaman Serisi Verileri:**
    - Milyonlarca log girişi sürekli akıyor.
    - Strateji: Bucket pattern ile günlük log verilerini tek bir belgede gruplandırın. Böylece belirli bir günün loglarını sorgulamak daha verimli hale gelir.
    - Avantaj: Zaman bazlı sorgularda performans, depolama optimizasyonu.
---
### 4.7.8 En İyi Uygulamaların Özeti
- **Sorgu Odaklı Tasarım:** En sık yapılan sorgularınıza göre veri modelini şekillendirin.
- **Doğru Denge:** Gömme vs. Referanslama, Normalizasyon vs. Denormalizasyon dengesini uygulama ihtiyaçlarınıza göre belirleyin.
- **Şema Desenlerini Bilin:** Attribute, Bucket, Polymorphic, Reference, Hybrid gibi desenleri ihtiyaçlarınıza göre kullanın.
- **Sharding’i Erken Planlayın:** Shard anahtarınızla uyumlu bir veri modeli kurgulayın.
- **İndeksleri Unutmayın:** Sorgu performansını destekleyecek indeksleri ekleyin.
- **Esneklik vs. Disiplin:** Her ne kadar şemasız bir yapı olsa da, alan adlarında, veri tiplerinde ve dokümantasyonda tutarlılığı elden bırakmayın.
- **Versiyonlama ve Evrim:** Şemanız zamanla değişebilir, buna hazırlıklı olun. Gerekirse belge versiyonlama stratejileri uygulayın.
