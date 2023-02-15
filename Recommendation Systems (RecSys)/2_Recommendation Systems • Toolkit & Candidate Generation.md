
## Recommendation Systems • Toolkit
### Embedding Space
- Embedding alanı, içine yüksek boyutlu vektörleri çevirebileceğiniz düşük boyutlu bir alandır. Yerleştirmeler, kelimeleri temsil eden seyrek vektörler gibi büyük girdilerde makine öğrenimi yapmayı kolaylaştırır.
Embedding, bir varlık için vektör gösterimleridir. Embedding aracılığıyla herhangi bir ayrık varlığı sürekli bir alana temsil edebilirsiniz. Vektördeki her öğe, o varlık için bir özelliği veya özelliklerin bir kombinasyonunu temsil eder.
- Örneğin, filmleri ve kullanıcı kimliklerini embedding olarak gösterebilirsiniz. Basit olması için, bu embeddingler aşağıdaki şemada gösterildiği gibi iki boyutlu vektör olduğunu varsayalım. 
Amaç, kullanıcıları ve filmleri benzer bir embedding alanına getirmek, böylece en yakın komşuya dayalı öneriyi uygulayabiliriz.
- Aşağıdaki şekil, user_1'in alanında movie_1 ve movie_2'ye movie_3'ten daha yakın olduğu varsayımsal bir örneği göstermektedir. Bu nedenle user_1'e movie_1 ve movie_2'yi önereceğiz.
- Embedding, anlamsal olarak benzer girdileri embedding alanında birbirine yakın yerleştirerek girdinin bazı anlamlarını yakalar. Embedding öğrenilebilir ve modeller arasında yeniden kullanılabilir.
Aynı kullanıcı tarafından izlenen benzer öğeler (videolar, filmler), Embedding alanında birbirine daha yakın hale gelir. Burada yakın benzerlik ölçüsü anlamına gelir.
![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*8NXH77Ylw5z5xfnU9fcmKg.png)

### Similarity Measure
Benzerlik ölçüsü, bir çift embedding alan ve bunların benzerlik ölçüsünü temsil eden bir skaler değer döndüren bir işlevdir.
* Örneğin
-- Cosine Similarity
-- Euclidean Distance
-- Dot Product
-- Alternating Least Squares
-- Matrix Factorization
-- Mean Normalization

## Recommendation Systems • Candidate Generation

### Content-based Filtering
- İçerik tabanlı filtreleme, kullanıcının beğendiklerine benzer diğer belgeleri önermek için belgeleri kullandığımız tiptir.
- Model, diğer kullanıcılarla ilgili verilere ihtiyaç duymaz, yalnızca mevcut kullanıcı için bilgiye ihtiyaç duyar. Ölçeklendirmeyi kolaylaştırır.
- Her kullanıcıya niş öğeler, diğer kullanıcıların ilgilenmeyebileceği öğeler önerebilir.
- Özellikler elle tasarlandığından çok fazla alan bilgisi gerektirir. Bu nedenle, model yalnızca elle tasarlanmış özellikler kadar iyidir.
- Model, yalnızca kullanıcının mevcut ilgi alanlarına göre önerilerde bulunur ve ilgi alanlarını genişletemez.

-- Örnek:
![](https://aman.ai/recsys/assets/recsys/17.jpg)

Film önermek için sinir ağlarını kullanarak yalnızca içerik tabanlı bir filtreleme sistemi ile oluşturulacak sistem aşağıdaki gibi olacaktır.

![](https://aman.ai/recsys/assets/recsys/23.jpg)

### Collaborative Filtering

İçerik tabanlı filtrelemenin bazı sınırlamalarını gidermek için işbirlikçi filtreleme, öneriler sağlamak için kullanıcılar ve öğeler arasındaki benzerlikleri eş zamanlı olarak kullanır. 
Böylece aslında tesadüfi tavsiyelere izin verir; yani işbirlikçi filtreleme modelleri A kullanıcısına B kullanıcısının ilgi alanına göre benzer tavsiye üretebilir.

İçerik tabanlı filtrelemenin aksine işbirlikçi filtreleme, elle tasarlanmış özelliklere güvenmeden embeddingleri otomatik olarak öğrenebilir.

İşbirliğine dayalı bir filtreleme öneri sisteminin amacı, iki vektör oluşturmaktır:
1) Kullanıcının zevklerini somutlaştıran her kullanıcı için bir "parametre vektörü".

2) vektörün iç çarpımı artı yanlılık terimi, kullanıcının o filme verebileceği derecelendirmenin bir tahminini üretmelidir.

