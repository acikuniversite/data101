### **6. Veri Ambarı ve Veri Gölü**

#### **Veri Ambarı (Data Warehouse) Nedir?**

- **Tanım:**
    - Analitik ve raporlama amaçlı yapılandırılmış verilerin merkezi ve tarihsel olarak saklandığı sistem.
- **Mimari Yaklaşımlar:**
    - **Kimball Metodolojisi:** Boyutlu modelleme ve yıldız şeması tasarımları.
    - **Inmon Metodolojisi:** Kurumsal veri ambarı ve konu odaklı veri pazarları (Data Marts).

#### **Veri Gölü (Data Lake) Nedir?**

- **Tanım:**
    - Her türlü verinin (yapılandırılmış, yarı yapılandırılmış, yapılandırılmamış) ham haliyle saklandığı merkezi depolama sistemi.
- **Özellikler:**
    - **Schema-on-Read:** Verinin okuma sırasında şemalandırılması.
    - **Esneklik ve Ölçeklenebilirlik:** Büyük miktarda veri depolama kapasitesi.
- **Zorluklar:**
    - **Veri Bataklığı (Data Swamp) Riski:** Yönetilmeyen veri göllerinin kullanılamaz hale gelmesi.

#### **Göl Evi (Lakehouse) Mimarisi**

- **Tanım:**
    - Veri gölü ve veri ambarının en iyi özelliklerini birleştiren hibrit mimari.
- **Özellikler:**
    - **ACID Desteği:** Veri bütünlüğü ve tutarlılığı.
    - **Performans Optimizasyonu:** Hızlı sorgu ve veri işleme yetenekleri.
- **Teknolojiler:**
    - **Delta Lake:** **Databricks** tarafından geliştirilen açık kaynaklı proje.
    - **Apache Hudi:** Uber tarafından geliştirilen veri yönetimi çerçevesi.
    - **Apache Iceberg:** Netflix tarafından geliştirilen tablosal veri biçimi.

#### **Teknolojiler ve Uygulamalar**

- **Bulut Tabanlı Veri Ambarları:**
    - **Snowflake:** Sunucusuz, ölçeklenebilir ve çoklu bulut desteği.
    - **Amazon Redshift Serverless:** Kullandıkça öde modeli ile esnek veri ambarı.
    - **Google BigQuery:** Sunucusuz, yüksek performanslı analitik veri ambarı.
- **Veri Gölü Yönetimi:**
    - **AWS Lake Formation:** Veri gölü oluşturma ve yönetme hizmeti.
    - **Azure Data Lake Storage Gen2:** Ölçeklenebilir ve yüksek performanslı veri gölü depolaması.
- **Veri Kataloğu ve Keşif Araçları:**
    - **AWS Glue Data Catalog**, **Apache Atlas**, **DataHub**.

---

