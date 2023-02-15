# Recommendation Systems (RecSys)
## Giriş
RecSys, gıda dağıtımından satışa kadar, modellerden gelen önerilerle yönlendirilen endüstrilerin ayrılmaz bir parçasıdır. Yalnızca işletmelerin büyümesine yardımcı olmakla kalmaz, aynı zamanda bireylerin daha önce karşılaşmamış olabilecekleri hoşlarına giden şeyleri keşfetmelerine de yardımcı olurlar.

- Aşağıdaki şekil; pilot müşteri A/B denemelerinden elde edilen sonuçları, önceki öneri sistemlerine kıyasla iş ölçümlerindeki (gelir, dönüşümler, tıklama oranı vb.) iyileştirmeleri göstermektedir.
![](https://storage.googleapis.com/gweb-cloudblog-publish/images/F2-results.max-1000x1000.png)

- Öneriler, kullanıcıların historical verilerine dayalı olarak veya benzer kullanıcı tercihlerine bakarak bir kullanıcı tercihini tahminleyen makine öğrenimi modelleridir.
- Örnek bir öneri sistemi modeli için ortak bir mimari aşağıda verilmiştir.
![](https://developers.google.com/machine-learning/recommendation/images/Process.svg?hl=tr)
### Candidate Generation (Aday Oluşturma)
Bu ilk aşamada, sistem muhtemelen devasa bir topluluktan başlar ve çok daha küçük bir aday alt kümesi oluşturur. Örneğin, YouTube'daki aday oluşturucu, milyarlarca videoyu yüzlerce veya binlerce videoya indirir. Maketin muazzam boyutuna göre modelin sorguları hızlı bir şekilde değerlendirmesi gerekir. Belirli bir modelde, her biri farklı bir aday alt kümesini temsil eden birden fazla aday oluşturucu oluşturulabilir.
- Örneğin, Netflix'te binlerce film var, ancak ana sayfanızda size hangilerini göstereceğini seçmesi gerekiyor!
- Modelin, sorguları büyük bir corpus üzerinde yüksek bir hızda değerlendirmesi gerekir ve bir modelin, her biri farklı aday alt kümelere sahip birden çok aday oluşturucu sağlayabileceğini akılda tutması gerekir.
### Scoring (Puanlama)
Daha sonra başka bir model, kullanıcıya gösterilecek öğe grubunu (10'luk sırayla) seçmek için adayları puanlar ve sıralar. Bu model, öğelerin nispeten küçük bir alt kümesini değerlendirdiğinden, sistem ek sorgulara dayanarak daha kesin bir model kullanabilir.
- Burada model daha küçük bir belge alt kümesi üzerinde çalışır, bu nedenle sıralama açısından daha yüksek precision hedefleyebiliriz.
### Re-Ranking (Yeniden sıralama)
Son olarak, sistem son sıralama için ek kısıtlamaları göz önünde bulundurmalıdır. Örneğin, sistem kullanıcının açık bir şekilde beğenmediği öğeleri kaldırır veya daha yeni içerik puanını artırır. Yeniden sıralama, çeşitlilik, yenilik ve adalet sağlamaya da yardımcı olabilir.
- Örneğin, kullanıcı bazı filmleri açıkça beğenmezse, Netflix'in bunları ana sayfanın dışına taşıması gerekecektir.

*Birçok büyük ölçekli öneri sistemi iki adımda uygulanır: Retrieval ve Ranking(Sıralama).*
#### Retrieval
![](https://aman.ai/recsys/assets/recsys/20.png)
Daha fazla öğenin alınması daha iyi sonuçlar verir ancak öneriler için hesaplamaları yavaşlatır.
Ek öğeler almanın daha alakalı önerilerle sonuçlanıp sonuçlanmadığını görmek için deneyler yapmalıyız.
#### Ranking

Ranking, kullanıcılara sıralı bir öğe listesi sağlamayı amaçlayan tavsiye sistemlerinde temel bir görevdir.
Her bir öğe için bir sıralama puanı üreten genel performansı optimize etmek için etiketli veri kümesinden bir sıralama işlevi öğrenilir.
Bir sıralama algoritması tarafından verilen sıralı listenin kalitesi, tavsiye sistemlerinin gelirinin yanı sıra kullanıcı memnuniyeti üzerinde de büyük etkiye sahiptir.
![](https://aman.ai/recsys/assets/recsys/21.png)
