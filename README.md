# 📚 Online Library API

Online Library API, bir üniversitenin kütüphane sistemini yönetmek amacıyla geliştirilen RESTful servistir. Kitaplar, öğrenciler ve ödünç alma işlemleri gibi temel işlevleri destekler. Bu API, OpenAPI 3.0.3 standardına göre tasarlanmıştır ve Swagger Editor üzerinden test edilebilir.

---

## 🚀 Özellikler

- 📘 Kitapları listeleme, ekleme, güncelleme ve silme (CRUD)
- 👨‍🎓 Öğrenci yönetimi (kayıt, güncelleme, silme, listeleme)
- 🔄 Kitap ödünç alma ve iade işlemleri
- ✅ Sayfalama desteği
- ❌ Standart hata mesajları

---

## 🏗️ Varlıklar (Entities)

### 1. `Book`
Kitapla ilgili bilgileri içerir.  
**Alanlar:** `id`, `title`, `author`, `isbn`, `publisher`, `pageCount`, `stock`

### 2. `Student`
Kütüphane sistemine kayıtlı öğrencileri temsil eder.  
**Alanlar:** `id`, `name`, `studentNumber`, `email`, `isActive`

### 3. `Loan`
Ödünç alma işlemlerini tanımlar.  
**Alanlar:** `id`, `studentId`, `bookId`, `loanDate`, `returnDate`, `status`

---

## 🔁 CRUD Endpoint'leri

### 📚 Kitaplar (`/books`)
- `GET /books` – Tüm kitapları listele (sayfalama ile)
- `POST /books` – Yeni kitap ekle
- `GET /books/{id}` – Belirli bir kitabı getir
- `PUT /books/{id}` – Kitabı güncelle
- `DELETE /books/{id}` – Kitabı sil

### 👨‍🎓 Öğrenciler (`/students`)
- `GET /students` – Tüm öğrencileri listele
- `POST /students` – Yeni öğrenci ekle
- `GET /students/{id}` – Öğrenci bilgisi getir
- `PUT /students/{id}` – Öğrenciyi güncelle
- `DELETE /students/{id}` – Öğrenciyi sil

### 📖 Ödünç İşlemleri (`/loans`)
- `GET /loans` – Tüm ödünç işlemleri
- `POST /loans` – Yeni ödünç kaydı oluştur
- `GET /loans/{id}` – Belirli bir ödünç kaydını getir
- `PATCH /loans/{id}/return` – Kitabı iade et

---

## 🧩 Components Kullanımı

### ✅ `components/schemas`
API'nin veri modelleri burada tanımlanır:
- `Book`
- `Student`
- `Loan`

### 🧭 `components/parameters`
Yol parametreleri ve sorgu parametreleri:
- `BookId`, `StudentId`, `LoanId`
- `PageParam`, `SizeParam`

### 🚨 `components/responses`
Yaygın hata durumları tanımlanır:
- `404 Not Found`

---

## 📄 Sayfalama Desteği

- `GET /books` çağrısında isteğe bağlı `page` ve `size` query parametreleriyle sayfalama yapılabilir.
- Örneğin: `GET /books?page=2&size=5`

---

## ⚠️ Hata Yönetimi

- `404 Not Found`: Kaynak bulunamadığında döner.
- `400 Bad Request`: Eksik ya da geçersiz veri gönderildiğinde (Swagger Editor validasyonu tarafından sağlanır).
- `500 Internal Server Error`: Uygulama içi beklenmeyen hatalar için (belgede tanımlı değil).

---

## 🧪 Test & Örnekler

Swagger Editor üzerinden yapılan testler ve örnekler için [OpenAPI_Delivery.md](./OpenAPI_Delivery.md) dosyasına göz atabilirsiniz.

---

## 📌 Gereksinimler

- OpenAPI 3.0.3 uyumlu araçlar (örneğin [Swagger Editor](https://editor.swagger.io/))
- Local sunucu örneği için: `http://localhost:8080/api`

---

## 👥 Katkı Sağlama

Pull request'ler ve öneriler memnuniyetle kabul edilir. Lütfen kod katkısı yapmadan önce bir issue açın.

---

## 📃 Lisans

Bu proje bir üniversite dersi kapsamında geliştirilmiş olup, yalnızca eğitim amaçlı kullanılabilir.

