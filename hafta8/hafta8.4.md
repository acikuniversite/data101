## **6. Şirketlerin Buluta Geçişi: Bir Örnek Olay İncelemesi**

### **6.1. Şirket Profili ve Mevcut Durum**

**Şirket:** XYZ E-Ticaret A.Ş.

**Sektör:** E-Ticaret

**Mevcut Altyapı:**

- **Veri Depolama:**
    - Yerel sunucularda barındırılan **SQL** veritabanları (MySQL).
    - **NoSQL** veritabanları (MongoDB) ürün ve müşteri verileri için kullanılıyor.
- **Veri İşleme:**
    - Yerel sunucularda çalışan ETL işlemleri.
    - Raporlama ve analitik için sınırlı kaynaklar.
- **Zorluklar:**
    - Ölçeklenebilirlik sorunları.
    - Yüksek bakım ve donanım maliyetleri.
    - Veri güvenliği ve yedekleme riskleri.

### **6.2. Buluta Geçiş Nedenleri**

- **Ölçeklenebilirlik İhtiyacı:** Artan müşteri ve işlem sayısı nedeniyle altyapının yetersiz kalması.
- **Maliyet Tasarrufu:** Donanım ve bakım maliyetlerini azaltmak.
- **Veri Güvenliği:** Gelişmiş güvenlik protokollerine ihtiyaç.
- **İş Sürekliliği ve Yedekleme:** Felaket kurtarma ve yedekleme stratejilerini iyileştirmek.
- **Güncel Teknolojilere Erişim:** Makine öğrenmesi ve veri analitiği için bulut hizmetlerinden faydalanmak.

### **6.3. Geçiş Stratejisi ve Planlaması**

- **Değerlendirme:**
    - Mevcut sistemlerin ve uygulamaların analizi.
    - Buluta taşınacak bileşenlerin belirlenmesi.
- **Seçim:**
    - Bulut sağlayıcısı olarak **Google Cloud Platform (GCP)** seçildi.
- **Planlama:**
    - Aşamalı geçiş stratejisi.
    - Öncelikle statik ve kolay taşınabilir verilerin taşınması.
    - Kritik sistemlerin ve veritabanlarının daha sonra taşınması.

### **6.4. Uygulama Adımları**

**Adım 1: Bulut Ortamının Hazırlanması**

- **GCP Projesi Oluşturma:**
    - Yeni bir GCP projesi başlatıldı.
- **Ekip ve Erişim Kontrolü:**
    - IAM ile ekip üyelerine roller ve izinler atandı.

**Adım 2: Veri Depolama ve Yedekleme**

- **Cloud Storage Kullanımı:**
    - Statik dosyalar ve medya içerikleri için Cloud Storage kullanıldı.
- **Veri Yedekleme:**
    - Mevcut veritabanlarının yedekleri Cloud Storage'a yüklendi.

**Adım 3: Veritabanlarının Taşınması**

- **Cloud SQL'e Geçiş:**
    - MySQL veritabanları Cloud SQL'e taşındı.
    - **Database Migration Service** kullanıldı.
- **Cloud Bigtable Kullanımı:**
    - MongoDB verileri, benzer yapıdaki Cloud Bigtable'a aktarıldı.

**Adım 4: Veri İşleme ve Analitiği**

- **BigQuery ile Veri Ambarı Oluşturma:**
    - Analitik ve raporlama için BigQuery kullanıldı.
- **Dataflow ile ETL İşlemleri:**
    - Veri dönüşümleri ve temizleme işlemleri Dataflow ile otomatikleştirildi.

**Adım 5: Uygulamaların Taşınması**

- **Compute Engine ve App Engine Kullanımı:**
    - Web uygulamaları ve API'lar bulut üzerinde yeniden yapılandırıldı.
- **Kubernetes Engine ile Mikroservisler:**
    - Mikroservis mimarisine geçilerek uygulamalar GKE üzerinde çalıştırıldı.

**Adım 6: Güvenlik ve Uyumluluk**

- **IAM ve Güvenlik Politikaları:**
    - Erişim kontrolü ve güvenlik politikaları tanımlandı.
- **Şifreleme ve Anahtar Yönetimi:**
    - Veri şifrelemesi için Cloud KMS kullanıldı.

### **6.5. Sonuçlar ve Kazanımlar**

- **Maliyet Tasarrufu:**
    - Donanım ve bakım maliyetlerinde %30 azalma.
- **Ölçeklenebilirlik:**
    - Trafik artışlarına hızlıca yanıt verebilme.
- **Performans Artışı:**
    - Veri işleme ve analitiğinde %50 hızlanma.
- **Güvenlik ve Güvenilirlik:**
    - Veri kaybı riskinin minimize edilmesi.
- **İnovasyon:**
    - Makine öğrenmesi ve yapay zeka projelerine başlama imkanı.