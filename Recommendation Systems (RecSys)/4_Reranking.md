# Recommendation Systems • Re-ranking

Bir öneri sisteminin son aşamasında, sistem adayları ek kriterler veya kısıtlamalar göz önünde bulundurarak yeniden sıralayabiliriz. Yeniden sıralama yaklaşımlarından biri, bazı adayları kaldıran filtreler kullanmaktır.
Örneğin, aşağıdakileri yaparak bir video tavsiye aracında yeniden sıralama uygulayabilirsiniz:
1. Bir videonun tıklama tuzağı olup olmadığını algılayan ayrı bir model eğitimi.
2. Bu modeli aday listesinde çalıştırmak.
3. Modelin tıklama tuzağı olarak sınıflandırdığı videoları kaldırma.

Başka bir yeniden sıralama yaklaşımı, sıralayıcı tarafından döndürülen puanı manuel olarak dönüştürmektir.
Örneğin sistem, puanı aşağıdakilerin bir fonksiyonu olarak değiştirerek videoları yeniden sıralar:
1. video yenilik durumu (belki daha yeni içeriği tanıtmak için)
2. video uzunluğu

Bu bölüm kısaca freshness, diversity ve faireness'ı tartışır. Bu faktörler, öneri sisteminizi geliştirmenize yardımcı olabilecek pek çok faktör arasındadır. Bu faktörlerin bazıları genellikle sürecin farklı aşamalarını değiştirmeyi gerektirir. Her bölüm, bireysel veya toplu olarak uygulayabileceğiniz çözümler sunar.
## Freshness-Yeni Olma-Tazelik
Çoğu öneri sistemi, mevcut kullanıcı geçmişi ve en yeni öğeler gibi en son kullanım bilgilerini dahil etmeyi amaçlar. Modeli taze tutmak, modelin iyi önerilerde bulunmasına yardımcı olur.
### Çözüm
En son eğitim verilerini öğrenmek için eğitimi mümkün olduğunca sık tekrar edin. Modelin sıfırdan yeniden öğrenmek zorunda kalmaması için eğitime sıcak bir şekilde başlamanızı öneririz. Mevcutta olanlardan başlatma, eğitim süresini önemli ölçüde azaltabilir. Örneğin, matris çarpanlarına ayırmada, modelin önceki örneğinde bulunan öğeler için embeddingleri Mevcutta olanlardan
başlatın.
Matris çarpanlara ayırma modellerinde yeni kullanıcıları temsil etmek için "ortalama" bir kullanıcı oluşturun. Her kullanıcı için aynı yerleştirmeye ihtiyacınız yoktur; kullanıcı özelliklerine göre kullanıcı kümeleri oluşturabilirsiniz.

Softmax modeli veya iki kule modeli gibi bir DNN kullanın. Model, özellik vektörlerini girdi olarak aldığından, eğitim sırasında görülmeyen bir sorgu veya öğe üzerinde çalıştırılabilir.

Bir özellik olarak belge yaşı ekleyin. Örneğin, YouTube bir videonun yaşını veya son görüntülenme zamanını bir özellik olarak ekleyebilir. 
## Diversity Çeşitlilik
Sistem her zaman sorgu yerleştirmeye "en yakın" öğeleri önerirse, adaylar birbirine çok benzer olma eğilimindedir. Bu çeşitlilik eksikliği, kötü veya sıkıcı bir kullanıcı deneyimine neden olabilir. Örneğin, YouTube, kullanıcının izlemekte olduğu videoya çok benzer videolar önerirse, örneğin yalnızca baykuş videoları (resimde gösterildiği gibi), kullanıcı büyük olasılıkla ilgisini hızla kaybedecektir.
### Çözüm
Farklı kaynaklar kullanarak birden çok aday oluşturucuyu eğitin.
Farklı amaç fonksiyonlarını kullanarak birden fazla ranker eğitin.
Çeşitliliği sağlamak için öğeleri türe veya diğer meta verilere göre yeniden sıralayın.
## Fairness - Adalet
Modeliniz tüm kullanıcılara adil davranmalıdır. Bu nedenle, modelinizin eğitim verilerinden bilinçsiz önyargıları öğrenmediğinden emin olun.
### Çözüm
Tasarım ve geliştirmeye farklı bakış açılarını dahil edin.
Makine öğrenimi modellerini kapsamlı veri kümelerinde eğitin. Verileriniz çok seyrek olduğunda (örneğin, belirli kategoriler yeterince temsil edilmediğinde) yardımcı verileri ekleyin.
Önyargıları izlemek için her demografideki metrikleri (örneğin, doğruluk ve mutlak hata) izleyin.
Yetersiz hizmet alan gruplar için ayrı modeller oluşturun.

