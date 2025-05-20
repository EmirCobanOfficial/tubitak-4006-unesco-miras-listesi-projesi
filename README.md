# 🗺️ Türkiye UNESCO Dünya Mirasları Haritası

Bu proje, Türkiye'deki **UNESCO Dünya Miras Listesi**'nde yer alan kültürel varlıkların etkileşimli bir harita üzerinde tanıtılmasını amaçlayan bir **web tabanlı bilgi sistemi**dir.

---

## 🎯 Amaç

Kullanıcıların Türkiye'nin tarihi ve kültürel mirasları hakkında bilgi edinmesini sağlamak; bu yerlerin:

- 📸 Fotoğraflarını  
- 📖 Yazılı açıklamalarını  
- 🔊 Sesli açıklamalarını  
- 🌀 360° sanal gezinti bağlantılarını  

tek bir platformda sunmak hedeflenmiştir.

---

## 🔍 Özellikler

- ✅ **Google Maps tabanlı interaktif harita**  
- 📍 Marker tıklanınca açılan bilgi penceresi:
  - Tanıtım fotoğrafı
  - Yazılı açıklama
  - Web Speech API ile sesli anlatım
  - Görsel galeri
  - 360° sanal tur bağlantısı  
- 🗨️ **Yorum sistemi:**
  - Her yer için kullanıcı yorumları
  - Yıldızlı puanlama
  - Ortalama puan hesaplama
- 🔄 Yorumlar **SQL Server veritabanında** saklanır

---

## 💻 Kullanılan Teknolojiler

- **Google Maps JavaScript API**
- **Web Speech API**
- **HTML, CSS, JavaScript**
- **Node.js + Express.js**
- **SQL Server (MSSQL)**

---

## 📷 Ekran Görüntüleri

| 📍 Marker | 📌 Marker'a Tıklama | ✍️ Yorum Ekleme | 🗨️ Yorumlar | 🖼️ Galeri |
|----------|---------------------|-----------------|-------------|------------|
| ![marker](https://github.com/user-attachments/assets/885bef1f-586f-4c52-bd1b-22400770c6a9) | ![görsel2](https://github.com/user-attachments/assets/2adc113f-391f-4def-9a0d-0cc473b03d99) | ![yorum-ekleme](https://github.com/user-attachments/assets/1d7acf36-d31e-422b-9f6c-3ae7bc67c120) | ![yorum](https://github.com/user-attachments/assets/90e594f8-18eb-4c1b-99bc-215623b52978) | ![galeri](https://github.com/user-attachments/assets/934c31a2-428f-4d42-8660-e844b1c7381a) |


---

🔒 Not
Bu proje, TÜBİTAK 4006-B Bilim Fuarı kapsamında okulum tarafından başvurusu yapılan ve kabul edilen bir proje olarak okul etkinliğinde sergilenmiştir.
Tüm yazılım geliştirme süreci tarafımdan bireysel olarak hazırlanmıştır.
Bu sayfa yalnızca sistemin genel yapısını ve görsellerini tanıtmak amacıyla hazırlanmıştır. Kodların tamamı paylaşılmamaktadır.

## 🗃️ Yorum Sistemi (Node.js + MSSQL)

Yorumlar hem eklenebilir hem de listelenebilir şekilde veritabanında saklanır.
