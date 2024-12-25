# Python-Final-ElifUras
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


import geopandas as gpd
import matplotlib.pyplot as plt

# Veri dosyasının tam yolu
shp_path = r'D:\python-final-elifuras\data\data.shp'  # Verinizin yolu

# Veriyi yükleyin
airbnb_data = gpd.read_file(shp_path)

# Veriyi görselleştirin
ax = airbnb_data.plot(marker='o', color='pink', markersize=10, edgecolor='black', linewidth=0.5)

# Başlık ve etiketler
plt.title("Airbnb Noktaları - Ankara ve Bolu")
plt.xlabel("Longitude")
plt.ylabel("Latitude")

# Görselleştirmeyi göster
plt.show()
import geopandas as gpd

# Veri dosyasının yolu
shp_path = r'D:\python-final-elifuras\data\data.shp'

# Veriyi yükleyin
airbnb_data = gpd.read_file(shp_path)

# Veri tipini ve ilk birkaç satırı kontrol edelim
print(airbnb_data.crs)  # Koordinat sistemi
print(airbnb_data.head())  # İlk 5 satır

from shapely.ops import nearest_points

# Her bir noktayı en yakın diğer noktaya bağlayalım
distances = []
for idx, point in airbnb_data.iterrows():
    # Diğer noktalar arasındaki mesafeleri hesaplayalım
    nearest_point = airbnb_data.geometry.apply(lambda x: nearest_points(point.geometry, x)[1])
    distance = point.geometry.distance(nearest_point.loc[nearest_point != point.geometry].iloc[0])  # Mesafeyi hesapla
    distances.append(distance)

# Yeni bir sütun ekleyelim
airbnb_data['nearest_distance'] = distances

# Sonuçları kontrol edelim
print(airbnb_data[['nearest_distance']].head())

import matplotlib.pyplot as plt

# Mesafe analizini görselleştirelim
airbnb_data.plot(column='nearest_distance', cmap='coolwarm', legend=True, figsize=(10, 6))

plt.title('En Yakın Airbnb Noktaları - Mesafe Analizi')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()

import geopandas as gpd
import folium
from folium.plugins import HeatMap
import pandas as pd

# Veri dosyasının tam yolu
shp_path = r'D:\python-final-elifuras\data\data.shp'  # Verinizin yolu

# Veriyi yükleyin
airbnb_data = gpd.read_file(shp_path)

# Latitude ve Longitude sütunlarını alın
coordinates = airbnb_data[['geometry']].apply(lambda x: (x.geometry.y, x.geometry.x), axis=1)
coordinates = pd.DataFrame(coordinates.tolist(), columns=['Latitude', 'Longitude'])

# Harita oluşturma - Başlangıç noktası olarak Ankara'nın merkezini alalım
m = folium.Map(location=[39.9334, 32.8597], zoom_start=12)

# Isı haritası oluşturma
HeatMap(data=coordinates).add_to(m)

# Haritayı kaydetme
m.save("heatmap.html")

import geopandas as gpd
import folium
from folium.plugins import HeatMap
import pandas as pd

# Veri dosyasının tam yolu
shp_path = r'D:\python-final-elifuras\data\data.shp'  # Verinizin yolu

# Veriyi yükleyin
airbnb_data = gpd.read_file(shp_path)

# Koordinatları çıkaralım
coordinates = airbnb_data[['geometry']].apply(lambda x: (x.geometry.y, x.geometry.x), axis=1)
coordinates = pd.DataFrame(coordinates.tolist(), columns=['Latitude', 'Longitude'])

# Harita oluşturma - Başlangıç noktası olarak Ankara'nın merkezini alalım
m = folium.Map(location=[39.9334, 32.8597], zoom_start=12)

# Isı haritası oluşturma
HeatMap(data=coordinates).add_to(m)

# Haritayı kaydetme
m.save("heatmap.html")



