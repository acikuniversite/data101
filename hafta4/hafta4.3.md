### 4.2 Aggregation Framework

Agregasyon çerçevesi, verileri işlemeye, dönüştürmeye ve hesaplanmış sonuçlar döndürmeye olanak tanır. SQL’deki GROUP
BY, HAVING, JOIN gibi işlemlere benzer kabiliyetler sunar.

#### 4.2.1 Aggregation Pipeline

Agregasyon işlemlerini (sıralama, filtreleme, gruplama, birleştirme) bir dizi işlem adımı (stage) ile gerçekleştirir.
| Operatör | Açıklama |
| --- | --- |
| `$match` | Belirli koşullara uyan belgeleri filtreler. |
| `$project` | Belirli alanları getirir veya yeni alanlar oluşturur. |
| `$group` | Belirli bir alanı gruplar ve toplama işlemleri yapar. |
| `$sort` | Belge sıralamasını değiştirir. |
| `$limit` | Belge sayısını sınırlar. |
| `$skip` | Belge sayısını atlar. |
| `$unwind` | Dizi alanlarını ayrıştırır. |

```
db.kullanicilar.aggregate([
  { $match: { yas: { $gte: 25 } } },
  { $group: { _id: "$il", toplam: { $sum: 1 } } },
  { $sort: { toplam: -1 } }
])
```

### 4.2.2 Projeksiyon Limit ve Skip

Limit ve Skip işlemleri ile sorgu sonuçlarını sınırlayabilir ve atlayabiliriz.

```
db.kullanicilar.aggregate([
  { $project: { isim: 1, email: 1, _id: 0 } },
  { $limit: 2 },
  { $skip: 1 }
])
```

### 4.2.3 Join İşlemleri: $lookup

`$lookup` operatörü, iki koleksiyon arasında birleştirme işlemi yapar, SQL'deki LEFT OUTER JOIN işlemine benzer.

```
db.kullanicilar.aggregate([
  {
	$lookup: {
	  from: "gonderiler",
	  localField: "kullanici_id",
	  foreignField: "kullanici_id",
	  as: "gonderiler"
	}
  },
  { $unwind: "$gonderiler" },
  { $project: { isim: 1, email: 1, "$gonderilen.text": 1 } }
])
```

Uyarı: NoSQL veritabanlarında JOIN işlemleri, SQL veritabanlarına göre daha karmaşıktır ve performans sorunlarına yol
açabilir. Bu nedenle, JOIN işlemlerini dikkatli bir şekilde kullanmalısınız. ve gerektiğinde veri modelinizi yeniden
dönüştürmelisiniz.

### 4.2.4 Performans İpuçları

Aggregation Framework kullanırken performansı artırmak için şu ipuçlarını uygulayabilirsiniz:

- **Index Kullanımı:** Aggregation işlemlerinde sık kullanılan alanlar için index oluşturun.
- **Proje İşlemlerini Sınırlayın:** `$project` işlemlerinde sadece gerekli alanları getirin.
- **Filtreleme İşlemlerini Önce Yapın:** `$match` işlemlerini mümkün olduğunca erken aşamalarda
- **Veri Boyutunu Azaltın:** `$project` işlemleri ile gereksiz alanları çıkarın.
- **Lookup İşlemlerini Dikkatli Kullanın:** `$lookup` işlemlerini gerektiğinde kullanın ve gereksiz birleştirme
  işlemlerinden kesinlikle kaçının.

### 4.3 Indeksleme Stratejileri ve Performans Optimizasyonu

Indexler, veritabanı sorgularının hızını artırmak için kullanılır. Indexler, belirli alanlara hızlı erişim sağlar ve
sorguların daha hızlı çalışmasını sağlar. Ancak, yanlış index kullanımı performans sorunlarına yol açabilir.

#### 4.3.1 Tek Alanlı Index
Basit sorgular için tek alanlı index oluşturulabilir.

```
db.kullanicilar.createIndex({ email: 1 }, { unique: true })
```

#### 4.3.2 Çok Alanlı Index
Birden fazla alan üzerinde index oluşturur.

