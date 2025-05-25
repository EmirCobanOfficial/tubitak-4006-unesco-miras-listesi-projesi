# TUBITAK-PROJESİ / TÜBİTAK PROJECT  
# 🗺️ Türkiye UNESCO Dünya Mirasları Haritası  
# 🗺️ Interactive Map of Turkey's UNESCO World Heritage Sites

Bu proje, Türkiye'deki **UNESCO Dünya Miras Listesi**'nde yer alan kültürel varlıkların etkileşimli bir harita üzerinde tanıtılmasını amaçlayan bir TÜBİTAK destekli web uygulamasıdır.  
This project is a TÜBİTAK-supported web application aimed at presenting the cultural heritage sites listed in Turkey's **UNESCO World Heritage List** on an interactive map.

---

## 🎯 Amaç / Purpose

Kullanıcıların Türkiye'nin tarihi ve kültürel mirasları hakkında bilgi edinmesini sağlamak; bu yerlerin:  
To enable users to learn about Turkey’s historical and cultural heritage sites, providing:

- 📸 Fotoğraflarını / Photos  
- 📖 Yazılı açıklamalarını / Written descriptions  
- 🔊 Sesli açıklamalarını / Audio narrations  
- 🌀 360° sanal gezinti bağlantılarını / 360° virtual tour links  

tek bir platformda kullanıcıya sunmaktır.  
in a single platform.

---

## 🔍 Özellikler / Features

- ✅ **Google Maps tabanlı interaktif harita** / Interactive map based on Google Maps  
- 📍 Marker tıklanınca açılan bilgi penceresi: / Info window on marker click:  
  - Tanıtım fotoğrafı / Introductory photo  
  - Yazılı açıklama / Text description  
  - Sesli anlatım (Web Speech API ile) / Audio narration (using Web Speech API)  
  - Daha fazla görsel için galeri / Gallery for more images  
  - 360° sanal tur bağlantısı / 360° virtual tour link  
- 🗨️ **Yorum sistemi:** / Comment system:  
  - Her yer için kullanıcı yorumları / User comments for each site  
  - Yıldızlı puanlama / Star rating  
  - Ortalama puan hesaplama / Average rating calculation  
- 🔄 Yorumlar **SQL Server veritabanında** tutulur / Comments stored in **SQL Server database**

---

## 💻 Teknolojiler / Technologies

- **Google Maps JavaScript API**  
- **Web Speech API**  
- **HTML, CSS, JavaScript**  
- **Node.js + Express.js**  
- **SQL Server (MSSQL)**

---

## 📷 Ekran Görüntüleri / Screenshots

| 📍 Marker | 📌 Marker'a Tıklama / Click on Marker | ✍️ Yorum Ekleme / Add Comment | 🗨️ Yorumlar / Comments | 🖼️ Galeri / Gallery |
|----------|---------------------|-----------------|-------------|------------|
| ![marker](https://github.com/user-attachments/assets/885bef1f-586f-4c52-bd1b-22400770c6a9) | ![görsel2](https://github.com/user-attachments/assets/2adc113f-391f-4def-9a0d-0cc473b03d99) | ![yorum-ekleme](https://github.com/user-attachments/assets/1d7acf36-d31e-422b-9f6c-3ae7bc67c120) | ![yorum](https://github.com/user-attachments/assets/90e594f8-18eb-4c1b-99bc-215623b52978) | ![galeri](https://github.com/user-attachments/assets/934c31a2-428f-4d42-8660-e844b1c7381a) |

---

### 🎪 Proje Sergisinden Kareler / Project Exhibition Photos (May 14–15, 2025)

> TÜBİTAK 4006-B Bilim Fuarı kapsamında okulumuzda gerçekleşen proje sergisine ait bazı anlar:  
> Moments from the project exhibition held at our school within the TÜBİTAK 4006-B Science Fair:

- İlk karede proje başında ben ve arkadaşım yer almaktayız.  
- In the first photo, me and my friend are at the project stand.  
- İkinci karede ise:  
- In the second photo:  
  - **Demirci Belediye Başkanı:** Erkan Kara / Mayor of Demirci: Erkan Kara  
  - **Demirci Ticaret ve Sanayi Odası Başkanı:** Kasım Kabak / President of Demirci Chamber of Commerce: Kasım Kabak  
  - **Demirci İlçe Millî Eğitim Müdürü:** Bilal Çetinkaya / District Education Director: Bilal Çetinkaya  
  - **Demirci Ahi Evran Mesleki ve Teknik Anadolu Lisesi Müdürü:** Ahmet Raşit Petekci / Principal of Demirci Ahi Evran Vocational High School: Ahmet Raşit Petekci  
- Öğretmenlerimiz ve ziyaretçiler de sergimizde yer almaktadır.  
- Our teachers and visitors also attended the exhibition.

![sergi-foto1](https://github.com/user-attachments/assets/533a446e-a669-4821-a42d-643ef9226ac1)  
![sergi-foto2](https://github.com/user-attachments/assets/d500cd47-80c9-4ed9-97b1-bbf282da0e76)

---

🔒 Not / Note:  
Bu proje, TÜBİTAK 4006-B Bilim Fuarı kapsamında Demirci Ahi Evran Mesleki ve Teknik Anadolu Lisesi tarafından başvurusu yapılmış ve kabul edilmiştir.  
Tüm yazılım geliştirme süreci tarafımdan bireysel olarak hazırlanmıştır.  
This project was applied and accepted within the TÜBİTAK 4006-B Science Fair by Demirci Ahi Evran Vocational High School.  
All software development was done individually by me.

Yalnızca sistemin genel yapısını ve görsellerini tanıtmak amacıyla hazırlanmıştır.  
Kodların tamamı paylaşılmamaktadır.  
This README only introduces the general system structure and visuals.  
Full source code is not shared.

---

## 🗃️ Yorum Sistemi Backend / Comment System Backend (Node.js + MSSQL)

Yorumlar hem eklenebilir hem de listelenebilir şekilde SQL Server üzerinde saklanır. Backend servisi aşağıdaki gibi çalışır:  
Comments can be added and retrieved from SQL Server. The backend service works as follows:

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
    console.log("✅ MSSQL bağlantısı başarılı / MSSQL connection successful");
  })
  .catch((err) => console.error("❌ MSSQL bağlantı hatası / MSSQL connection error:", err));

// Yorum ekleme / Add comment
app.post("/api/yorum-ekle", async (req, res) => {
  const { yerAdi, yorum, puan } = req.body;

  if (!yerAdi || !yorum || !puan) {
    return res.status(400).json({ error: "Eksik bilgi / Missing information" });
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
    console.error("❌ Veritabanı hatası (ekleme) / Database error (insert):", err);
    res.status(500).json({ error: "Veritabanı hatası / Database error" });
  }
});

// Yorumları çekme / Get comments
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
    console.error("❌ Yorumları çekme hatası / Error fetching comments:", err);
    res.status(500).send({ success: false });
  }
});

app.listen(port, () => {
  console.log(`🚀 Sunucu http://localhost:${port} üzerinde çalışıyor / Server running on http://localhost:${port}`);
});
