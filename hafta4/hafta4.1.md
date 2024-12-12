## **1. NoSQL Nedir ve Ne Zaman Kullanılır?**

### NoSQL Nedir?
- **NoSQL (Not Only SQL):** Geleneksel ilişkisel veritabanlarının dışında kalan ve çeşitli veri modellerini kullanan veritabanı sistemleridir.
- **Özellikleri:**
  - **Esnek Şema Yapısı:** Veri modelleri dinamik ve esnektir.
  - **Yatay Ölçeklenebilirlik:** Büyük veri hacimleri için uygun.
  - **Yüksek Performans:** Hızlı okuma ve yazma işlemleri. 
  - **Dağıtık Mimari:** Verilerin birden fazla sunucuya dağıtılması.

### Ne Zaman Kullanılır? (ve/veya)
- **Büyük Veri Uygulamaları:** Yüksek hacimli verilerin depolanması ve işlenmesi. (Bir uygulamanın 1 TB üstü event loglarını depolamanız gerekiyorsa...)
- **Gerçek Zamanlı Veri İşleme:** Düşük gecikmeli veri erişimi gereken uygulamalar. (Bir Sosyal medya uygulamasında like, comment, share gibi işlemlerin anlık olarak işlenmesi...)
- **Esnek Veri Modelleri:** Dinamik ve değişken veri yapılarıyla çalışırken. (Örneğin, bir e-ticaret uygulamasında ürünlerin özelliklerinin sürekli değişmesi, örneğin renk, beden, fiyat gibi...)
- **Yüksek Trafikli Web ve Mobil Uygulamalar:** Ölçeklenebilirlik ve performans için. (Anlık çok yüksek sayıda kullanıcıya hizmet veren bir uygulama gibi mesela bir sosyal medya uygulaması...)

## **2. NoSQL Veritabanı Türleri**
### Anahtar-Değer Depoları
- **Tanım:** Verileri basit bir anahtar ve değer çifti olarak depolar.
- **Kullanım Alanları:** Önbellekleme, oturum yönetimi, basit veri depolama.
- **Bazı Uygulamalar:** Redis, Riak, Amazon DynamoDB.
- **Örnek Senaryo:** 
  - Netflix izleme geçmişi ve kullanıcı tercihlerini saklamak için kullanıyor.
  - Twitter, Gerçek zamanlı analitik (örneğin, trendlerin belirlenmesi) için kullanıyor.
  - Riot Games, League of Legends oyununun Oyun içi oturum ve liderlik tabloları için kullanıyor.
### Belge Tabanlı Veritabanları
- **Tanım:** Verileri JSON, BSON gibi belge formatlarında saklar.
- **Kullanım Alanları:** Esnek ve karmaşık veri yapılarının depolanması.
- **Bazı Uygulamalar:** MongoDB, CouchDB.
- **Örnek Senaryo:** 
  - Ebay, Ürün kataloglarının ve kullanıcı verilerinin depolanması için kullanıyor.
  - LinkedIn, Profil bilgileri ve bağlantılarının saklanması için kullanıyor.
  - NV GL (Gemi inşaatı ve mühendislik), Teknik belgelerin ve verilerin saklanması için kullanıyor.
  - Facebook, Kullanıcı profilleri ve gönderilerin saklanması için kullanıyor.
### Sütun-Ailesi Depoları
- **Tanım:** Verileri sütun aileleri halinde depolar, büyük ve dağıtık veri setleri için optimize edilmiştir.
- **Kullanım Alanları:** Büyük veri analizleri, zaman serisi verileri.
- **Bazı Uygulamalar:** Apache Cassandra, HBase.
- **Örnek Senaryo:** 
  - Instagram, Kullanıcı aktiviteleri ve etkileşimlerin saklanması için kullanıyor.
  - Google, BigTable altyapısını kullanarak, Gmail, Google Takvim, Google Haritalar gibi hizmetlerde kullanıyor.
  - Adobe, Kullanıcı davranışlarının analitik verilerle işlenmesi için kullanıyor.
