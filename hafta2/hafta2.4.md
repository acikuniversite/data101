## 5. Workshop
### **Senaryo:**

Bir kütüphane, kitap ve üye kayıtlarını dijital bir veritabanında yönetmek istiyor. Üyeler kitap ödünç alabiliyor ve bu işlemlerin takip edilmesi gerekiyor. Kütüphane yönetimi sizden veritabanını oluşturmanızı ve SQL komutlarıyla bu işlemleri yönetmenizi istiyor.

#### **Etkinlik Aşamaları:**

1. **Grup Oluşturma (5 dakika):** Öğrenciler 4-5 kişilik gruplara ayrılır. Her gruba, kütüphanedeki kitaplar ve üyelerle ilgili veritabanı tasarımı ve yönetim görevleri verilir.
2. **Veritabanı ve Tabloların Tasarlanması (10 dakika):**
    - Her grup, kütüphaneye yönelik iki temel tabloyu tasarlar: **Kitaplar** ve **Üyeler**.
    - Gruplar, bu iki tablo arasındaki ilişkiyi belirler ve “Ödünç İşlemleri” tablosu ile ilişkiyi nasıl kuracaklarını tartışır.
    - Her grup, tabloların sütunlarını (kitap adı, yazar, ISBN, üye adı, e-posta vb.) belirleyerek tasarımı sınıfla paylaşır.
3. **SQL Komutlarıyla Tabloların Oluşturulması (10 dakika):**
    - Gruplar, SQL kullanarak tabloları oluşturur:
        - **CREATE TABLE Kitaplar** ve **CREATE TABLE Üyeler** komutlarıyla tabloları yazar.
        - Gerekli birincil ve yabancı anahtarları eklerler.
        - Gruplar, tabloları sınıfa sunar ve yapılarını tartışır.
4. **Veri Manipülasyonu (DML Komutları) (15 dakika):**
    - Her grup, kütüphaneye ait örnek veri setini kullanarak **INSERT INTO** komutu ile kitap ve üye bilgilerini ekler.
    - **UPDATE** komutu ile üyelerin e-posta adreslerini güncelleyebilirler.
    - Ödünç verilen kitapların stoklarını **UPDATE** komutuyla güncellerler.
    - **DELETE** komutunu kullanarak eski kayıtları silerler.
5. **Sorgu Yazma (15 dakika):**
    - Gruplar, belirli üyelerin ödünç aldığı kitapları listeleyen sorgular yazar:
        - **INNER JOIN** komutunu kullanarak üyeler ve kitaplar arasında ilişki kurarlar.
        - **WHERE** şartı ile belirli bir tarih aralığında ödünç alınan kitapları sorgularlar.
    - Her grup, yazdığı sorguları sınıfla paylaşır ve diğer grupların önerileriyle sorgularını optimize eder.
6. **Sonuç ve Tartışma (5 dakika):**
    - Gruplar, tablolarını ve sorgularını sunduktan sonra veritabanı yönetimi ile ilgili sorular ve görüşler sınıfta tartışılır.
    - Öğrenciler, veritabanı tasarımının ve SQL komutlarının gerçek dünyadaki kullanım alanlarına dair çıkarımlarda bulunurlar.