## **5. Amazon Web Services (AWS) ile Veri Yönetimi**

### **5.1. AWS'ye Giriş*
#### **5.1.1. AWS Hizmetlerinin Genel Bakışı*
**Amazon Web Services (AWS)**, Amazon tarafından sunulan ve geniş bir bulut hizmetleri yelpazesini içeren lider bir bulut platformudur. AWS, altyapıdan yapay zeka hizmetlerine kadar çeşitli çözümler sunarak işletmelerin dijital dönüşüm süreçlerini destekler.

**Temel Hizmet Kategorileri:*
- **Hesaplama (Compute):**
    - **Amazon EC2 (Elastic Compute Cloud):** Sanal sunucuların oluşturulması ve yönetimi.
    - **AWS Lambda:** Sunucusuz hesaplama hizmeti.
    - **Amazon ECS (Elastic Container Service) ve Amazon EKS (Elastic Kubernetes Service):** Konteyner orkestrasyonu için yönetilen hizmetler.
- **Depolama ve Veritabanları (Storage & Databases):**
    - **Amazon S3 (Simple Storage Service):** Nesne depolama hizmeti.
    - **Amazon EBS (Elastic Block Store):** Blok depolama hizmeti.
    - **Amazon RDS (Relational Database Service):** Yönetilen ilişkisel veritabanı.
    - **Amazon DynamoDB:** Tam yönetilen NoSQL veritabanı.
    - **Amazon Redshift:** Veri ambarı hizmeti.
- **Veri Analitiği (Analytics):**
    - **Amazon EMR (Elastic MapReduce):** Hadoop ve Spark için yönetilen hizmet.
    - **AWS Glue:** ETL (Extract, Transform, Load) ve veri kataloğu hizmeti.
    - **Amazon Kinesis:** Gerçek zamanlı akış verilerinin işlenmesi.
    - **Amazon Athena:** S3 üzerinde SQL sorguları çalıştırma hizmeti.
- **Makine Öğrenmesi ve Yapay Zeka (AI & Machine Learning):**
    - **Amazon SageMaker:** Makine öğrenmesi modellerinin geliştirilmesi ve dağıtılması.
    - **Amazon Rekognition, Comprehend, Polly:** Önceden eğitilmiş AI hizmetleri.
- **Ağ (Networking):**
    - **Amazon VPC (Virtual Private Cloud):** Özel ağlar oluşturma.
    - **Elastic Load Balancing (ELB):** Trafiği dengeleme.
    - **Amazon CloudFront:** İçerik dağıtım ağı hizmeti.
- **Güvenlik ve Yönetim Araçları:**
    - **AWS Identity and Access Management (IAM):** Erişim kontrolü.
    - **AWS Key Management Service (KMS):** Şifreleme anahtarlarının yönetimi.
    - **AWS CloudTrail:** Denetim günlükleri ve olay izleme.

#### **5.1.2. AWS'nin Avantajları*
- **Geniş Hizmet Yelpazesi:**
    - 200'den fazla hizmet ve sürekli genişleyen bir ekosistem.
- **Küresel Altyapı:**
    - 25'ten fazla coğrafi bölgede veri merkezleri ve 80'den fazla kullanılabilirlik bölgesi.
- **Güvenlik ve Uyumluluk:**
    - Gelişmiş güvenlik özellikleri ve ISO, SOC, HIPAA gibi çeşitli uyumluluk sertifikaları.
- **Esneklik ve Ölçeklenebilirlik:**
    - Otomatik ölçeklendirme, yük dengeleme ve elastik depolama seçenekleri.
- **Güçlü Topluluk ve Destek:**
    - Geniş bir kullanıcı topluluğu, kapsamlı dokümantasyon ve 7/24 teknik destek imkanı.

