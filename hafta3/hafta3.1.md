## **1. Veri Modelleme Kavramları**

### **1.1. Veri Modelleme Nedir? ve Önemi**
**Veri Modelleme Nedir?**
Veri modelleme, verilerin yapısını, ilişkilerini ve kısıtlamalarını belirlemek için kullanılan sistematik bir süreçtir. Bu süreç, iş gereksinimlerini teknik tasarımlara dönüştürerek, veritabanlarının etkin ve verimli bir şekilde yönetilmesini sağlar. Veri modelleme, verilerin nasıl depolanacağını, işleneceğini ve kullanılacağını planlayarak, işletmelerin bilgiye dayalı kararlar almasına katkıda bulunur.

**Veri Modellemenin Önemi:**
- **Anlaşılabilirlik:**
    - Karmaşık veri yapılarının **görselleştirilme**sini sağlayarak, tüm paydaşların veriyi kolayca anlamasına yardımcı olur.
- **Tutarlılık:**
    - Verilerin **tutarlı ve bütünsel bir şekilde yönetilmesi**ni sağlayarak, veri kalitesini artırır.
- **İletişim:**
    - Teknik ve teknik olmayan paydaşlar arasında **ortak bir dil** oluşturur, böylece proje gereksinimleri ve çözümleri daha etkili bir şekilde paylaşılabilir.
- **Veritabanı Tasarımı:**
    - **Etkin ve optimize edilmiş veritabanı** tasarımlarının temelini oluşturarak, performansı ve ölçeklenebilirliği artırır.

### **1.2. Veri Modelleme Süreci**
Veri modelleme süreci, veri sistemlerinin etkin ve verimli bir şekilde tasarlanması için kritik öneme sahiptir. Süreç genellikle dört ana aşamadan oluşur: Gereksinim Analizi, Kavramsal Modelleme, Mantıksal Modelleme ve Fiziksel Modelleme.

#### **1.2.1. Gereksinim Analizi**
**Tanım:** Gereksinim analizi, veri modelleme sürecinin ilk aşamasıdır ve iş gereksinimlerinin belirlenmesini içerir. Bu aşamada, veri ihtiyaçları, veri kaynakları ve iş gereksinimleri tanımlanır.

**Adımlar:**
1. **İş Gereksinimlerinin Toplanması:**
    - Paydaşlarla görüşmeler, toplantılar ve anketler yoluyla iş hedefleri ve ihtiyaçları belirlenir.
2. **Veri Kaynaklarının Belirlenmesi:**
    - Mevcut veri kaynakları, sistemler ve veri akışları analiz edilir.
3. **Fonksiyonel Gereksinimlerin Tanımlanması:**
    - Sistemin gerçekleştirmesi gereken işlemler ve fonksiyonlar detaylandırılır.
4. **Veri Gereksinimlerinin Analizi:**
    - Hangi verilerin toplanacağı, depolanacağı ve işleneceği belirlenir.
5. **Kısıtlamaların ve Varsayımların Belirlenmesi:**
    - Teknik, yasal ve operasyonel kısıtlamalar ile varsayımlar tanımlanır.
6. **Dokümantasyon ve Onay:**
    - Gereksinimler yazılı olarak dokümante edilir ve tüm paydaşların onayı alınır.

**Gerçek Hayat Örneği (C2C Taksi Uygulaması):**
Bir C2C (müşteriden müşteriye) taksi uygulaması geliştirmek isteyen bir girişim, gereksinim analizi aşamasını gerçekleştirir:
- **İş Gereksinimlerini Toplar:**
    - Sürücüler ve yolcular gibi ana paydaşlarla görüşerek, uygulamanın hangi özelliklere sahip olması gerektiğini belirler.
- **Veri Kaynaklarını Belirler:**
    - Kullanıcı kayıtları, seyahat geçmişi, ödeme işlemleri ve değerlendirmeler gibi veri kaynaklarını tespit eder.
- **Fonksiyonel Gereksinimleri Tanımlar:**
    - Kullanıcı kaydı, sürücü ve yolcu eşleştirmesi, gerçek zamanlı konum takibi ve ödeme işlemleri gibi fonksiyonları belirler.