- Alan bilgisi gerekmez: Embeddingler otomatik olarak öğrenildiği için önceden alan bilgisine sahip olmamıza gerek yoktur.
Serendipity: Model, kullanıcıların yeni ilgi alanları keşfetmesine yardımcı olabilir. Tek başına, makine öğrenimi sistemi kullanıcının belirli bir öğeyle ilgilendiğini bilmeyebilir, ancak benzer kullanıcılar o öğeyle ilgilendiğinden model yine de bunu önerebilir.
Harika bir başlangıç noktası: Sistem, bir matris çarpanlara ayırma modelini eğitmek için bir dereceye kadar yalnızca geri bildirim matrisine ihtiyaç duyar. Özellikle, sistemin bağlamsal özelliklere ihtiyacı yoktur. Pratikte bu, çoklu aday oluşturuculardan biri olarak kullanılabilir.

### 1D Embedding

Her filme, filmin çocuklar için mi (negatif değerler) yoksa yetişkinler için mi (pozitif değerler) olduğunu açıklayan [-1, 1] içinde bir skaler atadığımızı varsayalım. Ayrıca [-1, 1]'deki her kullanıcıya, kullanıcının çocuk filmlerine (-1'e yakın) veya yetişkin filmlerine (+1'e yakın) olan ilgisini açıklayan bir skaler atadığımızı varsayalım.

![](https://aman.ai/recsys/assets/recsys/1D.svg)

Aşağıdaki şemada her bir onay işareti, belirli bir kullanıcının izlediği bir filmi tanımlar. Üçüncü ve dördüncü kullanıcıların bu özellikle çok iyi açıklanan tercihleri vardır; üçüncü kullanıcı filmleri çocuklar için ve dördüncü kullanıcı filmleri yetişkinler için tercih eder. Ancak, birinci ve ikinci kullanıcıların tercihleri bu tek özellikle iyi açıklanmamaktadır.

![](https://aman.ai/recsys/assets/recsys/1Dmatrix.svg)

### 2D Embedding

Tüm kullanıcıların tercihlerini açıklamak için bir özellik yeterli değildi. Bu sorunun üstesinden gelmek için ikinci bir özellik ekleyelim: her filmin gişe rekorları kıran veya sanat filmi olma derecesi. İkinci bir özellikle, artık her filmi aşağıdaki iki boyutlu embedding ile temsil edebiliriz:
![](https://aman.ai/recsys/assets/recsys/2D.svg)

Geri bildirim matrisini en iyi şekilde açıklamak için kullanıcılarımızı tekrar aynı embedding alanına yerleştiriyoruz: her biri için (kullanıcı,öğe)  çifti olarak, kullanıcı filmi izlediğinde katıştıran kullanıcı ile öğe katıştıran nokta çarpımının 1'e, aksi takdirde 0'a yakın olmasını istiyoruz.

![](https://aman.ai/recsys/assets/recsys/2Dmatrix.svg)

- Gerçek dünyadan bir örnek olarak, etkileşimi (favorileri, beğenileri ve tıklamaları kullanarak) gösteren ikili etiketlere sahip bir örneğe bakalım:
![](https://aman.ai/recsys/assets/recsys/12.jpg)

Yukarıdaki veri kümesindeki her derecelendirmenin anlamı hakkında konuşalım. Etiketlerimizin her birinin ne anlama geldiğini seçebiliriz, bu nedenle burada aşağıdakileri seçtik:
1: öğe gösterildikten sonra kullanıcı etkileşimde bulundu.
0: kullanıcı öğeyi gösterdikten sonra etkileşimde bulunmadı.
?: öğe henüz kullanıcıya gösterilmemiştir.





