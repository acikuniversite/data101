## **4. İleri NoSQL**
### 4.5 Sharding ve Replikasyon
#### 4.5.1 Sharding
Sharding, büyük veri setlerini yatay olarak **bölümlendirip (partition)** birden fazla sunucuya (shard) dağıtarak veri depolama kapasitesini ve işlem performansını artırmayı hedefleyen bir yöntemdir. Sharding, MongoDB'de **yatay ölçeklenebilirlik** sağlamak için kullanılır.
##### Amaç:
- **Kapasite Artırma:** Büyük veri setlerini tek bir sunucuya sığdıramadığınız durumlarda, veriyi birden fazla sunucuya bölerek depolama kapasitesini artırmak.
- **Yük Dağılımı:** Sorgu ve yazma işlemlerini farklı shard'lar arasında dağıtarak performansı iyileştirmek.
- **Yüksek Erişilebilirlik:** Verilerin farklı fiziksel sunucularda olması, tek bir sunucu arızalandığında veri kaybını önler ve erişilebilirliği artırır.
##### Shard Etkinleştirme

```
sh.enableSharding("sosyalmedya")
```

**Amaç:** Bu komut, "sosyalmedya" adlı veritabanı için sharding'i etkinleştirir. Ancak, bu aşamada henüz herhangi bir koleksiyon shard edilmemiştir.
- **Detaylar:**
    - **Veritabanı:** Sharding, bir veritabanı düzeyinde etkinleştirilir. Bu, o veritabanındaki koleksiyonların sharding ile yönetilebileceği anlamına gelir.
    - **Ön Koşullar:** Sharding'i etkinleştirmek için MongoDB'nin bir sharded cluster (bölümlendirilmiş küme) yapısında çalışıyor olması gerekir. Bu, en az bir **config server** ve bir veya daha fazla **shard** içerir.

**Koleksiyona Shard Anahtarı Eklemek:** Verilerin eşit dağılımı için kritik öneme sahiptir.

```
sh.shardCollection("sosyalmedya.gonderiler", { kullanici_id: 1 })
```

- **Amaç:** "sosyalmedya" veritabanındaki "gonderiler" (yani gönderiler) koleksiyonunu shard etmek için `kullanici_id` alanını shard anahtarı olarak belirler.
- **Detaylar:**
    - **Shard Anahtarı:** Shard anahtarı, verilerin hangi shard'a gideceğini belirleyen bir veya daha fazla alandan oluşan bir yapıdır. İyi bir shard anahtarı, verilerin dengeli bir şekilde dağıtılmasını sağlar.
    - **{ kullanici_id: 1 }:** Bu, `kullanici_id` alanını shard anahtarı olarak belirler ve bu alana göre artan sırada (1 ile) indeks oluşturur.

 **Shard Anahtarı Seçiminin Önemi**

**Shard anahtarı**, verilerin dengeli bir şekilde dağıtılmasını sağlamak için kritik öneme sahiptir. İyi bir shard anahtarı seçimi, performansı artırırken, kötü bir seçim verilerin bazı shard'larda yoğunlaşmasına (hotspot) ve performans sorunlarına yol açabilir.

**İyi Bir Shard Anahtarının Özellikleri:**

1. **Yüksek Kardinalite:** Shard anahtarının yüksek kardinaliteye sahip olması (yani, birçok benzersiz değere sahip olması) verilerin daha dengeli dağıtılmasını sağlar.
2. **Sorgu Uyumluluğu:** Sık kullanılan sorgular shard anahtarı üzerinden yapılmalıdır. Bu, sorguların belirli shard'lara yönlendirilmesini ve daha hızlı yanıt almasını sağlar.
3. **Büyüme Potansiyeli:** Veritabanınız büyüdükçe shard anahtarının da esnek bir şekilde büyümesine izin vermelidir.

**`kullanici_id` Neden İyi Bir Shard Anahtarı Olabilir?**

- **Kardinalite:** Kullanıcı ID'leri genellikle yüksek kardinaliteye sahiptir, yani çok sayıda benzersiz değere sahiptir. Bu, verilerin shard'lar arasında dengeli bir şekilde dağıtılmasını sağlar.
- **Sık Sorgulama:** Sosyal medya uygulamalarında, genellikle belirli bir kullanıcının gönderilerine erişmek için sorgular yapılır. `kullanici_id` üzerinden yapılan bu sorgular, belirli shard'lara yönlendirilerek performansı artırır.

#### 4.5.2 Replikasyon
**Replica Set**, MongoDB'de verilerin yüksek erişilebilirlik ve veri güvenliği sağlamak için birden fazla MongoDB sunucusunun (node) birlikte çalıştığı bir yapıdır. Replica set, birincil (primary) ve ikincil (secondary) düğümlerden oluşur. Birincil düğüm, veritabanına yazma ve okuma işlemlerini gerçekleştirirken, ikincil düğümler birincil düğümün kopyalarını tutar ve gerektiğinde birincil düğümün yerini alabilirler.

 **Replica Set'in Avantajları**
1. **Yüksek Erişilebilirlik:** Birincil düğüm arızalandığında, ikincil düğümler otomatik olarak yeni bir birincil düğüm seçer. Bu sayede sistem kesintisiz çalışmaya devam eder.
2. **Veri Güvenliği:** Verilerin birden fazla kopyasının tutulması, veri kaybını önler.
3. **Okuma Performansını Artırma:** Okuma işlemlerini ikincil düğümlerden gerçekleştirebilir, böylece birincil düğüm üzerindeki yükü azaltabilirsiniz.
4. **Yedekleme Kolaylığı:** İkincil düğümler yedekleme için kullanılabilir.

**Adım Adım Replica Set Oluşturma**
 1. MongoDB'yi Replica Set Olarak Başlatma `mongod --replSet "rs0"`
	- **`mongod`**: MongoDB sunucusunu başlatmak için kullanılan komuttur.
	- **`--replSet "rs0"`**: Bu seçenek, MongoDB sunucusunu bir replica set üyesi olarak başlatır ve replica set'in adını "rs0" olarak belirler.
	  
	  **Açıklama:** Bu komut, MongoDB sunucusunu replica set modunda başlatır. "rs0" adı, replica set'inizi tanımlayan benzersiz bir isimdir. Replica set adı, aynı replica set'e dahil olacak diğer MongoDB sunucuları ile uyumlu olmalıdır.

	**Örnek:** Eğer birincil ve birkaç ikincil düğümünüz varsa, her birini aynı replica set adıyla başlatmanız gerekir:
	
	```
	mongod --replSet "rs0" --port 27017 --dbpath /data/db1
	mongod --replSet "rs0" --port 27018 --dbpath /data/db2
	mongod --replSet "rs0" --port 27019 --dbpath /data/db3
	```
2.  **MongoDB Shell'e Bağlanma:** Replica set yapılandırmasını başlatmak için MongoDB shell'e bağlanın. `mongo --port 27017`
3. **Replica Set'i Başlatma:** MongoDB shell'de aşağıdaki komutu çalıştırarak replica set'i başlatın `rs.initiate()`
### 4.6 Güvenlik ve Yetkilendirme
#### 4.6.1 Kimlik Doğrulama
Yetki Atama:
```
db.createUser({
  user: "uygulamaKullanicisi",
  pwd: "gizliSifre",
  roles: [{ role: "readWrite", db: "sosyalmedya" }]
})
```
4.6.2 Şifreleme
-  Aktarım Sırasında Şifreleme (TLS/SSL):
	- Sunucu ve istemci arasında güvenli iletişim sağlar.
- Veri At Rest Şifreleme:
	- Disk üzerindeki verileri şifreler.