### **5.2. AWS Veri Depolama Hizmetleri*
#### **5.2.1. Amazon S3*
**Amazon Simple Storage Service (S3)**, nesne depolama hizmetidir ve her tür veri için ölçeklenebilir ve dayanıklı bir depolama çözümü sunar
- **Özellikler:**
    - **Sınırsız Depolama Kapasitesi:** Büyük miktarda veriyi depolayabilir.
    - **Depolama Sınıfları:**
        - **S3 Standard:** Sık erişilen veriler için optimize edilmiştir.
        - **S3 Intelligent-Tiering:** Erişim modellerine göre otomatik sınıf geçişi.
        - **S3 Standard-IA (Infrequent Access):** Az erişilen veriler için düşük maliyetli depolama.
        - **S3 One Zone-IA:** Az erişilen veriler için tek bölgede depolama.
        - **S3 Glacier ve Glacier Deep Archive:** Uzun süreli arşivleme için düşük maliyetli seçenekler.
    - **Yüksek Dayanıklılık ve Erişilebilirlik:** %99.999999999 (11 dokuz) dayanıklılık.
    - **Veri Şifreleme:** Varsayılan olarak tüm veriler şifrelenebilir.
    - **Entegrasyon:** Diğer AWS hizmetleriyle sorunsuz entegrasyon.
- **Kullanım Durumları:**
    - Veri yedekleme ve arşivleme.
    - Medya içeriği depolama.
    - Veri gölleri ve büyük veri analitiği.
    - Statik web sitesi barındırma.
- **Örnek: Amazon S3'te Dosya Yükleme ve İndirme**
```
# AWS CLI kullanarak
# Bir dosyayı yüklemek
aws s3 cp yerel_dosya.txt s3://bucket_adı/

# Bir dosyayı indirmek
aws s3 cp s3://bucket_adı/dosya.txt yerel_klasör/
```
#### **5.2.2. Amazon RDS*
**Amazon Relational Database Service (RDS)**, tam yönetilen ilişkisel veritabanı hizmetidir
- **Desteklenen Veritabanları:**
    
    - **MySQL**
    - **PostgreSQL**
    - **Oracle**
    - **SQL Server**
    - **MariaDB**
    - **Amazon Aurora**
- **Özellikler:**
    - **Otomatik Yedekleme:** Verilerinizi otomatik olarak yedekler ve gerektiğinde geri yükleyebilirsiniz.
    - **Yüksek Erişilebilirlik:** Multi-AZ dağıtımı ile hata toleransı sağlar.
    - **Ölçeklenebilirlik:** İş yüklerine göre kaynakları ayarlayabilirsiniz.
    - **Güvenlik:** Veri şifreleme, ağ güvenliği ve erişim kontrolü.
- **Kullanım Durumları:**
    - İş uygulamaları ve web uygulamaları için veritabanı desteği.
    - Analitik ve raporlama veritabanları.
- **Örnek: Amazon RDS'de Veritabanı Oluşturma**
    - **Adım 1:** AWS Management Console'da **RDS** bölümüne gidin.
    - **Adım 2:** **Create database** butonuna tıklayın.
    - **Adım 3:** Veritabanı türünü ve sürümünü seçin.
    - **Adım 4:** Veritabanı ayarlarını ve yapılandırmalarını belirleyin.
    - **Adım 5:** **Create database**'e tıklayarak işlemi tamamlayın.
- **Örnek Komut:**
```
aws rds create-db-instance \
    --db-instance-identifier mydbinstance \
    --db-instance-class db.t2.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password password \
    --allocated-storage 20
```
* Tanımlar: 
	- **`--db-instance-identifier mydbinstance`**
	    - **Açıklama:** Oluşturulacak veritabanı örneğine verilen benzersiz isimdir. Bu isim, veritabanı örneğinizi AWS hesabınız içinde tanımlamak için kullanılır.
	    - **Örnek:** `mydbinstance`
	- **`--db-instance-class db.t2.micro`**
	    - **Açıklama:** Veritabanı örneğinin donanım özelliklerini belirler. Bu, CPU, bellek ve ağ kapasitesi gibi kaynakları içerir. `db.t2.micro`, düşük maliyetli ve küçük ölçekli uygulamalar için uygundur.
	    - **Örnek Değerler:** `db.t2.micro`, `db.m5.large`, `db.r5.xlarge` vb.
	- **`--engine mysql`**
	    - **Açıklama:** Kullanılacak veritabanı motorunu belirtir. Burada `mysql` kullanılmıştır, ancak diğer desteklenen motorlar arasında PostgreSQL, MariaDB, Oracle, SQL Server ve Amazon Aurora bulunur.
	    - **Örnek Değerler:** `mysql`, `postgres`, `oracle-se2`, `sqlserver-ex` vb.
	- **`--master-username admin`**
	    - **Açıklama:** Veritabanının yönetici (master) kullanıcı adını belirler. Bu kullanıcı, veritabanını yönetmek için gerekli izinlere sahiptir.
	    - **Örnek:** `admin`
	- **`--master-user-password password`**
	    - **Açıklama:** Yönetici kullanıcısı için belirlenen şifredir. Güvenli bir şifre seçmek önemlidir. Şifrenin karmaşık ve tahmin edilmesi zor olması tavsiye edilir.
	    - **Örnek:** `password` (Gerçek uygulamalarda daha güçlü bir şifre kullanmalısınız.)
	- **`--allocated-storage 20`**
	    - **Açıklama:** Veritabanı örneğine tahsis edilecek depolama alanını gigabayt (GB) cinsinden belirtir. Bu değer, veritabanınızın veri depolama ihtiyaçlarına göre ayarlanmalıdır.
	    - **Örnek:** `20` GB