```
db.kullanicilar.createIndex({ project_id: 1, kullanici_id: -1 })
```

#### 4.3.3 Text Index
Metin arama sorguları için text index oluşturulabilir.

```
db.kullanicilar.createIndex({ isim: "text" })
```

#### 4.3.4 Geospatial Index
Coğrafi sorgular için geospatial index oluşturulabilir.

```
db.kullanicilar.createIndex({ konum: "2dsphere" })
```

#### 4.3.5 Seyrek (Sparse) Index ve Kısmi (Partial) Index
Seyrek ve Kısmı index, daha verimli index oluşturmak için kullanılır.
- Seyrek index, belirli alanlara index oluştururken null veya eksik alanları dikkate almaz.
- Kısmi index, belirli koşullara uyan belgeler üzerinde index oluşturur.

```
db.kullanicilar.createIndex({ email: 1 }, { sparse: true }) // Seyrek Index
```
Yukarıdaki örnekte, email alanı null veya eksik olan belgeler indexlenmez.

```
db.kullanicilar.createIndex({ yas: 1 }, { partialFilterExpression: { yas: { $exists: true } } }) // Kısmi Index
```
Yukarıdaki örnekte, yas alanı olan belgeler üzerinde index oluşturulur.

**Kullanım amacı ne olabilir:**
- Örnek 1: Bir E-ticaret uygulamasında, stokta olmayan ürünlerin indexlenmemesi için seyrek index kullanılabilir.
- Örnek 2: Bir Sosyal Medya uygulamasında, aktif kullanıcılar üzerinde index oluşturmak için kısmi index kullanılabilir.
- Örnek 3: Bir Mesajlaşma uygulamasında, okunmamış mesajlar üzerinde index oluşturmak için kısmi index kullanılabilir.

## **4.4 NoSQL Veritabanlarında Transaction Kavramı**
NoSQL veritabanları geliştirilme felsefesine göre normal şartlarda ACID özelliklerini desteklemez. Ancak, bazı NoSQL
veritabanları (örneğin, MongoDB) belirli durumlarda transaction benzeri işlemleri desteleyebilir.

## **4.5 Sharding ve Replikasyon**
Büyük veri setlerini yönetmek için sharding ve replikasyon teknikleri kullanılır. Sharding, veriyi parçalara bölerek
farklı sunuculara dağıtır ve yükü dengeler. Replikasyon, veriyi yedekleyerek yüksek erişilebilirlik sağlar.

### 4.5.1 Sharding
Sharding, veriyi parçalara bölerek farklı sunuculara dağıtır ve yükü dengeler. Shard anahtarına göre veri parçaları
oluşturulur ve farklı sunuculara dağıtılır. Bu kısımda anahtar seçimi kritik öneme sahiptir.

**Neden:** Eğer yanlış bir anahtar seçilirse, veri dağılımı dengesiz olabilir ve bazı shard'lar diğerlerinden daha fazla
yük alabilir. Bu durumda, performans sorunları ve hatalar ortaya çıkabilir.

```
sh.enableSharding("sosyalmedya")
sh.shardCllection("sosyalmedya.gonderiler", { kullanici_id: 1 })
```

