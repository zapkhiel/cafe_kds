# Soulmate Cafe KDS - Backend Projesi

Sunucu Tabanlı Programlama dersi final ödevi olarak geliştirdiğim bu proje, Soulmate Cafe şubelerinin sipariş yönetimini sağlayan bir RESTful API servisidir. Proje, Node.js ve Express kullanılarak, **Strict MVC** (Model-View-Controller) mimarisine sadık kalınarak geliştirilmiştir.

### 📌 Proje Hakkında ve Senaryo
Bu sistem, şubelerden gelen siparişlerin mutfağa iletilmesini ve durumlarının takibini sağlar.

**Senaryo:**
Gerçek bir kafe ortamı simüle edilmiştir. Bir garson veya kasiyer sisteme sipariş girer. Ancak siparişin onaylanması için arkada çalışan bazı iş kuralları (Business Logic) vardır. Örneğin; sistem o an şubenin açık olup olmadığını kontrol eder, kapalıysa siparişi reddeder.

### 📂 Mimari Yapı (MVC)
Projeyi derste işlediğimiz MVC yapısına birebir uygun şekilde klasörledim:

* **src/models:** Veritabanı sorguları (SQL) burada bulunur.
* **src/controllers:** İş mantığı (Business Logic) ve kurallar burada işlenir.
* **src/routes:** Sadece URL yönlendirmeleri yapılır.
* **src/config:** Veritabanı bağlantı ayarları yer alır.

### ⚙️ Uygulanan İş Kuralları
Projede iki temel kısıtlama (Business Rule) bulunmaktadır:

1.  **Şube Kapalıysa Sipariş Alınamaz:**
    Sipariş oluşturulurken şubenin `is_open` durumuna bakılır. Eğer şube kapalıysa (0), API 400 hatası döner ve kayıt engellenir.

2.  **Sipariş Silme Koruması:**
    Sadece "Bekliyor" durumundaki siparişler iptal edilebilir. Eğer mutfak siparişi "Hazırlanıyor" aşamasına aldıysa, bu sipariş veri bütünlüğü için silinemez.

### 🚀 Kurulum ve Çalıştırma

Projeyi kendi bilgisayarınızda ayağa kaldırmak için:

1.  Projeyi indirin:
    `git clone https://github.com/zapkhiel/cafe_kds.git`

2.  Gerekli paketleri kurun:
    `npm install`

3.  Ayarlar dosyasını oluşturun:
    Ana dizindeki `.env.example` dosyasının adını `.env` olarak değiştirin ve kendi MySQL bilgilerinizi içine yazın.

4.  Projeyi başlatın:
    `npm start`

### 🔌 Önemli Endpoint'ler

| Metot | Adres | Ne İşe Yarar? |
|-------|----------------------|----------|
| **GET** | `/api/products` | Menüdeki tüm ürünleri getirir. |
| **POST** | `/api/orders` | Yeni sipariş oluşturur (Kurallar burada çalışır). |
| **PUT** | `/api/orders/:id` | Siparişin durumunu günceller (Hazır/Teslim Edildi vb.). |
| **DELETE**| `/api/orders/:id` | Siparişi siler (Sadece hazırlanmıyorsa). |

---
**Geliştirici:** Melihcan Çakmak