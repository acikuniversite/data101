## **4. Google Cloud Platform (GCP) ile Veri Yönetimi**

### **4.1. GCP'ye Giriş**

#### **4.1.1. GCP Hizmetlerinin Genel Bakışı**

**Google Cloud Platform (GCP)**, Google tarafından sunulan ve çeşitli bulut hizmetlerini içeren bir platformdur. GCP, altyapıdan platform hizmetlerine kadar geniş bir yelpazede çözümler sunar.

**Temel Hizmet Kategorileri:**
- **Hesaplama (Compute):**
    - **Compute Engine:** Sanal makinelerin oluşturulması ve yönetimi.
    - **App Engine:** Tam yönetilen uygulama platformu.
    - **Kubernetes Engine (GKE):** Konteyner orkestrasyonu için yönetilen Kubernetes hizmeti.
    - **Cloud Functions:** Sunucusuz hesaplama hizmeti.
- **Depolama ve Veritabanları (Storage & Databases):**
    - **Cloud Storage:** Nesne depolama hizmeti.
    - **Cloud SQL:** Yönetilen ilişkisel veritabanı (MySQL, PostgreSQL).
    - **Cloud Bigtable:** Büyük ölçekli NoSQL veritabanı.
    - **Cloud Spanner:** Küresel ölçekli ilişkisel veritabanı.
    - **Firestore:** Tamamen yönetilen NoSQL veritabanı.
- **Veri Analitiği (Data Analytics):**
    - **BigQuery:** Tam yönetilen veri ambarı ve analitik hizmeti.
    - **Dataflow:** Gerçek zamanlı ve toplu veri işleme.
    - **Dataproc:** Hadoop ve Spark için yönetilen hizmet.
    - **Pub/Sub:** Mesaj kuyruğu ve akış hizmeti.
- **Makine Öğrenmesi ve Yapay Zeka (AI & Machine Learning):**
    - **AI Platform:** Makine öğrenmesi modellerinin geliştirilmesi ve dağıtılması.
    - **AutoML:** Kod yazmadan makine öğrenmesi modelleri oluşturma.
    - **Vision API, Speech-to-Text API, Translate API:** Önceden eğitilmiş modellerin kullanımı.
- **Ağ (Networking):**
    - **Virtual Private Cloud (VPC):** Özel ağlar oluşturma.
    - **Cloud Load Balancing:** Trafiği dengeleme.
    - **Cloud CDN:** İçerik dağıtım ağı hizmeti.
- **Güvenlik ve Yönetim Araçları:**
    - **Identity and Access Management (IAM):** Erişim kontrolü.
    - **Cloud Key Management Service (KMS):** Şifreleme anahtarlarının yönetimi.
    - **Cloud Security Scanner:** Güvenlik taraması.

#### **4.1.2. GCP'nin Avantajları**
- **Google'ın Küresel Altyapısı:**
    - Hızlı ve güvenilir ağ bağlantıları.
    - Düşük gecikmeli iletişim ve yüksek performans.
- **Yenilikçi Teknolojiler:**
    - Makine öğrenmesi ve yapay zeka hizmetlerinde liderlik.
    - Büyük veri işleme ve analitiği için gelişmiş araçlar.
- **Açık Kaynak Desteği:**
    - Kubernetes, TensorFlow gibi projelerin gelişimine katkı.
    - Açık standartlara uyumluluk ve esneklik.
- **Esneklik ve Maliyet Etkinliği:**
    - Kullanıma dayalı fiyatlandırma.
    - Susturucu örnekler ve indirimli fiyatlandırma seçenekleri.
- **Güvenlik ve Uyumluluk:**
    - Gelişmiş güvenlik özellikleri ve uyumluluk sertifikaları.
    - Veri şifreleme ve erişim kontrolü.

### **5.1. GCP Temel Hizmetleri**

#### **5.1.1. Compute Engine**

**Compute Engine**, Google'ın ölçeklenebilir ve yüksek performanslı sanal makine hizmetidir. Kullanıcıların ihtiyaçlarına göre özelleştirilebilir ve farklı işletim sistemlerini destekler.

