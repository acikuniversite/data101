## **2. ER (Varlık-İlişki) Diyagramları**
### **2.1. ER Diyagramlarının Temel Bileşenleri**
**ER Diyagramları**, veritabanı tasarımının temel taşlarından biridir. Varlık-İlişki (Entity-Relationship) diyagramları, veritabanındaki varlıklar, bu varlıkların öznitelikleri ve varlıklar arasındaki ilişkileri görsel olarak temsil eder. Bu sayede, veritabanı yapısını daha iyi anlamak ve etkili bir şekilde tasarlamak mümkün olur.

#### **2.1.1. Varlıklar (Entities)**
- **Tanım:**
    - Varlıklar, bağımsız olarak tanımlanabilen nesneler veya kavramlardır. Gerçek dünyadan alınmış, veritabanında depolanacak bilgi parçalarını temsil ederler.
- **Özellikler:**
    - **İsimlendirme:** Varlık isimleri genellikle tekil isimlerle ifade edilir (örneğin, Müşteri, Ürün, Sipariş).
    - **Varlık Türleri:** Temel varlıklar (örneğin, Müşteri) ve zayıf varlıklar (örneğin, Sipariş_Detayı).
- **Örnekler:**
    - **Müşteri (Customer):** Bir e-ticaret sitesindeki müşterileri temsil eder.
    - **Ürün (Product):** Satılan ürünleri temsil eder.
    - **Sipariş (Order):** Müşterilerin verdikleri siparişleri temsil eder.

#### **2.1.2. Öznitelikler (Attributes)**
- **Tanım:**
    - Öznitelikler, varlıkların sahip olduğu özelliklerdir. Her öznitelik, varlık hakkında belirli bir bilgiyi içerir.
- **Özellikler:**
    - **Basit ve Bileşik Öznitelikler:** Basit öznitelikler tek parça iken, bileşik öznitelikler birden fazla alt özniteliğe sahip olabilir (örneğin, Ad ve Soyad bileşik bir öznitelik oluşturabilir).
    - **Tekrarlayan ve Çok Değerli Öznitelikler:** Bazı öznitelikler birden fazla değere sahip olabilir (örneğin, telefon numaraları).
- **Örnekler:**
    - **Müşteri Adı (Customer Name):** Müşterinin adını belirtir.
    - **Ürün Fiyatı (Product Price):** Ürünün satış fiyatını belirtir.
    - **Sipariş Tarihi (Order Date):** Siparişin verildiği tarihi belirtir.

#### **2.1.3. İlişkiler (Relationships)**
- **Tanım:**
    - İlişkiler, varlıklar arasındaki bağlantıları gösterir. Bu bağlantılar, varlıklar arasında nasıl bir etkileşim veya bağlantı olduğunu ifade eder.
- **Özellikler:**
    - **İlişki Türleri:** Bir varlık ilişkisi diğerine birden fazla şekilde bağlayabilir (bire-bir, bire-çok, çok-çok).
    - **Görsel Temsil:** İlişkiler genellikle çizgilerle bağlanmış ve ilişkilerin türünü belirtmek için etiketlenmiş olarak gösterilir.
- **Örnekler:**
    - **Müşteri Verir Sipariş (Customer Places Order):** Bir müşterinin bir veya daha fazla sipariş verebildiğini gösterir.
    - **Sipariş İçerir Ürün (Order Contains Product):** Bir siparişin bir veya daha fazla ürünü içerebildiğini gösterir.

---

### **2.2. Kardinalite ve İlişkiler**
**Kardinalite**, varlıklar arasındaki ilişkinin sayısal doğasını belirtir. Bir ilişkideki kardinalite, bir varlığın diğer varlıkla kaç kez ilişki kurabileceğini ifade eder.