#### **5.2.3. Amazon DynamoDB*
**Amazon DynamoDB**, tam yönetilen ve sunucusuz bir NoSQL veritabanıdır
- **Özellikler:** 
    - **Yüksek Performans:** Milisaniye altı gecikme ve yüksek verimlilik.
    - **Otomatik Ölçeklenebilirlik:** Trafik taleplerine göre otomatik ölçeklenir.
    - **Sunucusuz Mimari:** Altyapı yönetimine gerek yoktur.
    - **Entegre Güvenlik:** IAM ile erişim kontrolü.
- **Kullanım Durumları:**  
    - Mobil, web ve IoT uygulamaları.
    - Oyun uygulamaları ve oturum yönetimi.
    - Gerçek zamanlı analitik ve kişiselleştirme.
- **Örnek: Amazon DynamoDB'de Tablo Oluşturma** 
    - **Adım 1:** AWS Management Console'da **DynamoDB** bölümüne gidin.
    - **Adım 2:** **Create table** butonuna tıklayın.
    - **Adım 3:** Tablo adını ve birincil anahtarları belirleyin.
    - **Adım 4:** Ek ayarları yapılandırın (okuma/yazma kapasitesi, şifreleme).
    - **Adım 5:** **Create table**'a tıklayarak işlemi tamamlayın.
- **Örnek Kod (Python Boto3 Kullanarak):**
```
import boto3

dynamodb = boto3.resource('dynamodb')

table = dynamodb.create_table(
    TableName='Kullanicilar',
    KeySchema=[
        {
            'AttributeName': 'kullanici_id',
            'KeyType': 'HASH'  # Partition key
        }
    ],
    AttributeDefinitions=[
        {
            'AttributeName': 'kullanici_id',
            'AttributeType': 'S'
        }
    ],
    ProvisionedThroughput={
        'ReadCapacityUnits': 5,
        'WriteCapacityUnits': 5
    }
)

# Tabloyu oluşturmak için bekleme
table.meta.client.get_waiter('table_exists').wait(TableName='Kullanicilar')
print("Tablo oluşturuldu:", table.table_status)
```

#### **5.2.4. Amazon Redshift*
**Amazon Redshift**, tam yönetilen bir veri ambarı hizmetidir
- **Özellikler:**
    - **Petabayt Ölçeğinde Veri Analizi:** Büyük veri setlerini hızlı bir şekilde sorgulayabilir.
    - **Kolon Bazlı Depolama:** Sorgu performansını artırır.
    - **Gelişmiş Sıkıştırma:** Depolama maliyetlerini düşürür.
    - **MPP (Massively Parallel Processing):** Paralel işlem gücüyle yüksek performans.
- **Kullanım Durumları:**
    - İş zekâsı ve veri analitiği uygulamaları.
    - Büyük veri iş yükleri.
    - Veri görselleştirme ve raporlama.
- **Örnek: Amazon Redshift Cluster Oluşturma**
    - **Adım 1:** AWS Management Console'da **Redshift** bölümüne gidin.
    - **Adım 2:** **Create cluster** butonuna tıklayın.
    - **Adım 3:** Cluster yapılandırmalarını belirleyin (düğüm sayısı, düğüm türü).
    - **Adım 4:** Güvenlik ayarlarını ve veritabanı ayarlarını yapılandırın.
    - **Adım 5:** **Create cluster**'a tıklayarak işlemi tamamlayın.