- **Özellikler:**
    
    - **Özel Makine Türleri:** İş yükünüze uygun CPU ve bellek kombinasyonlarını seçebilirsiniz.
    - **Otomatik Ölçeklendirme:** Trafiğe veya iş yüküne göre kaynakları otomatik olarak ayarlayabilir.
    - **Sanal Özel Bulut (VPC) Entegrasyonu:** Ağ yapılandırmalarınızı özelleştirebilirsiniz.
    - **Depolama Seçenekleri:** Kalıcı diskler, yerel SSD'ler ve bulut depolama entegrasyonu.
- **Kullanım Durumları:**
    
    - Web ve uygulama sunucularının barındırılması.
    - Yüksek performanslı işlem gerektiren uygulamalar.
    - Özel uygulama ortamları ve test senaryoları.

**Örnek: Compute Engine'de Sanal Makine Oluşturma**

- **Adım 1:** Google Cloud Console'da **Compute Engine** bölümüne gidin.
- **Adım 2:** **VM Instances** sekmesinde **Create Instance** butonuna tıklayın.
- **Adım 3:** Makine yapılandırmasını belirleyin (bölge, makine türü, işletim sistemi).
- **Adım 4:** **Create** butonuna tıklayarak sanal makineyi oluşturun.

#### **5.1.2. Cloud Storage**

**Cloud Storage**, Google'ın nesne depolama hizmetidir ve her tür veri için ölçeklenebilir ve dayanıklı bir depolama çözümü sunar.

- **Özellikler:**
    
    - - **Yüksek Dayanıklılık ve Erişilebilirlik:** %99.999999999 (11 dokuz) dayanıklılık.
    - **Veri Şifreleme:** Varsayılan olarak tüm veriler şifrelenir.
    - **Entegrasyon:** Diğer GCP hizmetleriyle sorunsuz entegrasyon.
    - **Sınırsız Depolama Kapasitesi:** Büyük miktarda veriyi depolayabilir.
	    - **Depolama Sınıfları:**
			- **Standart Depolama:** Standart Depolama, sıkça erişilen ve yüksek performans gerektiren veriler için tasarlanmış bir depolama sınıfıdır. Düşük gecikme süresi ve yüksek kullanılabilirlik sunar, bu da onu aktif veri kullanımına uygun hale getirir.
				- **Kullanım Senaryoları:**
					- **Web Siteleri ve Uygulamalar:** Dinamik içerik sunumu ve kullanıcı verileri.
					- **Veritabanları:** Hızlı erişim gerektiren veritabanı işlemleri.
					- **Gerçek Zamanlı Analitik:** Anlık veri işleme ve analiz ihtiyaçları.
					- **Sık Erişilen Dosyalar:** Günlük olarak kullanılan belgeler ve medya dosyaları.
			- **Nearline Depolama:** Nearline Depolama, ayda en az bir kez erişilen veriler için ekonomik bir depolama seçeneğidir. Maliyet etkinliği yüksek olup, veri erişim maliyetleri Standart Depolamaya göre daha düşüktür, ancak erişim süresi biraz daha uzundur.
				- **Kullanım Senaryoları:**
					- **Yedeklemeler:** Düzenli yedekleme verilerinin saklanması.
					- **Felaket Kurtarma:** Olası veri kayıplarına karşı hazırlık.
					- **Periyodik Veri Analizi:** Belirli aralıklarla işlenen veri setleri.
					- **Arşivleme:** Geçici olarak saklanan ancak düzenli olarak erişilen veriler.	
			- **Coldline Depolama:** Coldline Depolama, çeyrek dönemde bir kez veya daha seyrek erişilen veriler için optimize edilmiştir. Depolama maliyetleri düşüktür ancak veri erişim maliyetleri daha yüksektir, bu da uzun süreli depolama için idealdir.
				- **Kullanım Senaryoları:**
					- **Uzun Vadeli Yedeklemeler:** Uzun süre saklanması gereken yedek veriler.
					- **Büyük Veri Setleri:** Uydu görüntüleri, sensör verileri gibi geniş veri kümeleri.
					- **Düşük Sıklıkta Erişilen Arşivler:** Eski projelere ait belgeler ve kayıtlar.
					- **Medya Arşivleme:** Dijital medya dosyalarının uzun süreli saklanması.
			- **Arşiv Depolama:** Arşiv Depolama, yıllık olarak veya daha seyrek erişilen veriler için en düşük maliyetli depolama sınıfıdır. Veri geri getirme süresi en uzun olup, maliyet etkinliği ön plandadır.	
				- **Kullanım Senaryoları:**
					- **Düzenleyici Arşivler:** Yasal gereklilikler nedeniyle uzun süre saklanması gereken veriler.
					- **Dijital Arşivler:** Tarihi belgeler, fotoğraflar ve videoların saklanması.
					- **Eski Proje Verileri:** Tamamlanmış projelere ait belgelerin arşivlenmesi.
					- **Uzun Vadeli Veri Saklama:** Kurumsal veri saklama politikalarına uygun uzun süreli depolama ihtiyaçları.
