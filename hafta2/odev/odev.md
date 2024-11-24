# Data101 Ödevi: C2C Yemek Uygulaması Veritabanı Tasarımı

## Ödev Konusu
Bu ödevde, öğrencilerden bir **C2C (Customer-to-Customer)** yemek uygulaması için uçtan uca bir veritabanı tasarımı yapmaları beklenmektedir. Bu platform, ev hanımlarının yemeklerini platform üzerinden satabileceği ve kullanıcıların bu yemekleri satın alabileceği bir yapıyı temel almaktadır.

---

## Ödevin Kapsamı ve Beklentiler
### Genel Gereksinimler
1. **Veritabanı Tasarımı ve İlişkiler (50 puan)**:
   - Uygun tabloların tasarlanması ve doğru ilişkilerin kurulması.
   - Tablolar arasında referans bütünlüğünün sağlanması.

2. **Saklı Yordamlar (Stored Procedures) (25 puan)**:
   - 5 adet saklı yordam yazılması.
   - Saklı yordamlar üzerinden veritabanı işlemlerinin otomatikleştirilmesi.

3. **Veri Manipülasyonu (25 puan)**:
   - Belirlenen 5 senaryo üzerinden sorguların yazılması.
   - Veri manipülasyonunda performans ve veri doğruluğu dikkate alınmalıdır.

### Teknik Gereksinimler
- En az **5 ana tablo** tasarımı.
- Belirlenen tabloları destekleyecek **5 ek tablo** tasarımı.
- **Trigger** ve **Index** gibi ileri düzey veritabanı unsurlarının kullanımına açık olunması.
- **Normalizasyon** kurallarına uygunluk.

---

## Platform İçeriği
### Tablolar
1. **Kullanıcılar**:
   - Kullanıcı profilleri (ev hanımları ve müşteriler için ayrım yapılmalı).
   - Alanlar: `id`, `ad_soyad`, `magaza_adi` `email`, `telefon`, `kullanici_tur_id`, `adres`, `oluşturulma_tarihi`.
   - 
2. **Kullanıcı Türleri**:
   - Ev Hanımları, Müşteriler, Catering, Zincir Mağazalar
   - Alanlar: `id`, `kullanici_tipi`, 'komisyon_orani`, `is_satici`

3. **Yemekler**:
   - Ev hanımlarının eklediği yemek bilgileri.
   - Alanlar: `id`, `yemek_adı`, `fiyat`, `kategori`, `tanım`, `hazırlık_süresi`, `kullanıcı_id`.

4. **Kategoriler**:
   - Yemeklerin Kategorileri
   - Alanlar: `id`, `yemek_id`, `kategori_adi`

5. **Siparişler**:
   - Siparişlerin yönetimi ve takibi.
   - Alanlar: `id`, `kullanıcı_id`, `sipariş_durumu`, `toplam_tutar`, `oluşturulma_tarihi`.

6. **Sipariş Yemekleri**:
   - Sipariş içeriğini gösteren tablo
   - Alanlar: `id`, `sipariş_id`, `yemek_id`

7. **Sipariş Geçmişi**:
   - Sipariş durumu güncellemelerinin kayıt altına alınması.
   - Alanlar: `id`, `sipariş_id`, `durum`, `güncelleme_tarihi`.

8. **Değerlendirme ve Geri Bildirim**:
   - Sipariş ve kullanıcılar için puanlama ve yorumlama sistemi.
   - Alanlar: `id`, `siparis_id`, `kullanıcı_id`, `puan`, `yorum`, `tarih`.

---

## Saklı Yordamlar ve Fonksiyonlar
1. Satıcının ortalama sipariş bazlı geliri
2. Satıcının ortalama teslimat süresi
3. Satıcının Memnun müşteri sayısı (bir iki ikinci defa sipariş verdiyse ve puanı düşmediyse memnun diyebiliriz)

---

## View Örnekleri
1. Sipariş durumu güncellendiğinde sipariş geçmişine kaydetme.
2. Kullanıcı&Kullanıcı bazlı toplam yaptığı sipariş sayısı, harcadığı tutar ve verdiği ortalama puanı gösteren view
3. Belirli bir kategorideki en popüler yemeklerin listeleyen view.
4. Sistemin kar marjının en çok hangi yönden olduğunu aylık gösteren tablo (ev hanımları, yemek firmaları, mağazalar)
5. Haftalık Sadık müşteri sayısı hesaplaması (pazartesi'den pazara kadar aynı kişi kaç defa sipariş vermiş bakarız, pazartesi günü sipariş verdi, salıda verdiyse 1 olur, çarşamba verdiyse 2 olur sadece perşembe verse bile pazartesinin tekrarı olduğu için 1 olur, en fazla 6 olabilir)

---

## Veri Manipülasyonu Senaryoları
1. Maksimum Sipariş Tutarını 10bin TL'dir üstünde sipariş oluşturulamamlı
2. Her mail adresi tek bir hesaba ait olmalı
3. Negatif fiyatlı sipariş veya ürün olamaz
4. Bir siparişe bir yorum girilebilir.
5. Kişi kendi dükkanından sipariş veremez.

---

## Değerlendirme Kriterleri
| **Bölüm**                   | **Puan** |
|-----------------------------|----------|
| Veritabanı Tasarımı         | 50       |
| Saklı Yordamlar ve Viewler            | 25       |
| Veri Manipülasyonu Senaryoları | 25       |
| **Toplam**                  | **100**  |

---

## Önemli Notlar
- Öğrenciler, projeye kendi farklı bakışlarını **eklemelidir**.
- Ödev teslimi sırasında SQL dosyaları ve projeye ait açıklamalar içeren bir rapor gönderilmelidir.
- En orijinal ve etkileyici tasarım haftanın birincisi olarak seçilecektir.

---
Başarılar!
