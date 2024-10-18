## **1. NoSQL Nedir ve Ne Zaman Kullanılır?**

### NoSQL Nedir?
- **NoSQL (Not Only SQL):** Geleneksel ilişkisel veritabanlarının dışında kalan ve çeşitli veri modellerini kullanan veritabanı sistemleridir.
- **Özellikleri:**
- **Esnek Şema Yapısı:** Veri modelleri dinamik ve esnektir.
- **Yatay Ölçeklenebilirlik:** Büyük veri hacimleri için uygun.
- **Yüksek Performans:** Hızlı okuma ve yazma işlemleri.
- **Dağıtık Mimari:** Verilerin birden fazla sunucuya dağıtılması.

### Ne Zaman Kullanılır?
- **Büyük Veri Uygulamaları:** Yüksek hacimli verilerin depolanması ve işlenmesi.
- **Gerçek Zamanlı Veri İşleme:** Düşük gecikmeli veri erişimi gereken uygulamalar.
- **Esnek Veri Modelleri:** Dinamik ve değişken veri yapılarıyla çalışırken.
- **Yüksek Trafikli Web ve Mobil Uygulamalar:** Ölçeklenebilirlik ve performans için.

## **2. NoSQL Veritabanı Türleri**
### Anahtar-Değer Depoları
- **Tanım:** Verileri basit bir anahtar ve değer çifti olarak depolar.
- **Kullanım Alanları:** Önbellekleme, oturum yönetimi, basit veri depolama.
- **Örnekler:** Redis, Riak, Amazon DynamoDB.
### Belge Tabanlı Veritabanları
- **Tanım:** Verileri JSON, BSON gibi belge formatlarında saklar.
- **Kullanım Alanları:** Esnek ve karmaşık veri yapılarının depolanması.
- **Örnekler:** MongoDB, CouchDB.
### Sütun-Ailesi Depoları
- **Tanım:** Verileri sütun aileleri halinde depolar, büyük ve dağıtık veri setleri için optimize edilmiştir.
- **Kullanım Alanları:** Büyük veri analizleri, zaman serisi verileri.
- **Örnekler:** Apache Cassandra, HBase.
### Grafik Veritabanları
- **Tanım:** Verileri düğümler ve kenarlar şeklinde depolar, ilişkileri doğrudan temsil eder.
- **Kullanım Alanları:** Sosyal ağlar, öneri sistemleri, bağlantı analizi.
- **Örnekler:** Neo4j, OrientDB.

## **3. NoSQL Tasarım Kuralları ve Optimizasyon**
#### NoSQL Tasarım İlkeleri:
-  **Denormalizasyon:**
	- Performans için **veri tekrarlanmasına izin verilir**
	- Okuma işlemlerini hızlandırmak için veri bir arada tutulur
- **Veri Modelleme Yaklaşımları:**
	- **Belge Tabanlı Modellerde:**
		- İlişkili verileri aynı belgede saklamak
		- Örneğin, bir kullanıcının ve onun gönderilerinin aynı belgede tutulması
	- **Erişim Desenleri:**
		- Uygulamanın veriye nasıl erişeceği tasarımda belirleyici olur
		- Sık kullanılan sorgulara göre veri modelleme