- **Kullanım Durumları:**
    - Veri yedekleme ve arşivleme.
    - Medya içeriği depolama.
    - Büyük veri analitiği için veri gölü oluşturma.
    - Statik web sitesi barındırma.
#### **5.1.3. BigQuery**

**BigQuery**, tam yönetilen ve sunucusuz bir veri ambarı ve analitik hizmetidir
- **Özellikler:**
    - **SQL Sorguları:** Standart SQL kullanarak veri sorgulama.
    - **Gerçek Zamanlı Analitik:** Akış verilerini gerçek zamanlı olarak analiz edebilirsiniz.
    - **Otomatik Ölçeklenebilirlik:** Veritabanını ve altyapıyı yönetmek zorunda değilsiniz.
    - **Düşük Maliyetli Depolama ve Sorgu Fiyatlandırması:** Kullanıma dayalı fiyatlandırma modeli.
- **Kullanım Durumları:**
    - Büyük veri analitiği ve iş zekâsı.
    - Makine öğrenmesi modellerinin eğitimi için veri hazırlığı.
    - Veri görselleştirme ve raporlama.
#### **5.1.4. Dataflow**

**Dataflow**, gerçek zamanlı ve toplu veri işleme için tam yönetilen bir hizmettir.

- **Özellikler:**
    
    - **Apache Beam SDK Desteği:** Java ve Python ile veri işleme boru hatları oluşturma.
    - **Sunucusuz ve Otomatik Ölçeklenebilirlik:** Altyapı yönetimine gerek yoktur.
    - **Gerçek Zamanlı ve Toplu İşleme:** Tek bir API ile hem akış hem de toplu verileri işleyebilirsiniz.
- **Kullanım Durumları:**
    
    - ETL (Extract, Transform, Load) işlemleri.
    - Veri temizleme ve zenginleştirme.
    - Gerçek zamanlı analitik ve makine öğrenmesi uygulamaları.
#### **5.1.5. Pub/Sub**

**Pub/Sub**, mesajlaşma ve akış veri işleme için tam yönetilen bir hizmettir.

- **Özellikler:**
    
    - **Gerçek Zamanlı Mesajlaşma:** Üretici ve tüketiciler arasında asenkron iletişim sağlar.
    - **Yüksek Ölçeklenebilirlik:** Büyük miktarda veriyi düşük gecikmeyle işleyebilir.
    - **Entegrasyon:** Diğer GCP hizmetleriyle sorunsuz entegrasyon.
- **Kullanım Durumları:**
    
    - Gerçek zamanlı veri akışı ve işleme.
    - Uygulama bileşenleri arasında iletişim.
    - IoT cihazlarından gelen verilerin toplanması.
#### **5.1.6. Cloud Functions**

**Cloud Functions**, sunucusuz ve olay tabanlı bir hesaplama hizmetidir.
- **Özellikler:**
    - **Olay Tabanlı Çalışma:** Belirli bir olay gerçekleştiğinde otomatik olarak tetiklenir.
    - **Sunucusuz Mimari:** Altyapı yönetimi gerektirmez.
    - **Farklı Programlama Dilleri Desteği:** Node.js, Python, Go ve diğerleri.
- **Kullanım Durumları:**
    - Arka plan işlemleri ve otomasyon.
    - API ve web hizmetleri oluşturma.
    - Veri işleme ve dönüşümü.
#### **5.1.7. Cloud Run**

**Cloud Run**, konteyner tabanlı, sunucusuz bir uygulama çalıştırma platformudur. Geliştiricilere konteynerlerin esnekliği ile sunucusuz altyapının yönetim kolaylığını bir arada sunar.

