# Evcil Hayvan Sahiplendirme Platformu 🐾
Bu döküman, Evcil Hayvan Sahiplendirme Platformu için oluşturulan veritabanı tasarımını ve kullanım detaylarını içerir.

---

## 🗂️ Veritabanı Tasarımı

### 1. **users**
**Amacı**: Kullanıcı bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `users ↔ ads`: Kullanıcı birden fazla ilan oluşturabilir (1:N).
- `users ↔ messages`: Kullanıcı birden fazla mesaj gönderebilir (1:N).
- `users ↔ pets`: Kullanıcı birden fazla evcil hayvana sahip olabilir (1:N).
- `users ↔ favorite_ads`: Kullanıcı birden fazla ilanı favorilerine ekleyebilir (1:N).

**Önemli Alanlar**:
- `id`: Kullanıcının benzersiz kimliği.
- `name`: Kullanıcının adı.
- `email`: Kullanıcının e-posta adresi.
- `password`: Kullanıcının şifre bilgisi.

---

### 2. **ads**
**Amacı**: İlanları tutar. Her ilan bir kullanıcıya, bir hayvana, bir adrese ve bir statüye bağlıdır.  
**Tablolar Arası İlişkiler**:
- `ads ↔ users`: İlanı oluşturan kullanıcıyla `belongsTo` ilişkisi (N:1).
- `ads ↔ pets`: İlanın ait olduğu hayvanla `belongsTo` ilişkisi (N:1).
- `ads ↔ addresses`: İlanın adresiyle `belongsTo` ilişkisi (N:1).
- `ads ↔ statuses`: İlanın durumuyla `belongsTo` ilişkisi (N:1).
- `ads ↔ favorite_ads`: İlanın favori olarak eklendiği kayıtlarla `hasMany` ilişkisi (1:N).
- `ads ↔ contacts`: İlanın iletişim bilgisiyle `belongsTo` ilişkisi (N:1).

**Önemli Alanlar**:
- `user_id`: İlanı oluşturan kullanıcının kimliği.
- `pet_id`: İlanın hangi hayvana ait olduğunu belirtir.
- `title`: İlanın başlığı.
- `description`: İlan açıklaması.
- `status_id`: İlanın durumunu belirler.
- `address_id`: İlanın adres bilgisi.
- `image_url`: İlanın görsel bağlantısı.
- `contact_id`: İlanla ilgili iletişim bilgisi.

---

### 3. **addresses**
**Amacı**: Adres bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `addresses ↔ districts`: Her adres bir mahalleye aittir, `belongsTo` ilişkisi (N:1).
- `addresses ↔ ads`: Bir adres birden fazla ilana bağlı olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `street`: Sokağın adı.
- `postal_code`: Posta kodu.
- `district_id`: Adresin bağlı olduğu ilçe kimliği.

---

### 4. **districts**
**Amacı**: İlçe bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `districts ↔ cities`: Her mahalle bir şehre aittir, `belongsTo` ilişkisi (N:1).
- `districts ↔ addresses`: Bir mahalle birden fazla adrese sahip olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: Mahallenin benzersiz kimliği.
- `name`: Mahallenin adı.
- `city_id`: Mahallenin bağlı olduğu şehrin kimliği.

---

### 5. **cities**
**Amacı**: Şehir bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `cities ↔ districts`: Bir şehir birden fazla mahalleye sahip olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: Şehrin benzersiz kimliği.
- `name`: Şehrin adı.

---

### 6. **contact**
**Amacı**: İletişim bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `contact ↔ ads`: Bir iletişim kaydı birden fazla ilana bağlı olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: İletişim kaydının benzersiz kimliği.
- `phone_number`: İletişim için telefon numarası.
- `email`: İletişim için e-posta adresi.

---

### 7. **favorite_ads**
**Amacı**: Kullanıcıların favorilerine ekledikleri ilanları saklar.  
**Tablolar Arası İlişkiler**:
- `favorite_ads ↔ users`: Her favori ilan bir kullanıcıya aittir, `belongsTo` ilişkisi (N:1).
- `favorite_ads ↔ ads`: Her favori ilan bir ilana aittir, `belongsTo` ilişkisi (N:1).

**Önemli Alanlar**:
- `id`: Favori ilan kaydının benzersiz kimliği.
- `user_id`: Favori ilanı ekleyen kullanıcının kimliği.
- `ad_id`: Favori ilanı temsil eden ilan kimliği.

---