**Soru**: Sosyal Medya uygulamasında postları country alanına göre sharding yapmak istesek bu mantıklı olur mu? Nasıl bir yaklaşım izlemeliyiz?
**Cevap**:
Sosyal medya uygulamasında post’ları ülke (country) alanına göre sharding yapmak ilk bakışta mantıklı gibi görünse de, pratikte bazı problemler doğurabilir. Sharding’in temel amacı, veriyi yatay olarak ölçekleyerek yükü dengeli bir şekilde farklı shard’lara dağıtmaktır. Bu nedenle seçeceğiniz shard key’in veri dağılımında dengesizlik yaratmaması ve sorgu örüntülerinize uygun olması çok önemlidir.
Nedenleri:
1. Düşük Kardinalite:  Ülkelerin sayısı sınırlıdır (genellikle birkaç yüzle sınırlı). Bu durum, shard’lar arasında verinin eşit dağılmamasına neden olabilir. Örneğin, verinizin büyük bölümü birkaç popüler ülkeye (örneğin ABD, Hindistan, Brezilya gibi) aitse, bu ülkeleri temsil eden shard’lar hızlıca aşırı dolup diğer shard’lara oranla çok daha büyük veritabanı boyutlarına ulaşır. Bu, “hotspot” denilen performans darboğazlarına sebep olur.
2. Tek Taraflı Yükleme: Kullanıcıların çoğu belli başlı ülkelerden gelebiliyorsa, shard’ların çoğu boş ya da az veri tutarken birkaç shard çok yoğun veri tutacaktır. Bu dengesiz dağılım, yatay ölçeklenmenin sağladığı avantajları büyük oranda ortadan kaldırır.
3. Sorgu Örüntüleri: Eğer sorgularınız genellikle ülke bazlı değil de, kullanıcı bazlı ya da zamana dayalı (örneğin “son 24 saatteki en popüler postlar” şeklinde) bir desen izliyorsa, country bazlı sharding sorgu performansına da doğrudan katkı sağlamayabilir. Yani veri parçalanmış olsa bile sorgularınızın çoğu yine birden fazla shard’a dağılacak ve “scatter-gather” tipi maliyetli sorgu işlemleri ortaya çıkacaktır.

Daha Mantıklı Yaklaşım ne olabilir:
1. Yüksek Kardinaliteli Bir Alan Seçme:
    - Kullanıcı ID’si, post ID’si veya timestamp gibi yüksek kardinaliteye sahip alanlar sharding için daha uygundur. Örneğin:
    - UserID ile Sharding: Kullanıcı sayısı çok fazlaysa, kullanıcı ID’sini shard key olarak kullanmak, verilerin daha dengeli dağılmasına yardımcı olabilir.
    - Zamana Dayalı Sharding (timestamp): Eğer uygulamanızda veriler zamansal olarak ekleniyorsa (örneğin sürekli artan bir post ID veya timestamp), hashing kullanılarak zamana bağlı alan üzerinde sharding yapmak veriyi eşit dağıtabilir.
2. Bileşik Shard Key Kullanımı:
    - Tek bir alan yerine iki veya daha fazla alanı birleştirerek shard key oluşturmak, daha dengeli bir dağılıma yardımcı olabilir. Örneğin:
    - `{ country: 1, createdAt: 1 }` gibi bir kombinasyon kullanıldığında, sadece ülkelerin değil aynı zamanda zamansal dağılımın da hesaba katılması sağlanır. Ancak burada da country alanının düşük kardinalite sorunu giderilemezse, ek bir alanla dengelemek gerekebilir.
3. Hashed Shard Key Kullanımı:
- Hashed index kullanarak belirli bir alan üzerinde hashing yapmak, veriyi rastgele dağıtır. Örneğin, hashed UserID ya da hashed postID gibi bir shard key veriyi doğal olarak dağıtır ve hotspotları engeller. Bu sayede yüksek trafiğe sahip shard’lar yerine daha dengeli bir dağılım elde edersiniz.
- Örneğin: `{ _id: "hashed" }` şeklinde bir shard key kullanarak, veriyi rastgele dağıtabilirsiniz.
4. Eğer Cografya bazlı sharding yapmak istiyorsanız
    - Eğer amacınız gerçekten coğrafi bazda ayrıştırma yapmaksa, o zaman her ülkeyi değil, kıta veya büyük bölge bazında sharding yaparak bölge sayısını artırmak, ya da ülke bazlı dağıtım yapmak istiyorsanız ülkeleri gruplara ayırarak sharding stratejisinde bir tür “bölgesel” yaklaşım kullanabilirsiniz. Fakat bu durumda bile büyük bir ülkeye denk gelen shard’ın büyümesi sorunu yaşanabilecektir.

Amacımız datayı bölmekten çok bölgesel olarak dağıtmak ise `zone sharding` kullanılabilir. Bu durumda veriyi coğrafi olarak bölmek yerine, veriyi farklı bölgelere da