- **Özellikler:**
    - **Konteyner Desteği:** Her türlü programlama dili ve kütüphaneyi destekleyen konteynerler çalıştırabilirsiniz.
    - **Otomatik Ölçeklenebilirlik:** Trafiğe göre otomatik olarak ölçeklenir ve sıfırdan başlayabilir veya durabilir.
    - **Sunucusuz Yönetim:** Altyapıyı yönetmek zorunda kalmazsınız; sadece kodunuzu veya konteynerinizi geliştirirsiniz.
    - **Entegrasyon:** Diğer GCP hizmetleriyle (Pub/Sub, Cloud SQL, vb.) kolay entegrasyon.
    - **Ödeme Modeli:** Sadece kullandığınız kaynaklar için ödeme yaparsınız.
- **Kullanım Durumları:**
    - Web uygulamaları ve API'ler.
    - Mikro hizmet mimarileri.
    - Arka plan işleme görevleri.
    - Gerçek zamanlı veri işleme uygulamaları.
## **5.1.8. Compute Engine**
**Compute Engine**, Google Cloud Platform'un (GCP) yüksek performanslı, ölçeklenebilir ve esnek sanal makine (VM) hizmetidir. Kullanıcılara, kendi özel yapılandırmalarını seçerek ihtiyaçlarına uygun VM'ler oluşturma ve yönetme imkanı tanır. Compute Engine, geniş bir makine türü yelpazesi, özelleştirilebilir depolama seçenekleri ve güçlü ağ özellikleri ile çeşitli kullanım senaryolarına uyum sağlar.
- **Özellikler:**
	- **Özel Makine Türleri:**
	    - **Standart, Yüksek Bellek ve Yüksek CPU:** Farklı iş yüklerine uygun olarak çeşitli makine türleri sunar.
	    - **Özelleştirilebilir Kaynaklar:** Kullanıcılar, ihtiyaçlarına göre CPU ve bellek miktarını özelleştirebilirler.
	- **Otomatik Ölçeklendirme:**
	    - **Otomatik VM Oluşturma ve Silme:** Trafik veya iş yüküne bağlı olarak VM sayısını otomatik olarak artırır veya azaltır.
	    - **Hizmet İlişkili Otomatik Ölçeklendirme:** Belirli hizmetler için otomatik olarak kaynak ayarlaması yapar.
	- **Sanal Özel Bulut (VPC) Entegrasyonu:**
	    - **Ağ Güvenliği ve Yönetimi:** Özel ağlar oluşturabilir, güvenlik duvarı kuralları tanımlayabilir ve trafik akışını kontrol edebilirsiniz.
	    - **Global Ağ Altyapısı:** GCP'nin küresel ağ altyapısı sayesinde düşük gecikme süreleri ve yüksek bant genişliği sunar.
	- **Depolama Seçenekleri:**
	    - **Kalıcı Diskler:** Yüksek performanslı SSD veya maliyet-etkin HDD seçenekleri.
	    - **Yerel SSD'ler:** Düşük gecikmeli geçici depolama için idealdir.
	    - **Bulut Depolama Entegrasyonu:** Compute Engine, Cloud Storage gibi diğer GCP depolama hizmetleriyle sorunsuz entegrasyon sağlar.
	- **Güvenlik:**
	    - **Veri Şifreleme:** Hem atıl durumda hem de aktarım halindeyken veri şifrelemesi sağlar.
	    - **Identity and Access Management (IAM):** Rol tabanlı erişim kontrolü ile güvenliği artırır.
	    - **Güvenlik Güncellemeleri:** Otomatik güvenlik yamaları ve güncellemeleri ile güvenliği sağlar.
	- **Yüksek Erişilebilirlik ve Dayanıklılık:**
	    - **Canary Dağıtımları:** Yeni sürümlerin güvenli bir şekilde dağıtılmasını sağlar.
	    - **Otomatik Yedekleme ve Geri Yükleme:** Verilerinizi otomatik olarak yedekler ve gerektiğinde geri yüklemenize olanak tanır.
- **Kullanım Senaryoları:**
	- **Web ve Uygulama Sunucuları:**
	    - Yüksek trafikli web siteleri ve uygulamalar için güçlü ve ölçeklenebilir altyapı sağlar.
	- **Veri İşleme ve Analitiği:**
	    - Büyük veri setlerini işlemek ve analiz etmek için güçlü hesaplama kaynakları sunar.
	- **Geliştirme ve Test Ortamları:**
	    - Farklı yapılandırmalarda geliştirme ve test ortamları oluşturmak için idealdir.
	- **Özel Uygulama Ortamları:**
	    - Belirli gereksinimleri olan özel uygulamalar için tam kontrol sağlar.
	- **Mühendislik ve Simülasyonlar:**
	    - Karmaşık mühendislik simülasyonları ve modellemeler için yüksek performanslı hesaplama kaynakları sunar.

