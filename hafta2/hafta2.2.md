## 2. DDL ve DML Komutları

### Veri Tanımlama Dili (DDL)
- **Tanım:** Veritabanı nesnelerinin (tablolar, indeksler, şemalar) tanımlanması ve değiştirilmesi için kullanılır.
- **Temel DDL Komutları:**
	- **CREATE:** Yeni veritabanı nesneleri oluşturur.
	- Örnek: CREATE TABLE, CREATE INDEX
```
CREATE TABLE users (
  
    id SERIAL PRIMARY KEY,  
    username VARCHAR(255) NOT NULL,  
    password VARCHAR(255) NOT NULL,  
    email VARCHAR(255) NOT NULL,  
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    
    -- Benzersiz kullanıcı adı ve e-posta  
    UNIQUE (username),  
    UNIQUE (email),  
    
    -- Kullanıcı adı ve şifre uzunluk kontrolü ve e-posta formatı kontrolü
    CHECK (char_length(username) > 3),  
    CHECK (char_length(password) > 5),  
    CHECK (email ~ '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$')  
)
```

- **ALTER:** Mevcut veritabanı nesnelerini değiştirir.
	- Örnek: ALTER TABLE ile tabloya sütun eklemek.
``` 
ALTER TABLE users ADD COLUMN first_name VARCHAR(255);
ALTER TABLE users ALTER COLUMN username SET NOT NULL;
ALTER TABLE users DROP COLUMN first_name;
```

- **DROP:** Veritabanı nesnelerini siler.
	- Örnek: DROP TABLE, DROP INDEX
``` 
DROP TABLE users;
```

- **TRUNCATE:** Bir tablodaki tüm verileri hızlıca siler.
```
TRUNCATE TABLE users;		
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
SELECT * FROM users; 
```

### WHERE Şartı
- **Amaç:** Sorgularda belirli koşulları uygulamak için kullanılır.
- **Sözdizimi:**

```
SELECT sütun1, sütun2, ... FROM tablo_adi
WHERE koşul;
```

**Örnek**
`SELECT * FROM users WHERE username = 'admin';`
### INSERT INTO Komutu

- **Amaç:** Tabloya yeni veri eklemek için kullanılır.
- **Sözdizimi:**
```
INSERT INTO tablo_adi (sütun1, sütun2, ...)
VALUES (değer1, değer2, ...);
```
**Örnek**
```
INSERT INTO users (username, password, email) VALUES ('admin', '123456', 'email@email.com');
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
UPDATE users SET password = '654321' WHERE username = 'admin';
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
DELETE FROM users WHERE username = 'admin';
```

