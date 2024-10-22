## 2. DDL ve DML Komutları

### Veri Tanımlama Dili (DDL)
- **Tanım:** Veritabanı nesnelerinin (tablolar, indeksler, şemalar) tanımlanması ve değiştirilmesi için kullanılır.
- **Temel DDL Komutları:**
	- **CREATE:** Yeni veritabanı nesneleri oluşturur.
	- Örnek: CREATE TABLE, CREATE INDEX
	```
	CREATE TABLE kitaplar (
	    kitap_id INT PRIMARY KEY,
	    kitap_adi VARCHAR(255),
	    yazar VARCHAR(255),
	    stok INT
	);
	```
	- **ALTER:** Mevcut veritabanı nesnelerini değiştirir.
	- Örnek: ALTER TABLE ile tabloya sütun eklemek.
	``` 
	ALTER TABLE kitaplar ADD yayinevi_id INT;
	```
	- **DROP:** Veritabanı nesnelerini siler.
	- Örnek: DROP TABLE, DROP INDEX
	``` 
	DROP TABLE kitaplar;
	```
	- **TRUNCATE:** Bir tablodaki tüm verileri hızlıca siler.
	```
	TRUNCATE TABLE kitaplar;		
	```

### Veri Manipülasyon Dili (DML)
- **Tanım:** Veritabanındaki verileri eklemek, güncellemek ve silmek için kullanılır.
- **Temel DML Komutları:**
	- **SELECT:** Verileri sorgular ve getirir.
	- **INSERT INTO:** Yeni veri ekler.
	- **UPDATE:** Mevcut verileri günceller.
	- **DELETE:** Verileri siler.


## 3. Temel SQL Sorguları ve İşlemleri
### SELECT Sorgusu
- **Amaç:** Veritabanından veri çekmek için kullanılır.
- **Sözdizimi:**
```
SELECT sütun1, sütun2, ...
FROM tablo_adi;
```
**Örnek**
``` 
SELECT kitap_adi, yazar FROM kitaplar 
```

### WHERE Şartı
- **Amaç:** Sorgularda belirli koşulları uygulamak için kullanılır.
- **Sözdizimi:**

```
SELECT kitap_adi, yazar FROM kitaplar WHERE kitap_id = 1;
```

**Örnek**
`SELECT * FROM kitaplar WHERE yazar = "Necip Fazıl Kısakürek"`
### INSERT INTO Komutu

- **Amaç:** Tabloya yeni veri eklemek için kullanılır.
- **Sözdizimi:**
```
INSERT INTO tablo_adi (sütun1, sütun2, ...)
VALUES (değer1, değer2, ...);
```
**Örnek**
```
INSERT INTO kitaplar (kitap_id, kitap_adi, yazar, stok) 
VALUES (1, 'Kaldırımlar', 'Necip Fazıl Kısakürek', 50);
```

### UPDATE Komutu

- **Amaç:** Mevcut verileri güncellemek için kullanılır.
- **Sözdizimi:**
```
UPDATE tablo_adi
SET sütun1 = değer1, sütun2 = değer2, ...
WHERE koşul;
```
**Örnek**
```
UPDATE kitaplar SET stok = stok - 1 WHERE kitap_id = 1;
```
### DELETE Komutu

- **Amaç:** Verileri silmek için kullanılır.
- **Sözdizimi:**
```
DELETE FROM tablo_adi
WHERE koşul;
```

**Örnek**:
```
DELETE FROM kitaplar WHERE kitap_id = 1;
```

