# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Burak Akça
- **Öğrenci Numarası**: 170422005

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyasını projenizin GitHub reposuna yükleyiniz.
- Swagger Editor ile test ettiğinizden emin olunuz.

### 🔗 GitHub Repo Linki
https://github.com/Burak-Akca/OpenApiDesign
---

## 📝 API Açıklaması

# 📚 Online Library API

Bu proje, bir üniversitenin kütüphane sistemi için geliştirilmiş RESTful API tasarımıdır. API, kitaplar, öğrenciler ve ödünç alma işlemleri gibi temel işlevleri içerir. OpenAPI 3.0.3 standardına uygun olarak tanımlanmıştır.

## 🌐 API Bilgileri

- **Base URL:** `http://localhost:8080/api`
- **API Versiyonu:** 1.0.0

---

## 📦 Varlıklar (Entities)

### 🟦 Book
- `id`, `title`, `author`, `isbn`, `publisher`, `pageCount`, `stock`

### 🟩 Student
- `id`, `name`, `studentNumber`, `email`, `isActive`

### 🟨 Loan
- `id`, `studentId`, `bookId`, `loanDate`, `returnDate`, `status`

---

## 🔄 CRUD Endpoint’leri

### 📘 Books
| İşlem | HTTP Yöntemi | Endpoint |
|-------|---------------|----------|
| Listele | `GET` | `/books` |
| Ekle | `POST` | `/books` |
| Tekil Getir | `GET` | `/books/{id}` |
| Güncelle | `PUT` | `/books/{id}` |
| Sil | `DELETE` | `/books/{id}` |

### 👨‍🎓 Students
| İşlem | HTTP Yöntemi | Endpoint |
|-------|---------------|----------|
| Listele | `GET` | `/students` |
| Ekle | `POST` | `/students` |
| Tekil Getir | `GET` | `/students/{id}` |
| Güncelle | `PUT` | `/students/{id}` |
| Sil | `DELETE` | `/students/{id}` |

### 🔁 Loans
| İşlem | HTTP Yöntemi | Endpoint |
|-------|---------------|----------|
| Listele | `GET` | `/loans` |
| Ödünç Al | `POST` | `/loans` |
| Tekil Getir | `GET` | `/loans/{id}` |
| Geri Getir (Return) | `PATCH` | `/loans/{id}/return` |

---

## ⚙️ Components Kullanımı

### 📑 `schemas`
- Ortak nesne yapıları: `Book`, `Student`, `Loan`

### 📌 `parameters`
- Tekrar kullanılabilir parametre tanımları:
  - `BookId`, `StudentId`, `LoanId`
  - Sayfalama için: `page`, `size`

### ⚠️ `responses`
- Ortak hata mesajı:
  - `404 NotFound` → `"Resource not found."`

---

## 📄 Sayfalama Desteği

- `GET /books` endpoint'inde desteklenir.
- Parametreler:
  - `page`: Sayfa numarası (varsayılan: `1`)
  - `size`: Sayfa başına veri sayısı (varsayılan: `10`)

---

## ❌ Hata Yönetimi

- 404 durumları için `NotFound` bileşeni tanımlıdır.
- Örnek:
  ```json
  {
    "error": "Resource not found."
  }

---

## 🧪 Test Notları (Opsiyonel)

📘 GET /books – Tüm Kitapları Listele
✅ Başarılı Yanıt (200 OK)

[
  {
    "id": "b123",
    "title": "Artificial Intelligence 101",
    "author": "Ali Veli",
    "isbn": "978-3-16-148410-0",
    "publisher": "Library Publications",
    "pageCount": 320,
    "stock": 5
  },
  {
    "id": "b124",
    "title": "Data Structures",
    "author": "Ayşe Yılmaz",
    "isbn": "978-1-23-456789-0",
    "publisher": "CS Books",
    "pageCount": 200,
    "stock": 3
  }
]
Yanıt bir dizi kitap nesnesinden oluşur.

Sayfalama parametreleri (page, size) opsiyoneldir ve kullanıldığında sonucu sınırlar.


👨‍🎓 POST /students – Yeni Öğrenci Ekle
📥 Örnek İstek (requestBody)

{
  "id": "s001",
  "name": "Mehmet Yılmaz",
  "studentNumber": "20220001",
  "email": "mehmet.yilmaz@example.com",
  "isActive": true
}
✅ Beklenen Yanıt (201 Created)

{
  "message": "Student created successfully."
}
Not: Yanıt içeriği Swagger tanımında belirtilmemiştir, sadece 201 statü kodu döner.

⚠️ Hatalı İstek – Eksik Alanla POST /students

❌ Hatalı Örnek:

{
  "id": "s002",
  "name": "Ahmet",
  "studentNumber": "20220002",
  "isActive": true
}
Bu istekte email alanı eksiktir.

Swagger Editor üzerinde test edildiğinde 400 hatası alınabilir.

🔴 Yanıt Örneği:

{
  "error": "Request body validation failed. 'email' is required."
}
400 Bad Request türü hata dönüşü, API tanımında components.responses altında açıkça tanımlanmamıştır ancak otomatik olarak Swagger UI üzerinden gözlemlenebilir.

