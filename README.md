# MyFinalProject

Katmanlı mimari (N-Tier Architecture) ile geliştirilmiş bir **.NET 8 Web API** projesidir.  
Bu versiyon yalnızca backend tarafını içermektedir. Angular frontend entegrasyonu ve mimari iyileştirmeler sonraki aşamalarda eklenecektir.

---

## 📌 Proje Amacı

Bu proje aşağıdaki yazılım prensiplerini uygulamak amacıyla geliştirilmiştir:

- Katmanlı mimari kurmak
- SOLID prensiplerini uygulamak
- Entity Framework Core ile veri erişimini yönetmek
- Generic repository altyapısı oluşturmak
- Result pattern kullanarak standart response modeli oluşturmak
- RESTful API geliştirmek

---

## 🏗️ Mimari Yapı

Proje aşağıdaki katmanlardan oluşmaktadır:

### 🔹 Entities
Veritabanı tablolarına karşılık gelen sınıflar ve DTO'lar bulunur.

- Concrete
  - Product
  - Category
  - Customer
  - Order
- DTOs
  - ProductDetailDto

---

### 🔹 Core
Ortak altyapı katmanıdır.

- IEntityRepository<T>
- EfEntityRepositoryBase<T>
- IResult
- IDataResult
- SuccessResult
- ErrorResult
- SuccessDataResult
- ErrorDataResult

Bu katman sayesinde:
- Generic repository yapısı kurulmuştur.
- Servis dönüşleri standart hale getirilmiştir.

---

### 🔹 DataAccess
Veri erişim katmanıdır.

- Abstract
  - IProductDal
  - ICategoryDal
- Concrete
  - EntityFramework
    - EfProductDal
    - EfCategoryDal
    - NorthwindContext
  - InMemory
    - InMemoryProductDal

Entity Framework Core kullanılmaktadır.

---

### 🔹 Business
İş kurallarının bulunduğu katmandır.

- Abstract
  - IProductService
  - ICategoryService
- Concrete
  - ProductManager
  - CategoryManager
- Constants
  - Messages

Bu katmanda:
- Validasyon
- İş kuralları
- Manager sınıfları
yer almaktadır.

---

### 🔹 WebAPI
REST servis katmanıdır.

- ProductsController
- Swagger entegrasyonu

Dependency Injection Program.cs üzerinden yapılmaktadır.

---

### 🔹 ConsoleUI
Service katmanını test etmek amacıyla oluşturulmuş console uygulamasıdır.

---

## 🛠️ Kullanılan Teknolojiler

- .NET 8
- ASP.NET Core Web API
- Entity Framework Core
- SQL Server
- Swagger (Swashbuckle)

---

## ⚙️ Kurulum

### Gereksinimler
- .NET SDK 8.x
- SQL Server veya LocalDB

### Connection String

NorthwindContext içerisinde connection string manuel tanımlıdır:

```csharp
optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=master;Trusted_Connection=true");
```

Bu kısmı kendi veritabanınıza göre düzenlemeniz gerekir.

---

## 🚀 Projeyi Çalıştırma

### WebAPI

```bash
dotnet run --project WebAPI
```

Development ortamında Swagger otomatik açılır.

---

### ConsoleUI

```bash
dotnet run --project ConsoleUI
```

---

## 🌐 API Endpointleri

Base Route:

```
api/products
```

### Tüm ürünleri getir
```
GET /api/products/getall
```

### Id'ye göre ürün getir
```
GET /api/products/getbyid?productId=1
```

### Ürün ekle
```
POST /api/products/add
```

Örnek JSON:

```json
{
  "productId": 0,
  "categoryId": 1,
  "productName": "Kalem",
  "unitsInStock": 10,
  "unitPrice": 25.5
}
```

---

## 📋 İş Kuralları

ProductManager içerisinde:

- ProductName 2 karakterden küçük olamaz.
- Örnek bakım saati kontrolü bulunmaktadır.
- Tüm servis dönüşleri Result pattern ile yapılmaktadır.

---



## 🎯 Not

Bu proje aktif geliştirme aşamasındadır.  
Mimari yapı ilerleyen süreçte daha kurumsal bir seviyeye taşınacaktır.
