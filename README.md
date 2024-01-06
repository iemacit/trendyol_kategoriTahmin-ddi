# markaTahmin-ddi

### Projeyi Hazırlayanlar;
İBRAHİM ETHEM MACİT 213405050

  
### PROJENİN AMACI  
Piyasada hali hazırda satılmakta olan ürünlerin Trendyol e ticaret sitesindeki kategori bazlı dağılımını görerek ve aynı zamanda fiyat ortalamasını alarak bu sayede  e-ticaret yapan bireysel satıcılara kolaylık sağlamak amaçlanmıştır. Örneğin 9000 veri bulunan veri setimde Saat Seti en az satılan üründü ve fiyatına dikkat çekersek en pahalı ürün olduğu görülmektedir. Bu sayede bireysel e-ticaret satıcısı hem rekabet edeceği firmanın az olduğunu görecek hem de ortalama fiyatın yüksek olması sebebiyle satış ve kazanç miktarı artacak. Ben burada erkek giyim ve aksesuarı başlıkları altındaki ürünlerin 9000 tanesi ile bu veriye ulaşmış oldum. Sadece bu  başlıklar için modelim çalışmıyor. İstediğiniz farklı başlıklar altındaki Trendyol linklerini de yapıştırarak bu model de verilere ulaşabilirsiniz.
(Örneğin; Elektronik eşya satan bir mağaza Trendyol üzerindeki ürün satış potansiyelini ve ortalama ürün başı fiyatını görmek isterse elektronik ürünlerin bulunduğu başlığın olduğu linki yapıştırması ona modeli kullanmasında yardımcı olacaktır.) 

# TRENDYOL.COM SİTESİNDEN SATIŞI YAPILAN ÜRÜNLERİN KATEGORİ TAHMİNİ
Bu projede trendyol.com sitesinden alınmış erkek giyim ve aksesuar başlıkları altında bulunan farklı kategorilerden (Sweatshirt,Gömlek,Pantolon,Saat,Kemer vb.) ürünlerin yer aldığı ilanlar ile modelimizi eğitiyoruz ve modele bir ürün başlığı yazdığımızda o ürünün hangi kategoriye ait olduğunu ve  Trendyol üzerindeki ortalama fiyatınıda bizlere bildiriyor. 
#### Kullanılan Kütüphaneler
-Pandas      
-Numpy  
-Pyplot  
-Scikit-Learn  
-BeautifulSoup  

##### Veri Setinin Oluşturulması
Veri setimiz trendyol.com da web scrapping işlemi yaparak farklı kategorilerden oluşan ilanlardan oluşuyor. Modelimizi doğru eğitebilmemiz için verilerimizin düzgün, eksiksiz veriler olması gerekir. Bu yüzden ürünler bazı kriterlere dikkat edilerek çekilmiştir. Örneğin ürün başlığında ürünün kategorisinin geçmesine önemle dikkat çekilmiştir.Trendyol üzerinden veriyi çekerken bazı linklere giriş yaparken modelim internet hızından dolayı bazılarında ürün bilgisi çekerken gecikme kaynaklı bilgiler eksik geldiği saptanmış ve bu durum oluşan ürünler listeye eklenmeden contunie ile çıkarılmıştır.Ürünleri çekebilmek için web scrapping işlemi yapan BeatufilSoup kütüphanesi kullanılmıştır. Veri setimde yaklaşık 9000 veri vardır.

##### Veri Setinde Bulunan Ürünlerin Kategori Dağılıöı
![Veri Seti](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/veri-seti.png)  
  
##### Veri Setinde Bulunan Kategorilerin Ortalama Fiyat Grafiği
![Veri Seti](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/veri-seti.png)  
        
Bu verileri çekmek ortalama 120 dakika sürmüştür.

Veri setindeki kolonlarımız aşağıdaki gibidir;  
-Ürün İsmi
-Ürün Linki
-Ürün Fiyatı
-Ürün Etiketi
Veri setinde ürünler Trendyol üzerindeki linkleri,fiyatları ve kategorileri ile ekleniyorlar. Bunun amacı oluşturulacak olan modeli eğitmek için hangi kategoriye ait olduğunu bilmek ve fiyatları alarak kategori bazlı istatislik oluşturmak.

*Oluşturulmuş Veri Seti*  
![Oluşturulmuş Veri Seti](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/olusturulmus-veri-seti.png)

