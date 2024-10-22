## **1. Giriş**

Bu ders notunda, veri bilimi ve iş zekası alanlarında derinlemesine bir yolculuğa çıkacağız. Amacımız, bu alanlarda hiç bilgisi olmayan birinin orta düzeyde uzmanlık kazanmasını ve kendi uygulamalarını geliştirebilecek seviyeye gelmesini sağlamaktır.

---

## **2. Veri Bilimine Derinlemesine Bakış**

### **2.1. Veri Biliminin Tanımı ve Önemi**

**Veri Bilimi Nedir?**

Veri bilimi, yapılandırılmış ve yapılandırılmamış büyük veri setlerinden değerli bilgiler elde etmek için matematik, istatistik, bilgisayar bilimi ve alan uzmanlığını birleştiren disiplinler arası bir alandır.

**Veri Biliminin Önemi**

- **Karar Verme:** İşletmelerin veriye dayalı kararlar almasını sağlar.
- **Rekabet Avantajı:** Pazardaki trendleri ve müşteri davranışlarını analiz ederek rekabetçi kalmayı sağlar.
- **İnovasyon:** Yeni ürün ve hizmetlerin geliştirilmesine yardımcı olur.

### **2.2. Veri Bilimcinin Rolü ve Sorumlulukları**

**Ana Sorumluluklar:**

- **Veri Analizi ve Yorumlama:** Verileri analiz ederek anlamlı içgörüler elde etmek.
- **Model Geliştirme:** Makine öğrenmesi modelleri oluşturmak ve optimize etmek.
- **Sonuçların İletişimi:** Elde edilen bulguları teknik olmayan ekiplere aktarmak.

**Gerekli Beceriler:**

- **Programlama Dilleri:** Python, R, SQL.
- **İstatistik ve Matematiksel Yetkinlik.**
- **Makine Öğrenmesi ve Derin Öğrenme Teknikleri.**

### **2.3. Veri Bilimi Süreci**

**Adımlar:**

1. **Problemin Tanımlanması**
2. **Veri Toplama ve Erişim**
3. **Veri Ön İşleme ve Temizleme**
4. **Keşifsel Veri Analizi**
5. **Modelleme ve Algoritma Geliştirme**
6. **Model Değerlendirme ve Doğrulama**
7. **Sonuçların Sunumu ve Dağıtımı**

---

## **3. Veri Ön İşleme ve Hazırlama**

Veri ön işleme, veri bilimi sürecinin en kritik adımlarından biridir. Kaliteli bir model için temiz ve düzenli veri şarttır.

### **3.1. Eksik Verilerin İşlenmesi**

**Eksik Verilerin Türleri:**

- **MCAR (Completely at Random):** Veri tamamen rastgele eksik.
- **MAR (At Random):** Eksiklik bazı gözlemlere bağlı.
- **MNAR (Not at Random):** Eksiklik gözlemlenemeyen bir nedenden kaynaklı.

**Eksik Verileri İşleme Yöntemleri:**

- **Silme Yöntemleri:**
    - **Listwise Deletion:** Eksik verisi olan satırları tamamen silmek.
    - **Pairwise Deletion:** Analizlerde sadece mevcut verileri kullanmak.
- **Tahmin Yöntemleri:**
    - **Ortalama veya Medyan ile Doldurma.**
    - **Regresyon İmputasyonu.**
    - **K-NN İmputasyonu.**
### **3.2. Aykırı Değerlerin Tespiti ve İşlenmesi**

**Aykırı Değer Nedir?**

Veri setindeki diğer gözlemlerden önemli ölçüde farklı olan değerlerdir.

**Tespit Yöntemleri:**

- **Boxplot Grafikleri.**
- **Z-Skoru Hesaplama.**
- **IQR (Interquartile Range) Metodu.**

### **3.3. Veri Normalizasyonu ve Standardizasyonu**

**Normalizasyon:**
Verileri 0 ile 1 arasına ölçeklendirme işlemidir.

**Standardizasyon:**
Verilerin ortalamasını 0, standart sapmasını 1 olacak şekilde ölçeklendirme işlemidir.

### **3.4. Kategorik Verilerin Kodlanması**

**One-Hot Encoding:**

Kategorik değişkenleri ikili (binary) değişkenlere dönüştürür.

```
df_encoded = pd.get_dummies(df, columns=['cinsiyet', 'ülke'])
```

## **4. Keşifsel Veri Analizi (EDA)**

EDA, verileri daha iyi anlamak ve içgörüler elde etmek için kullanılan tekniklerin bütünüdür.

### **4.1. Tanımlayıcı İstatistikler**

**Ölçüler:**

- **Merkezi Eğilim Ölçüleri:**
    - **Ortalama:** Verilerin aritmetik ortalaması.
    - **Medyan:** Verilerin ortanca değeri.
    - **Mod:** En sık görülen değer.
- **Dağılım Ölçüleri:**
    - **Varyans:** Verilerin ortalamadan ne kadar saptığı.
    - **Standart Sapma:** Varyansın karekökü.
    - **IQR:** Üst ve alt çeyrekler arası fark.

```
df['gelir'].describe()
```

### **4.2. Veri Görselleştirme Teknikleri**

- **Histogramlar:** Verilerin dağılımını gösterir.
- **Kutu Grafikleri (Boxplot):** Aykırı değerleri ve dağılımı gösterir.
- **Dağılım Grafikleri (Scatterplot):** İki değişken arasındaki ilişkiyi gösterir.

```
import matplotlib.pyplot as plt
import seaborn as sns

# Histogram
plt.hist(df['yas'])
plt.title('Yaş Dağılımı')
plt.show()

# Boxplot
sns.boxplot(x=df['gelir'])
plt.title('Gelir Dağılımı')
plt.show()
```

### **4.3. Korelasyon Analizi**

**Korelasyon Katsayısı (Pearson):**

İki değişken arasındaki doğrusal ilişkiyi ölçer.

- **Değer Aralığı:** -1 ile 1 arası.
    - **1:** Mükemmel pozitif ilişki.
    - **-1:** Mükemmel negatif ilişki.
    - **0:** Hiçbir ilişki yok.

```
corr_matrix = df.corr()
sns.heatmap(corr_matrix, annot=True)
plt.show()
```

