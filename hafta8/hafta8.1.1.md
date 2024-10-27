## **1. Giriş**

### **8.1. Hafta Önemi ve Önceki Haftalarla Bağlantısı**

İlk 7 haftada, veri yönetimi ve analitiği konularında temel ve orta düzeyde bilgi edindik. Veritabanları, veri modelleme, veri mühendisliği, veri bilimi ve iş zekası gibi konuları ele aldık. Bu hafta, tüm bu öğrendiklerimizi bir üst seviyeye taşıyarak **bulut teknolojileri** ve **bulutta veri yönetimi** konularına odaklanacağız.

**Neden Bulut?**

- **Büyüyen Veri Hacmi:** Günümüzde üretilen veri miktarı sürekli artıyor ve geleneksel yöntemlerle bu verileri yönetmek zorlaşıyor.
- **Esneklik ve Ölçeklenebilirlik İhtiyacı:** İşletmeler, talebe göre kaynaklarını hızlıca ölçeklendirebilmek istiyor.
- **Maliyet Etkinliği:** Bulut hizmetleri, ön yatırım maliyetlerini azaltarak işletmelerin bütçelerini daha verimli kullanmalarını sağlıyor.

**Bu Haftanın Amacı:**

- Bulut bilişim kavramlarını ve avantajlarını anlamak.
- GCP (Google Cloud Platform) ağırlıklı olmak üzere, AWS gibi diğer bulut sağlayıcılarını tanımak.
- Dağıtık ve sunucusuz bilişimin veri yönetimindeki rolünü öğrenmek.
- On-prem'den buluta geçiş sürecini ve dikkat edilmesi gerekenleri kavramak.
- Pratik bir uygulama ile GCP üzerinde veri işleme pipeline'ı oluşturmak.
## **2. Bulut Bilişime Genel Bakış**

### **2.1. Bulut Bilişim Nedir?**

**Bulut Bilişim**, internet üzerinden (bulut) bilgi işlem kaynaklarına (sunucular, depolama, veritabanları, ağ iletişimi, yazılım vb.) isteğe bağlı olarak erişim sağlayan ve bu kaynakları yönetmeyi kolaylaştıran bir teknoloji modelidir.

**Temel Özellikleri:**

- **İsteğe Bağlı Self-Servis:** Kullanıcılar, ihtiyaç duydukları kaynakları otomatik olarak sağlayabilir.
- **Geniş Ağ Erişimi:** Hizmetler, internet üzerinden farklı cihazlar aracılığıyla erişilebilir.
- **Kaynak Havuzu:** Kaynaklar, birden çok kullanıcı arasında paylaştırılır.
- **Hızlı Esneklik:** Kaynaklar, hızlı bir şekilde ölçeklendirilebilir.
- **Ölçümlenebilir Hizmet:** Kullanım, şeffaf bir şekilde ölçülür ve faturalandırılır.

### **2.2. Bulut Servis Modelleri**

#### **IaaS, PaaS, SaaS**

1. **IaaS (Infrastructure as a Service):** Altyapı Hizmeti
    - Kullanıcılar, sanal sunucular, depolama, ağ ve işletim sistemleri gibi temel bilgi işlem altyapılarına erişir.
    - **Örnek:** GCP'de Compute Engine, AWS'de EC2.
2. **PaaS (Platform as a Service):** Platform Hizmeti
    - Geliştiriciler, uygulamalarını oluşturmak, test etmek ve dağıtmak için platformlara erişir.
    - **Örnek:** GCP'de App Engine, AWS'de Elastic Beanstalk.
3. **SaaS (Software as a Service):** Yazılım Hizmeti
    - Kullanıcılar, uygulamalara internet üzerinden erişir ve kullanır.
    - **Örnek:** Google Workspace (Gmail, Docs), Salesforce.

### **2.3. Bulut Dağıtım Modelleri**

#### **Genel, Özel, Hibrit, Çoklu Bulut**

1. **Genel Bulut (Public Cloud):**
    - Hizmetler, genel halka açık internet üzerinden sunulur.
    - **Örnek:** GCP, AWS, Microsoft Azure.
2. **Özel Bulut (Private Cloud):**
    - Hizmetler, tek bir işletme için özel olarak sunulur.
    - Daha fazla kontrol ve güvenlik sağlar.
3. **Hibrit Bulut (Hybrid Cloud):**
    - Genel ve özel bulutların kombinasyonudur.
    - Verilerin ve uygulamaların paylaşımı için esneklik sağlar.
4. **Çoklu Bulut (Multi-Cloud):**
    - Birden fazla bulut hizmet sağlayıcısının kullanılması.
    - Farklı hizmetlerin avantajlarından yararlanmayı sağlar.
## **3. Bulut Bilişimin Avantajları**

### **3.1. Ölçeklenebilirlik ve Esneklik**

- **Dinamik Ölçeklenebilirlik:** İş yüküne bağlı olarak kaynakları artırıp azaltabilme.
- **Esnek Kaynak Yönetimi:** İhtiyaç duyulan kaynakları hızlıca sağlayabilme.

### **3.2. Maliyet Etkinliği**

- **Ön Yatırım Maliyeti Yok:** Donanım ve altyapı yatırımı yapmadan kaynak kullanımı.
- **Kullandığın Kadar Öde Modeli:** Sadece kullanılan kaynaklar için ödeme yapma.

### **3.3. Yüksek Kullanılabilirlik ve Güvenilirlik**

- **Veri Yedekliliği:** Verilerin birden çok bölgede saklanması.
- **Kesintisiz Hizmet:** Hizmet sağlayıcıların sunduğu SLA'lar (Service Level Agreements) ile yüksek erişilebilirlik garantisi.

### **3.4. Yönetilen Hizmetler ve Bakım Kolaylığı**

- **Yönetilen Altyapı:** Donanım bakımı ve güncellemelerle uğraşmadan hizmetleri kullanabilme.
- **Güvenlik Güncellemeleri:** Hizmet sağlayıcı tarafından otomatik olarak yapılır.