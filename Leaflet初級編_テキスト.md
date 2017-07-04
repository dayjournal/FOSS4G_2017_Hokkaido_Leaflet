# 2017.06.30 FOSS4G 2017 Hokkaido ハンズオン

## 事前準備できてますか??
http://day-journal.com/blog/day-016

## ハンズオン結果表示確認用URL
http://day-journal.com/example/FOSS4G2017Hokkaido


## ハンズオン内容

### 初期表示

---

```

<!DOCTYPE html>
<html lang="ja">

<head>

    <meta charset="UTF-8">
    <title>Leaflet Sample</title>

    <!-- Leafletライブラリ読み込み -->
    <script src="./library/leaflet-0.7.3/leaflet.js"></script>
    <link href="./library/leaflet-0.7.3/leaflet.css" rel="stylesheet" />

    <!-- CSS読み込み -->
    <link href="./css/stylesheet.css" rel="stylesheet" />
    
</head>
<body>

    <!-- Map読み込み -->
    <div id="map"></div>
    <!-- JS読み込み -->
    <script src="./js/script.js"></script>

</body>
</html>

```

```

   html, body {
        height: 100%;
        padding: 0;
        margin: 0;
    }

    #map {
        z-index: 0;
        height: 100%;
    }


```

### OSM表示

---

```

var map = L.map('map');

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);

map.setView([35.680899409847584, 139.76712226867676], 16);

```

### 地理院タイル表示

---

```

L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png', {
    attribution: "<a href='http://www.gsi.go.jp/kikakuchousei/kikakuchousei40182.html' target='_blank'>国土地理院</a>"
}).addTo(map);


L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg', {
    attribution: "<a href='http://www.gsi.go.jp/kikakuchousei/kikakuchousei40182.html' target='_blank'>国土地理院</a>"
}).addTo(map);

```

### MIERUNE地図表示

---

```

L.tileLayer('https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png', {
    attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
}).addTo(map);

```

### レイヤ統合

---

```

var t_pale = new L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png', {
    attribution: "<a href='http://www.gsi.go.jp/kikakuchousei/kikakuchousei40182.html' target='_blank'>国土地理院</a>"
});

var t_ort = new L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg', {
    attribution: "<a href='http://www.gsi.go.jp/kikakuchousei/kikakuchousei40182.html' target='_blank'>国土地理院</a>"
});

var o_std = new L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
});

var m_mono = new L.tileLayer('https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png', {
    attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
});


var lat = 35.680899409847584;
var lng = 139.76712226867676;

var map = L.map('map', {
    center: [lat, lng],
    zoom: 15,
    maxZoom: 18,
    zoomControl: true,
    layers: [m_mono]
});

var Map_BaseLayer = {
    "地理院地図 淡色": t_pale,
    "地理院地図 オルソ": t_ort,
    "OpenStreetMap 標準": o_std,
    "MIERUNE地図 MONO": m_mono
};

L.control.layers(
    Map_BaseLayer, 
    null
).addTo(map);

```

### レイヤアクティブ

---

```

L.control.layers(
    Map_BaseLayer, 
    null, 
    {collapsed:false}
).addTo(map);

```

### スケールバー

---

```

L.control.scale({
    imperial: false,
    maxWidth: 300
}).addTo(map);

```

### ズームバー

---

```

var map = L.map('map', {
    center: [lat, lng],
    zoom: 15,
    maxZoom: 18,
    zoomControl: false,
    layers: [m_mono]
});

```

### マーカー

---

```

var Map_Point = L.marker(
    [35.68089940984, 139.7671222686]
    ).addTo(map);

var comment = '東京駅だよ!!';
Map_Point.bindPopup(comment);

```

```

var IconPin01 = L.icon({
    iconUrl: "./img/pin01.png",
    iconSize: [25, 25],
    iconAnchor: [0, 25],
    popupAnchor: [0, -35]
});

var Map_Point = L.marker(
    [35.68089940984, 139.7671222686],
    { icon: IconPin01 } 
).addTo(map);
    

```


### ライン

---

```

var Map_Line = L.polyline([
    [35.67500798914924,139.75952625274658],
    [35.67845922918971,139.76094245910645],
    [35.689369743530044,139.76420402526855]
    ],{
    "color": "#2DE9C4",
    "weight": 5,
    "opacity": 0.6
}).addTo(map);

```

### ポリゴン

---

```

var Map_Polygon = L.polygon([
    [35.675949251235025,139.76617813110352],
    [35.67410157813001,139.77188587188718],
    [35.67455478492641,139.77227210998535],
    [35.683757812281115,139.77862358093262],
    [35.68431553740134,139.77343082427979],
    [35.68469897115985,139.77094173431396],
    [35.679923346539084,139.76871013641357],
    [35.675949251235025,139.76617813110352]
    ],{
    "color": "#E92D63",
    "weight": 3,
    "opacity": 0.8,
    "fillColor": "#562DE9",
    "fillOpacity": 0.4
}).addTo(map);

```

### オーバーレイヤ

