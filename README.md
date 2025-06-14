 # 📧 E-Posta Phishing Tespit Sistemi (ML Destekli)

Bu proje, e-posta yoluyla gerçekleştirilen **phishing (kimlik avı)** saldırılarını tespit etmek için çeşitli makine öğrenmesi ve derin öğrenme algoritmaları kullanılarak geliştirilmiştir. Proje kapsamında, model Flask API olarak servis haline getirilmiş ve bir tarayıcı eklentisi ile gerçek zamanlı çalışabilecek duruma getirilmiştir.

## 🎯 Amaç

Siber güvenlik alanında yaygın olan phishing saldırılarına karşı, e-posta içeriğini analiz ederek gerçek zamanlı tehdit algılama yeteneği olan bir sistem geliştirmek.

## 🚀 Hedefler

- E-posta metinlerini işleyerek yapısal ve anlamsal özellikler çıkarmak.
- Birden fazla ML/DL modeliyle phishing tespiti yapmak ve karşılaştırmak.
- En iyi performans gösteren modeli bir Flask API ile sunmak.
- Bu API’yi bir tarayıcı eklentisine entegre ederek kullanıcıya gerçek zamanlı koruma sağlamak.

## 📁 Kullanılan Veri Setleri

Kaggle üzerindeki [Phishing Email Dataset](https://www.kaggle.com/datasets) içerisindeki:
- `Nazario.csv`: Phishing e-postaları (1565 adet)
- `Ceas.csv`: Normal e-postalar (17312 adet) (yalnızca `Label=0` olanlar)

## 🧹 Veri Ön İşleme

- HTML etiketleri, URL’ler ve e-posta adresleri temizlendi.
- Noktalama işaretleri ve özel karakterler kaldırıldı.
- Tüm metin küçük harfe dönüştürüldü.
- `sender`, `subject`, `body` alanları birleştirilerek `combined_text` oluşturuldu.

## 🧠 Özellik Mühendisliği

E-posta başına:
- **41 yapısal özellik** (uzunluk, büyük harf oranı, URL sayısı, keyword varlığı, urgency skoru vb.)
- **1500 TF-IDF özellik** (otomatik öğrenilen kelime/bigram temsilleri)

Toplamda: **1541 boyutlu vektör** her e-posta için oluşturulmuştur.

## 🧪 Kullanılan Algoritmalar

- **Logistic Regression** ✅ *(En iyi sonuç)*
- Random Forest, Gradient Boosting, LightGBM, XGBoost
- Naive Bayes
- Support Vector Machines (SVM)
- Deep Neural Network (DNN)

### 🧩 Dengeleme Stratejileri

- `SMOTE`: Azınlık sınıfı artırıldı
- `RandomUnderSampler`: Çoğunluk sınıfı azaltıldı
- `Class Weights`: Ceza oranı dengelemesi
- `BalancedRandomForest`: Model tabanlı dengeleme

## 📊 Model Performansı

- **Logistic Regression** modeli en iyi F1 skoruna (~0.98) ulaşmıştır.
- Diğer modellerle de karşılaştırmalı değerlendirme yapılmış, en uygun model Flask API arkasında kullanılmak üzere seçilmiştir.
- Değerlendirme metrikleri: `Accuracy`, `Precision`, `Recall`, `F1-Score`, `ROC AUC`, `Confusion Matrix`

## 🌐 Flask Arayüzü & Eklenti

- Flask tabanlı bir REST API geliştirildi.
- Ngrok ile dış dünyaya açılarak bir **tarayıcı eklentisine** entegre edildi.
- Kullanıcı bir e-postayı seçtiğinde sistem otomatik olarak analiz yapıyor.

## 💡 Öneriler ve Gelecek Çalışmalar

- Daha gerçekçi ve güncel veri setleriyle yeniden eğitim yapılmalı.
- BERT, GPT gibi büyük dil modelleri ile daha güçlü temsil öğrenimi sağlanabilir.
- Görsel phishing tespiti için **OCR sistemleri** entegre edilebilir.
- **Kullanıcı geri bildirimleri** ile dinamik öğrenme mekanizması kurulabilir.
- Hibrit yaklaşım: metin + URL + header analizi entegre sistemler önerilmektedir.

## 📚 Kaynaklar

- [Makale: Phishing Üzerine Analiz (DergiPark)](https://dergipark.org.tr/tr/download/article-file/1204603)
