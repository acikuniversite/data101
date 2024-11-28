## **3. SQL Tasarım Kuralları ve Normalizasyon**

Veritabanı tasarımı, verilerin etkin bir şekilde depolanması, yönetilmesi ve erişilmesi için kritik bir rol oynar. İyi bir veritabanı tasarımı, veri bütünlüğünü korur, performansı artırır ve bakım maliyetlerini azaltır. Bu bölümde, SQL tasarım kuralları ve normalizasyon kavramlarını detaylı bir şekilde ele alacağız.

### **3.1. Veritabanı Tasarım Kuralları**

Veritabanı tasarımında dikkate alınması gereken temel kurallar şunlardır:

#### **3.1.1. Veri Bütünlüğü**

Veri bütünlüğü, verilerin doğruluğunu ve tutarlılığını korumak için uygulanan kısıtlamaları ifade eder. Veri bütünlüğünü sağlamak için aşağıdaki unsurlar kullanılır:

- **Birincil Anahtarlar (Primary Keys):**
    
    - Her tabloda, satırları benzersiz bir şekilde tanımlayan bir birincil anahtar olmalıdır.
    - **Örnek (C2C Taksi Uygulaması):**
        - **Kullanıcı** tablosunda `KullanıcıID` birincil anahtar olarak kullanılır.
        - **Araç** tablosunda `AraçID` birincil anahtar olarak kullanılır.
- **Yabancı Anahtarlar (Foreign Keys):**
    
    - Tablolar arasındaki ilişkileri tanımlamak için kullanılır.
    - Yabancı anahtarlar, başka bir tablodaki birincil anahtara referans verir.
    - **Örnek (C2C Taksi Uygulaması):**
        - **Araç** tablosunda `KullanıcıID`, **Kullanıcı** tablosundaki `KullanıcıID`ye referans veren bir yabancı anahtardır.
        - **Seyahat** tablosunda `SürücüID` ve `YolcuID`, **Kullanıcı** tablosundaki `KullanıcıID`ye referans verir.
- **Benzersizlik ve Doğruluk Kısıtlamaları:**
    
    - **UNIQUE** kısıtlamaları, bir sütundaki değerlerin benzersiz olmasını sağlar.
        - **Örnek:** **Kullanıcı** tablosunda `TelefonNumarası` sütunu için **UNIQUE** kısıtlaması uygulanarak, her kullanıcının benzersiz bir telefon numarasına sahip olması sağlanır.
    - **NOT NULL** kısıtlamaları, bir sütunun boş bırakılamayacağını belirtir.
        - **Örnek:** **Seyahat** tablosunda `BaşlamaZamanı` sütunu **NOT NULL** olarak tanımlanır, böylece her seyahatin bir başlangıç zamanı olması zorunlu kılınır.
    - **CHECK** kısıtlamaları, bir sütundaki değerlerin belirli bir koşulu sağlamasını zorunlu kılar.
        - **Örnek:** **Ödeme** tablosunda `Tutar` sütunu için `CHECK (Tutar > 0)` kısıtlaması uygulanarak, ödeme tutarının sıfırdan büyük olması sağlanır.

#### **3.1.2. Şema Tasarımı**

Şema tasarımı, veritabanındaki tabloların ve ilişkilerin nasıl yapılandırılacağını belirler. İyi bir şema tasarımı için aşağıdaki unsurlara dikkat edilmelidir:

- **Tablo ve Alan İsimlendirme Standartları:**
    
    - Anlamlı ve anlaşılır isimler kullanın.
    - İsimlendirmede tutarlılık sağlayın (örneğin, tüm tablo isimleri tekil veya çoğul olabilir, ancak karıştırılmamalıdır).
    - **Örnek (C2C Taksi Uygulaması):**
        - Tablo isimleri: `Kullanıcı`, `Araç`, `Seyahat`, `Ödeme`.
        - Sütun isimleri: `KullanıcıID`, `İsim`, `Soyisim`, `TelefonNumarası`.
