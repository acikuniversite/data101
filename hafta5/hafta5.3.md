### **Senaryo:**

Bir mobil ticaret oyunu geliştiriyorsunuz. Bu oyunda oyuncular, kaynakları alıp satabiliyor, üretim yapabiliyor ve dünya genelinde ticaret yapabiliyorlar. Ayrıca, şirketler kurabilir, pazarlara giriş yapabilir ve diğer oyuncularla ortaklıklar kurabilirler. Farklı veri türleri (ürün verileri, oyuncu finans bilgileri, ticaret işlemleri, stratejik ortaklıklar vb.) için en uygun veritabanı çözümünü belirlemeniz gerekiyor.

### **Etkinlik Aşamaları:**

1. **Grup Oluşturma (5 dakika):**
    
    - Öğrencileri 4-5 kişilik gruplara ayırın. Her grup, mobil ticaret oyunundaki farklı veri türleri için veritabanı tasarımı yapacak.
2. **Veri Türlerini Anlama (10 dakika):**
    
    - Gruplara, oyundaki farklı veri türlerini açıklayın:
        - **Ürün Verileri:** Dinamik ve esnek veri yapısına sahip, birçok farklı ürün özelliği olabilir.
        - **Finansal İşlemler:** Güçlü veri tutarlılığı gerektiren ödeme ve ticaret bilgileri.
        - **Oyuncu Bilgileri ve Ortaklıklar:** Sosyal grafikler, oyuncular arası ilişkiler ve ortaklıklar.
    - Gruplar, bu veri türlerini analiz ederek her veri yapısı için en uygun veritabanı teknolojisini (SQL, NoSQL) belirleyecek.
3. **Veritabanı Seçimi ve Tasarımı (20 dakika):**
    
    - Gruplar, her veri türü için uygun bir veritabanı seçimi yapacak:
        - **NoSQL (MongoDB, Redis, Neo4j)**: Esnek veri yapıları, graf ilişkiler veya yüksek hızlı veri işlemleri için.
        - **SQL (PostgreSQL, MySQL)**: Yüksek veri tutarlılığı, ACID gereksinimleri olan işlemler için.
    - Her grup, ürün verileri için NoSQL, finansal işlemler için SQL ve oyuncu ilişkileri için grafik veritabanı önerisi yapabilir.
4. **Hibrit Mimari Tasarımı (15 dakika):**
    
    - Gruplar, belirledikleri veritabanı türlerini hibrit bir yapı içinde nasıl kullanacaklarını tartışacak:
        - **Veri akışını** nasıl yöneteceklerini ve **veriler arasındaki entegrasyonu** nasıl sağlayacaklarını belirleyecekler.
        - **ETL süreçleri** ile NoSQL ve SQL arasında veri aktarımını nasıl yöneteceklerini tartışacaklar.
    - Her grup, oyun için geliştirdikleri veritabanı mimarisini sınıfa sunacak.