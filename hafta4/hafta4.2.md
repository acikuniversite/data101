## **3. NoSQL Giriş Seviye**

### 3.1 Docker ile MongoDB Kurulumu

Docker kullanarak MongoDB veritabanını kolayca başlatabilir ve test edebilirsiniz.

```
docker run -d -p 27017:27017 --name mongodb mongo
```

- **`-d`:** Arka planda çalıştırma.
- **`-p 27017:27017`:** Port yönlendirme (host:container).
- **`--name mongodb`:** Container adı.
- **`mongo`:** Kullanılacak imaj.

### 3.2 Mongo Compass ile Veritabanı Yönetimi

Mongo Compass, MongoDB veritabanlarını görsel bir arayüzle yönetmenizi sağlar.

### 3.3 NoSQL İşlemler

#### 3.3.1 Veritabanı ve Koleksiyon Oluşturma

```
use sosyalmedya
db.createCollection("kullanicilar")
```

#### 3.3.2 Veri Ekleme

```
db.kullanicilar.insertOne({
  isim: "Ahmet",
  email: "ahmet@acikunviersite.org",
  yas: 25
})
```

#### 3.3.3 Veri Sorgulama

Tüm Kullanıcıları Getir:

```
db.kullanicilar.find()
```

Belirli Kullanıcıları Getir:

```
db.kullanicilar.find({ isim: "Ahmet" })
```

#### 3.3.4 Veri Güncelleme

```
db.kullanicilar.updateOne(
  { isim: "Ahmet" },
  { $set: { yas: 26 } }
)
```

#### 3.3.5 Veri Silme

```
db.kullanicilar.deleteOne({ isim: "Ahmet" })
```

### 3.3.6 Veri İçinde Dizi Kullanımı

```
db.kullanicilar.insertOne({
  isim: "Mehmet",
  email: "mehmet@acikuniversite.org",
  yas: 30,
  ilgiAlanlari: ["Yüzme", "Müzik", "Kitap Okuma"]
})
```

ve dizi içinde arama yapabiliriz:

```
db.kullanicilar.find({ ilgiAlanlari: "Yüzme" })
```

### 3.3.7 Veri İçinde Döküman Kullanımı

```
db.kullanicilar.insertOne({
  isim: "Ayşe",
  email: "ayse@acikuniversite.org",
  yas: 28,
  adres: {
	il: "İstanbul",
	ilce: "Kadıköy",
	mahalle: "Moda"
  }
})
```

aynı şekilde döküman içinde arama yapabiliriz:

```
db.kullanicilar.find({ "adres.il": "İstanbul" })
```

### 3.3.8 Veri Sıralama ve Sınırlandırma

```
db.kullanicilar.find().sort({ yas: -1 }).limit(2)
```

### 3.3.9 Veri Sayma

```
db.kullanicilar.count()
```

### 3.3.10 Veri İçinde Metin Arama

```
db.kullanicilar.createIndex({ isim: "text" })
db.kullanicilar.find({ $text: { $search: "Ahmet" } })
```

## **4. İleri NoSQL**

### 4.1 İleri Düzey Sorgular

#### 4.1.1 Sorgu Operatörleri

**Karşılaştırma Operatörleri:** `$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`

```
db.kullanicilar.find({ yas: { $gte: 25 } })
```

**Mantıksal Operatörler:** `$and`, `$or`, `$not`

```
db.kullanicilar.find({ $and: [{ yas: { $gte: 25 } }, { yas: { $lte: 30 } }] })
```

**Dizi Operatörleri:** `$in`, `$nin`, `$all`

```
db.kullanicilar.find({ ilgiAlanlari: { $in: ["Yüzme", "Müzik"] } })
```

**Eleman Operatörleri:** `$exists`, `$type`

```
db.kullanicilar.find({ adres: { $exists: true } })
```

#### 4.1.2 Projeksiyon

Hangi alanların getirileceğini belirlemek için projeksiyon kullanılır.

```
db.kullanicilar.find({durum: "aktif"}, {_id: 0, isim: 1, email: 1})
```

### 4.1.3 Metin Arama

```
db.kullanicilar.createIndex({ isim: "text" })
db.kullanicilar.find({ $text: { $search: "Ahmet" } })
```

### 4.1.4 Coğrafi Sorgular

```
db.kullanicilar.createIndex({ konum: "2dsphere" })
db.kullanicilar.find({
  konum: {
	$near: {
	  $geometry: {
		type: "Point",
		coordinates: [29.012, 41.012]
	  },
	  $maxDistance: 1000
	}
  }
})
```