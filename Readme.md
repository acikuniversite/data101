**Hafta 1: Veri Temelleri ve Veritabanı Kavramları**
[Ders Notu](hafta1/README.md)
- **Konu Başlıkları:**
	- **Veri ve Bilgi Arasındaki Fark**
	    - Veri (Data)
	    - Bilgi (Information)
	    - Veri ve Bilgi Arasındaki İlişki
	- **Veritabanı Nedir ve Neden Önemlidir?**
	    - Veritabanı (Database)
	    - Veritabanının Önemi
	    - Veritabanı Yönetim Sistemi (DBMS)
	- **Veritabanı Türleri**
	    - İlişkisel Veritabanları (Relational Databases)
	    - İlişkisel Olmayan Veritabanları (NoSQL Databases)
- **Workshop:**
	- **Senaryo:** Bir küçük işletme, müşteri ve ürün verilerini etkin bir şekilde yönetmek istiyor.
	- **Görev:** Müşteri ve ürün bilgilerini içeren basit bir veri modeli oluşturun. İlişkisel ve NoSQL veritabanlarının bu senaryo için avantajlarını ve dezavantajlarını tartışın.


**Hafta 2: SQL ile İlişkisel Veritabanları**
[Ders Notu](hafta2/README.md)
- **Konu Başlıkları:**
	- **SQL’in Temelleri**
	    - SQL Nedir?
	    - SQL’in Tarihçesi
	    - SQL Standartları
	- **DDL ve DML Komutları**
	    - Veri Tanımlama Dili (DDL)
	    - Veri Manipülasyon Dili (DML)
	- **Temel SQL Sorguları ve İşlemleri**
	- **İleri SQL**
	    - JOIN İşlemleri
	    - Alt Sorgular (Subqueries)
	    - Gruplama ve Toplulaştırma Fonksiyonları
	    - Pencere Fonksiyonları
	    - Görünümler (Views)
	    - Saklı Yordamlar (Stored Procedures)
	    - Tetikleyiciler (Triggers)
	    - İşlemler (Transactions)
	    - İndeksleme ve Performans Optimizasyonu
	    - Kısıtlamalar ve Veri Bütünlüğü
	    - Kullanıcı Tanımlı Fonksiyonlar
- **Workshop:**
	- **Senaryo:** Bir kütüphane, kitap ve üye kayıtlarını dijitalleştirmek istiyor.
	- **Görev:** 
		- Bir ilişkisel veritabanı oluşturun ve “Kitaplar” ve “Üyeler” tablolarını tasarlayın.
		- SQL kullanarak tabloları oluşturun, verileri ekleyin ve güncelleyin.
		- Belirli üyelerin ödünç aldığı kitapları listeleyen sorgular yazın.

**Hafta 3: Veri Modelleme ve ER Diyagramları**
[Ders Notu](hafta3/README.md)
- **Konu Başlıkları:**
	1. **Veri Modelleme Kavramları**
		1. Veri Modellemenin Tanımı ve Önemi
		2. Veri Modelleme Süreci
	2. **ER (Varlık-İlişki) Diyagramları**
		1. ER Diyagramlarının Temel Bileşenleri
		2. Kardinalite ve İlişkiler
	1. **SQL Tasarım Kuralları ve Normalizasyon**
		1. Veritabanı Tasarım Kuralları
		2. Normalizasyon
- **Workshop:**
	- **Senaryo:** Bir online alışveriş sitesi için veri modeli oluşturmak.
	- **Görev:**
	- Müşteriler, siparişler, ürünler ve ödemeleri içeren bir ER diyagramı çizin.
	- Varlıklar arasındaki ilişkileri belirleyin ve kartisiteyi belirtin.


**Hafta 4: NoSQL Veritabanları**
[Ders Notu](hafta4/README.md)
- **Konu Başlıkları:**
	- **NoSQL Nedir ve Ne Zaman Kullanılır?**
	    - NoSQL Nedir?
	    - NoSQL Ne Zaman Kullanılır?
	- **NoSQL Veritabanı Türleri**
	    - Anahtar-Değer Depoları
	    - Belge Tabanlı Veritabanları
	    - Sütun-Ailesi Depoları
	    - Grafik Veritabanları
	- **NoSQL Tasarım Kuralları ve Optimizasyon**
	    - Denormalizasyon
	    - Veri Modelleme Yaklaşımları
	- **İleri NoSQL**
	    - İleri düzey sorgulama işlemleri
	    - Agregasyon çerçevesi
	    - İndeksleme stratejileri
	    - Sharding ve replikasyon
	    - Güvenlik ve yetkilendirme
	    - Veri Modelleme En İyi Uygulamaları
	        - Gömme ve referanslama
	        - Şema tasarım desenleri (Öznitelik, Bucket, Referans, Polymorphic, Hybrid)
	        - Bileşik anahtarlar ve denormalizasyon
	        - Indexed lookup ve join deseni
- **Workshop:**
	- **Senaryo:** Bir sosyal medya uygulaması, kullanıcı profillerini ve gönderilerini depolamak istiyor.
	- **Görev:**
		- MongoDB gibi bir belge tabanlı NoSQL veritabanı kullanarak kullanıcı profilleri ve gönderiler için koleksiyonlar oluşturun.
		- Temel CRUD (Oluşturma, Okuma, Güncelleme, Silme) işlemlerini gerçekleştirin.
		- Kullanıcıların gönderilerini sorgulamak için örnek sorgular yazın.

  
  