### Grafik Veritabanları
- **Tanım:** Verileri düğümler ve kenarlar şeklinde depolar, ilişkileri doğrudan temsil eder.
- **Kullanım Alanları:** Sosyal ağlar, öneri sistemleri, bağlantı analizi.
- **Bazı Uygulamalar:** Neo4j, OrientDB.
- **Örnek Senaryo:** 
  - Uber, Sürücülerin ve yolcuların ilişkilerini ve etkileşimlerini saklamak için kullanıyor.
  - eBay, Ürünlerin ve kullanıcıların ilişkilerini saklamak için kullanıyor.
  - Facebook, Arkadaşlık ilişkileri ve etkileşimlerin saklanması için kullanıyor.
  - Airbus, Havayolu ağlarının ve uçuş rotalarının saklanması için kullanıyor.

## **3. NoSQL Tasarım Kuralları**

NoSQL veritabanları tasarlanırken, ilişkisel veritabanlarından farklı bir yaklaşıma ihtiyaç duyulur. Aşağıdaki tasarım kuralları, NoSQL sistemlerinden en iyi şekilde yararlanmanızı sağlar:
### **3.1. Veriyi Erişim Desenine Göre Tasarla**
- **Açıklama:** NoSQL'de, veritabanı tasarımı uygulamanın erişim ihtiyaçlarına göre yapılır. Sık kullanılan sorgular ve okuma/yazma işlemleri ön planda tutulur.
- **Örnek:**
	- **E-ticaret:** Bir kullanıcı ürün sayfasını görüntülediğinde hem ürün detayları hem de öneriler aynı anda hızlı bir şekilde yüklenmeli. MongoDB gibi belge tabanlı bir veritabanında ürün detayları ve öneriler aynı belge içinde saklanabilir.
### **3.2. Yatay Ölçeklenebilirliği Düşün**
- **Açıklama:** NoSQL sistemleri, yatay olarak ölçeklenebilir. Veritabanı tasarımında, verinin farklı sunuculara dağıtılması dikkate alınmalıdır.
- **Örnek:**
	- **Sosyal Medya:** Twitter, kullanıcı oturum bilgilerini Redis kullanarak yatay olarak ölçeklendirir. Böylece milyonlarca kullanıcı eş zamanlı oturum açabilir.
### **3.3. Şema Tasarımında Esneklik Sağla**
- **Açıklama:** Şema tasarımı dinamik olmalı. Veritabanında farklı türden veri saklanabilmesi için önceden sabit şema tanımlamaktan kaçınılır.
- **Örnek:**
	- **E-ticaret Platformları:** Amazon'da her ürün farklı özelliklere sahiptir (renk, beden, malzeme). Bu farklılıkları belge tabanlı veritabanlarında JSON formatında esnek bir şekilde saklamak mümkündür.
### **3.4. Veri Tekrarlamasını Stratejik Kullan**
- **Açıklama:** NoSQL'de, ilişkisel veritabanlarındaki normalizasyon yerine denormalizasyon tercih edilir. Veriler sık kullanılan sorgulara göre birden fazla yerde tekrarlanabilir.
- **Örnek:**
	- **Haber Platformları:** Haber başlıkları, özetler ve yazar bilgileri birden fazla koleksiyonda saklanarak hızlı erişim sağlanır.
### **3.5. Tutarlılık, Kullanılabilirlik ve Bölünme Toleransı (CAP Teoremi)**
- **Açıklama:** NoSQL tasarımı sırasında CAP teoremi göz önünde bulundurulur. Tutarlılık (Consistency), Kullanılabilirlik (Availability) ve Bölünme Toleransı (Partition Tolerance) arasında denge sağlanır.
  - Tutarlılık(Consistency): Her okuma işlemi, en son yazılan veriyi gösterir.
  - Kullanılabilirlik(Availability): Her istek, başarılı bir yanıt alır.
  - Bölünme Toleransı(Partition Tolerance): Ağda oluşabilecek kesintilere rağmen sistem çalışmaya devam eder.
