---
title: Using GeoPandas and Mplleaflet to handle Tainan GIS Data
excerpt: GeoPandas is so funny!
header:
  image: 
  teaser: https://raw.githubusercontent.com/Min-Sheng/Min-Sheng.github.io/master/_current_projects/images/tainan_villages&river_observs.png
---
> 最近想利用 Pythont 處理地理資訊系統(GIS)做疊圖、最短距離分析，意外發現 GeoPandas 這好用的東西，以下就用台灣的政府開放資料來玩玩看吧！

首先，先安裝好 pandas、numpy、geopandas、shapely、fiona、matplotlib、mplleaflet 等 Python 套件。

並下載政府資料開放平台的　![村里界圖(TWD97經緯度)]<https://data.gov.tw/dataset/7438>　、　![河川流域範圍圖]<https://data.gov.tw/dataset/9823>　，下載完後新增一個資料夾名為 Village ，解壓縮到此資料夾內。

先將該 inmport 的套件、繪圖設定等 set up 好：

```python
import geopandas as gpd
import pandas as pd
import shapely
from shapely.geometry import Point, MultiPoint
from shapely.ops import nearest_points
import matplotlib.pyplot as plt
import numpy as np
import fiona
import mplleaflet
fiona.drvsupport.supported_drivers['kml'] = 'rw' # enable KML support which is disabled by default
fiona.drvsupport.supported_drivers['KML'] = 'rw' # enable KML support which is disabled by default
plt.style.use('bmh')
%pylab inline
pylab.rcParams['figure.figsize']=(20.0,20.0)
```
使用 geopandas 讀取 shp檔：
```python
villages_shp=gpd.read_file('./Village/VILLAGE_MOI_1070312.shp')
villages_shp.head()
```
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VILLCODE</th>
      <th>COUNTYNAME</th>
      <th>TOWNNAME</th>
      <th>VILLNAME</th>
      <th>VILLENG</th>
      <th>COUNTYID</th>
      <th>COUNTYCODE</th>
      <th>TOWNID</th>
      <th>TOWNCODE</th>
      <th>NOTE</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10013030S01</td>
      <td>屏東縣</td>
      <td>東港鎮</td>
      <td>None</td>
      <td>None</td>
      <td>T</td>
      <td>10013</td>
      <td>T03</td>
      <td>10013030</td>
      <td>未編定村里</td>
      <td>POLYGON ((120.4805919500001 22.42686214900004,...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>64000130006</td>
      <td>高雄市</td>
      <td>林園區</td>
      <td>中門里</td>
      <td>Zhongmen Vil.</td>
      <td>E</td>
      <td>64000</td>
      <td>E13</td>
      <td>64000130</td>
      <td>None</td>
      <td>POLYGON ((120.3677206890001 22.49564452100009,...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10018010054</td>
      <td>新竹市</td>
      <td>東區</td>
      <td>關新里</td>
      <td>Guanxin  Vil.</td>
      <td>O</td>
      <td>10018</td>
      <td>O01</td>
      <td>10018010</td>
      <td>None</td>
      <td>POLYGON ((121.0216527890001 24.78572117700008,...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>64000130008</td>
      <td>高雄市</td>
      <td>林園區</td>
      <td>港埔里</td>
      <td>Gangpu Vil.</td>
      <td>E</td>
      <td>64000</td>
      <td>E13</td>
      <td>64000130</td>
      <td>None</td>
      <td>POLYGON ((120.3732513370001 22.49123186400004,...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64000100010</td>
      <td>高雄市</td>
      <td>旗津區</td>
      <td>上竹里</td>
      <td>Shangzhu Vil.</td>
      <td>E</td>
      <td>64000</td>
      <td>E10</td>
      <td>64000100</td>
      <td>None</td>
      <td>POLYGON ((120.2897623490001 22.57316931000008,...</td>
    </tr>
  </tbody>
</table>
</div>



使用 Mplleaflet 可以將 GeoPandas 處理完的 Dataframe繪製在真實地圖上：

<iframe src="https://hmvmgga3dvbaxrnyqrms9g-on.drv.tw/intelcityfile/village/map/_map.html" width="80" height="720" frameborder="0" scrolling="no"></iframe>