- **Veri Gereksinimlerini Analiz Eder:**
    - Kullanıcı bilgileri, araç detayları, seyahat kayıtları ve ödeme bilgilerinin toplanması gerektiğini saptar.
- **Kısıtlamaları ve Varsayımları Belirler:**
    - Veri güvenliği, gizlilik ve yerel ulaşım düzenlemeleri ile ilgili yasal kısıtlamaları göz önünde bulundurur.
- **Dokümantasyon ve Onay Alır:**
    - Tüm gereksinimleri ayrıntılı bir şekilde dokümante eder ve ilgili paydaşların onayını alır.
#### **1.2.2. Kavramsal Modelleme**

**Tanım:** Kavramsal modelleme, gereksinim analizinde belirlenen iş gereksinimlerini yüksek seviyede görselleştirir. Bu aşamada, veri yapıları ve ilişkileri soyut bir şekilde tanımlanır.

**Adımlar:**

1. **Varlıkların Belirlenmesi:**
    - Sistemdeki temel nesneler veya varlıklar (örneğin, Kullanıcı, Araç, Seyahat) tanımlanır.
2. **İlişkilerin Tanımlanması:**
    - Varlıklar arasındaki ilişkiler (örneğin, Kullanıcı yapar Seyahat) belirlenir.
3. **Özniteliklerin Tanımlanması:**
    - Her varlığın temel özellikleri veya öznitelikleri tanımlanır.
4. **Kavramsal Modelin Oluşturulması:**
    - Varlık-İlişki (ER) diyagramları gibi görsel araçlarla model oluşturulur.
5. **Doğrulama ve Onay:**
    - Model, iş paydaşları ile birlikte gözden geçirilir ve onaylanır.

**Gerçek Hayat Örneği (C2C Taksi Uygulaması):**

- **Varlıkların Belirlenmesi:**
    - Kullanıcı (Sürücü ve Yolcu), Araç, Seyahat, Ödeme
- **İlişkilerin Tanımlanması:**
    - Kullanıcı **kullanır** Araç
    - Kullanıcı **yapar** Seyahat
    - Seyahat **içerir** Ödeme
- **Özniteliklerin Tanımlanması:**
    - **Kullanıcı:** KullanıcıID, İsim, Soyisim, TelefonNumarası, Rol (Sürücü/Yolcu)
    - **Araç:** AraçID, PlakaNo, Marka, Model, Renk, KullanıcıID
    - **Seyahat:** SeyahatID, BaşlangıçKonumu, BitişKonumu, BaşlamaZamanı, BitişZamanı, SürücüID, YolcuID
    - **Ödeme:** ÖdemeID, SeyahatID, Tutar, ÖdemeYöntemi, ÖdemeZamanı
- **Kavramsal Modelin Oluşturulması:**
    - ER diyagramı çizilerek varlıklar ve ilişkileri görselleştirilir.
- **Doğrulama ve Onay:**
    - Model, geliştirici ekip ve paydaşlarla gözden geçirilerek doğrulanır.

#### **1.2.3. Mantıksal Modelleme**

**Tanım:** Mantıksal modelleme, kavramsal modelin daha teknik ve detaylı bir temsilidir. Bu aşamada, veritabanı türünden bağımsız olarak veri yapıları ve ilişkileri detaylandırılır.

**Adımlar:**

1. **Tabloların Oluşturulması:**
    - Varlıklar, tablo olarak tanımlanır.
2. **Alanların ve Veri Tiplerinin Belirlenmesi:**
    - Her tablodaki alanlar ve bunların veri tipleri tanımlanır.
3. **Anahtarların Belirlenmesi:**
    - Birincil anahtarlar (PK) ve yabancı anahtarlar (FK) belirlenir.
4. **İlişkilerin Detaylandırılması:**
    - Tablolar arasındaki ilişkiler ve kardinaliteler netleştirilir.
5. **Normalizasyon:**
    - Veri tekrarı ve tutarsızlıkları önlemek için tablolar normalleştirilir.