```
aws redshift create-cluster \
    --cluster-identifier myredshiftcluster \
    --node-type dc2.large \
    --master-username admin \
    --master-user-password password \
    --number-of-nodes 2
```

### **5.3. AWS ile Veri İşleme ve Analitiği*
#### **5.3.1. AWS Glue*
**AWS Glue**, tam yönetilen bir ETL (Extract, Transform, Load) hizmetidir
- **Özellikler:**  
    - **Veri Kataloğu:** Verilerinizi otomatik olarak keşfeder ve şema oluşturur.
    - **ETL İşleri:** PySpark kullanarak veri dönüşümleri yapabilirsiniz.
    - **Sunucusuz:** Altyapı yönetimine gerek yoktur.
- **Kullanım Durumları:**
    - Veri entegrasyonu ve dönüştürme.
    - Veri keşfi ve şema oluşturma.
    - Veri gölleri ve analitik platformlar.
- **Örnek: AWS Glue ile ETL İşi Oluşturma** 
    - **Adım 1:** AWS Management Console'da **Glue** bölümüne gidin.
    - **Adım 2:** **Add database** ile bir veritabanı oluşturun.
    - **Adım 3:** **Crawlers** ile veri kaynaklarını taratarak şemaları oluşturun.
    - **Adım 4:** **Jobs** bölümünde yeni bir ETL işi oluşturun.
    - **Adım 5:** PySpark kodu yazarak veri dönüşümlerini tanımlayın.
    - **Adım 6:** İşi çalıştırın ve sonuçları kontrol edin.
- **Örnek PySpark Kodu:**
```
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job

args = getResolvedOptions(sys.argv, ['JOB_NAME'])
sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)
job.init(args['JOB_NAME'], args)

# Veri Kaynağını Okuma
datasource0 = glueContext.create_dynamic_frame.from_catalog(database = "mydatabase", table_name = "mytable", transformation_ctx = "datasource0")

# Veri Dönüşümü
applymapping1 = ApplyMapping.apply(frame = datasource0, mappings = [("id", "string", "id", "string"), ("name", "string", "name", "string")], transformation_ctx = "applymapping1")

# Hedefe Yazma
datasink2 = glueContext.write_dynamic_frame.from_options(frame = applymapping1, connection_type = "s3", connection_options = {"path": "s3://mybucket/output/"}, format = "json", transformation_ctx = "datasink2")

job.commit()
```

#### **5.3.2. Amazon SageMaker**
**Amazon SageMaker**, makine öğrenmesi modellerinin geliştirilmesi, eğitilmesi ve dağıtılması için kapsamlı bir platformdur.
- **Özellikler:**

    - **Eğitim ve Doğrulama:** Dağıtık ve ölçeklenebilir model eğitimi.
    - **Tahmin Hizmetleri:** Modelleri gerçek zamanlı veya toplu olarak sunma.
    - **Hiperparametre Optimizasyonu:** Otomatik olarak en iyi model parametrelerini bulma.
    - **Yerleşik Algoritmalar ve Önceden Eğitilmiş Modeller:** Süreci hızlandırır.
- **Kullanım Durumları:**

    - Görüntü ve metin sınıflandırma.
    - Tahmin ve tahminleme.
    - Doğal dil işleme ve öneri sistemleri.
- **Örnek: SageMaker ile Model Eğitimi**

    - **Adım 1:** AWS Management Console'da **SageMaker** bölümüne gidin.
    - **Adım 2:** **Notebooks** ile bir Jupyter Notebook başlatın.
    - **Adım 3:** Veri setini yükleyin ve ön işleme yapın.
    - **Adım 4:** SageMaker'ın yerleşik algoritmalarını veya kendi modelinizi kullanarak eğitim işini başlatın.
    - **Adım 5:** Eğitilen modeli dağıtın ve tahminler yapın.
- **Örnek Kod (Python Boto3 Kullanarak):**
```
import boto3
import sagemaker
from sagemaker import get_execution_role
from sagemaker.estimator import Estimator

sagemaker_session = sagemaker.Session()
role = get_execution_role()

# Eğitim için Estimator Oluşturma
estimator = Estimator(
    image_uri='docker/image-uri',
    role=role,
    instance_count=1,
    instance_type='ml.m4.xlarge',
    output_path='s3://mybucket/output/',
    sagemaker_session=sagemaker_session
)

# Model Eğitimi
estimator.fit({'train': 's3://mybucket/train-data/'})

# Model Dağıtımı
predictor = estimator.deploy(initial_instance_count=1, instance_type='ml.m4.xlarge')

# Tahmin Yapma
response = predictor.predict({'feature1': value1, 'feature2': value2})
print(response)
```

