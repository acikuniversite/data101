## 1. SQL’in Temelleri
### SQL Nedir?**
- **SQL (Structured Query Language):**
- İlişkisel veritabanlarıyla iletişim kurmak için kullanılan standart bir sorgulama dilidir.
- Veritabanlarından veri **sorgulamak**, **eklemek**, **güncellemek** ve **silmek** için kullanılır.
### SQL’in Tarihçesi
- **1970’ler:** IBM’de Edgar F. Codd tarafından ilişkisel veritabanı kavramının geliştirilmesi.
- **1974:** SEQUEL (Structured English Query Language) olarak ilk versiyonun tanıtılması.
- **1979:** Relational Software, Inc. (daha sonra Oracle Corporation) ilk ticari SQL ürününü piyasaya sürdü.
- **1986:** ANSI tarafından SQL’in ilk standart sürümü yayınlandı.
### SQL Standartları
- **ANSI/ISO Standartları:**
	- **SQL-86:** İlk resmi standart.
	- **SQL-89:** Küçük iyileştirmeler.
	- **SQL-92:** Genişletilmiş fonksiyonlar ve veri türleri.
	- **SQL:1999:** Nesne ilişkisel özellikler ve yeni veri türleri.
	- **SQL:2003:** XML desteği ve pencere fonksiyonları.
	- **SQL:2011:** Zaman yolculuğu ve temporal veritabanları.
- **Not:** Farklı veritabanı yönetim sistemleri (DBMS) kendi SQL genişletmelerine sahip olabilir (örneğin, T-SQL, PL/SQL).


## Sonraki Sayfaya Geçmeden Önce
Aşağıdaki komutu kullanarak PostgreSQL'li docker ile ayağa kaldırabilirsiniz

```
docker run --name my-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql
```

Bu komutun açıklaması:
- `--name my-mysql`: Container için bir isim belirliyoruz.
- `-e MYSQL_ROOT_PASSWORD=my-secret-pw`: MySQL root kullanıcısı için bir şifre belirliyoruz.
- `-p 3306:3306`: Host sistemdeki 3306 portunu, container’daki MySQL’in çalıştığı 3306 portuna yönlendiriyoruz.
- `-d`: Container'ı arka planda çalıştırıyoruz.
- `mysql`: MySQL Docker image'ini kullanıyoruz.

Container çalıştıktan sonra, PostgreSQL'in komut satırına erişmek için aşağıdaki komutu kullanabilirsin:

```
docker exec -it my-postgres psql -U postgres
```