6. **İş Kurallarının Uygulanması:**
    - Veri bütünlüğünü sağlamak için kısıtlamalar ve kurallar tanımlanır.
7. **Mantıksal Modelin Dokümantasyonu:**
    - Model detaylı bir şekilde dokümante edilir ve doğrulanır.

**Gerçek Hayat Örneği (C2C Taksi Uygulaması):**

- **Tabloların Oluşturulması:**
    - **Kullanıcılar**, **Araçlar**, **Seyahatler**, **Ödemeler**
- **Alanların ve Veri Tiplerinin Belirlenmesi:**
	- **Kullanıcılar**

| Alan Adı        | Veri Tipi | Açıklama              |
| --------------- | --------- | --------------------- |
| KullanıcıID     | Integer   | PK                    |
| İsim            | Varchar   | Kullanıcının adı      |
| Soyisim         | Varchar   | Kullanıcının soyadı   |
| TelefonNumarası | Varchar   | İletişim numarası     |
| Rol             | Varchar   | 'Sürücü' veya 'Yolcu' |
	- **Araçlar

| Alan Adı    | Veri Tipi | Açıklama        |
| ----------- | --------- | --------------- |
| AraçID      | Integer   | PK              |
| PlakaNo     | Varchar   | Araç plakası    |
| Marka       | Varchar   | Araç markası    |
| Model       | Varchar   | Araç modeli     |
| Renk        | Varchar   | Araç rengi      |
| KullanıcıID | Integer   | FK, Araç sahibi |

- **Seyahatler**
  
| Alan Adı  | Veri Tipi | Açıklama |
| --------- | --------- | -------- |
|SeyahatID|Integer|PK|
|BaşlangıçKonumu|Varchar|Adres veya koordinatlar|
|BitişKonumu|Varchar|Adres veya koordinatlar|
|BaşlamaZamanı|Datetime|Seyahatin başlangıcı|
|BitişZamanı|Datetime|Seyahatin bitişi|
|SürücüID|Integer|FK, Kullanıcılar tablosuna|
|YolcuID|Integer|FK, Kullanıcılar tablosuna|

- **Ödemeler**
  
| Alan Adı     | Veri Tipi | Açıklama                 |
| ------------ | --------- | ------------------------ |
| ÖdemeID      | Integer   | PK                       |
| SeyahatID    | Integer   | FK, Seyahatler tablosuna |
| Tutar        | Decimal   | Ödeme miktarı            |
| ÖdemeYöntemi | Varchar   | Kredi kartı, nakit vs.   |
| ÖdemeZamanı  | Datetime  | Ödemenin yapıldığı zaman |


- **Yorumlar**

| Alan Adı    | Veri Tipi | Açıklama        |
| ----------- | --------- | --------------- |
| YorumID      | Integer   | PK              |
| SeyahatID      |Integer|FK, Seyahatler tablosuna|
| MusteriID      |Integer|FK, Kullanıcı tablosuna|
| Puan      |Integer|0-9 arasına puan ataması|
| Yorum      |Varchar|255 Karakter Sınırlaması|

- **Kuponlar, Kredi Kartları, Firmalar, Kullanıcı Tipleri, Ücretli Hizmetler,

- **Anahtarların Belirlenmesi:**
    - **KullanıcıID**, **AraçID**, **SeyahatID**, **ÖdemeID** birincil anahtarlar.
    - **KullanıcıID** (Araçlar tablosunda) ve **SürücüID**, **YolcuID**, **SeyahatID** yabancı anahtarlar.
- **İlişkilerin Detaylandırılması:**
    - **Kullanıcılar** ve **Araçlar** arasında bire çok ilişki.
    - **Seyahatler** tablosu, **SürücüID** ve **YolcuID** ile **Kullanıcılar** tablosuna bağlanır.
    - **Ödemeler** tablosu, **SeyahatID** ile **Seyahatler** tablosuna bağlanır.
- **Normalizasyon:**
    - Tablolar 3. normal forma uygun olarak düzenlenir.
