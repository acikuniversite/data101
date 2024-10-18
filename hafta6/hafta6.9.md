## Workshop
### Senaryo:
Bir yazılım geliştirici topluluğu, Github üzerindeki trend projeleri ve konuları takip etmek istiyor. Amacınız, Github Trends sayfasından en popüler projelerin bilgilerini toplayarak, bu veriyi analiz etmeye uygun bir formata dönüştürmek ve veri ambarına yüklemek. Toplanan verilerdeki projelerin adı, yıldız sayısı, dil bilgisi ve açıklamaları gibi alanlar yer alıyor.

### **Etkinlik Aşamaları:**

-  **1. Web Scraping ile Veri Toplama (30 dakika):**
	- Öğrenciler, Github Trends sayfasından web scraping tekniklerini kullanarak veri toplayacaklar.
	- **Adım 1:** Github Trends sayfasına erişim ve veri elementlerinin belirlenmesi.
	    - Proje adı, yıldız sayısı, açıklama ve kullanılan dil gibi bilgileri almak için HTML yapılarını inceleyin.
	- **Adım 2:** Python ile scraping işlemi gerçekleştirin (örneğin, **BeautifulSoup** veya **Scrapy** kullanarak).
	- **Adım 3:** Scraping sonucunda elde edilen verileri bir CSV dosyasına kaydedin.

-  **2. ETL Süreci: Veriyi Temizleme ve Dönüştürme (20 dakika):**
	- Öğrenciler, topladıkları veriyi ETL adımlarıyla temizleyip dönüştürecekler.
	- **Veri Temizleme:**
	    - Eksik verileri doldurun veya temizleyin (örneğin, dil bilgisi olmayan projeler).
	    - Gereksiz HTML öğelerini temizleyin (örneğin, metinlerdeki fazla boşluklar).
	- **Veri Dönüştürme:**
	    - Yıldız sayısı verilerini sayısal bir formata dönüştürün (örneğin, 1.5k → 1500).
	    - Python'da pandas kullanarak CSV verisini dataframe'e çevirin ve dönüşüm işlemlerini uygulayın
-  **3. Veri Ambarına Yükleme (20 dakika):**
	- Öğrenciler, dönüştürdükleri veriyi bir veri ambarına veya SQL veritabanına yükleyecekler.
	- **Veritabanı Oluşturma:** Öğrenciler PostgreSQL gibi bir veritabanı sistemi kullanarak veritabanı oluşturacaklar ve verilerini yükleyecekler.
-  **4. Performans ve Ölçeklenebilirlik (10 dakika):**
	- Öğrenciler, topladıkları veri büyüdüğünde performansı nasıl optimize edebileceklerini ve ölçeklenebilirlik için hangi teknikleri kullanacaklarını tartışacaklar.
	- **İndeksleme:** Veritabanındaki sorgu performansını artırmak için indeksleme yapın (örn. proje adı veya yıldız sayısına göre).
	- **Veri Şekillendirme:** Büyük veri kümeleri ile çalışırken veri bölme (partitioning) stratejilerini tartışın.
- **5. Sonuç ve Tartışma (10 dakika):**
	- Öğrenciler, ETL süreçlerinde karşılaştıkları zorlukları, çözüm önerilerini ve Github trends verisi üzerinden elde ettikleri sonuçları paylaşırlar.