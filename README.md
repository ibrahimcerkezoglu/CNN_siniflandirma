# BLG407 – CNN ile Bardak / Şişe Sınıflandırma Projesi

Bu repo, BLG407 – Makine Öğrenmesi dersi kapsamında hazırladığım 
**“Kendi görüntü veri setimle CNN sınıflandırma modeli geliştirme”** ödevini içermektedir.

---

## 📌 1. Öğrenci Bilgileri
**Ad:** İbrahim Çerkezoğlu  
**Okul Numarası:** 2112721046  
**Ders:** BLG407 – Makine Öğrenmesi  
**Ödev Konusu:** Bardak / Şişe görüntülerinin CNN modelleri ile sınıflandırılması  
**GitHub Repo:** https://github.com/ibrahimcerkezoglu/CNN_siniflandirma  

---

## 📌 2. Projenin Amacı

Amaç, telefon kamerası ile çektiğim **bardak** ve **şişe** nesnelerine ait görüntülerden oluşan veri setimi kullanarak  
üç farklı CNN modeli eğitmek ve performanslarını karşılaştırmaktır:

- **Model 1: Transfer Learning (VGG16)**
- **Model 2: Sıfırdan tasarlanmış temel CNN**
- **Model 3: Hiperparametreleri değiştirilmiş ve veri artırımı eklenmiş gelişmiş CNN**

---

## 📌 3. Veri Seti Açıklaması

Veri seti tamamen **tarafımdan çekilmiş**, özgün görüntülerden oluşmaktadır.

- Sınıflar: `bardak`, `sise`
- Her sınıf için en az **50 görüntü**
- Toplamda **100+ görüntü**
- Görseller farklı:
  - açılardan,
  - ışık koşullarında,
  - arka planlarda çekilmiştir
- Görseller **128×128 piksel** boyutuna yeniden boyutlandırılmıştır
- Eğitim/Test oranı: **%80 / %20**

Klasör yapısı:

dataset/
train/
bardak/
sise/
test/
bardak/
sise/

---

### 📌 4. Modellerin Açıklamaları

#### Model 1 – Transfer Learning (VGG16)
- ImageNet ağırlıkları ile başlatıldı, üst katmanlar çıkarılıp kendi Dense katmanlarım eklendi.
- Fine-tuning yapılmadı.
- Test doğruluğu: **%59.38**

#### Model 2 – Basit CNN
- 3 Conv bloklu, sıfırdan eğitilen temel CNN modeli.
- Küçük veri setine en iyi uyumu gösterdi.
- Test doğruluğu: **%75.00** (en iyi model)

#### Model 3 – Geliştirilmiş CNN + Veri Artırımı
- Model 2 üzerinde şu değişiklikler yapıldı:
  - Batch size değişti (32 → 16),
  - Öğrenme oranı denendi (0.0003 ve 0.0005),
  - Dropout artırıldı,
  - `ImageDataGenerator` ile veri artırımı eklendi.
- Test doğruluğu: **%37.50** (Model 2’nin gerisinde).


---

## 📌 5. Deney Tablosu (Model 3)

| Deney No | Batch Size | Filtre Sayısı | Dropout      | Öğrenme Oranı | Veri Artırımı | Test Doğruluğu | Not |
|---------|------------|---------------|-------------|---------------|--------------|----------------|-----|
| 1       | 32         | 32–64–128     | 0.25–0.40   | 0.0003        | Var          | %18.75         | Model ağır, val acc çok düşük |
| 2       | 16         | 32–64–128     | 0.40        | 0.0005        | Var          | **%37.50**     | En iyi Model 3 sonucu |
| 3       | 16         | 32–64–128     | 0.40        | 0.0003        | Var          | %34.38         | LR’yi düşürmek fayda etmedi |

---

## 📌 6. Çalıştırma Talimatları

```bash
git clone https://github.com/ibrahimcerkezoglu/CNN_siniflandirma
cd CNN_siniflandirma
pip install tensorflow matplotlib numpy
jupyter notebook
```
---

Ardından ilgili model .ipynb dosyasını çalıştırarak eğitimi başlatabilirsiniz.

---

## 📌 7. Sonuç ve Değerlendirme

Küçük veri setlerinde basit CNN (Model 2) en iyi performansı verdi.

Transfer learning modeli (VGG16) orta düzeyde başarı sağladı.

Model 3’te yapılan değişiklikler teoride faydalı olsa da veri setinin küçük olması sebebiyle aşırı öğrenmeye yol açtı.

En iyi model Model 2 olmuştur.

---
