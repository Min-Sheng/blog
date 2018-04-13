---
title: Using GeoPandas and Mplleaflet to handle Tainan GIS Data
excerpt: GeoPandas is so funny!
header:
  image: 
  teaser: https://raw.githubusercontent.com/Min-Sheng/Min-Sheng.github.io/master/_current_projects/images/tainan_villages&river_observs.png
---
> 最近想利用 Pythont 處理地理資訊系統(GIS)做疊圖、最短距離分析，意外發現 GeoPandas 這好用的東西，以下就用台灣的政府開放資料來玩玩看吧！

首先，先安裝好 pandas、numpy、geopandas、shapely、fiona、matplotlib、mplleaflet 等 Python 套件。

其次，下載政府資料開放平台的[村里界圖(TWD97經緯度)](https://data.gov.tw/dataset/7438)、[河川流域範圍圖](https://data.gov.tw/dataset/9823)，下載完後新增一個資料夾名為 Village ，解壓縮到此資料夾內。

我使用 google map 額外整理出台南河川水質觀測站的位置圖，請點選前往地圖匯出成KML檔：

<iframe src="https://www.google.com/maps/d/u/0/embed?mid=16LaPUTI3GzyXe9v3f5o02x06y5xBBcP4" width="640" height="480"></iframe>

以下是我用 jupyter notebook 寫的 python 程式碼，

目標是將台南各里範圍與河川流域範圍圖做疊圖分析，歸納出位於各流域的是哪些里，

並計算這些里的地理中心(centroid)，分析出距離最近的觀測站，並據此分區。

<iframe src="https://60rtgvubb3azlosi4lvvqa-on.drv.tw/Tainan_Villages/Village.html" width="800" height="480" frameborder="0"></iframe>

最後，使用 Mplleaflet 可以將 GeoPandas 處理完的 Dataframe繪製在真實地圖上：

```python
ax=tainan_villages_shp.plot(color='white',edgecolor='k')
river1_shp.plot(ax=ax,facecolor=(0.9804, 0, 0.9804, 0.01),edgecolor='red')
river2_shp.plot(ax=ax,facecolor=(0.5294, 0.8078, 0.9803, 0.01),edgecolor='blue')
river3_shp.plot(ax=ax,facecolor=(0.5960, 0.9843, 0.5960, 0.01),edgecolor='green')
river4_shp.plot(ax=ax,facecolor=(0.5450, 0, 0.5450, 0.01),edgecolor='purple')
river5_shp.plot(ax=ax,facecolor=(1, 1, 0, 0.01),edgecolor='orange')
river_villages_shp.plot(ax=ax, column='nearest_observ', cmap='tab10_r',edgecolor='k',categorical=True)
observ_shp.plot(ax=ax, column='Name', cmap='tab10_r', edgecolor='k', marker='D',markersize=100)
tainan_villages_shp.centroid.plot(ax=ax,color='black',markersize=2)
mplleaflet.show()
```

<iframe src="https://hmvmgga3dvbaxrnyqrms9g-on.drv.tw/intelcityfile/village/map/_map.html" width="800" height="480" frameborder="0" scrolling="no"></iframe>

