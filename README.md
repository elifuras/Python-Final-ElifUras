﻿# Python-Final-ElifUras
Bu proje, Python kullanarak bir mekansal analiz yapmayı ve bunun sonucunda elde edilen verileri görselleştirmeyi amaçlıyor. İlk olarak, Airbnb konaklama noktalarını içeren bir veriyi yükledim ve bu verinin coğrafi koordinatlarını inceledim. Veri, Shapefile formatında olup, GeoPandas kütüphanesiyle okundu. Veri setinde her bir Airbnb noktasının coğrafi konumunu temsil eden geometrik veriler bulunuyor.

İlk adımda, veriyi yükledikten sonra, her bir konaklama noktasının en yakın diğer noktaya olan mesafesini hesapladım. Bunun için Shapely kütüphanesini kullandım. Shapely, coğrafi nesnelerle işlem yapmamıza olanak tanıyan bir Python kütüphanesi. Her bir noktayı, veri setindeki diğer noktalarla karşılaştırarak, en yakın komşusunu buldum ve mesafelerini hesapladım.

Hesapladığım mesafeleri veri setine yeni bir sütun olarak ekledim. Bu yeni sütun, her bir konaklama noktasının en yakın diğer noktaya olan mesafesini içeriyor.

Son adımda, bu mesafeleri görselleştirdim. Görselleştirme için Matplotlib kütüphanesini kullandım. Bu kütüphane ile, mesafeleri renklerle göstererek, her bir noktanın diğerlerine olan uzaklığını görsel olarak sundum. Kullanılan renk skalası, mesafeleri daha kısa olan bölgeleri sıcak renklerle, uzun mesafeleri ise soğuk renklerle gösterdi.

Projemin başında, Python kodumu QGIS’te çalıştırabilmek için gerekli modüllerin doğru bir şekilde yüklendiğinden emin oldum. QGIS, kendi Python ortamını kullanıyor ve bazı dış kütüphanelerin (örneğin, GeoPandas, Shapely, Folium) yüklenmesi ve doğru sürümlerinin kullanılması gerekiyor. QGIS'in Python konsolunda dış kütüphaneleri yüklemek için OSGeo4W Shell kullanarak modülleri yükledim. Ancak bu süreçte, QGIS'in Python ortamının sistemimdeki Python'dan farklı sürümlere sahip olabileceğini fark ettim ve modüllerin doğru Python ortamına yüklenmesi gerekti.

Modülleri güncellerken zaman zaman uyumsuzluk sorunlarıyla karşılaştım. Bu tür durumlar genellikle modüllerin sürüm uyumsuzluğundan kaynaklanıyordu. Bu yüzden, her modülün uyumlu sürümünü bulmak ve güncellemek için zaman harcadım. QGIS'in Python ortamındaki modül dizinini doğru tanımak için gerekli yolları güncelledim.

Yüklediğim kütüphanelerle birlikte, QGIS üzerinde yazdığım Python kodlarını QGIS Python konsoluna entegre ettim. QGIS içindeki Python konsolunda kodları çalıştırarak, veri setini yükledim ve üzerinde mekansal analizler gerçekleştirdim. Veri yükleme, mesafe hesaplama ve görselleştirme işlemleri Python kodu ile gerçekleştirildi. Bu süreçte, GeoPandas ve Shapely gibi kütüphaneleri kullanarak, her bir Airbnb konaklama noktasının en yakın diğer noktaya olan mesafelerini hesapladım.

Python modüllerini QGIS ortamına entegre etme süreci, bazı modüllerin QGIS’in Python ortamında uyumsuz olmasından dolayı zorlu olabiliyor. Bu nedenle, kullanmak istediğim kütüphanelerin sürümlerini güncelledim ve her bir modülün bağımlılıklarını dikkatlice kontrol ettim. Güncelleme işlemleri sırasında karşılaştığım hatalar, genellikle modül bağımlılıklarıyla ilgiliydi. Bu nedenle, her modülün gereksinimlerini takip ederek, en uyumlu sürümleri yükledim.

QGIS Python konsolunu kullanarak, analiz adımlarını başarıyla tamamladım. Yüklediğim veriler üzerinde mesafe hesaplama, yoğunluk analizi ve görselleştirme işlemlerini QGIS arayüzü ile birleştirerek gerçekleştirdim. Analizlerin her bir adımını Python kodlarıyla çalıştırarak, QGIS’in arayüzünde bu verileri görselleştirdim.

Ayrıca, Python'un Folium kütüphanesini kullanarak, harita üzerinde bir heatmap (ısı haritası) oluşturmayı başardım. Bu heatmap, Airbnb konaklama noktalarının yoğunluklarını gösteren bir görselleştirme yöntemi olarak kullanıldı. Harita üzerinde konumlar yer alırken, bu konumların yoğunlukları renk tonlarıyla ifade edilerek, harita üzerinden görsel bir analiz yapılmasına olanak tanındı.
