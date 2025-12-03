# 📂 ABD Suç Verileri Analizi ve Çözülebilirlik Tahmini (US Crime Solvability Prediction)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn%20%7C%20Pandas-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

Bu proje, ABD'deki geçmiş suç verilerini (US Crime Dataset) analiz ederek, işlenen bir suçun kolluk kuvvetleri tarafından **aydınlatılma (çözülme) ihtimalini** makine öğrenmesi algoritmalarıyla tahmin etmeyi amaçlamaktadır.

## 🎯 Proje Amacı ve Problem Tanımı
Suç oranlarının yüksek olduğu bölgelerde kolluk kuvvetlerinin kaynaklarını (zaman, personel, bütçe) verimli kullanması kritiktir. Bu çalışma, **"Faili meçhul dosyalar ile çözülen dosyaları birbirinden ayıran temel faktörler (silah, bölge, mağdur profili vb.) nelerdir?"** sorusuna cevap arar.

Proje kapsamında, hedef değişken olan `Crime Solved` (Evet/Hayır) tahmini için 4 farklı model mimarisi geliştirilmiş ve kıyaslanmıştır.

## 📊 Veri Seti ve Ön İşleme
* **Veri Kaynağı:** ABD Federal Suç Raporları (FBI UCR Verileri).
* **Veri Boyutu:** ~638.000 Satır.
* **Sınıf Dengesi:** %70 Çözüldü (Majority) - %30 Çözülemedi (Minority).
* **Veri Sızıntısı Önleme (Leakage Prevention):** Modelin gerçekçi çalışması için, failin kimliği belli olduğunda dolu olan (`Perpetrator Age`, `Perpetrator Sex`, `Perpetrator Race`, `Relationship`) sütunlar eğitimden önce **tamamen çıkarılmıştır.**
* **Dengesizlik Yönetimi:** Tüm modellerde `class_weight='balanced'` stratejisi uygulanmıştır.

## 👥 Proje Ekibi ve Roller

Proje kapsamında 4 farklı temel model (Baseline) geliştirilmiş ve her üye belirli bir algoritma ailesine odaklanmıştır:

| Geliştirici | Model | Özellik Seçimi (Feature Selection) | Açıklama |
| :--- | :--- | :--- | :--- |
| **Baran Karakuş** | Logistic Regression | Korelasyon Matrisi | Değişkenler arası doğrusal ilişkileri test eden temel (baseline) model. |
| **Yiğit Kutluğ** | Gaussian Naive Bayes | Mutual Information | Olasılık tabanlı ve özelliklerin bağımsız olduğu varsayımıyla çalışan model. |
| **Enes B. Salman** | Decision Tree | Chi-Square (Ki-Kare) | Karar kurallarını görselleştiren ve doğrusal olmayan ilişkileri yakalayan model. |
| **Kerem Oğuz** | **Random Forest** | **Lasso (L1 Regularization)** | Topluluk (Ensemble) öğrenme ile varyansı düşüren ve en yüksek başarıyı veren model. |

## 🏆 Sonuçlar (Model Performansı)

Modeller, dengesiz veri seti göz önüne alınarak **Accuracy (Doğruluk)** ve **ROC AUC (Ayırt Edicilik)** metriklerine göre değerlendirilmiştir.

| Model | Accuracy | ROC AUC | Sonuç |
| :--- | :--- | :--- | :--- |
| **Random Forest (Kerem Oğuz)** | **0.7323** | **0.7270** | 🏆 **Şampiyon Model** |
| Decision Tree (Enes B. Salman) | 0.6121 | 0.6694 | Orta Seviye |
| Naive Bayes (Yiğit Kutluğ) | 0.5805 | 0.6074 | Geliştirilmeli |
| Logistic Regression (Baran Karakuş)| 0.5532 | 0.6096 | Baseline |

> **Bulgu:** Kerem Oğuz tarafından geliştirilen **Random Forest** modeli, **Lasso** ile yapılan hibrit özellik seçimi sayesinde karmaşıklığı azaltmış ve Baseline modele göre yaklaşık **18 puanlık** bir artış sağlamıştır.