#### **2.2.1. Kardinalite Türleri**
1. **Bire-Bir (1:1):**
    - **Tanım:** Bir varlığın bir diğer varlıkla sadece bir kez ilişki kurabildiği durumdur.
    - **Örnek:** Her çalışan, bir adet kimlik kartına sahip olabilir.
    - **Görsel:** İki varlık arasındaki ilişkiyi temsil eden çizginin her iki ucunda da "1" işareti bulunur.
    !(img1.png)[img1.png]
   2. **Bire-Çok (1:M):**
    - **Tanım:** Bir varlığın birden fazla diğer varlıkla ilişki kurabildiği durumdur.
    - **Örnek:** Bir müşteri birçok sipariş verebilir.
    - **Görsel:** Bir varlık ile bir diğer varlık arasındaki ilişkiyi temsil eden çizginin bir ucunda "1", diğer ucunda "*" işareti bulunur.

    !(img2.png)[img2.png]

3. **Çok-Çok (M:M):**
    
    - **Tanım:** Birden fazla varlığın birden fazla diğer varlıkla ilişki kurabildiği durumdur.
    - **Örnek:** Bir öğrenci birçok derse kayıt olabilir ve bir ders birçok öğrenci tarafından alınabilir.
    - **Görsel:** İki varlık arasındaki ilişkiyi temsil eden çizginin her iki ucunda da "*" işareti bulunur.

    !(img3.png)[img3.png]
#### **2.2.2. İlişki Dereceleri**
- **Tanım:** İlişkide yer alan varlıkların sayısını belirtir.
    - **İkili İlişkiler:** İki varlık arasında olan ilişkiler (örneğin, Müşteri ve Sipariş).
    - **Üçlü İlişkiler:** Üç varlık arasında olan ilişkiler (örneğin, Öğrenci, Ders ve Öğretmen).

#### **2.2.3. Zorunluluğa Bağlı Kardinalite Gösterimi**
Zorunluluk, bir varlığın ilişkiye katılıp katılmaması gerektiğini belirtir.
- **1:** Tam olarak bir varlık.
- **0..1:** Sıfır veya bir varlık.
- **0..*:** Sıfır veya daha fazla varlık.
- **1..*:** Bir veya daha fazla varlık.

**Örnek Gösterim:**
- **Müşteri ve Sipariş Arasındaki Zorunluluk:**
    - Her siparişin bir müşteriye ait olması gerektiği için sipariş tarafında "1" zorunluluk bulunur.
    - Bir müşterinin hiç siparişi olmaması da mümkündür, bu yüzden müşteri tarafında "0..*" zorunluluk bulunur.

!(img4.png)[img4.png]

### **2.3. ER Diyagramı Çizimi**
ER diyagramları, veritabanı tasarımının görsel bir temsilidir. Aşağıda, ER diyagramı çizimi için temel adımlar ve örnek bir senaryo üzerinden nasıl çizileceği anlatılmaktadır.

#### **2.3.1. ER Diyagramı Çizim Adımları**
1. **Varlıkları Belirleme:**
    - İlk olarak, veritabanında yer alacak temel varlıkları tanımlayın.
    - Örneğin, bir e-ticaret sitesi için **Müşteri**, **Ürün**, **Sipariş** varlıkları.
2. **Öznitelikleri Tanımlama:**
    - Her varlığın sahip olması gereken öznitelikleri belirleyin.
    - **Müşteri:** ID, Ad, Soyad, E-posta.
    - **Ürün:** ID, İsim, Fiyat, Stok.
    - **Sipariş:** ID, MüşteriID, Tarih.
3. **İlişkileri Tanımlama:**
    - Varlıklar arasındaki ilişkileri belirleyin.
    - **Müşteri Verir Sipariş** ilişkisi (1:M).
    - **Sipariş İçerir Ürün** ilişkisi (M:M).
4. **Kardinaliteyi Belirleme:**
    - İlişkilerin kardinalitesini belirleyin ve diyagramda gösterin.
