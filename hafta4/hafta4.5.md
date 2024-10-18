## **5. Workshop**
**Senaryo**
Bir sosyal medya uygulaması, kullanıcı profillerini ve gönderilerini depolamak istiyor. Uygulama, kullanıcıların profillerini, arkadaşlarını ve paylaştıkları gönderileri takip etmeyi amaçlıyor.

  

**Görevler**

1. **MongoDB Kullanarak Koleksiyonların Oluşturulması**
	-  Kullanıcı Profilleri Koleksiyonu (**users)**
	-  Gönderiler Koleksiyonu (**posts)**
2. **Temel CRUD (Oluşturma, Okuma, Güncelleme, Silme) İşlemlerini Gerçekleştirin**
	-  Kullanıcı Ekleme (CREATE)
	-  Kullanıcıları Okuma (READ)
	-  Kullanıcı Güncelleme (UPDATE)
	-  Kullanıcı Silme (DELETE)
	-  Gönderi Ekleme, Okuma, Güncelleme ve Silme İşlemleri
3. **Kullanıcıların Gönderilerini Sorgulamak İçin Örnek Sorgular Yazın**
	-  Belirli bir kullanıcının tüm gönderilerini listeleme
	-  Belirli kriterlere göre gönderi arama (örn. beğeni sayısına göre)
4. **Koleksiyonlar İçin İdeal İndeksleri Seçiniz**
	-  users **Koleksiyonu İçin İndeksler:**
	-  Email alanında benzersiz indeks
	-  İsim alanında metin indeksi
	-  Oluşturma tarihi alanında indeks
	-  posts **Koleksiyonu İçin İndeksler:**
		-  Kullanıcı ID alanında indeks
		-  Etiketler alanında çoklu anahtar indeksi
		-  Tarih alanında indeks
		-  Beğeni sayısı alanında indeks
		-  Bileşik indeks (kullanici_id, tarih)
1. **Alttaki Sorguları Yazınız**

| İstek                                                                                                                                                    | Sorgu                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **1. Yaşı `int` olmayan öğrencileri ve en az 4 derse sahip olanları bulma**                                                                              | ```db.students.find({ "age": { "$not": { "$type": "int" } }, "courses": { "$size": { "$gte": 4 } } })``` |
| **2.Hem "Mathematics" hem de "Physics" derslerini alan ve ya yaşı 20'den büyük ya da ders sayısı 5'ten az olan öğrencileri bulma**                       |                                                                                                          |
| **3. En az bir varyasyonu fiyatı 100'den fazla ve stoğu en az 50 olan ürünleri bulma**                                                                   |                                                                                                          |
| **4. Etiketleri "new" olan ve "discounted" olmayan ürünleri bulma**                                                                                      |                                                                                                          |
| **5. Yaşı mevcut olan ve ya `age` 25'e eşit değil ya da `courses` dizisinde en az 3 ders bulunan öğrencileri bulma**                                     |                                                                                                          |
| **6. `courses` dizisinde hem "Chemistry" hem de en az bir ders kredisi 5 olan öğrencileri bulma**                                                        |                                                                                                          |
| **7. `tags` dizisi tam olarak 3 etikete sahip olan ve herhangi bir etiketi "sale" olmayan ürünleri bulma**                                               |                                                                                                          |
| **8. `age` 18 ile 30 arasında olan ve ya `courses` dizisinde "Biology" dersini alan ya da `variants` dizisinde stoğu 100'den fazla olan ürünleri bulma** |                                                                                                          |
|                                                                                                                                                          |                                                                                                          |

