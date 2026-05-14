# leaflet-kml
[
![npm version](https://img.shields.io/npm/v/leaflet-kml.svg)
](https://www.npmjs.com/package/leaflet-kml)
[
![license](https://img.shields.io/npm/l/leaflet-kml.svg)
](LICENSE)

KMLデータを解析し、地図上に表示するためのLeafletプラグインです。Placemark、Line、Polygon、GroundOverlayなど様々なKML要素を処理し、KMLファイル内のスタイル情報を適用します。

## デモ
ライブデモは以下で確認できます:
*   **Windy.com Uploader:** https://www.windy.com/uploader

## 機能
- **KMLジオメトリの解析:** Point、LineString、Polygon、Trackを表示します。
- **複雑な構造の処理:** Folder、MultiGeometry、GroundOverlayをサポートします。
- **KMLスタイルの適用:** `<Style>` および `<StyleMap>` タグで定義されたスタイル（色、線の太さ、アイコンなど）をレンダリングします。
- **情報付きポップアップ:** `<name>` および `<description>` タグを使用してPlacemarkにポップアップを作成し、HTMLコンテンツを保持します。

## 要件
- Leaflet 1.0以上

## 使い方
1.  HTMLにLeafletのCSSおよびJavaScriptファイルを読み込みます。
2.  `leaflet-kml` プラグインのスクリプトを読み込みます。
3.  KMLデータを取得してXMLとして解析し、`L.KML` レイヤーに渡します。

以下は、そのまま実行可能な完全な例です:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>leaflet-kml デモ</title>
  
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    html, body, #map {
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>
<body>
  <div id="map"></div>

  <!-- Leaflet JavaScript -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

  <!-- leaflet-kml プラグイン -->
  <script type="module">
    // この例ではマップ初期化用のヘルパーを使用していますが、標準のLeafletを使用することもできます:
    // const map = L.map('map').setView([47.5, 13.0], 5);
    // L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
    import { LeafletGSI } from "https://js.sabae.cc/LeafletGSI.js";
    import {} from "https://code4fukui.github.io/leaflet-kml/L.KML.js";

    // マップを初期化
    const map = await LeafletGSI.initMap(map);

    // KMLファイルを読み込む
    const kmltext = await (await fetch("assets/example1.kml")).text();
    const parser = new DOMParser();
    const kml = parser.parseFromString(kmltext, "text/xml");

    // 新しいKMLレイヤーを作成し、マップに追加する
    const track = new L.KML(kml);
    map.addLayer(track);

    // KMLコンテンツが表示されるようにマップを調整する
    const bounds = track.getBounds();
    if (bounds.isValid()) {
      map.fitBounds(bounds);
    }
  </script>
</body>
</html>
```