**Hafta 5: Veritabanı Tasarımı ve Mimari**
[Ders Notu](hafta5/README.md)
- **Konu Başlıkları:**
	- **Gerçek Dünya Senaryoları Üzerinden Veritabanı Seçimi**
	    - E-Ticaret Uygulaması
	        - Ürün Kataloğu (NoSQL - MongoDB)
	        - Sipariş ve Ödeme İşlemleri (SQL - PostgreSQL)
	    - Sosyal Medya Uygulaması
	        - Kullanıcı Profilleri ve İlişkileri (Grafik Veritabanı - Neo4j)
	        - Gönderiler ve Mesajlaşma (NoSQL - MongoDB)
	        - Finansal İşlemler ve Raporlama (SQL - MySQL)
	    - IoT (Nesnelerin İnterneti) Uygulaması
	        - Zaman Serisi Verileri (NoSQL - InfluxDB veya Cassandra)
	        - Kullanıcı ve Cihaz Yönetimi (SQL - PostgreSQL)
	- **Hibrit Yaklaşımın Uygulanması**
	    - Veri Entegrasyonu ve Senkronizasyon
	    - Performans ve Güvenlik İhtiyaçlarının Karşılanması
	- **Hibrit Yaklaşımın Avantajları ve Dezavantajları**
	- **Hibrit Yaklaşımın Zorlukları ve Çözümleri**
	    - Veri Entegrasyonu
	    - Yönetim Karmaşıklığı
	    - Güvenlik
	    - Maliyet
- **Workshop:**
- **Senaryo:** Bir finans kuruluşu, büyük miktarda işlem verisini hızlı ve güvenli bir şekilde işlemek istiyor.
- **Görev:**
	- Veritabanını normalizasyon kurallarına göre tasarlayın.
	- Sorgu performansını artırmak için hangi alanlarda indeksleme yapacağınızı belirleyin.
	- Veri güvenliği ve yedekleme stratejileri hakkında bir plan hazırlayın.

  

**Hafta 6: Veri Mühendisliği ve ETL Süreçleri**
[Ders Notu](./hafta6.md)
- **Konu Başlıkları:**
	- **Veri Mühendisliğine Giriş**
	- **ETL ve ELT Süreçleri**
	    - ETL ve ELT Nedir?
	    - Extract (Çıkarma) Yöntemleri
	    - Transform (Dönüştürme) Yöntemleri
	    - Load (Yükleme) Yöntemleri
	    - Güncel ETL/ELT Araçları ve Teknolojileri
	- **Zamanlama ve Orkestrasyon Araçları ile N-1 Çalışmak**
	    - Zamanlama ve Orkestrasyon Nedir?
	    - N-1 Çalışmak Nedir?
	    - Orkestrasyon Araçları
	    - Teknik Detaylar ve Kullanım Örnekleri
	- **Veri Entegrasyonu ve Veri Kalitesi Yönetimi**
	    - Veri Entegrasyonu
	    - Veri Kalitesi Yönetimi
	    - Veri Kalitesi Araçları
	- **Büyük Veri ve Büyük Veri Mühendisliği**
	    - Büyük Veri Nedir?
	    - Büyük Veri Teknolojileri
	    - Büyük Veri Mühendisinin Rolü
	    - Güncel Teknolojiler ve Trendler
	- **Veri Ambarı ve Veri Gölü**
	    - Veri Ambarı Nedir?
	    - Veri Gölü Nedir?
	    - Göl Evi (Lakehouse) Mimarisi
	    - Teknolojiler ve Uygulamalar
	- **Veri Güvenliği ve Uyum**
	    - Veri Güvenliği Prensipleri
	    - Yasal Düzenlemeler
	    - Veri Anonimleştirme ve Maskelme Teknikleri
	- **Sonuç ve Öneriler**
	    - Veri Mühendisliği Kariyerine Başlamak İçin Öneriler
	    - Öğrenilecek Teknolojiler ve Sertifikasyonlar
- **Workshop:**
	- **Senaryo:** Farklı kaynaklardan gelen satış verilerini bir veri ambarında toplamak isteyen bir şirket. 
	- **Görev:**
		- Basit bir ETL süreci tasarlayın ve uygulayın.
		- Veri temizleme tekniklerini kullanarak verileri dönüştürün.
		- Veri kalitesini değerlendirmek için metrikler belirleyin.

  

**Hafta 7: Veri Bilimi ve Analitiği**
[Ders Notu](./hafta7)
- **Konu Başlıkları:**
- Veri bilimine giriş
- Temel istatistik ve veri görselleştirme
- Makine öğrenmesine giriş
- **Workshop:**
- **Senaryo:** Bir e-ticaret şirketi, müşteri davranışlarını analiz etmek ve kişiselleştirilmiş öneriler sunmak istiyor.
- **Görev:**
	- Verilen müşteri ve alışveriş verilerini analiz edin.
	- Veri görselleştirme araçları kullanarak bulgularınızı sunun.
	- Basit bir makine öğrenmesi algoritmasıyla ürün önerileri oluşturun.

  

**Hafta 8: Bulut Teknolojileri ve Veri Yönetimi**
[Ders Notu](./hafta8)
- **Konu Başlıkları:**
	- Bulut bilişime giriş
	- Bulutta veritabanı hizmetleri (AWS RDS, Azure SQL Database, Google Cloud SQL)
	- Bulut ve yerel veritabanları arasındaki farklar
- **Workshop:**
- **Senaryo:** Bir startup, uygulamasını ölçeklendirmek için bulut tabanlı veritabanlarına geçmek istiyor.
- **Görev:**
	- AWS, Azure veya Google Cloud platformlarından birini kullanarak bir bulut veritabanı oluşturun.
	- Veritabanınızı buluta taşımanın adımlarını planlayın.
	- Bulutta veri güvenliği ve maliyet optimizasyonu stratejilerini tartışın.