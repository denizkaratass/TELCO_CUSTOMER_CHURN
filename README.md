# Telco Customer Churn – Analysis & Feature Engineering

Telco Customer Churn veri seti üzerinde keşifçi veri analizi (EDA), veri ön işleme, feature engineering ve modelleme çalışması.

Amaç, müşterilerin şirketten ayrılıp ayrılmayacağını (`Churn`) tahmin eden modeller kurmak ve feature engineering adımlarının model performansına katkısını değerlendirmektir.

> Bu proje, Miuul eğitim programında verilen "Telco Churn Feature Engineering" vaka çalışması üzerine tarafımdan hazırlanmıştır. Veri analizi, oluşturulan yeni değişkenler, modelleme ve tüm yorumlar bana aittir.

## Veri Seti

- **Kaynak:** [IBM Telco Customer Churn (Kaggle)](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- 7043 gözlem, 21 değişken
- Hedef değişken: `Churn` (Yes / No) — yaklaşık %26.5 churn oranı

## Proje Adımları

1. Veri yükleme
2. Genel bakış ve `TotalCharges` veri tipi düzeltmesi (`tenure = 0` olan 11 müşteri)
3. Değişken türlerinin belirlenmesi
4. Kategorik ve numerik değişken analizi
5. Hedef değişken analizi
6. Aykırı değer analizi (IQR)
7. Eksik değer analizi
8. Korelasyon analizi
9. Baseline modeller (feature engineering öncesi)
10. Feature engineering
11. Encoding (Label Encoding, One-Hot Encoding)
12. Standardization
13. Modelleme ve karşılaştırma
14. Genel değerlendirme

## Oluşturulan Yeni Değişkenler

| Değişken | Açıklama |
|---|---|
| `NEW_Monthly_Echeck` | Month-to-month sözleşme + Electronic check ödeme |
| `NEW_Fiber_NoSupport` | Fiber optic internet + TechSupport yok |
| `NEW_TenureGroup` | Müşteri süresi grupları (0-12, 13-24, 25-48, 49-72 ay) |
| `NEW_InternetAddonCount` | Kullanılan ek internet hizmeti sayısı |
| `NEW_AutoPayment` | Otomatik ödeme kullanımı |

## Sonuçlar (Feature Engineering Sonrası, Test Seti)

| Model | Accuracy | Churn Recall | Churn F1 |
|---|---|---|---|
| Logistic Regression | 0.80 | 0.52 | 0.58 |
| Random Forest | 0.78 | 0.49 | 0.54 |
| Gradient Boosting | 0.80 | 0.52 | 0.58 |
| CatBoost | 0.80 | 0.54 | 0.59 |
| Balanced Logistic Regression | 0.73 | 0.79 | 0.61 |

- Feature engineering, model performansında belirgin bir artış sağlamamıştır; yeni değişkenler büyük ölçüde mevcut bilgiyi yeniden temsil etmektedir, ancak churn davranışının yorumlanmasına katkı sağlamıştır.
- Genel doğruluk önceliklendirildiğinde standart modeller, churn müşterilerinin mümkün olduğunca fazla yakalanması hedeflendiğinde ise yüksek recall sağlayan **Balanced Logistic Regression** tercih edilebilir.

## Dosyalar

- `telco_churn_feature_engineering.ipynb` – Analiz ve modelleme notebook'u
- `Telco-Customer-Churn.csv` – Veri seti
- `requirements.txt` – Gerekli Python paketleri

## Çalıştırma

```bash
pip install -r requirements.txt
jupyter notebook telco_churn_feature_engineering.ipynb
```