### 4.5.2 Replikasyon
Replication, veriyi yedekleyerek yüksek erişilebilirlik sağlar. Veritabanı sunucuları arasında veri kopyalama işlemi
gerçekleştirir ve veri kaybını önler. Primary-Secondary replikasyon modeli yaygın olarak kullanılır.

```
mongod --port 27017 --dbpath /data/db1 --replSet rs0 // ile primary sunucu oluşturulur
mongod --port 27018 --dbpath /data/db2 --replSet rs0 // ile secondary sunucu oluşturulur
mongod --port 27019 --dbpath /data/db3 --replSet rs0 // ile secondary sunucu oluşturulur
```

```
rs.initiate({
  _id: "rs0",
  members: [
	{ _id: 0, host: "localhost:27017" },
	{ _id: 1, host: "localhost:27018" },
	{ _id: 2, host: "localhost:27019" }
  ]
})
```

### 4.5.3 Sharding ve Replikasyon Kullanım Senaryoları
Sharding ve replikasyon, büyük veri setlerini yönetmek ve yüksek erişilebilirlik sağlamak için kullanılır. Aşağıda

**Sharding Kullanım Senaryoları:**
- **Yüksek Trafikli Uygulamalar:** E-ticaret, sosyal medya, oyun gibi yüksek trafikli uygulamalar için sharding
  kullanılabilir. Veriyi parçalara bölerek yükü dengeler ve performansı artırır.
- **Coğrafi Dağıtım:** Farklı coğrafi bölgelerdeki kullanıcılar için veriyi coğrafi olarak dağıtmak için sharding
  kullanılabilir. Bu sayede veriye daha hızlı erişim sağlanır.
- **Büyük Veri Setleri:** Büyük veri setlerini yönetmek için sharding kullanılabilir. Veriyi parçalara bölerek
  performansı artırır ve yükü dengeler.
- **Yüksek Erişilebilirlik:** Yüksek erişilebilirlik sağlamak için sharding kullanılabilir. Veriyi farklı sunuculara
  dağıtarak yedekleme yapar.
- **Performans Optimizasyonu:** Performansı artırmak için sharding kullanılabilir. Veriyi parçalara bölerek yükü
  dengeler.
- **Veri Dağıtımı:** Veriyi farklı sunuculara dağıtmak için sharding kullanılabilir. Veriyi parçalara bölerek yükü
  dengeler.

**Replikasyon Kullanım Senaryoları:**
- **Yüksek Değerli Veriler:** Yüksek değerli verileri yedeklemek için replikasyon kullanılabilir. Veriyi farklı sunuculara
  kopyalar.
- **Veri Yedekleme:** Veriyi yedeklemek ve kurtarmak için replikasyon kullanılabilir. Veriyi farklı sunuculara kopyalar.
- **Felaket Kurtarma:** Felaket durumlarında veriyi kurtarmak için replikasyon kullanılabilir. Veriyi farklı sunuculara
  kopyalar.


### 4.6 Güvenlik ve Yetkilendirme
NoSQL veritabanlarında da güvenlik, kimlik doğrulama, yetkilendirme ve şifreleme önemli konulardan biridir.

#### 4.6.1 Kimlik Doğrulama
Kullanıcı oluşturma ve rol bazlı yetkilendirme işlemleri yapılabilir.

```
db.createUser({
  user: "uygulamaHesaabi",
  pwd: "sifre123",
  roles: [{ role: "readWrite", db: "sosyalmedya" }]
})
```

#### 4.6.2 Yetkilendirme
Yetkilendirme işlemleri ile kullanıcıların belirli veritabanları ve koleksiyonlara erişimini kontrol edebilirsiniz.

```
db.grantRolesToUser("uygulamaHesabi", [{ role: "readWrite", db: "sosyalmedya" }])
```

#### 4.6.3 Şifreleme
- Aktarım Sırasında: TLS/SSL protokolü ile veri aktarımını şifreleyebilirsiniz.
- Depolama Sırasında: Veritabanında depolanan verileri şifreleyebilir veya disk tam şifreleme kullanabilirsiniz.
