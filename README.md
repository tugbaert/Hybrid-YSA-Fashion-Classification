# Multimodal (Görüntü + Metin) E-Ticaret Ürün Sınıflandırması 🚀

[![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/tugbaert/Hybrid-YSA-Fashion-Classification/blob/main/hibrit_ysa_model_gelistirme.ipynb)

Bu proje, e-ticaret platformlarındaki ürünleri sadece görsellerine veya sadece isimlerine bakarak değil, **her iki veri tipini aynı anda (Multimodal) işleyerek** doğru ana kategoriye atayan bir Yapay Sinir Ağı (YSA) projesidir.

## 📌 Proje Özeti
Sınıflandırma problemlerinde tek bir veri tipi bazen yetersiz kalabilir. Örneğin, beyaz bir tişört ile beyaz bir havlu sadece görsel olarak analiz edildiğinde karışabilir. Veya "Free Items" (Bedava Ürün) gibi promosyonel metin etiketleri, ürünün fiziksel gerçekliğini gizleyebilir. Bu projede, bu tarz zorlukları aşmak için Geç Özellik Birleştirme (Late Feature Fusion) stratejisi kullanılmıştır.

* **Veri Seti:** Kaggle - [Fashion Product Images (Small)](https://www.kaggle.com/datasets/paramaggarwal/fashion-product-images-small)
* **Modaliteler:** 128x128x3 RGB Görüntü + Maksimum 10 kelimelik Ürün İsmi
* **Sınıf Sayısı:** 6 Ana Kategori (Apparel, Accessories, Footwear, Personal Care, Free Items, Sporting Goods)

## 🧠 Mimari Yaklaşım ve Modeller
Kontrollü bir deney ortamı yaratmak için projede 4 farklı aşamadan geçilmiştir:

1. **Baseline Model (Sadece Görüntü):** Tek katmanlı basit 2D Evrişim (CNN).
2. **Model-1 (Sadece Metin):** Çift yönlü ardışık anlamsal analiz yapan BiLSTM ağı.
3. **Model-2 (Sadece Görüntü):** Transfer Learning kullanılarak ImageNet ağırlıklarıyla dondurulmuş MobileNetV2.
4. **Hibrit Model (Görüntü + Metin):** MobileNetV2'den gelen 64 boyutlu uzamsal vektör ile BiLSTM'den gelen 64 boyutlu anlamsal vektörün uç uca eklendiği (Concatenate) çok girişli (Multi-Input) yapı.

## 📊 Karşılaştırmalı Sonuçlar
Projede sınıf dengesizliği bulunduğu için ana metrik olarak **Macro F1-Score** kullanılmıştır.

| Model Türü | Kullanılan Veri | Test Accuracy | Test Macro F1 |
| :--- | :--- | :--- | :--- |
| Baseline (CNN) | Sadece Görüntü | % 95.40 | % 62.03 |
| Model-1 (BiLSTM) | Sadece Metin | % 99.47 | % 66.28 |
| Model-2 (MobileNetV2)| Sadece Görüntü | % 98.20 | % 64.97 |
| **Hibrit Model** | **Görüntü + Metin** | **% 99.20** | **% 65.96** |

## 🔍 Hata Analizi ve Modelin Gücü
Model test setinde 1500 örnekten 1489'unu doğru bilerek %99 doğruluğa ulaşmıştır. Ancak hibrit yapının asıl gücü yapılan Hata Analizinde ortaya çıkmıştır:
Veri setinde "Free Items" (Bedava Ürünler) olarak hatalı veya ticari amaçla etiketlenmiş sırt çantası ve ruj gibi ürünler, hibrit model tarafından fiziksel gerçekliğe uygun biçimde "Aksesuar" ve "Kişisel Bakım" olarak düzeltilmiştir. Model örüntüleri ezberlememiş, etiket gürültüsünü aşabilen bir genelleme kapasitesine ulaşmıştır.

## 🛠️ Kullanılan Teknolojiler
* Python, TensorFlow, Keras Functional API
* Pandas, NumPy, Scikit-Learn
* Matplotlib, Seaborn

## 👨‍💻 Geliştiriciler
* **Tuğba Ertengi**
* **Hatice Kübra Ünal**
* **Sümeyye İkiz**
* **Fatma Merve Kılıçarslan**