5. **Görsel Temsil:**
    - Varlıkları dikdörtgenlerle, öznitelikleri ovalarla ve ilişkileri çizgilerle temsil edin.
    - Kardinaliteyi ilişki çizgilerinin uçlarına ekleyin.

#### **2.3.2. Örnek ER Diyagramı Senaryosu**
**Senaryo:** Bir e-ticaret sitesi, müşterilerin verdiği siparişleri yönetmek istiyor. Her müşteri bir veya daha fazla sipariş verebilir ve her sipariş bir veya daha fazla ürünü içerebilir.

**Adımlar:**
1. **Varlıklar:**
    - **Müşteri (Customer)**
    - **Ürün (Product)**
    - **Sipariş (Order)**
    - **Sipariş_Urun (Order_Product)** (Çok-Çok ilişkiler için bağlantı varlığı)
2. **Öznitelikler:**
    - **Müşteri:**
        - ID (INT, PK)
        - Ad (VARCHAR)
        - Soyad (VARCHAR)
        - E-posta (VARCHAR)
    - **Ürün:**
        - ID (INT, PK)
        - İsim (VARCHAR)
        - Fiyat (DECIMAL)
        - Stok (INT)
    - **Sipariş:**
        - ID (INT, PK)
        - MüşteriID (INT, FK)
        - Tarih (DATE)
    - **Sipariş_Urun:**
        - SiparişID (INT, FK)
        - ÜrünID (INT, FK)
        - Miktar (INT)
3. **İlişkiler:**
    - **Müşteri Verir Sipariş (1:M):**
        - Bir müşteri birçok sipariş verebilir.
    - **Sipariş İçerir Ürün (M:M):
        - Bir sipariş birçok ürünü içerebilir ve bir ürün birçok siparişte yer alabilir.
        - Bu ilişkiyi yönetmek için **Sipariş_Urun** adlı bir bağlantı varlığı kullanılır.
4. **Kardinalite ve Zorunluluk:**
    - **Müşteri - Sipariş:**
        - Müşteri tarafı: 1
        - Sipariş tarafı: 0..*
    - **Sipariş - Ürün:**
        - Sipariş tarafı: 1
        - Ürün tarafı: 0..*

#### **2.3.3. ER Diyagramı Örneği**
Aşağıda, yukarıdaki senaryo için oluşturulmuş örnek bir ER diyagramı bulunmaktadır:

!(img5.png)[img5.png]

- **Müşteri** tablosu, **Sipariş** tablosu ile bire-çok ilişki içerisindedir.
- **Sipariş** ve **Ürün** tabloları arasında çok-çok ilişki bulunmaktadır ve bu ilişki **Sipariş_Urun** tablosu aracılığıyla yönetilmektedir.

!(img6.png)[img6.png]
### **2.4. ER Diyagramı Çizimi İçin İpuçları ve En İyi Uygulamalar**
- **Net ve Tutarlı İsimlendirme:**
    - Varlık ve öznitelik isimlerini anlaşılır ve tutarlı şekilde adlandırın. Örneğin, "Müşteri" yerine "Customer", "Ad" yerine "FirstName".
- **Özniteliklerin Doğru Türde Tanımlanması:**
    - Veri türlerini doğru seçmek, veritabanının performansı ve veri bütünlüğü açısından önemlidir. Örneğin, tarih için DATE, metin için VARCHAR kullanın.
- **Anahtarların Belirlenmesi:**
    - Her varlık için benzersiz bir birincil anahtar (PK) belirleyin. Yabancı anahtarlar (FK) aracılığıyla ilişkileri tanımlayın.
- **İlişkilerin Doğru Tanımlanması:**
    - İlişkilerin kardinalite ve zorunluluklarını doğru belirleyin. Bu, veritabanının doğru şekilde çalışmasını sağlar.
- **Görsel Temizliği Sağlama:**
    - Diyagramınızı sade ve okunabilir tutun. Karmaşık ilişkileri minimize etmek için bağlantıları düzenli bir şekilde yerleştirin.
