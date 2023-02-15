

# Recommendation Systems • Ranking

- Aday oluşturma işleminden sonra başka bir model, görüntülenecek öğe grubunu seçmek için oluşturulan adayları puanlar ve sıralar. Öneri sistemi, aşağıdakiler gibi farklı kaynakları kullanan birden fazla aday oluşturucuya sahip olabilir:
Örneğin,
- Kişiselleştirilmiş kullanıcı özellikleri.
- Coğrafi bilgiler
- Popüler veya trend olan ürünler.
- Sosyal grafik; yani arkadaşlar tarafından beğenilen veya önerilen öğeler.
Sistem farklı kaynakları, daha sonra tek bir model tarafından puanlanan ve bu puana göre sıralanan ortak bir aday havuzunda birleştirir.
Örneğin, sistem, bir kullanıcının YouTube'da video izleme olasılığını tahmin etmek için bir model eğitebilir:
- Sorgu özellikleri (örneğin, kullanıcı izleme geçmişi, dil, ülke, saat)
- Video özellikleri (örneğin, başlık, etiketler, video yerleştirme)
Sistem daha sonra aday havuzundaki videoları modelin öngörüsüne göre sıralayabilir.

## Tıklamaya Göre Verilirse Dezavantaj
Puanlama işlevi tıklamalar için optimize edilirse, sistemler clickbait videoları önerebilir. Bu puanlama işlevi, tıklamalar oluşturur ancak iyi bir kullanıcı deneyimi sağlamaz. Kullanıcıların ilgisi hızla kaybolabilir.
## İzlenme Süresine Göre Verilirse Dezavantaj
Puanlama işlevi izlenme süresi için optimize edilirse sistem çok uzun videolar önerebilir ve bu da kötü bir kullanıcı deneyimine yol açabilir. Birden fazla kısa süreli videonun, tek bir uzun süreli video kadar iyi olabileceğini unutmayın.
