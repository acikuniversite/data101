### **5. Büyük Veri ve Büyük Veri Mühendisliği**

#### **Büyük Veri Nedir?**

- **Tanım:**
    - **5V** ile tanımlanır:
        - **Hacim (Volume):** Büyük miktarda veri.
        - **Hız (Velocity):** Verinin hızlı bir şekilde üretilmesi ve işlenmesi.
        - **Çeşitlilik (Variety):** Farklı tiplerde veri (yapılandırılmış, yarı yapılandırılmış, yapılandırılmamış).
        - **Doğruluk (Veracity):** Verinin doğruluğu ve güvenilirliği.
        - **Değer (Value):** Verinin iş değeri.

#### **Büyük Veri Teknolojileri**

- **Hadoop Ekosistemi:**
    - **HDFS (Hadoop Distributed File System):**
        - Büyük verilerin dağıtık olarak depolanması.
    - **MapReduce:**
        - Büyük veri setlerinin paralel işlenmesi.
    - **YARN:**
        - Kaynak yönetimi ve iş planlama.
    - **Hive, Pig:**
        - Büyük veri üzerinde sorgulama ve veri işleme.
- **Apache Spark:**
    - **Özellikler:**
        - Bellek içi veri işleme ile hızlı ve ölçeklenebilir.
        - **Modüller:**
            - **Spark SQL:** Yapılandırılmış verilerin işlenmesi.
            - **Spark Streaming:** Gerçek zamanlı veri işleme.
            - **MLlib:** Makine öğrenmesi kütüphanesi.
            - **GraphX:** Grafik verilerinin işlenmesi.
- **NoSQL Veritabanları:**
    - **Sütun Tabanlı:** **Apache HBase**, **Cassandra**.
    - **Belge Tabanlı:** **MongoDB**, **CouchDB**.
    - **Anahtar-Değer Tabanlı:** **Redis**, **Riak**.
- **Gerçek Zamanlı Veri İşleme:**
    - **Apache Kafka:**
        - Dağıtık yayın abonelik sistemi, veri akışlarının yönetimi.
    - **Apache Flink:**
        - Akış ve yığın veri işleme için düşük gecikmeli ve yüksek performanslı bir platform.
    - **Apache Beam:**
        - Yüksek seviye veri işleme API'si, farklı arka uçlarla çalışabilir (Spark, Flink, Dataflow).

#### **Büyük Veri Mühendisinin Rolü**

- **Altyapı Yönetimi:**
    - Büyük veri işleme platformlarının kurulumu, yapılandırılması ve yönetimi.
- **Veri Boru Hatları Oluşturma:**
    - Büyük veri setlerinin işlenmesi için ölçeklenebilir ve güvenilir süreçlerin geliştirilmesi.
- **Performans Optimizasyonu:**
    - İş yüklerinin optimize edilmesi, kaynak kullanımının iyileştirilmesi.
- **Güvenlik ve Erişim Kontrolleri:**
    - Veri erişim politikalarının uygulanması, yetkilendirme ve kimlik doğrulama.

#### **Güncel Teknolojiler ve Trendler**

- **Bulut Tabanlı Büyük Veri Çözümleri:**
    - **Amazon EMR**, **Google Cloud Dataproc**, **Azure HDInsight**.
- **Lakehouse Mimarisi:**
    - **Delta Lake**, **Apache Hudi**, **Apache Iceberg** ile veri göllerinin yapılandırılması ve ACID özelliklerinin sağlanması.
- **Kubernetes ve Büyük Veri:**
    - **Spark on Kubernetes**, **Flink on Kubernetes** ile konteynerize büyük veri iş yükleri.
- **Sunucusuz (Serverless) Veri İşleme:**
    - **AWS Lambda**, **Google Cloud Functions**, **Azure Functions** ile esnek ve ölçeklenebilir veri işleme.

---