### **5.4. AWS'de Veri Güvenliği ve Yönetimi**
#### **5.4.1. Identity and Access Management (IAM)**
**AWS Identity and Access Management (IAM)**, AWS kaynaklarına güvenli erişim sağlamak için kullanılan bir hizmettir.
- **Kullanıcı ve Rol Yönetimi:**
    - Kullanıcılar, gruplar ve roller oluşturarak erişim kontrolü sağlar.
- **Politika Tabanlı İzinler:**
    - JSON biçimindeki politikalarla izinler tanımlanır.
- **En İyi Uygulamalar:**
    - **En Az Yetki İlkesi:** Kullanıcılara sadece ihtiyaç duydukları izinleri verin.
    - **MFA Kullanımı:** Çok faktörlü kimlik doğrulama ile güvenliği artırın.
    - **Düzenli İnceleme:** Erişim izinlerini ve politikalarını düzenli olarak gözden geçirin.
#### **5.4.2. Şifreleme ve Anahtar Yönetimi**
- **AWS Key Management Service (KMS):**

    - **Anahtar Yönetimi:** Şifreleme anahtarlarınızı oluşturabilir, döndürebilir ve yönetebilirsiniz.
    - **Entegrasyon:** S3, EBS, RDS gibi hizmetlerle entegre çalışır.
- **Şifreleme:**

    - **Atıl Durumdaki Veri:** Veriler KMS ile yönetilen anahtarlarla şifrelenebilir.
    - **İletim Halindeki Veri:** TLS/SSL kullanılarak şifrelenir.
#### **5.4.3. Denetim ve Uyumluluk**
- **AWS CloudTrail:**
    - **Denetim Günlükleri:** AWS hesaplarınızda gerçekleşen tüm API çağrılarını kaydeder.
    - **İzleme ve Uyarılar:** Güvenlik olaylarını tespit etmek için CloudTrail ile entegrasyonlu izleme ve uyarı sistemleri kurabilirsiniz.
- **Uyumluluk Sertifikaları:**
    - AWS, ISO 27001, SOC 1/2/3, HIPAA, GDPR gibi birçok uyumluluk standardını karşılar.
- **AWS Security Hub:**
    - **Güvenlik Durumu İzleme:** Güvenlik durumunuzu merkezi bir noktadan izleyebilir ve yönetebilirsiniz.
### **5.5. AWS Hesaplama Hizmetleri**
#### **5.5.1. Amazon EC2 (Elastic Compute Cloud)**
**Amazon EC2**, esnek ve ölçeklenebilir sanal sunucular sağlayan bir hizmettir.
- **Özellikler:**

    - **Çeşitli Makine Türleri:** Farklı iş yüklerine uygun CPU, bellek ve depolama kombinasyonları.
    - **Otomatik Ölçeklendirme:** EC2 Auto Scaling ile talebe göre kaynakları otomatik olarak ayarlayın.
    - **Kapsamlı Ağ Desteği:** Amazon VPC ile entegre çalışır, güvenlik grupları ve alt ağlar oluşturabilirsiniz.
    - **Depolama Seçenekleri:** Amazon EBS, yerel SSD'ler ve Instance Store.
- **Kullanım Durumları:**

    - Web ve uygulama sunucuları.
    - Büyük veri işleme ve analiz uygulamaları.
    - Geliştirme ve test ortamları
#### **5.5.2. AWS Lambda**
**AWS Lambda**, sunucusuz bir hesaplama hizmetidir ve kodunuzu sadece çalıştırıldığında çalıştırmanızı sağlar.
- **Özellikler:**

    - **Olay Tabanlı Tetikleme:** S3, DynamoDB, Kinesis, SNS ve diğer AWS hizmetlerinden gelen olaylarla tetiklenir.
    - **Otomatik Ölçeklenebilirlik:** Gelen isteğe göre otomatik olarak ölçeklenir.
    - **Çeşitli Diller Desteği:** Node.js, Python, Java, C#, Go, Ruby ve PowerShell.
