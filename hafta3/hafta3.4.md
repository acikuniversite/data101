## 4. Workshop
### **Senaryo:**
Bir restoran zinciri, tüm müşteri siparişlerini, menü öğelerini ve çalışan bilgilerini merkezi bir sistemde toplamak istiyor. Bu sistem, müşterilerin verdikleri siparişlerin takip edilmesini, menüdeki yemeklerin stoklarının kontrol edilmesini ve çalışanların yönetimini sağlamalı. Şirket bu verilerin hepsini yönetmek için bir veritabanı tasarımı talep ediyor ve sizin grubunuzdan bu veritabanını modellemenizi istiyor.

#### **Etkinlik Aşamaları:**
1. **Gereksinim Analizi:**
    - Gruplar, restoran için gerekli verileri ve ilişkileri belirler:
        - Hangi bilgiler toplanmalı? (Müşteriler, siparişler, yemekler, çalışanlar)
        - Bu bilgiler nasıl ilişkili olmalı? (Müşteri, sipariş oluşturur; sipariş menüdeki yemekleri içerir; çalışanlar siparişleri yönetir)
    - Her grup, verileri ve ilişkileri tanımlayan bir liste hazırlar ve sınıfla paylaşır.
2. **Kavramsal Modelleme:**
    - Gruplar, varlıkları ve bu varlıklar arasındaki ilişkileri tanımlayan bir **ER Diyagramı** çizer.
        - Varlıklar: **Müşteri**, **Sipariş**, **Yemek**, **Çalışan**
        - İlişkiler: Müşteri sipariş verir (1-N), sipariş birden fazla yemeği içerir (N-N).
    - Her grup, diyagramlarını sınıfa sunarak varlıkları ve ilişkileri açıklar.
3. **Mantıksal Modelleme:**
    - Gruplar, kavramsal modeli kullanarak her varlık için tablolar oluşturur.
        - **Müşteri Tablosu**: ID, Ad, Soyad, Telefon
        - **Sipariş Tablosu**: ID, MüşteriID, Tarih
        - **Yemek Tablosu**: ID, YemekAdı, Fiyat, Stok
        - **Çalışan Tablosu**: ID, Ad, Pozisyon
    - Tablolar arası ilişkiler, birincil ve yabancı anahtarlar eklenir.
    - Her grup, mantıksal model tasarımını sınıfla paylaşır.