- **Modüler Yaklaşım:**
    - Büyük ve karmaşık veri modellerini küçük parçalara ayırarak yönetilebilir hale getirin. Örneğin, her bölüm için ayrı ER diyagramları oluşturabilirsiniz.

---

### **2.5. ER Diyagramı Çizimi Örnekleri**
#### **2.5.1. E-Ticaret Veri Modelleme ER Diyagramı**
**Senaryo:** Bir e-ticaret sitesi, müşterilerin verdiği siparişleri ve bu siparişlerdeki ürünleri yönetmek istiyor. Her müşterinin birden fazla siparişi olabilir ve her sipariş birden fazla ürünü içerebilir.

**Açıklama:**
- **Müşteri** varlığı, **Sipariş** varlığı ile bire-çok ilişkiye sahiptir.
- **Sipariş** varlığı, **Sipariş_Urun** varlığı üzerinden **Ürün** varlığı ile çok-çok ilişkiye sahiptir.
- **Sipariş_Urun** varlığı, her siparişin birden fazla ürünü içerebilmesini sağlar.

#### **2.5.2. Sağlık Sektörü Veri Modelleme ER Diyagramı**
**Senaryo:** Bir hastane, hastaların randevularını, doktorlarını ve tedavi süreçlerini yönetmek istiyor. Her hastanın birden fazla randevusu olabilir ve her randevu bir doktora atanabilir.

**ER Diyagramı:**
!(img7.png)[img7.png]

**Açıklama:**
- **Hasta** varlığı, **Randevu** varlığı ile bire-çok ilişkiye sahiptir.
- **Randevu** varlığı, **Doktor** varlığı ile bire-çok ilişkiye sahiptir.
- **Randevu** varlığı, **Tedavi** varlığı ile bire-çok ilişkiye sahiptir.

---

### **2.6. ER Diyagramı Çizimi için Araçlar ve Teknolojiler**
ER diyagramları çizmek için birçok araç mevcuttur. Bu araçlar, veri modelleme sürecini kolaylaştırır ve diyagramların profesyonel görünmesini sağlar.
- **Lucidchart:**
    - Bulut tabanlı, kullanıcı dostu bir diyagram oluşturma aracıdır.
    - ER diyagramları için hazır şablonlar ve semboller sunar.
    - Ekip çalışmasına uygun özellikler içerir.
- **Microsoft Visio:**
    - Güçlü bir diyagram ve çizim aracıdır.
    - Veri modelleme için kapsamlı araç setleri ve şablonlar sağlar.
    - Microsoft ekosistemi ile entegrasyon avantajı sunar.
- **Draw.io (diagrams.net):**
    - Ücretsiz ve açık kaynaklı bir diyagram oluşturma aracıdır.
    - ER diyagramları için çeşitli semboller ve şablonlar sunar.
    - Tarayıcı tabanlı olması sayesinde kolay erişim sağlar.
- **MySQL Workbench:**
    - MySQL veritabanları için entegre bir modelleme aracıdır.
    - ER diyagramları oluşturma, veritabanı tasarlama ve yönetme imkanı sunar.
    - SQL kodu ile otomatik senkronizasyon sağlar.
- **ER/Studio:**
    - Karmaşık veri modellerini görselleştirmek için profesyonel bir araçtır.
    - Gelişmiş özellikler ve veri yönetimi imkanları sunar.
    - Büyük ölçekli projeler için uygundur.

---

### **2.7. ER Diyagramı Çizimi İçin En İyi Uygulamalar**
- **Net ve Tutarlı İsimlendirme:**
    - Varlık ve öznitelik isimlerini anlamlı ve tutarlı şekilde adlandırın. Örneğin, "Müşteri" yerine "Customer", "Ad" yerine "FirstName".
