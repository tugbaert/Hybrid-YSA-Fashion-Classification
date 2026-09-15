# Multimodal (Görüntü + Metin) E-Ticaret Ürün Sınıflandırması 🚀

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tugbaert/Hybrid-YSA-Fashion-Classification/blob/main/hibrit_ysa_model_gelistirme.ipynb)

Bu proje, e-ticaret platformlarındaki ürünleri sadece görsellerine veya sadece isimlerine bakarak değil, **her iki veri tipini aynı anda (Multimodal) işleyerek** ana kategoriye atayan bir Yapay Sinir Ağı (YSA) projesidir.

## 📌 Proje Özeti
Sınıflandırma problemlerinde tek bir veri tipi bazen yetersiz kalabilir. Bu projede; görsel verilerin (CNN/MobileNetV2) ve metin verilerinin (BiLSTM) birbirinin zayıflıklarını örtmesi amacıyla Geç Özellik Birleştirme (Late Feature Fusion) stratejisi ile çok girişli (multi-input) gerçek bir hibrit yapı tasarlanmıştır.

## 📊 Karşılaştırmalı Sonuçlar
*Not: Sınıf dengesizliği nedeniyle temel metrik olarak Macro F1-Score kullanılmıştır. Test ve Validation metrikleri net olarak ayrıştırılmıştır.*

| Model Türü | Veri Tipi | Val Accuracy | Test Accuracy | Val Macro F1 | Test Macro F1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Baseline (CNN) | Sadece Görüntü | % 93.73 | % 95.40 | % 60.15 | % 62.03 |
| **Model-1 (BiLSTM)** | **Sadece Metin** | % 98.90 | **% 99.47** | % 65.80 | **% 66.28** |
| Model-2 (MobileNetV2)| Sadece Görüntü | % 97.50 | % 98.20 | % 63.45 | % 64.97 |
| Hibrit Model (Var.3) | Görüntü + Metin | **% 99.10** | % 99.20 | % 64.90 | % 65.96 |

## 🎯 Mimari Tercih Savunması: Neden Hibrit Model?
Tabloda görüldüğü üzere, salt metin işleyen **BiLSTM modeli (%66.28)**, sayısal Macro F1 skorunda Hibrit modeli (%65.96) geçmiştir. Bu durum, e-ticaret verilerinde ürün isimlerinin çok güçlü bir ayırt edici olduğunu göstermektedir. 

Ancak nihai mimari olarak **Çok Girişli Hibrit Model** savunulmaktadır. Bunun nedeni sayısal liderlik değil, **kavramsal esneklik ve sınır durum (edge-case) yönetimidir.** Hata analizinde kanıtlandığı üzere hibrit model; "Free Items" (Bedava Ürün) olarak etiketlenmiş çanta ve ruj gibi ürünlerde metin etiketindeki ticari gürültüyü aşarak, görsel verinin yardımıyla fiziksel gerçekliğe uygun (Aksesuar ve Kişisel Bakım) kararlar verebilmektedir. 

## ⚠️ Sınırlılıklar ve Sıfır Başarı Vakası
Bu projedeki mimari başarı, veri setinin yapısal problemleri nedeniyle belirli sınırlara takılmıştır:
1. **Azınlık Sınıflarında Çöküş:** Sınıflar arası şiddetli dengesizlik nedeniyle model, "Free Items" ve "Sporting Goods" gibi ekstrem azınlık sınıflarında tamamen başarısız olmuş ve bu sınıflar için **F1 = 0.00** skoru üretmiştir.
2. **Veri Çoğaltma (Augmentation) Eksikliği:** Eğitim sürecinde sistematik bir Data Augmentation veya sentetik veri üretme tekniği uygulanmamıştır. Model sadece ham verinin mevcut dağılımı üzerinden eğitilmiştir.

## 🛠️ Kullanılan Teknolojiler
* Python, TensorFlow, Keras Functional API
* Pandas, NumPy, Scikit-Learn
* Matplotlib, Seaborn

## 👨‍💻 Geliştiriciler
* **Tuğba Ertengi**
* **Hatice Kübra Ünal**
* **Sümeyye İkiz**
* **Fatma Merve Kılıçarslan**