---


```

var Map_AddLayer = {
    "Point": Map_Point,
    "Line": Map_Line,
    "Polygon": Map_Polygon
};

L.control.layers(
    Map_BaseLayer, 
    Map_AddLayer, 
    {collapsed:false}
).addTo(map);

```

### GeoJSON

---


```

<script src="./vecter/map.geojson"></script>

```

```

var GeoJsonSample = L.geoJson(sampledata).addTo(map);

```

### ポイントGeoJSON (室蘭オープンデータ)

---

```

<script src="./vecter/point.geojson"></script>

```

```

var lat = 42.333174;
var lng = 141.004646;


zoom: 13,


var IconPin02 = L.icon({
    iconUrl: "./img/pin02.png",
    iconSize: [25, 25],
    iconAnchor: [15, 20],
    popupAnchor: [-5, -30]
});

var PointAll = L.layerGroup().addTo(map);
var PointGeojson = L.geoJson(pointdata, {
    onEachFeature: function (feature, layer) {
        var field ="目標地点: " + feature.properties.OBJECTID;
        layer.bindPopup(field);
    },
    pointToLayer: function (feature, layer) {
        if (feature.properties.OBJECTID > 25) {
            return L.marker(layer, { icon: IconPin01 });
        }else if (feature.properties.OBJECTID <= 25) {
            return L.marker(layer, { icon: IconPin02 });
        }
    }
}).addTo(PointAll);

var Map_AddLayer = {
    "目標地点": PointAll
};

L.control.layers(
    Map_BaseLayer, 
    Map_AddLayer, 
    {collapsed:false}
).addTo(map);

```

### ラインGeoJSON (室蘭オープンデータ)

---

```

<script src="./vecter/line.geojson"></script>

```

```

var LineAll = L.layerGroup().addTo(map);
    var line_geojson = L.geoJson(linedata, {
        style: {
            "color": "#58BE89",
            "weight": 3,
            "opacity": 0.7,
            "dashArray":[10, 5]
        },
        onEachFeature: function (feature, layer) {
            var field ="距離(m): " + feature.properties.Shape_len;
            layer.bindPopup(field);
    },
        clickable: true
    }).addTo(LineAll);

var Map_AddLayer = {
    "目標地点": PointAll,
    "避難経路": LineAll
};

```

### ポリゴンGeoJSON (室蘭オープンデータ)

---

```

<script src="./vecter/polygon.geojson"></script>

```

```

var PolygonAll = L.layerGroup().addTo(map);
var PolygonGeojson = L.geoJson(polygondata, {
        style: function(feature) {
            if (feature.properties.MEANmax_ < 2) {
                return {
                    "color": "#90D6E5",
                    "weight": 0.5,
                    "fill": true,
                    "fillColor":"#90D6E5",
                    "fillOpacity":0.4
                };
            }else if (feature.properties.MEANmax_ >= 2 && feature.properties.MEANmax_ < 4) {
                return {
                    "color": "#2A5CAA",
                    "weight": 0.5,
                    "fill": true,
                    "fillColor":"#2A5CAA",
                    "fillOpacity":0.4
                };
            }else if (feature.properties.MEANmax_ >= 4 && feature.properties.MEANmax_ < 6) {
                return {
                    "color": "#F4EE4F",
                    "weight": 0.5,
                    "fill": true,
                    "fillColor":"#F4EE4F",
                    "fillOpacity":0.6
                };
            }else if (feature.properties.MEANmax_ >= 6 && feature.properties.MEANmax_ < 8) {
                return {
                    "color": "#F08167",
                    "weight": 0.5,
                    "fill": true,
                    "fillColor":"#F08167",
                    "fillOpacity":0.6
                };
            }else if (feature.properties.MEANmax_ >= 8) {
                return {
                    "color": "#EE2E2A",
                    "weight": 0.5,
                    "fill": true,
                    "fillColor":"#EE2E2A",
                    "fillOpacity":0.8
                };
            }
        },
        onEachFeature: function (feature, layer) {
            var field ="浸水深さ(m): " + feature.properties.MEANmax_;
            layer.bindPopup(field);
        }
    }).addTo(PolygonAll);

var Map_AddLayer = {
    "目標地点": PointAll,
    "避難経路": LineAll,
    "津波区域": PolygonAll
};

```

### プラグイン1

---

```

<script src="./plugin/leaflet-locatecontrol/L.Control.Locate.min.js"></script>
<link href="./plugin/leaflet-locatecontrol/L.Control.Locate.min.css" rel="stylesheet"/>
<link href="//maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css" rel="stylesheet" >

```

```

L.control.locate().addTo(map); 

```

### プラグイン2

---

```

<script src="./plugin/leaflet-label/leaflet.label.js"></script>
<link href="./plugin/leaflet-label/leaflet.label.css" rel="stylesheet"/>

```

```

onEachFeature: function (feature, layer) {
            var field ="浸水深さ(m): " + feature.properties.MEANmax_;
            layer.bindLabel(field);
}

```

---
