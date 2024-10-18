### **2. ETL ve ELT Süreçleri**

#### **ETL ve ELT Nedir?**

- **ETL (Extract, Transform, Load):**
    - Verilerin kaynak sistemlerden **çıkarılması**, hedef sistemlere uygun hale getirilmesi için **dönüştürülmesi** ve hedef sistemlere **yüklenmesi** sürecidir.
- **ELT (Extract, Load, Transform):**
    - Verilerin kaynak sistemlerden **çıkarılması**, doğrudan hedef sisteme **yüklenmesi** ve dönüşümlerin hedef sistem üzerinde **yapılması** sürecidir.
    - **Not:** Bulut tabanlı ve büyük veri ortamlarında yaygın olarak kullanılır, çünkü hedef sistemlerin işlem gücü dönüşümleri hızlı bir şekilde gerçekleştirebilir.

#### **2.1 Extract (Çıkarma) Yöntemleri**

- **Veri Kaynakları ve Teknikleri:**
    - **Veritabanları (SQL, NoSQL):**
        - **JDBC/ODBC** bağlantıları, **SQL** sorguları, **Change Data Capture (CDC)** teknikleri.
    - **Dosya Sistemleri:**
        - **FTP/SFTP**, **Amazon S3**, **Hadoop HDFS** gibi sistemlerden veri çekme.
    - **API'lar ve Web Servisleri:**
        - **RESTful API**, **GraphQL** kullanarak veri çekme.
    - **Gerçek Zamanlı Akışlar:**
        - **Apache Kafka**, **Amazon Kinesis**, **Google Pub/Sub** gibi mesajlaşma sistemleri.
- **Artımlı Veri Çekme:**
    - **Change Data Capture (CDC):**
        - Veritabanlarındaki değişiklikleri (INSERT, UPDATE, DELETE) izleyerek sadece değişen verileri çekme.
        - **Araçlar:** **Debezium**, **Oracle GoldenGate**, **AWS DMS**.
    - **Zaman Damgası veya Artan Anahtarlar:**
        - Kayıtlardaki son değişiklik zamanına veya artan bir anahtara göre verileri filtreleme.

#### **2.2 Transform (Dönüştürme) Yöntemleri**

- **Veri Temizleme ve Doğrulama:**
    - **Eksik Değerlerin İşlenmesi:**
        - **İmputation** teknikleriyle eksik değerleri doldurma (ortalama, medyan, en sık görülen değer).
    - **Anormal Değerlerin Tespiti:**
        - **Z-skoru**, **IQR (Interquartile Range)** gibi istatistiksel yöntemlerle aykırı değerleri belirleme.
    - **Veri Tipi Dönüşümleri:**
        - Örneğin, string'den tarih formatına veya float'tan integer'a dönüşüm.
- **Veri Zenginleştirme:**
    - **Lookup Tabloları:**
        - Kodları açıklamalara dönüştürme.
    - **Coğrafi Veriler:**
        - **GIS** sistemleri veya **API'lar** kullanarak coğrafi koordinatlardan adres bilgisi elde etme.
- **Veri Birleştirme ve Bölme:**
    - **Join İşlemleri:**
        - **Inner Join**, **Left Outer Join**, **Right Outer Join**, **Full Outer Join**.
    - **Union ve Union All:**
        - Veri setlerini birleştirme.
    - **Veri Bölme:**
        - Büyük veri setlerini mantıksal parçalara ayırma.
- **Kurallar ve İş Mantığı Uygulama:**
    - **İş Kuralları:**
        - Örneğin, belirli bir satış tutarının üzerindeki işlemlerin işaretlenmesi.
    - **Veri Maskeleme ve Anonimleştirme:**
        - Kişisel verilerin gizliliğini korumak için.

#### **2.3 Load (Yükleme) Yöntemleri**

- **Yükleme Modları:**
    - **Tam Yükleme:**
        - **Truncate and Load:** Hedef tablonun temizlenip yeniden doldurulması.
    - **Artımlı Yükleme:**
        - **Upsert (Update or Insert):** Var olan kayıtları güncelleme, yeni kayıtları ekleme.
        - **Append Only:** Sadece yeni kayıtları ekleme.
- **Hedef Sistemler ve Teknolojiler:**
    - **Veri Ambarları:**
        - **Amazon Redshift**, **Google BigQuery**, **Snowflake**, **Azure Synapse Analytics**.
    - **Veri Gölleri:**
        - **Amazon S3**, **Azure Data Lake Storage**, **Google Cloud Storage**.
    - **NoSQL Veritabanları:**
        - **MongoDB**, **Cassandra**, **Elasticsearch**.

#### **Güncel ETL/ELT Araçları ve Teknolojileri**

- **Geleneksel ETL Araçları:**
    - **Informatica PowerCenter**, **IBM DataStage**, **Microsoft SSIS**, **Talend**.
- **Bulut Tabanlı ETL/ELT Araçları:**
    - **AWS Glue**, **Azure Data Factory**, **Google Cloud Dataflow**, **Matillion**, **Fivetran**.
- **Kod Tabanlı ETL Çözümleri:**
    - **Apache Beam**, **Apache Spark** ile **PySpark** veya **Scala** kullanarak özelleştirilmiş veri işleme.
- **Gerçek Zamanlı Veri İşleme:**
    - **Kafka Streams**, **Apache Flink**, **Apache Storm**.

---

