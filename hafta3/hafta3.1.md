## 1. Veri Modelleme Kavramları

### Veri Modellemenin Tanımı ve Önemi

- **Veri Modelleme Nedir?**
	- Verilerin yapısını, ilişkilerini ve kısıtlamalarını belirlemek için kullanılan bir süreçtir.
	- İş gereksinimlerini teknik tasarımlara dönüştürür.
- **Önemi:**
	- **Anlaşılabilirlik:** Karmaşık veri yapılarının görselleştirilmesini sağlar.
	- **Tutarlılık:** Verilerin tutarlı ve bütünsel bir şekilde yönetilmesine yardımcı olur.
	- **İletişim:** Teknik ve teknik olmayan paydaşlar arasında ortak bir dil oluşturur.
	- **Veritabanı Tasarımı:** Etkin ve optimize edilmiş veritabanı tasarımlarının temelini oluşturur.

### Veri Modelleme Süreci
1. **Gereksinim Analizi:**
	- Bu aşamada, veritabanının hangi iş gereksinimlerine cevap vereceğini belirlemeliyiz. Örneğin, bir e-ticaret sitesi için müşteri bilgileri, siparişler ve ürünler gibi veri ihtiyaçları belirlenir.
	- **Adımlar:**
		- Müşteriler, ürünler, siparişler gibi hangi tür verilerin yönetilmesi gerektiğini belirleyin.
		- Veri gereksinimlerini çıkarın: Her veri parçası nereden geliyor, nasıl kullanılacak?
	- **Örnek**: Bir e-ticaret sitesi için müşteri bilgilerini (ad, soyad, e-posta), ürünleri (isim, fiyat, stok durumu) ve siparişleri (sipariş numarası, ürün, müşteri, tarih) yönetmek gerekiyor.

2. **Kavramsal Modelleme:**
	- Kavramsal modellemede, iş gereksinimlerine uygun şekilde veritabanının temel yapısını belirleriz. Varlıklar (entity), ilişkiler (relationship) ve özellikler (attribute) tanımlanır.
	- **Adımlar**:
		- Temel varlıkları (örneğin, müşteri, ürün, sipariş) belirleyin.
		- Bu varlıkların özelliklerini tanımlayın (örneğin, müşteri: ad, soyad, e-posta; ürün: isim, fiyat, stok durumu).
		- Varlıklar arasındaki ilişkileri tanımlayın (örneğin, bir müşteri birçok sipariş verebilir).
	- **Örnek:**
		- Varlıklar: **Müşteri**, **Ürün**, **Sipariş**
		- İlişkiler: Bir müşteri birden fazla sipariş verebilir (1-N), her sipariş birden fazla üründen oluşabilir (N-N).

3. **Mantıksal Modelleme:**
	- Bu aşamada, kavramsal modeli detaylandırıp mantıksal bir düzeye indiriyoruz. Veri türleri, anahtarlar, kısıtlamalar gibi detaylar eklenir.
	-  **Adımlar**:
		- Her varlık için tablolar oluşturun. Örneğin, "müşteri" tablosu, "ürün" tablosu ve "sipariş" tablosu.
		- Her bir tablo için alan adlarını ve veri türlerini belirleyin (örneğin, müşteri ismi için `VARCHAR`, müşteri numarası için `INT`).
		- Birincil anahtarları ve yabancı anahtarları belirleyin.
	-  **Örnek**:
		- **Müşteri**: ID (INT, PK), ad (VARCHAR), soyad (VARCHAR), e-posta (VARCHAR).
		- **Ürün**: ID (INT, PK), isim (VARCHAR), fiyat (DECIMAL), stok (INT).
		- **Sipariş**: ID (INT, PK), müşteriID (INT, FK), tarih (DATE).

4. **Fiziksel Modelleme:**
	- Bu aşamada, mantıksal modelin fiziksel veritabanı yapısına dönüştürülmesi işlemi yapılır. Fiziksel modelde, veritabanı performansı, indeksler ve veri saklama gibi detaylar eklenir.
	-  **Adımlar**:
		- Veritabanı yönetim sistemine (DBMS) göre modelinizi optimize edin (örneğin, MySQL, PostgreSQL gibi).
		- Performans için indeksler ve diğer optimizasyon tekniklerini belirleyin.
		- Veritabanının fiziksel yapısını, disk alanı ve diğer donanım kaynakları açısından optimize edin.
	- **Örnek:**
		- **Indeksleme**: Sipariş tablosunda müşteriID ve tarih alanlarına indeks ekleyerek sorgu performansını artırabilirsiniz.
		- **Veritabanı Tablolarının Fiziksel Yaratımı**: SQL komutlarıyla tabloları oluşturup veri türlerini ve kısıtlamaları tanımlayabilirsiniz.
```
CREATE TABLE Musteri (
    ID INT PRIMARY KEY,
    Ad VARCHAR(100),
    Soyad VARCHAR(100),
    Eposta VARCHAR(100)
);

CREATE TABLE Urun (
    ID INT PRIMARY KEY,
    Isim VARCHAR(100),
    Fiyat DECIMAL(10, 2),
    Stok INT
);

CREATE TABLE Siparis (
    ID INT PRIMARY KEY,
    MusteriID INT,
    Tarih DATE,
    FOREIGN KEY (MusteriID) REFERENCES Musteri(ID)
);
```

