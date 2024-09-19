Projemde animelere ait bazı  özellikleri içeren bi veri seti kullandım. Veri setini https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database 
adresinden aldım.(anime.csv ve rating.csv dosyaları veri setinin dosyalarıdır)

Bu veri seti, 73.516 kullanıcı tarafından 12.294 farklı animeye verilen derecelendirme ve tercih verilerini içermektedir. 
Her kullanıcı izlediği animeleri tamamladığında, animeye puan vererek değerlendirme yapabilmektedir.Veri seti, bu kullanıcı puanlamalarının derlenmiş halidir.
Her anime için benzersiz bir kimlik numarası (anime_id), adı, türü (genre), formatı (TV, film, OVA vb.), bölüm sayısı, kullanıcıların ortalama puanı 
ve animeyi izleyen topluluk üyelerinin sayısı gibi bilgileri içerir. Bu veri seti, anime izleme eğilimleri ve popülerliği hakkında detaylı analiz yapma olanağı sağlar.

Projede, veri setini çeşitli ön işleme adımlarına tabi tutarak analiz ettim ve belirli kriterlere göre grafikler oluşturdum. 
Ayrıca, animeleri puanlarına göre 3 gruba ayıran bir model geliştirdim ve modelin performansını değerlendirdim.

Gözetimli öğrenme için Lojistik Regrosyon kullanarak animeleri ratinglerine göre sınıflandıralım. Sınıflandırma için 3 tür grup kullandık. Rating'i 0 ile 6.5 arasında olan animeler "LOW" sütünuna 6.5 ile 7.5 arasında olanlar "MEDİUM" sütünuna 7.5 ile 10 arasında olanlar "HİGH" sütünuna girecek şekilde bi model oluşturdum.
Çıkan sonuçlar:

  1. classification_report Analizi:

     High:
     Precision: 0.71 (Yüksek dereceli tahminlerinizin %71'i doğru. Ancak, tahminlerinizin %29'u yanlış olabilir.)
     Recall: 0.31 (Gerçek yüksek dereceli animelerin %31'i doğru tahmin ediliyor. Yani, yüksek dereceli animelerin %69'u kaçırılıyor.)
     F1-score: 0.43 (Precision ve recall'ün dengeli bir ortalaması. Bu sınıf için performans hala düşük, ama önceki sonuçlardan biraz iyileşme var.)
     
    Low:
    Precision: 0.67 (Düşük dereceli tahminlerinizin %67'si doğru.)
    Recall: 0.90 (Gerçek düşük dereceli animelerin %90'ı doğru tahmin ediliyor. Bu, düşük dereceli animelerin çoğunu doğru tahmin edebildiğinizi gösterir.)
    F1-score: 0.77 (Düşük dereceli animeler için dengeli bir performans.)
    
    Medium:
    Precision: 0.58 (Orta dereceli tahminlerinizin %58'i doğru.)
    Recall: 0.46 (Gerçek orta dereceli animelerin %46'sı doğru tahmin ediliyor.)
    F1-score: 0.52 (Orta dereceli animeler için dengeli bir performans)

 Accuracy: 0.64 (Genel doğru tahmin oranı %64. )
 
 2. confusion_matrix Analizi:
    
    İlk Satır: Gerçek High kategorisindeki animeler için tahminler:
   
             154 doğru yüksek dereceli tahmin
             70 yanlış düşük dereceli tahmin
             277 yanlış orta dereceli tahmin
             
    İkinci Satır: Gerçek Low kategorisindeki animeler için tahminler:
  
               1407 doğru düşük dereceli tahmin
               5 yanlış yüksek dereceli tahmin
               146 yanlış orta dereceli tahmin
               
    Üçüncü Satır: Gerçek Medium kategorisindeki animeler için tahminler:
  
               596 doğru orta dereceli tahmin
               59 yanlış yüksek dereceli tahmin
               634 yanlış düşük dereceli tahmin

Gözetimsiz öğrenme için K-Means kümeleme algoritması kullandım. Veri setini genre_encoded , episodes , members , type_encoded'i guruplara ayırarak her küme, seçilen özellikler açısından benzer anime'leri içeren gruplar oluşturdum.

Lojistik Regresyon  için çapraz doğrulama yaptım. Sonuçlar:
     Genel Performans: Ortalama skor (%63) modelimiz genel performansının yeterli olduğunu ve modelinizin genellikle iyi çalıştığını gösterir. Standart sapmanın düşük 
     olması, modelimizin çeşitli veri alt kümelemelerinde tutarlı performans gösterdiğini belirtir.
     Standart sapma, doğruluk skorlarının ne kadar değiştiğini gösterir. Burada 0.0371 olarak hesaplanmıştır. Bu düşük standart sapma, modelinizin çapraz doğrulama 
     sırasında performansının tutarlı olduğunu gösterir.


K-Means gibi kümeleme algoritmalarında çapraz doğrulama doğrudan uygulanmaz çünkü bu algoritmalar denetimsizdir ve genellikle etiketlenmiş verilerle test edilemezler. Ancak, bazı yöntemlerle kümeleme kalitesini değerlendirebilir ben o yöntemlerden Silhouette Skorunu kullandım.Sonuçlar:
   
   Yüksek Skor: Skor 0.8693, kümelerinizin oldukça iyi bir şekilde ayrıldığını ve kümeler içindeki benzerliklerin yüksek, kümeler arasındaki farkların ise belirgin 
   olduğunu gösterir.
   Kümeleme Kalitesi: Bu skor, K-Means modelimizin oldukça başarılı bir şekilde kümelendiğini ve her bir kümenin içindeki noktaların birbirine çok benzediğini 
   gösterir. Kümeler arasında belirgin ayrımlar var.



   Kaggle'daki nootbook adresim : https://www.kaggle.com/code/zeynepravzadursun/al-ma?scriptVersionId=197356867
   kaggle profilim : https://www.kaggle.com/zeynepravzadursun
  


