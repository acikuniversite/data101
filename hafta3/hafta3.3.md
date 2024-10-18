## 3 SQL Tasarım Kuralları ve Normalizasyon
#### Veritabanı Tasarım Kuralları:
-  **Veri Bütünlüğü:**
	- Birincil anahtarlar (Primary Keys)
	- Yabancı anahtarlar (Foreign Keys)
	- Benzersizlik ve doğruluk kısıtlamaları
- **Şema Tasarımı:**
	- Tablo ve alan isimlendirme standartları
	- Veri tiplerinin doğru seçimi
	- İlişkilerin doğru tanımlanması

#### Normalizasyon:
-  **Amaç:**
	- Veri tekrarlanmasını azaltmak
	- Veri bütünlüğünü sağlamak
	- Güncelleme, ekleme ve silme anormalliklerini önlemek
- **Normal Formlar:**
	- **Birinci Normal Form (1NF):**
		- Her alan atomik olmalı (bölünemez)
		- Tabloda yinelenen sütunlar olmamalı
	- **İkinci Normal Form (2NF):**
		- 1NF şartlarını sağlamalı
		- Her bir alan, birincil anahtarın tamamına bağımlı olmalı
	- **Üçüncü Normal Form (3NF):**
		- 2NF şartlarını sağlamalı
		- Anahtar olmayan alanlar, diğer anahtar olmayan alanlara bağımlı olmamalı
#### Örnekler: 
#####  1\. Normal Form (1NF) Örneği:
**Hatalı Tasarım:**  
  
| MüşteriID | İsim         | Telefon1  | Telefon2  |     |
| --------- | ------------ | --------- | --------- | --- |
| 1         | Ahmet Yılmaz | 555\-1234 | 555\-5678 |     |
| 2         | Ayşe Demir   | 555\-8765 | NULL      |     |
Burada, müşterilerin birden fazla telefon numarası olduğunda, ek sütunlar eklenerek veriler tutulmuş.  

**Doğru Tasarım:**
**Müşteri** tablosu: 

| MüşteriID | İsim         |     |
| --------- | ------------ | --- |
| 1         | Ahmet Yılmaz |     |
| 2         | Ayşe Demir   |     |

**MüşteriTelefon** tablosu:  

| TelefonID | MüşteriID | Telefon |  
| --- | --- | --- |  
| 1 | 1 | 555\-1234 |  
| 2 | 1 | 555\-5678 |  
| 3 | 2 | 555\-8765 |  
- Böylece, her telefon numarası ayrı bir satırda tutulur ve tablo atomik hale gelir.  
##### 2. Normal Form (2NF) Örneği

**Hatalı Tasarım:**  
Birincil anahtarın bileşik olduğu ve bazı sütunların sadece anahtarın bir parçasına bağımlı olduğu bir tablo düşünelim.  
  
**SiparişDetay** tablosu:  
  
| SiparişID | ÜrünID | ÜrünAdı | Miktar |  
| --- | --- | --- | --- |  
| 1001 | 2001 | Kalem | 10 |  
| 1001 | 2002 | Defter | 5 |  
Burada, *ÜrünAdı* sadece *ÜrünID*'ye bağımlı, ancak *SiparişID* ile ilgisi yok.  

**Doğru Tasarım:**
- Tabloları aşağıdaki gibi normalleştirebiliriz:  
  
**SiparişDetay** tablosu:  
  
| SiparişID | ÜrünID | Miktar |  
| --- | --- | --- |  
| 1001 | 2001 | 10 |  
| 1001 | 2002 | 5 |  
  
**Ürünler** tablosu:  

| ÜrünID | ÜrünAdı |  
| --- | --- |  
| 2001 | Kalem |  
| 2002 | Defter |  
- Böylece, *ÜrünAdı* sadece *ÜrünID*'ye tam bağımlı hale gelir ve 2NF sağlanır.  
##### 3\. Normal Form (3NF) Örneği:

#####  Yanlış Tasarım
  Bir tabloda transitif bağımlılık varsa, yani bir sütun diğer bir sütuna, o da anahtar sütuna bağımlıysa 3NF ihlal edilir.
  
  
  **Çalışan** tablosu: 

| ÇalışanID | İsim       | DepartmanID | DepartmanAdı |     |
| --------- | ---------- | ----------- | ------------ | --- |
| 1         | Ali Veli   | 10          | Pazarlama    |     |
| 2         | Ayşe Fatma | 20          | Muhasebe     | -   |

Burada, *DepartmanAdı* sadece *DepartmanID*'ye bağımlıdır, ancak *DepartmanID* de *ÇalışanID*'ye bağımlıdır.**

**Doğru Tasarım:**
Tabloları şu şekilde ayırabiliriz:  
  
**Çalışan** tablosu:  
  
| ÇalışanID | İsim | DepartmanID |  
| --- | --- | --- |  
| 1 | Ali Veli | 10 |  
| 2 | Ayşe Fatma | 20 |  
  
**Departman** tablosu:  

| DepartmanID | DepartmanAdı |  
| --- | --- |  
| 10 | Pazarlama |  
| 20 | Muhasebe |  
- Böylece, transitif bağımlılık ortadan kalkar ve 3NF sağlanır.  

##### **Boyce\-Codd Normal Formu (BCNF) Örneği:**  

**Hatalı Tasarım:**    
Bir tabloda her determinant aday anahtar değilse BCNF ihlal edilir.  
  
**DersAtama** tablosu:  

| DersID | ÖğretmenID | ÖğretmenAdı |  
| --- | --- | --- |  
| MAT101 | 501 | Mehmet Hoca |  
| FIZ101 | 502 | Ayşe Hoca |  
- Burada, *ÖğretmenAdı* sadece *ÖğretmenID*'ye bağımlı, ancak *ÖğretmenID* aday anahtar değil.  
**Doğru Tasarım:**
Tabloları aşağıdaki gibi ayırabiliriz:  
  
**DersAtama** tablosu:  

| DersID | ÖğretmenID |  
| --- | --- |  
| MAT101 | 501 |  
| FIZ101 | 502 |  
  
**Öğretmen** tablosu:  

| ÖğretmenID | ÖğretmenAdı |  
| --- | --- |  
| 501 | Mehmet Hoca |  
| 502 | Ayşe Hoca |  
- Böylece, tüm determinantlar aday anahtar olur ve BCNF sağlanır.  

##### **4\. Normal Form (4NF) Örneği:**  

**Hatalı Tasarım:**
Çoklu bağımsız çok\-değerli bağımlılıklar varsa 4NF ihlal edilir.  
  
**SanatçıEser** tablosu:  

| Sanatçı | Enstrüman | Tür |  
| --- | --- | --- |  
| Ali | Gitar | Rock |  
| Ali | Bateri | Rock |  
| Ali | Gitar | Blues |  
| Ali | Bateri | Blues |  
- Burada, *Sanatçı* ile *Enstrüman* ve *Sanatçı* ile *Tür* arasında bağımsız çok\-değerli bağımlılıklar var.  

**Doğru Tasarım:**
Tabloları şu şekilde ayırabiliriz:  
**SanatçıEnstrüman** tablosu:  
  
| Sanatçı | Enstrüman |  
| --- | --- |  
| Ali | Gitar |  
| Ali | Bateri |  
  
**SanatçıTür** tablosu:  

| Sanatçı | Tür   |     |
| ------- | ----- | --- |
| Ali     | Rock  |     |
| Ali     | Blues |     |
Böylece, çok\-değerli bağımlılıklar ayrı tablolarda tutulur ve 4NF sağlanır.  