- **Kullanım Durumları:**
    - Veri işleme ve dönüşümleri.
    - API arka uçları ve mikro hizmetler.
    - Gerçek zamanlı dosya işleme.

```
import json

def lambda_handler(event, context):
    # Olay verisini işleme
    print("Received event: " + json.dumps(event, indent=2))
    
    return {
        'statusCode': 200,
        'body': json.dumps('Merhaba Dünya!')
    }
```

#### **5.5.3. Amazon ECS ve EKS**
**Amazon ECS (Elastic Container Service)** ve **Amazon EKS (Elastic Kubernetes Service)**, konteyner tabanlı uygulamaların yönetimi için hizmetlerdir.
- **Amazon ECS:**

    - **Yönetilen Konteyner Orkestrasyonu:** AWS tarafından yönetilen Docker konteynerleri.
    - **FaaS ve PaaS Desteği:** Fargate ile sunucusuz konteyner çalıştırma seçeneği.
- **Amazon EKS:**

    - **Kubernetes Yönetimi:** Tam yönetilen Kubernetes hizmeti.
    - **Geniş Ekosistem Desteği:** Kubernetes topluluğu ve araçları ile uyumlu.
- **Kullanım Durumları:**

    - Mikro hizmet mimarileri.
    - Ölçeklenebilir web uygulamaları.
    - DevOps ve CI/CD süreçleri.
### **5.6. AWS Güvenlik ve Yönetim Araçları**
#### **5.6.1. AWS CloudTrail**
**AWS CloudTrail**, AWS hesaplarınızda gerçekleşen tüm API çağrılarını kaydeden bir hizmettir.
- **Özellikler:**
    - **Denetim Günlükleri:** AWS hesaplarınızda gerçekleşen tüm API çağrılarını, kimlerin hangi kaynaklarla etkileşime geçtiğini kaydeder.
    - **Olay İzleme:** Güvenlik olaylarını ve uyumluluk gereksinimlerini karşılamak için kullanılır.
    - **Entegrasyon:** CloudWatch ile entegrasyon sayesinde olay tabanlı uyarılar oluşturabilirsiniz.
- **Kullanım Durumları:**
    - Güvenlik ve uyumluluk denetimleri.
    - Olay analizleri ve hata ayıklama.
    - Hesap etkinliklerini izleme.
#### **5.6.2. AWS Security Hub**
**AWS Security Hub**, AWS hesaplarınızın güvenlik durumunu merkezi bir noktadan izlemenizi sağlar.
- **Özellikler:**
    - **Güvenlik Standartları:** CIS AWS Foundations Benchmark gibi güvenlik standartlarını destekler.
    - **Tehdit Algılama:** Güvenlik tehditlerini tespit etmek için çeşitli AWS hizmetlerinden gelen verileri analiz eder.
    - **Entegrasyon:** Diğer güvenlik araçları ve hizmetleriyle entegre çalışır.
- **Kullanım Durumları:**
    - Güvenlik durumunu merkezi olarak izleme.
    - Güvenlik uyumluluğunu sağlama.
    - Tehdit algılama ve yanıt süreçlerini iyileştirme.

#### **Hangi Durumda Hangisi Tercih Edilmeli?**
- **Amazon EC2** tercih edilmelidir:
    - Sürekli çalışan, tam kontrol gerektiren uygulamalar için.
    - Özel yapılandırmalar ve uzun süreli işlemler gerektiğinde.
    - Altyapı yönetimini kendiniz yapmak istediğiniz durumlarda.
- **AWS Lambda** tercih edilmelidir:
    - Olay tetiklemeli, kısa süreli ve düşük kaynak gereksinimli işlemler için.
    - API arka uçları ve mikro hizmetler geliştirmek istediğinizde.
    - Hızlı geliştirme ve dağıtım süreçlerine ihtiyaç duyulduğunda.
- **Amazon ECS/EKS** tercih edilmelidir:
    - Mikro hizmet mimarisi ve konteyner tabanlı uygulamalar geliştirmek istediğinizde.
    - Daha karmaşık ve uzun süreli iş yükleri için.
    - Esnek dil ve bağımlılık desteği gerektiğinde.
    - Yüksek özelleştirme ve kontrol gerektiren durumlarda.