##### ürünlerin Temizlenmesi ve Lemmatization İşlemi
Veri seti oluşturulduktan sonra modelin daha iyi çalışması ve başarı oranının daha yüksek olması için ürünlerin temizlenmesi gerekmektedir. ürünlerin içerisinde ürün kodları, emojiler, noktalama işaretleri, stop wordsler, linkler gibi istenmeyen ve modelin başarısını düşürecek veriler ürünlerin içerisinden temizleniyor.  
  
*Oluşturulmuş Temiz Ürün Başlığı Gösteremi*  
![Oluşturulan Temiz İlan](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/olusturulan-temiz-ilan.png)

##### Modelin Oluşturulması ve Ürünlerin Kategorilendirilmesi
###### Model Seçimi
Yapılacak sınıflandırma işleminin hangi modelde daha yüksek başarı oranı vereceğini tespit etmek amacıyla araştırma yapılıp aynı zamanda bazı modeller üzerinde de test edilmiştir.2 model üzerinde denemeler yapılmıştır. Bu modeller Naive bayes ve Decision Tree modelleridir. Projedeki test veri seti sonuçlarına bakıldığında;
Naive Bayes Modeli Başarısı:0.96
Decision Tree Modeli Başarısı:0.78
Sonuçlar Naive Bayes modelinin projede kullanılan veri seti için daha doğru sonuç verdiği tespit  edilmiştir.Bu projede hem Naive Bayes hem de  Decision Tree Modeli ile modeli eğittim.

##### Modelin Oluşturulmaya Başlanması
###### Etiketleme
Temizlenmiş Ürün Başlıkları
df["Etiket"] = df.apply(lambda row: etiketle(row), axis=1)
koduyla etiketleyip
df.to_csv("cleaned_data.csv", index=False) ile
cleaned_data.csv tablosuna aktarıyoruz.
Ürünlerin hangi kategoriye ait olduğu kelime şeklinde kayıtlı olduğu için bu ürünlerin 0,1,2,3,… gibi bilgisayarın anlayacağı bir formata dönüştürüyoruz. Etiket adında yeni bir kolon açıp kategoriye göre (veri setimizde 10 kategori var) bu yüzden 0‘dan 9'a kadar etiketleme yapıyoruz. Örneğin Gömlrk için 3, T-Shirt için 1 etiketlemesi yapıyoruz.

*Etiketlenmiş Veri Seti*  
![Etiketlenmiş Veri Seti](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/veri-seti-son.png)

##### Veri Setinin Parçalanması
Model başarısını doğru şekilde değerlendirebilmek için, eğitim ve test aşamalarında farklı veri kümeleri kullanmak önemlidir. Modelin eğitiminde kullanılan veriler, test aşamasında tekrar kullanılmamalıdır çünkü bu durum modelin başarısını yanıltıcı bir şekilde yüksek gösterebilir. Bu sebeple, veri setini bölmek gereklidir. Bu proje için, veri setinin %80'i modelin eğitimi için kullanılacak, geri kalan %20'si ise modelin test edilmesi için ayrılacaktır. Veri setini parçalamak için train_test_split() fonksiyonu kullanılmıştır.

##### Ürünlerin Vektörel Matrisinin Çıkarılması
TF-IDF vektörleme yöntemi kullanılarak, her bir ürün başlığındaki kelimelerin belge içindeki önemi istatistiksel olarak hesaplanmıştır. Bu süreçte, yaygın stopwords'lar gibi anlam taşımayan kelimeler filtrelenerek, model için gereksiz olan unsurların etkisi azaltılmıştır. Bu sayede, anlamlı ve bilgi taşıyan özellikler belirginleştirilmiştir, modelin doğruluğunu artırmak adına daha sağlam bir temel oluşturulmuştur.

#### Modelin Eğitilmesi
Decision Tree metoduyla modelimiz eğitilmiştir. Modeli eğitmek için sklearn kütüphanesinden faydalanılmıştır.
##### Modelin Başarısının Hesaplanması
Hesaplama aşağıdaki görseldedir  
![Model Başarısı](https://github.com/UtkuYURT/markaTahmin-ddi/blob/main/images/model-basarisi.png)

### SONUÇ
Özetle yaptığım projede seçilen modelin ne kadar önemli olduğu görülmektedir. Projemde iki model yöntemi ile eğitmem sonucunda görüldüğü üzere iki modelde veri setimdeki ürün başlıkları ile eğitilmesi sonucunda yüksek başarı oranları vermiştir . Ancak model seçiminin önemi kadar veri setinin de güzel bir şekilde hazırlanmış olması, güzel temizlenmesi, veri setindeki veri miktarı, veri setinin dengesiz olup olmaması, eğitim-test setinin parçalanma oranı vb. faktörler modelin başarısına etki edildiği anlaşılmıştır.