- **Veri Tiplerinin Doğru Seçimi:**
    
    - Sütunlar için uygun veri tiplerini seçmek, veritabanının performansını ve veri bütünlüğünü etkiler.
    - **Örnek (C2C Taksi Uygulaması):**
        - `TelefonNumarası` için `VARCHAR(15)` kullanarak hem ulusal hem de uluslararası numaraları kapsayabilirsiniz.
        - `Tutar` için `DECIMAL(10,2)` kullanarak hassas para değerlerini saklayabilirsiniz.
        - `BaşlamaZamanı` ve `BitişZamanı` için `TIMESTAMP` veya `DATETIME` veri tiplerini kullanın.
- **İlişkilerin Doğru Tanımlanması:**
    
    - Tablolar arasındaki ilişkileri net bir şekilde belirleyin (bire-bir, bire-çok, çok-çok).
    - İlişkiler için uygun yabancı anahtarlar ve kısıtlamalar ekleyin.
    - **Örnek (C2C Taksi Uygulaması):**
        - **Kullanıcı** ve **Araç** tabloları arasında bire-çok ilişki vardır. Bir kullanıcı birden fazla araca sahip olabilir.
        - **Seyahat** tablosu, **Kullanıcı** tablosuyla (sürücü ve yolcu olarak) yabancı anahtarlar aracılığıyla ilişkilendirilmiştir.

---

### **3.2. Normalizasyon**

Normalizasyon, veritabanı tasarımında verilerin organize edilmesi için kullanılan bir süreçtir. Amaç, veri tekrarlanmasını azaltmak, veri bütünlüğünü sağlamak ve anormallikleri önlemektir.

#### **3.2.1. Normalizasyonun Amacı**

- **Veri Tekrarlanmasını Azaltmak:**
    - Verileri mümkün olduğunca atomik hale getirerek, aynı verinin birden fazla yerde depolanmasını önler.
- **Veri Bütünlüğünü Sağlamak:**
    - Veri tutarsızlıklarını ve hatalarını önler.
    - Verilerin güncel ve doğru kalmasını sağlar.
- **Anormallikleri Önlemek:**
    - **Güncelleme Anormallikleri:** Veri değişikliklerinin tüm ilgili yerlerde yapılmaması durumunda ortaya çıkan tutarsızlıklar.
    - **Ekleme Anormallikleri:** Yeni veri eklerken zorunlu olmayan alanların olmaması nedeniyle yaşanan sorunlar.
    - **Silme Anormallikleri:** Veri silindiğinde, istenmeyen başka verilerin de silinmesi durumu.

#### **3.2.2. Normal Formlar**

Normalizasyon süreci, veritabanının belirli normal formlara uygun olarak yapılandırılmasını içerir. Başlıca normal formlar şunlardır:

##### **a. Birinci Normal Form (1NF)**

- **Tanım:**
    
    - Her tablo hücresi tek bir değere sahip olmalıdır (atomik olma).
    - Tabloda yinelenen sütunlar veya gruplar olmamalıdır.
- **Amaç:**
    
    - Verilerin atomik hale getirilmesi ve tekrarlanan veri gruplarının kaldırılması.
- **Örnek (C2C Taksi Uygulaması):**
    
**Hatalı Tasarım:**

Kullanıcı Tablosu:

| KullanıcıID | İsim    | Telefon1 | Telefon2 |
|---------------|----------|-----------|----------|
| 1           | Ahmet   | 12345678 | 87654321 |
| 2           | Ayşe    | 23456789 |          |

**Sorun:**
- Bir kullanıcının birden fazla telefon numarası varsa, yeni sütunlar eklenerek veri tutulmuş.
- Yeni bir telefon numarası eklemek için tablo yapısını değiştirmek gerekecek.

##### **Doğru Tasarım:**
**Kullanıcı** tablosu:

| KullanıcıID | İsim  |
| ----------- | ----- |
| 1           | Ahmet |
| 2           | Ayşe  |

**KullanıcıTelefon** tablosu:

| KullanıcıID | Telefon   |
|--------------|--------------|
| 1           | 12345678  |
| 1           | 87654321  |
| 2           | 23456789  |

- **Açıklama:**
    - Telefon numaraları ayrı bir tabloda tutulur ve her telefon numarası için ayrı bir satır oluşturulur.
    - Böylece, veriler atomik hale gelir ve 1NF sağlanır.