- **İş Kurallarının Uygulanması:**
    - Örneğin, bir aracın sadece bir kullanıcıya ait olabileceği kısıtlaması.
- **Mantıksal Modelin Dokümantasyonu:**
    - Tüm tablolar, alanlar ve ilişkiler detaylı bir şekilde belgelenir.

#### **1.2.4. Fiziksel Modelleme**
**Tanım:** Fiziksel modelleme, mantıksal modelin belirli bir veritabanı yönetim sistemi (DBMS) üzerinde fiziksel olarak uygulanmasıdır. Bu aşamada, veri depolama yapıları ve performans optimizasyonları dikkate alınır.

**Adımlar:**
1. **Veritabanı Platformunun Seçimi:**
    - Örneğin, MySQL, PostgreSQL, Oracle gibi bir DBMS seçilir.
2. **Fiziksel Tabloların Oluşturulması:**
    - Mantıksal modeldeki tablolar, seçilen DBMS'e özgü özelliklerle tasarlanır.
3. **Veri Tiplerinin Belirlenmesi:**
    - DBMS'e özgü veri tipleri kullanılarak alanlar tanımlanır.
4. **Indekslerin Oluşturulması:**
    - Sorgu performansını artırmak için indeksler tanımlanır.
5. **Güvenlik ve Erişim Kontrollerinin Ayarlanması:**
    - Kullanıcı yetkilendirmeleri ve veri güvenliği için önlemler alınır.
6. **Performans Optimizasyonları:**
    - Partitioning, sharding gibi tekniklerle performans iyileştirmeleri yapılır.
7. **Fiziksel Modelin Uygulanması ve Testi:**
    - Veritabanı oluşturulur ve test verileri ile doğrulama yapılır.

**Gerçek Hayat Örneği (C2C Taksi Uygulaması):**
- **Veritabanı Platformunun Seçimi:**
    - PostgreSQL seçilir.
- **Fiziksel Tabloların Oluşturulması:**
    - Tablolar, PostgreSQL'in özelliklerine göre tasarlanır.
- **Veri Tiplerinin Belirlenmesi:**
- **Kullanıcılar**
```
CREATE TABLE Kullanıcılar (
    KullanıcıID SERIAL PRIMARY KEY,
    İsim VARCHAR(50) NOT NULL,
    Soyisim VARCHAR(50) NOT NULL,
    TelefonNumarası VARCHAR(15) UNIQUE NOT NULL,
    Rol VARCHAR(10) CHECK (Rol IN ('Sürücü', 'Yolcu')) NOT NULL
);
```

- **Seyahatler**
```
CREATE TABLE Seyahatler (
    SeyahatID SERIAL PRIMARY KEY,
    BaşlangıçKonumu POINT NOT NULL,
    BitişKonumu POINT NOT NULL,
    BaşlamaZamanı TIMESTAMP NOT NULL,
    BitişZamanı TIMESTAMP,
    SürücüID INTEGER REFERENCES Kullanıcılar(KullanıcıID),
    YolcuID INTEGER REFERENCES Kullanıcılar(KullanıcıID)
);
```
- **Indekslerin Oluşturulması:**
    - **TelefonNumarası** ve **PlakaNo** alanları üzerinde indeksler oluşturulur.
    - **Seyahatler** tablosunda **SürücüID** ve **YolcuID** alanları için indeksler tanımlanır.
- **Güvenlik ve Erişim Kontrollerinin Ayarlanması:**
    - Kullanıcı rolleri ve yetkilendirmeler belirlenir.
    - Hassas verilere erişim kısıtlanır.
- **Performans Optimizasyonları:**
    - Sık kullanılan sorgular için ek indeksler oluşturulur.
    - Büyük tablolar için partitioning uygulanabilir.
- **Fiziksel Modelin Uygulanması ve Testi:**
    - Veritabanı sunucusunda tablolar oluşturulur.
    - Test verileri yüklenerek sistemin düzgün çalışıp çalışmadığı kontrol edilir.
