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

## 📌 4. Modellerin Açıklamaları

### **Model 1 – Transfer Learning (VGG16)**
- ImageNet ağırlıkları ile başlatılmıştır.
- Üst katmanlar çıkarılarak kendi sınıflarım için yeni Dense katmanları eklenmiştir.
- Fine-tuning uygulanmamıştır.
- En iyi doğruluk **~%59.3**

---

### **Model 2 – Basit CNN**
- 3 adet Conv bloktan oluşan temel CNN.
- Sıfırdan eğitildi.
- Küçük veri setine en iyi uyumu gösterdi.
- En iyi doğruluk **~%75.0**

---

### **Model 3 – Geliştirilmiş CNN + Veri Artırımı**
Model 2 üzerinde aşağıdaki geliştirmeler yapıldı:

- Batch size değiştirildi
- Öğrenme oranı azaltıldı
- Dropout oranı yükseltildi
- `ImageDataGenerator` ile data augmentation eklendi:
  - rotation_range=15  
  - width/height shift 0.1  
  - zoom_range=0.1  
  - horizontal_flip=True  

Performansı Model2’den düşük kalmıştır (**~%37.5**).  
Sebep: veri setinin küçük olması + model karmaşıklığının artması.

---

## 📌 5. Deney Tablosu (Model 3)

| Deney No | Batch Size | Filtre Sayısı | Dropout | LR | Veri Artırımı | Test Accuracy | Not |
|---------|------------|---------------|---------|----|----------------|----------------|------|
| 1 | 32 | 32–64–128 | 0.3 | 0.0005 | Hayır | %68 | Temel model |
| 2 | 64 | 32–64–128 | 0.3 | 0.0005 | Evet | %74 | Veri artırımı iyileştirdi |
| 3 | 64 | 64–128–256 | 0.4 | 0.0003 | Evet | %37.5 | Daha derin mimari overfit oldu |

---

## 📌 6. Çalıştırma Talimatları

```bash
git clone https://github.com/<kullanici>/CNN_siniflandirma
cd CNN_siniflandirma
pip install tensorflow matplotlib numpy
jupyter notebook
Ardından ilgili model .ipynb dosyasını çalıştırarak eğitimi başlatabilirsiniz.

📌 7. Sonuç ve Değerlendirme

Küçük veri setlerinde basit CNN (Model 2) en iyi performansı verdi.

Transfer learning modeli (VGG16) orta düzeyde başarı sağladı.

Model 3’te yapılan değişiklikler teoride faydalı olsa da veri setinin küçük olması sebebiyle aşırı öğrenmeye yol açtı.

En iyi model Model 2 olmuştur.