### **Compute Engine vs. Cloud Run**
#### **Compute Engine (VM)**
- **Sürekli Çalışma:** Compute Engine, sanal makineler (VM'ler) sağlar ve bu VM'ler, başlatıldıklarında sürekli olarak çalışır durumdadır. VM'leri durdurmadıkça veya kapatmadıkça, her zaman erişilebilir ve işlem yapabilirler.
- **Altyapı Yönetimi:** Kullanıcıların işletim sistemi güncellemeleri, güvenlik yamaları ve diğer altyapı yönetim görevlerini kendilerinin yapması gerekir.
- **Kaynak Kullanımı:** VM'ler, tahsis edilen CPU, bellek ve depolama kaynaklarına göre ücretlendirilir, bu da kaynaklar kullanılmasa bile maliyetin devam etmesine neden olabilir.
- **Kullanım Senaryoları:**
    - Sürekli çalışan sunucular.
    - Yüksek performans gerektiren uygulamalar.
    - Özel yapılandırmalar ve uzun süreli işlemler.
#### **Cloud Run**
- **Sunucusuz ve Talep Üzerine Çalışma:** Cloud Run, konteyner tabanlı sunucusuz bir hizmettir. Uygulamalarınıza gelen isteklere göre otomatik olarak ölçeklenir. Trafik olmadığında, kaynaklar otomatik olarak ölçeklenir ve maliyet düşer.
- **Altyapı Yönetimi Gerektirmez:** Cloud Run, altyapıyı otomatik olarak yönetir, böylece kullanıcıların sunucu yönetimiyle uğraşmasına gerek kalmaz.
- **Konteyner Desteği:** Herhangi bir programlama dili veya kütüphane ile uyumlu konteynerler çalıştırabilirsiniz.
- **Maliyet Etkinliği:** Sadece uygulamanız aktif olarak çalıştığında (istek alındığında) kaynaklar için ödeme yaparsınız. Trafik olmadığında maliyet düşer veya sıfır olabilir.
- **Kullanım Senaryoları:**
    - Mikro hizmetler ve API'ler.
    - Web uygulamaları.
    - Arka plan işleme görevleri.
    - Gerçek zamanlı veri işleme uygulamaları.
### **5.2. GCP’de Veri Yönetimi Senaryoları**
**Örnek Senaryo 1: Büyük Veri Analitiği**
- **Durum:** Bir şirket, büyük miktarda müşteri verisini analiz ederek pazarlama stratejilerini optimize etmek istiyor.
- **Çözüm:**
    - **Veri Depolama:** Müşteri verileri **Cloud Storage** veya **BigQuery**'de depolanır.
    - **Veri İşleme:** **Dataflow** kullanarak veriler temizlenir ve işlenir.
    - **Analiz ve Raporlama:** **BigQuery** ile SQL sorguları çalıştırılır ve sonuçlar görselleştirilir.

**Örnek Senaryo 2: Gerçek Zamanlı IoT Veri İşleme**
- **Durum:** Bir üretim tesisi, sensörlerden gelen verileri gerçek zamanlı olarak izlemek istiyor.
- **Çözüm:**
    - **Veri Toplama:** Sensör verileri **Pub/Sub** kullanarak toplanır.
    - **Veri İşleme:** **Dataflow** ile gerçek zamanlı analiz yapılır.
    - **Depolama ve Görselleştirme:** İşlenmiş veriler **BigQuery**'de depolanır ve dashboard'lar üzerinden izlenir.

**Örnek Senaryo 3: Web Uygulaması Barındırma**
- **Durum:** Bir startup, ölçeklenebilir bir web uygulaması geliştirmek istiyor.
- **Çözüm:**
    - **Hesaplama Kaynakları:** **Compute Engine** veya **App Engine** kullanılır.
    - **Veri Depolama:** Uygulama verileri **Cloud SQL** veya **Firestore**'da tutulur.
    - **Statik İçerik:** Resimler ve diğer statik dosyalar **Cloud Storage**'da depolanır.
    - **Sunucusuz Fonksiyonlar:** **Cloud Functions** ile arka plan işlemleri ve API'ler oluşturulur.