### **1.3. Veri Modelleme Araçları ve Teknolojileri**
Veri modelleme sürecinde kullanılan çeşitli araçlar ve teknolojiler vardır. Bu araçlar, veri modellemenin her aşamasını kolaylaştırır ve veritabanı tasarımını daha verimli hale getirir.

#### **1.3.1. Veri Modelleme Araçları**
- **ER/Studio:** Karmaşık veri modellerini görselleştirmek için güçlü bir araçtır.
- **PowerDesigner:** Veri mimarisi ve iş süreçlerini modellemek için kullanılır.
- **Lucidchart:** Bulut tabanlı, kullanıcı dostu diyagram oluşturma aracı.
- **MySQL Workbench:** MySQL veritabanları için entegre bir modelleme aracı.
- **Microsoft Visio:** Genel amaçlı diyagram oluşturma aracı, veri modelleme için de kullanılabilir.

#### **1.3.2. Veri Modelleme Teknikleri**
- **Yıldız Şeması (Star Schema):**
    - Merkezi bir gerçek tablo (fact table) ve etrafını saran boyut tablolarından oluşur.
    - Basit ve anlaşılır yapısıyla hızlı sorgulara olanak tanır.
- **Kar Tanesi Şeması (Snowflake Schema):**
    - Yıldız şemasının normalleştirilmiş hali; boyut tabloları daha fazla alt tabloya ayrılır.
    - Veri tutarlılığını artırırken, karmaşıklığı da artırır.
- **Normallendirme:**
    - Veri tekrarını azaltmak ve veri bütünlüğünü sağlamak için tabloların bölünmesi sürecidir.
    - İlk normal form (1NF) ile beşinci normal form (5NF) arasında farklı seviyeler bulunur.

### **1.4. Veri Modelleme Örnek Vakalar**
#### **1.4.1. E-Ticaret Sitesi Veri Modelleme**
**Senaryo:** Bir e-ticaret sitesi, müşteri bilgilerini, ürünleri ve siparişleri yönetmek istiyor. Bu verilerin etkili bir şekilde yönetilmesi için veri modelleme süreci uygulanacaktır.

**Veri Modelleme Aşamaları:**
1. **Gereksinim Analizi:**
    - **Veri İhtiyaçları:**
        - **Müşteri:** Ad, soyad, e-posta, adres.
        - **Ürün:** İsim, fiyat, stok durumu, kategori.
        - **Sipariş:** Sipariş numarası, müşteri ID, ürün ID, miktar, tarih.
2. **Kavramsal Modelleme:**
    - **Varlıklar:**
        - **Müşteri**, **Ürün**, **Sipariş**
    - **İlişkiler:**
        - Bir müşteri birçok sipariş verebilir (1-N).
        - Bir sipariş birçok ürünü içerebilir ve bir ürün birçok siparişte yer alabilir (N-N).
3. **Mantıksal Modelleme:**
    - **Tabloların Oluşturulması:**
        - **Müşteri Tablosu:** ID (INT, PK), Ad (VARCHAR), Soyad (VARCHAR), Eposta (VARCHAR)
        - **Ürün Tablosu:** ID (INT, PK), Isim (VARCHAR), Fiyat (DECIMAL), Stok (INT), Kategori (VARCHAR)
        - **Sipariş Tablosu:** ID (INT, PK), MusteriID (INT, FK), Tarih (DATE)
        - **Siparis_Urun Tablosu:** SiparisID (INT, FK), UrunID (INT, FK), Miktar (INT)
4. **Fiziksel Modelleme:**
**Tabloların Oluşturulması ve İndeksleme**
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
    Stok INT,
    Kategori VARCHAR(50)
);

CREATE TABLE Siparis (
    ID INT PRIMARY KEY,
    MusteriID INT,
    Tarih DATE,
    FOREIGN KEY (MusteriID) REFERENCES Musteri(ID)
);

CREATE TABLE Siparis_Urun (
    SiparisID INT,
    UrunID INT,
    Miktar INT,
    PRIMARY KEY (SiparisID, UrunID),
    FOREIGN KEY (SiparisID) REFERENCES Siparis(ID),
    FOREIGN KEY (UrunID) REFERENCES Urun(ID)
);

