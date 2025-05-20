# TUBITAK-PROJESI  
# 🗺️ Türkiye UNESCO Dünya Mirasları Haritası (TÜBİTAK Projesi)

Bu proje, Türkiye'deki **UNESCO Dünya Miras Listesi**'nde yer alan kültürel varlıkların etkileşimli bir harita üzerinde tanıtılmasını amaçlayan bir TÜBİTAK destekli web uygulamasıdır.

---

## 🎯 Amaç

Kullanıcıların Türkiye'nin tarihi ve kültürel mirasları hakkında bilgi edinmesini sağlamak; bu yerlerin:

- 📸 Fotoğraflarını  
- 📖 Yazılı açıklamalarını  
- 🔊 Sesli açıklamalarını  
- 🌀 360° sanal gezinti bağlantılarını  

tek bir platformda kullanıcıya sunmaktır.

---

## 🔍 Özellikler

- ✅ **Google Maps tabanlı interaktif harita**  
- 📍 Marker tıklanınca açılan bilgi penceresi:
  - Tanıtım fotoğrafı
  - Yazılı açıklama
  - Sesli anlatım (Web Speech API ile)
  - Daha fazla görsel için galeri
  - 360° sanal tur bağlantısı
- 🗨️ **Yorum sistemi:**
  - Her yer için kullanıcı yorumları
  - Yıldızlı puanlama
  - Ortalama puan hesaplama
- 🔄 Yorumlar **SQL Server veritabanında** tutulur

---

## 💻 Teknolojiler

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

### 🎪 Proje Sergisinden Kareler (14–15 Mayıs 2025)

> TÜBİTAK 4006-B Bilim Fuarı kapsamında okulumuzda gerçekleşen proje sergisine ait bazı anlar:

- İlk karede proje başında ben ve arkadaşım yer almaktayız.  
- İkinci karede ise:  
  - **Demirci Belediye Başkanı:** Erkan Kara  
  - **Demirci Ticaret ve Sanayi Odası Yönetim Kurulu Başkanı:** Kasım Kabak  
  - **Demirci İlçe Millî Eğitim Müdürü:** Bilal Çetinkaya  
  - **Demirci Ahi Evran Mesleki ve Teknik Anadolu Lisesi Müdürü:** Ahmet Raşit Petekci  
  - Öğretmenlerimiz ve ziyaretçiler de sergimizde yer almaktadır.

![sergi-foto1](https://github.com/user-attachments/assets/533a446e-a669-4821-a42d-643ef9226ac1)  
![sergi-foto2](https://github.com/user-attachments/assets/d500cd47-80c9-4ed9-97b1-bbf282da0e76)

---

🔒 Not:
 Bu proje, TÜBİTAK 4006-B Bilim Fuarı kapsamında Demirci Ahi Evran Mesleki ve Teknik Anadolu Lisesi tarafından başvurusu yapılmış ve kabul edilmiştir.
Tüm yazılım geliştirme süreci tarafımdan bireysel olarak hazırlanmıştır.

Yalnızca sistemin genel yapısını ve görsellerini tanıtmak amacıyla hazırlanmıştır.
Kodların tamamı paylaşılmamaktadır.

---

## 🗃️ Yorum Sistemi Backend (Node.js + MSSQL)

Yorumlar hem eklenebilir hem de listelenebilir şekilde SQL Server üzerinde saklanır. Backend servisi aşağıdaki gibi çalışır:

```js
const express = require("express");
const bodyParser = require("body-parser");
const cors = require("cors");
const sql = require("mssql");

const app = express();
const port = 3000;

const config = {
  user: "",
  password: "",
  server: "",
  database: "",
  options: {
    encrypt: true,
    trustServerCertificate: true,
  },
};

app.use(cors());
app.use(bodyParser.json());

let pool;

sql
  .connect(config)
  .then((p) => {
    pool = p;
    console.log("✅ MSSQL bağlantısı başarılı");
  })
  .catch((err) => console.error("❌ MSSQL bağlantı hatası:", err));

// Yorum ekleme
app.post("/api/yorum-ekle", async (req, res) => {
  const { yerAdi, yorum, puan } = req.body;

  if (!yerAdi || !yorum || !puan) {
    return res.status(400).json({ error: "Eksik bilgi" });
  }

  try {
    await pool
      .request()
      .input("yerAdi", sql.NVarChar(255), yerAdi)
      .input("yorum", sql.NVarChar(sql.MAX), yorum)
      .input("puan", sql.Int, puan)
      .input("tarih", sql.DateTime, new Date()).query(`
        INSERT INTO yorumlar (yerAdi, yorum, puan, tarih)
        VALUES (@yerAdi, @yorum, @puan, @tarih)
      `);

    res.json({ success: true });
  } catch (err) {
    console.error("❌ Veritabanı hatası (ekleme):", err);
    res.status(500).json({ error: "Veritabanı hatası" });
  }
});

// Yorumları çekme
app.get("/api/yorumlar/:yerAdi", async (req, res) => {
  const yerAdi = req.params.yerAdi;

  try {
    const yorumlar = await pool
      .request()
      .input("yerAdi", sql.NVarChar(255), yerAdi)
      .query(
        `SELECT * FROM Yorumlar WHERE yerAdi = @yerAdi ORDER BY tarih DESC`
      );

    const ortalama = await pool
      .request()
      .input("yerAdi", sql.NVarChar(255), yerAdi)
      .query(
        `SELECT AVG(CAST(puan AS FLOAT)) AS ortalamaPuan FROM Yorumlar WHERE yerAdi = @yerAdi`
      );

    res.send({
      yorumlar: yorumlar.recordset,
      ortalamaPuan: ortalama.recordset[0].ortalamaPuan || 0,
    });
  } catch (err) {
    console.error("❌ Yorumları çekme hatası:", err);
    res.status(500).send({ success: false });
  }
});

app.listen(port, () => {
  console.log(`🚀 Sunucu http://localhost:${port} üzerinde çalışıyor`);
});