- **Örnek:**
  - **Finansal Uygulamalar:**
      - Banka sistemleri, genellikle **tutarlılık** ve **kullanılabilirlik** arasında bir denge kurar. Örneğin:
          - Para transferi gibi kritik işlemler, Cassandra gibi NoSQL sistemlerde güçlü tutarlılık (strong consistency) sağlanacak şekilde yapılandırılır. Bu, işlem sırasında verilerin hemen senkronize edilmesini gerektirir.
          - Daha düşük öncelikli işlemler (örneğin, ATM bakiye sorgulama) gecikmeli tutarlılık (eventual consistency) ile çalışabilir, çünkü bu işlemler birkaç saniyelik gecikmeyi tolere edebilir.
      - **Kullanılabilirlik** ve **bölünme toleransı** da kritik önem taşır. Örneğin, bir ağ kesintisi sırasında müşteri işlemleri kabul edilir ve daha sonra tutarlılık sağlanır.
  - **E-ticaret Uygulamaları:**
      - Amazon gibi büyük e-ticaret platformları, ürün önerileri ve stok bilgileri için **kullanılabilirlik** ve **bölünme toleransı** özelliklerini önceliklendirir. Bu sayede, bir kullanıcı ürünü sepete eklediğinde işlemi hemen görebilir; ancak stok bilgilerinin birkaç saniye gecikmeyle güncellenmesi kabul edilebilir.
  - **Sosyal Medya Uygulamaları:**
      - Twitter, Redis gibi NoSQL sistemlerde **kullanılabilirlik** ve **bölünme toleransı** özelliklerini ön planda tutar. Trend belirleme ve tweet dağıtımı gibi işlemler, gecikmeli tutarlılık ile çalışır; böylece milyonlarca kullanıcıya eş zamanlı hizmet verilir.
### **3.6. Okuma ve Yazma Yüklerini Dengeli Dağıt**
- **Açıklama:** Veri, okuma ve yazma işlemleri arasında dengeli bir şekilde dağıtılmalıdır. Aşırı okuma/yazma yükü performansı düşürebilir.
- **Örnek:**
	- **Çevrimiçi Oyunlar:** Riot Games, liderlik tabloları için Riak kullanarak yazma işlemlerinin hızlı ve tutarlı olmasını sağlar.
### **3.7. Veri Bölümleme (Sharding) Kullan**
- **Açıklama:** Büyük veri kümelerini yönetmek için veritabanı parçalanır (sharding). Her parça belirli bir sunucuda depolanır.
- **Örnek:**
	- **Sosyal Ağlar:**  Instagram, kullanıcı ve içerik verilerini coğrafi bölgelere ve kullanıcı kimlik aralıklarına göre Cassandra üzerinde böler. Böylece yük dengelemesi ve ölçeklenebilirlik sağlanırken, belirli bir coğrafi bölgedeki kullanıcıların verilerine daha düşük gecikme ile erişilir.
### **3.8. Veri Tutarlılığı Stratejisi Belirle**
- **Açıklama:** Kullanım senaryosuna göre, veritabanının tutarlılık modeli (güçlü tutarlılık, eventual consistency vb.) seçilmelidir.
- **Örnek:**
	- **E-Ticaret:** Amazon DynamoDB, stok yönetiminde tutarlı verileri önceliklendirirken, kullanıcı önerilerinde eventual consistency kullanır.
### **3.9. Yedekleme ve Felaket Kurtarma Planları Yap**
- **Açıklama:** Dağıtık yapılar, veritabanının yedekleme ve felaket kurtarma stratejileriyle desteklenmelidir.
- **Örnek:**
	- **Finansal Sistemler:** PayPal, Cassandra'nın yedekleme ve veri çoğaltma özelliklerini kullanarak sistemin her zaman erişilebilir olmasını sağlar.

