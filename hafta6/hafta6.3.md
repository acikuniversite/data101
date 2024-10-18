### **3. Zamanlama ve Orkestrasyon Araçları ile N-1 Çalışmak**

#### **Zamanlama ve Orkestrasyon Nedir?**

- **Zamanlama (Scheduling):**
    - İşlerin belirli zamanlarda veya periyotlarda otomatik olarak çalıştırılması.
- **Orkestrasyon:**
    - Birden fazla görevin veya işin bağımlılıklarının yönetilmesi, izlenmesi ve hata durumlarının ele alınması.

#### **N-1 Çalışmak Nedir?**

- **Tanım:**
    - Bir veri işleme sürecinde, bir önceki günün veya dönemin verilerini işlemek anlamına gelir.
- **Örnek Senaryo:**
    - **Günlük İşlemler:**
        - Her gün saat 03:00'da çalışan bir ETL süreci, bir önceki günün (N-1) verilerini işler.
- **Neden Kullanılır?**
    - Verilerin kaynak sistemlerde tam olarak oluşması için gereken süreyi sağlamak.
    - Gün sonu işlemleri, batch süreçler veya veri güncellemelerinin tamamlanmasını beklemek.

#### **Orkestrasyon Araçları**

- **Apache Airflow:**
    - **Özellikler:**
        - **Python** ile yazılmış, açık kaynaklı bir iş akışı yönetim platformu.
        - **DAG (Directed Acyclic Graph)** yapısı ile görevlerin ve bağımlılıkların tanımlanması.
        - Zamanlama, izleme, hata yönetimi ve yeniden deneme mekanizmaları.
    - **Kullanım Örnekleri:**
        - Günlük ETL işlemlerinin planlanması.
        - Karmaşık bağımlılıkların yönetimi.
- **Prefect:**
    - **Özellikler:**
        - Modern, bulut uyumlu ve **Python** tabanlı bir orkestrasyon aracı.
        - **Flow** ve **Task** yapıları ile esnek iş akışı tasarımı.
        - Hata toleransı ve yeniden deneme politikaları.
- **Dagster:**
    - **Özellikler:**
        - Veri varlıklarına odaklanan tip güvenli bir orkestrasyon platformu.
        - Veri boru hatlarının test edilebilirliği ve yeniden kullanılabilirliği.
- **Kubernetes CronJobs:**
    - **Özellikler:**
        - **Kubernetes** üzerinde zamanlanmış görevlerin çalıştırılması.
        - Mikro hizmet mimarilerinde veri işlemlerinin orkestrasyonu.

#### **Teknik Detaylar ve Kullanım Örnekleri**

- **Airflow'da N-1 Tarihleri ile Çalışma:**
```
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from datetime import datetime, timedelta

default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2023, 10, 17),
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

dag = DAG(
    'n_minus_one_example',
    default_args=default_args,
    schedule_interval='@daily',
)

def process_data(execution_date):
    n_minus_one_date = execution_date - timedelta(days=1)
    # N-1 tarihli verileri işle
    print(f"N-1 Date: {n_minus_one_date}")

process_task = PythonOperator(
    task_id='process_n_minus_one',
    provide_context=True,
    python_callable=process_data,
    dag=dag,
)
```
- **Bağımlılık Yönetimi:**
    - Görevlerin doğru sırayla ve bağımlılıklarına göre çalışmasını sağlamak.
    - Örneğin, veri çekme işlemi tamamlanmadan veri dönüşümü işleminin başlamaması.
- **Hata Yönetimi ve Yeniden Deneme:**
    - Hata durumlarında otomatik olarak yeniden deneme politikaları belirlemek.
    - Örneğin, bir API çağrısı başarısız olursa 3 kez daha denemek.

---