### 8. **health_statuses**
**Amacı**: Evcil hayvanların sağlık durumunu saklar.  
**Tablolar Arası İlişkiler**:
- `health_statuses ↔ pets`: Her sağlık durumu bir evcil hayvana aittir, `hasOne` ilişkisi (1:1).

**Önemli Alanlar**:
- `id`: Sağlık durumu kaydının benzersiz kimliği.
- `vaccination`: Hayvanın aşı durumu.
- `internal_parasite`: Hayvanın iç parazit durumu.
- `external_parasite`: Hayvanın dış parazit durumu.
- `health_description`: Hayvanın sağlık durumu hakkında açıklama.

---

### 9. **messages**
**Amacı**: Kullanıcıların gönderdikleri mesajları saklar.  
**Tablolar Arası İlişkiler**:
- `messages ↔ users`: Her mesaj bir kullanıcıya aittir, `belongsTo` ilişkisi (N:1).

**Önemli Alanlar**:
- `id`: Mesaj kaydının benzersiz kimliği.
- `user_id`: Mesajı gönderen kullanıcının kimliği.
- `name`: Mesajı gönderen kişinin adı.
- `email`: Mesajı gönderen kişinin e-posta adresi.
- `subject`: Mesajın konusu.
- `content`: Mesajın içeriği.

---

### 10. **pets**
**Amacı**: Evcil hayvan bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `pets ↔ pet_breeds`: Her evcil hayvan bir ırka aittir, `belongsTo` ilişkisi (N:1).
- `pets ↔ health_statuses`: Her evcil hayvan bir sağlık durumuna sahiptir, `belongsTo` ilişkisi (N:1).
- `pets ↔ users`: Her evcil hayvan bir kullanıcıya aittir, `belongsTo` ilişkisi (N:1).
- `pets ↔ training_infos`: Her evcil hayvanın eğitim bilgisi olabilir, `hasOne` ilişkisi (1:1).
- `pets ↔ ads`: Her evcil hayvan bir ilanla ilişkili olabilir, `hasOne` ilişkisi (1:1).

**Önemli Alanlar**:
- `id`: Evcil hayvan kaydının benzersiz kimliği.
- `name`: Evcil hayvanın adı.
- `breed_id`: Evcil hayvanın ırkı.
- `age`: Evcil hayvanın yaşı.
- `gender`: Evcil hayvanın cinsiyeti.
- `health_status_id`: Evcil hayvanın sağlık durumu.
- `user_id`: Evcil hayvanın sahibi olan kullanıcının kimliği.

---

### 11. **pet_breeds**
**Amacı**: Evcil hayvan ırklarını saklar.  
**Tablolar Arası İlişkiler**:
- `pet_breeds ↔ pet_types`: Her ırk bir türe aittir, `belongsTo` ilişkisi (N:1).
- `pet_breeds ↔ pets`: Her ırk birden fazla evcil hayvana ait olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: Evcil hayvan ırkı kaydının benzersiz kimliği.
- `name`: Evcil hayvan ırkının adı.
- `type_id`: Evcil hayvan ırkının ait olduğu tür.

---

### 12. **pet_types**
**Amacı**: Evcil hayvan türlerini saklar.  
**Tablolar Arası İlişkiler**:
- `pet_types ↔ pet_breeds`: Her tür birden fazla evcil hayvan ırkına ait olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: Evcil hayvan türü kaydının benzersiz kimliği.
- `name`: Evcil hayvan türünün adı (Köpek, Kedi vb.).

---

### 13. **statuses**
**Amacı**: İlan durumlarını saklar.  
**Tablolar Arası İlişkiler**:
- `statuses ↔ ads`: Her durum birden fazla ilana ait olabilir, `hasMany` ilişkisi (1:N).

**Önemli Alanlar**:
- `id`: İlan durumu kaydının benzersiz kimliği.
- `name`: İlan durumunun adı (Örneğin: 'Aktif', 'Pasif', 'Beklemede').

---

### 14. **training_infos**
**Amacı**: Evcil hayvanların eğitim bilgilerini saklar.  
**Tablolar Arası İlişkiler**:
- `training_infos ↔ pets`: Eğitim bilgisi her evcil hayvana aittir, `belongsTo` ilişkisi (N:1).

**Önemli Alanlar**:
- `id`: Eğitim kaydının benzersiz kimliği.
- `training_type`: Eğitim türü (Temel, İleri vb.).
- `start_date`: Eğitimin başlangıç tarihi.
- `end_date`: Eğitimin bitiş tarihi.
- `description`: Eğitim açıklaması.