-- İndeksleme
CREATE INDEX idx_MusteriID ON Siparis(MusteriID);
CREATE INDEX idx_Tarih ON Siparis(Tarih);
CREATE INDEX idx_UrunID ON Siparis_Urun(UrunID);
```

#### **1.4.2. Sağlık Sektörü Veri Modelleme**
**Senaryo:** Bir hastane, hasta bilgilerini, doktorları, randevuları ve tedavi süreçlerini yönetmek istiyor. Veri modelleme süreci, bu bilgilerin etkin bir şekilde yönetilmesini sağlayacaktır.

**Veri Modelleme Aşamaları:**
1. **Gereksinim Analizi:**
    - **Veri İhtiyaçları:**
        - **Hasta:** Hasta ID, Ad, Soyad, Doğum Tarihi, Cinsiyet, İletişim Bilgileri.
        - **Doktor:** Doktor ID, Ad, Soyad, Branş, İletişim Bilgileri.
        - **Randevu:** Randevu ID, Hasta ID, Doktor ID, Tarih, Saat.
        - **Tedavi:** Tedavi ID, Randevu ID, Tedavi Detayları, İlaç Bilgileri.
2. **Kavramsal Modelleme:**
    - **Varlıklar:**
        - **Hasta**, **Doktor**, **Randevu**, **Tedavi**
    - **İlişkiler:**
        - Bir hasta birçok randevu alabilir (1-N).
        - Bir doktor birçok randevu verebilir (1-N).
        - Her randevu birçok tedavi içerebilir (1-N).
3. **Mantıksal Modelleme:**
    - **Tabloların Oluşturulması:**
        - **Hasta Tablosu:** ID (INT, PK), Ad (VARCHAR), Soyad (VARCHAR), DogumTarihi (DATE), Cinsiyet (VARCHAR), Iletisim (VARCHAR)
        - **Doktor Tablosu:** ID (INT, PK), Ad (VARCHAR), Soyad (VARCHAR), Brans (VARCHAR), Iletisim (VARCHAR)
        - **Randevu Tablosu:** ID (INT, PK), HastaID (INT, FK), DoktorID (INT, FK), Tarih (DATE), Saat (TIME)
        - **Tedavi Tablosu:** ID (INT, PK), RandevuID (INT, FK), TedaviDetaylari (TEXT), IlacBilgileri (TEXT)
4. **Fiziksel Modelleme:**
    - **Tabloların Oluşturulması ve İndeksleme:**
```
CREATE TABLE Hasta (
    ID INT PRIMARY KEY,
    Ad VARCHAR(100),
    Soyad VARCHAR(100),
    DogumTarihi DATE,
    Cinsiyet VARCHAR(10),
    Iletisim VARCHAR(100)
);

CREATE TABLE Doktor (
    ID INT PRIMARY KEY,
    Ad VARCHAR(100),
    Soyad VARCHAR(100),
    Brans VARCHAR(50),
    Iletisim VARCHAR(100)
);

CREATE TABLE Randevu (
    ID INT PRIMARY KEY,
    HastaID INT,
    DoktorID INT,
    Tarih DATE,
    Saat TIME,
    FOREIGN KEY (HastaID) REFERENCES Hasta(ID),
    FOREIGN KEY (DoktorID) REFERENCES Doktor(ID)
);

CREATE TABLE Tedavi (
    ID INT PRIMARY KEY,
    RandevuID INT,
    TedaviDetaylari TEXT,
    IlacBilgileri TEXT,
    FOREIGN KEY (RandevuID) REFERENCES Randevu(ID)
);

-- İndeksleme
CREATE INDEX idx_HastaID ON Randevu(HastaID);
CREATE INDEX idx_DoktorID ON Randevu(DoktorID);
CREATE INDEX idx_RandevuID ON Tedavi(RandevuID);
```

**Sonuç:** Bu veri modeli, hastanenin hasta, doktor, randevu ve tedavi verilerini etkili bir şekilde yönetmesini sağlar. İlişkilerin doğru tanımlanması, veri bütünlüğünü ve erişim performansını artırır.