##### **b. İkinci Normal Form (2NF)**

- **Tanım:**
    
    - Tablonun 1NF'de olması gerekir.
    - Her bir öznitelik, birincil anahtarın tamamına tam bağımlı olmalıdır (kısmi bağımlılık olmamalı).
- **Amaç:**
    
    - Bileşik birincil anahtarın parçalarına bağımlı olan öznitelikleri ayırmak.
- **Örnek (C2C Taksi Uygulaması):**
    
    **Hatalı Tasarım:**
    
**SeyahatDetay** tablosu:

| SürücüID | YolcuID | AraçPlaka   | BaşlangıçKonumu | ... |
|-----------|----------|--------------|------------------|------|
| 5        | 10      | 34ABC123    | ...             |     |
| 6        | 11      | 34XYZ789    | ...             |     |

**Sorun:**

- `AraçPlaka`, sadece `SürücüID`'ye bağımlıdır, ancak `YolcuID` ile ilgisi yoktur.
- Bu durum, kısmi bağımlılığa yol açar ve 2NF ihlal edilir.

##### **Doğru Tasarım:**

 **Seyahat** tablosu:

| SeyahatID | SürücüID | YolcuID | ... |
| --------- | -------- | ------- | --- |
| 1001      | 5        | 10      | ... |
| 1002      | 6        | 11      | ... |

**Araç** Tablosu:

| AraçID | KullanıcıID (SürücüID) | PlakaNo  | ... |
| ------ | ---------------------- | -------- | --- |
| 1      | 5                      | 34ABC123 |     |
| 2      | 6                      | 34XYZ789 |     |

- **Açıklama:**
    - `AraçPlaka` bilgisi, **Araç** tablosunda tutulur ve **Seyahat** tablosunda tekrarlanmaz.
    - Böylece, kısmi bağımlılıklar ortadan kalkar ve 2NF sağlanır.

##### **c. Üçüncü Normal Form (3NF)*
- **Tanım:**
    - Tablonun 2NF'de olması gerekir.
    - Anahtar olmayan öznitelikler, diğer anahtar olmayan özniteliklere bağımlı olmamalıdır (transitif bağımlılık olmamalı).
- **Amaç:**
    - Transitif bağımlılıkları ortadan kaldırarak veri tutarsızlıklarını önlemek.
- **Örnek (C2C Taksi Uygulaması):**
    **Hatalı Tasarım:**
    - **Kullanıcı** tablosu:

| KullanıcıID | İsim  | İlID | İlAdı    |
| ----------- | ----- | ---- | -------- |
| 1           | Ahmet | 34   | İstanbul |
| 2           | Ayşe  | 6    | Ankara   |

**Sorun:**
- `İlAdı`, `İlID`'ye bağımlıdır, ancak `İlID` de `KullanıcıID`'ye bağımlıdır.
- Bu durum transitif bağımlılığa yol açar ve 3NF ihlal edilir.

**Doğru Tasarım:**
**Kullanıcı** tablosu:

| KullanıcıID | İsim  | İlID |
|-|-|-|
| 1           | Ahmet | 34   |
| 2           | Ayşe  | 6    |

**İl** tablosu:

| İlID | İlAdı      |
|-|-|
| 34   | İstanbul   |
| 6    | Ankara     |

- **Açıklama:**
    
    - `İlAdı`, `İlID`'ye tam bağımlı hale gelir ve ayrı bir tabloda tutulur.
    - Transitif bağımlılıklar ortadan kalkar ve 3NF sağlanır.

### **3.3. İleri Düzey Normalizasyon**

Bazı durumlarda, veritabanını daha da optimize etmek için ileri düzey normalizasyon formları kullanılır.

#### **3.3.1. Boyce-Codd Normal Formu (BCNF)**

- **Tanım:**
    
    - Her determinant, aday anahtar olmalıdır.
    - BCNF, 3NF'nin bir genellemesidir ve daha sıkı kurallar içerir.
- **Örnek (C2C Taksi Uygulaması):**
    
    **Hatalı Tasarım:**
    
- **SürücüTakvim** tablosu:

| SürücüID | Gün          | ÇalışmaSaatleri |
|-|-|-|
| 5        | Pazartesi    | 08:00 - 18:00   |
| 5        | Salı         | 08:00 - 18:00   |

**Sorun:**

- `ÇalışmaSaatleri`, `SürücüID` ve `Gün` bileşik anahtarına bağımlı, ancak eğer `Gün` için belirli bir `ÇalışmaSaatleri` standardı varsa, bu durum BCNF ihlaline yol açar.

**Doğru Tasarım:**

- **SürücüTakvim** tablosu:

| SürücüID | GünID |
|-|-|
| 5        | 1     |
| 5        | 2     |

Gün Tablosu:

| GünID | GünAdı    | Saat |
| ----- | --------- | ---- |
| 1     | Pazartesi | ...  |
| 2     | Salı      | ...  |

- **Açıklama:**
    - Tüm determinantlar aday anahtar olur ve BCNF sağlanır.

#### **3.3.2. Dördüncü Normal Form (4NF)**
- **Tanım:**
    - Bir tablo, çoklu bağımsız çok-değerli bağımlılıklar içermemelidir.
    - 4NF, bir tabloda tek bir çok-değerli bağımlılık olmasını gerektirir.
- **Örnek (C2C Taksi Uygulaması):**
    **Hatalı Tasarım:**
**KullanıcıİlgiAlanları** tablosu:

| KullanıcıID | Hobiler | Diller    |
| ----------- | ------- | --------- |
| 1           | Futbol  | İngilizce |
| 1           | Müzik   | Fransızca |

**Sorun:**

- `Hobiler` ve `Diller` arasında bağımsız çok-değerli bağımlılıklar vardır.
- Bu durum 4NF ihlaline yol açar.

**Doğru Tasarım:**

- **KullanıcıHobi** tablosu:

| KullanıcıID | Hobi        |
|-|-|
| 1           | Futbol      |
| 1           | Müzik       |

**KullanıcıDil** tablosu:

| KullanıcıID | Dil         |
|-|----------------------------|
| 1           | İngilizce   |
| 1           | Fransızca   |

- **Açıklama:**
    
    - Çok-değerli bağımlılıklar ayrı tablolarda tutulur.
    - 4NF sağlanır.

---

### **3.4. Normalizasyonun Faydaları ve Dikkat Edilmesi Gerekenler**

#### **3.4.1. Faydaları**

- **Veri Tutarlılığı:**
    - Veri tutarsızlıkları ve anormallikleri önlenir.
    - Güncellemeler ve silmeler daha güvenli hale gelir.
- **Depolama Verimliliği:**
    - Veri tekrarı azaltıldığı için depolama alanı verimli kullanılır.
- **Bakım Kolaylığı:**
    - Veritabanının yönetimi ve bakımı daha kolay hale gelir.

#### **3.4.2. Dikkat Edilmesi Gerekenler**

- **Performans Etkisi:**
    
    - Aşırı normalizasyon, çok sayıda tablo ve karmaşık sorgulara yol açabilir.
    - Performans ihtiyaçlarına göre denge sağlanmalıdır.
    - **Örnek:** Sık kullanılan ve birleştirme gerektiren veriler için denormalizasyon düşünülebilir.
- **İhtiyaçlara Uygunluk:**
    
    - Her proje için en uygun normalizasyon seviyesini belirlemek önemlidir.
    - Bazen denormalizasyon (bilinçli veri tekrarı) performansı artırabilir.
    - **Örnek (C2C Taksi Uygulaması):** Seyahat geçmişi raporlaması için bazı verileri tek bir tabloda tutmak performansı artırabilir.
- **Unutulmaması Gerekenler:**
    
    - **Veri Bütünlüğünü Sağlayın:**
        - Birincil ve yabancı anahtarlar, benzersizlik ve doğruluk kısıtlamaları kullanarak verilerin tutarlı kalmasını sağlayın.
    - **Normalizasyon İlkelerine Uyun:**
        - Veri tekrarlanmasını azaltın, anormallikleri önleyin ve uygun normal formları uygulayın.
    - **Dengeyi Sağlayın:**
        - Performans ve veri bütünlüğü arasında denge kurun.
        - Gerektiğinde denormalizasyon tekniklerini kullanın.