- **Veri Türlerinin Doğru Seçilmesi:**
    - Her öznitelik için doğru veri türünü belirleyin (örneğin, tarih için DATE, metin için VARCHAR).
- **Anahtarların Belirlenmesi:**
    - Her varlık için benzersiz bir birincil anahtar (PK) belirleyin. Yabancı anahtarlar (FK) aracılığıyla ilişkileri tanımlayın.
- **İlişkilerin Doğru Tanımlanması:**
    - İlişkilerin kardinalite ve zorunluluklarını doğru belirleyin. Bu, veritabanının doğru şekilde çalışmasını sağlar.
- **Görsel Temizliği Sağlama:**
    - Diyagramınızı sade ve okunabilir tutun. Karmaşık ilişkileri minimize etmek için bağlantıları düzenli bir şekilde yerleştirin.
- **Modüler Yaklaşım:**
    - Büyük ve karmaşık veri modellerini küçük parçalara ayırarak yönetilebilir hale getirin. Örneğin, her bölüm için ayrı ER diyagramları oluşturabilirsiniz.
- **Dokümantasyon:**
    - ER diyagramlarını detaylı bir şekilde dokümante edin. Her varlık, öznitelik ve ilişki için açıklamalar ekleyerek, diyagramın anlaşılabilirliğini artırın.
- **Güvenlik ve Erişim Kontrolleri:**
    - Veritabanı erişimlerini doğru şekilde yapılandırarak, veri güvenliğini sağlayın.

---

### **2.8. ER Diyagramı Çiziminde Sık Karşılaşılan Hatalar ve Çözümleri**
- **Aşırı Karmaşıklık:**
    - **Hata:** Diyagramın çok karmaşık olması, anlaşılmasını zorlaştırır.
    - **Çözüm:** Diyagramı sade tutun, gereksiz detaylardan kaçının ve büyük modelleri bölümlere ayırın.
- **Tutarsız İsimlendirme:**
    - **Hata:** Varlık ve öznitelik isimlerinin tutarsız olması, anlaşılmayı zorlaştırır.
    - **Çözüm:** İsimlendirme kuralları belirleyin ve tüm diyagram boyunca bu kurallara uyun.
- **Yanlış Kardinalite Gösterimi:**
    - **Hata:** İlişkilerin kardinalite ve zorunluluklarının yanlış belirtilmesi.
    - **Çözüm:** Kardinalite kurallarını iyi anlayın ve doğru şekilde uygulayın.
- **Eksik veya Fazla Öznitelik:**
    - **Hata:** Varlıkların gerekli özniteliklerinin eksik veya gereksiz özniteliklerle dolu olması.
    - **Çözüm:** Veri gereksinimlerini dikkatlice analiz edin ve sadece gerekli öznitelikleri ekleyin.
- **İlişkilerin Doğru Tanımlanmaması:**
    - **Hata:** Varlıklar arasındaki ilişkilerin yanlış veya eksik tanımlanması.
    - **Çözüm:** İlişkileri net bir şekilde belirleyin ve doğru şekilde temsil edin.

---

### **2.9. Örnek ER Diyagramı**
Üye ve Ödünç Alma arasında bire-çok, Kitap ve Ödünç Alma arasında bire-çok, Kitap ve Yazar arasında çok-çok ilişki gösterilmektedir
  
!(img8.png)[img8.png]

**Açıklama:**
- **Üye** varlığı, **Ödünç Alma** varlığı ile bire-çok ilişkiye sahiptir. 
- **Kitap** varlığı, **Ödünç Alma** varlığı ile bire-çok ilişkiye sahiptir. 
- **Kitap** ve **Yazar** varlıkları arasında çok-çok ilişki bulunmaktadır ve bu ilişki **Kitap_Yazar** adlı bir bağlantı varlığı aracılığıyla yönetilmektedir. 
- **Kitap_Yazar** varlığı, her kitabın birden fazla yazar tarafından yazılabilmesini sağlar.