## 2. ER (Varlık-İlişki) Diyagramları
#### ER Diyagramlarının Temel Bileşenleri

- **Varlıklar (Entities):**
	- Bağımsız olarak tanımlanabilen nesneler veya kavramlardır.
	- Örnekler: Müşteri, Ürün, Sipariş.
- **Öznitelikler (Attributes):**
	- Varlıkların özellikleridir.
	- Örnekler: Müşteri adı, Ürün fiyatı.
- **İlişkiler (Relationships):**
	- Varlıklar arasındaki bağlantıları gösterir.
	- Örnekler: Müşteri verir Sipariş, Sipariş içerir Ürün.
#### Kardinalite ve İlişkiler
- **Kardinalite:**
	- Varlıklar arasındaki ilişki sayısını belirtir.
- **Türleri:**
	- **Bire-Bir (1:1):** Bir varlığın bir diğer varlıkla tek bir ilişkisi vardır.
	- **Bire-Çok (1:N):** Bir varlık, birden fazla diğer varlıkla ilişki kurabilir.
	- **Çok-Çok (M:N):** Birden fazla varlık, birden fazla diğer varlıkla ilişki kurabilir.
- **İlişki Dereceleri:**
	- İlişkide yer alan varlıkların sayısını belirtir (örn., ikili, üçlü ilişkiler).
- **Zorunluluğa Bağlı Kardinalite Gösterimi**
	- **1:** Tam olarak bir varlık.
	- **0..1:** Sıfır veya bir varlık.
	- **0..*:** Sıfır veya daha fazla varlık.
	- **1..*:** Bir veya daha fazla varlık.

