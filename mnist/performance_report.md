## 1. Kullanılabilecek Ölçütler

Eğitim veya test performansını değerlendirirken genellikle şu metrikler kullanılır:
| Ölçüt                       | Açıklama                                               | Kullanım Amacı                                        |
| --------------------------- | ------------------------------------------------------ | ----------------------------------------------------- |
| **Accuracy (Doğruluk)**     | Doğru tahmin edilen örneklerin toplam örneğe oranı     | En temel ölçüt. Dengeli veri kümelerinde uygundur.    |
| **Precision (Kesinlik)**    | Pozitif tahminlerin gerçekten pozitif olma oranı       | Yanlış pozitifleri azaltmak istediğimizde önemlidir.  |
| **Recall (Duyarlılık)**     | Gerçek pozitiflerin ne kadarının doğru tahmin edildiği | Kaçırılan örnekleri azaltmak istediğimizde önemlidir. |
| **F1-Score**                | Precision ve Recall’un harmonik ortalaması             | Dengesiz verilerde dengeli bir ölçü sağlar.           |
| **Error Rate (Hata Oranı)** | 1 - Accuracy                                           | Hata üzerinden ifade etmek istiyorsak.                |


## 2. Bu Görev İçin En Uygun Ölçüt

Bu bir sınıflandırma problemi (10 sınıf: 0–9) olduğundan,
ve MNIST gibi dengeli bir veri kümesi üzerinde eğitildiği için,
en anlamlı ölçüt genellikle “doğruluk (accuracy)” olur.

Ancak bizim ek testlerimiz artık modelin görmediği farklı bir veri dağılımını (senin el yazın) temsil ediyor.
Yani burada asıl önemli olan:

🔸 Modelin genelleme kabiliyeti
🔸 Farklı stil ve yazım biçimlerini doğru tanıma başarısı

Bu durumda tek başına doğruluk yanıltıcı olabilir.
Dolayısıyla F1 skoru burada daha uygun bir ölçüttür çünkü:

Her sınıfın (0–9) tahmin başarısını dengeli biçimde yansıtır,

Hem yanlış pozitifleri (örneğin 3’ü 8 sanma) hem de yanlış negatifleri (örneğin 8’i hiç bulamama) dikkate alır.

## 3. Neden F1 Skoru?

Bizim sonuçlarına bakalım:

| Gerçek | Tahmin | Olasılık |
| ------ | ------ | -------- |
| 4      | 8      | 96.2%    |
| 3      | 7      | 78.8%    |
| 9      | 3      | 77.6%    |
| 2      | 2      | 99.4%    |
| 7      | 1      | 46.8%    |


Doğruluk oranı = 1 / 5 = %20
Ancak model bazı hatalı tahminlerinde yüksek güvenle yanlış söylüyor (%96 gibi).
Bu, modelin overfitting yaptığını (MNIST verisini ezberlediğini) gösterir.

F1 skoru ise bu tür durumlarda, yanlış tahminleri (özellikle karıştırılan rakamları) daha ağır cezalandırdığı için daha gerçekçi bir performans ölçütü sunar.

## 4. Özet Sonuç
| Durum                                        | En uygun ölçüt                        | Neden                                                                        |
| -------------------------------------------- | ------------------------------------- | ---------------------------------------------------------------------------- |
| **MNIST test verisinde**                     | **Accuracy (Doğruluk)**               | Veri dengeli, sınıflar eşit sayıda.                                          |
| **El yazımda (gerçek dünya testinde)**       | **F1 Skoru veya Ortalama Hata Oranı** | Model farklı dağılımda genelleyemiyor, F1 sınıflar arası dengeyi gösteriyor. |
## Confusion Matrix
<img width="575" height="470" alt="matrix" src="https://github.com/user-attachments/assets/10fce95f-f16b-4216-a265-d57b2310afe2" />

Sınıf Bazlı Değerler:

                   precision    recall  f1-score   support

    1                 0.000     0.000     0.000       0
    2                 1.000     1.000     1.000       1
    3                 0.000     0.000     0.000       1
    4                 0.000     0.000     0.000       1
    7                 0.000     0.000     0.000       1
    8                 0.000     0.000     0.000       0
    9                 0.000     0.000     0.000       1

    accuracy                              0.200       5
    macro avg         0.143     0.143     0.143       5
    weighted avg      0.200     0.200     0.200       5
