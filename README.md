# Leaflet KML layer plugin

![Example](assets/screenshot.jpg)

Demo: https://www.windy.com/uploader

This plugin was extracted from Pavel Shramov's Leaflet Plugins [repository](https://github.com/shramov/leaflet-plugins) in order to maintain this code more frequently and separate KML layer from other plugins.

So far we have fixed few issues.

Probably will work on Leaflet 1+, tested on Leaflet 1.4.

## How to use

```html
<!DOCTYPE html><html lang="ja"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width">
<title>leaflet-kml demo</title>
</head><body>
<div style="width: 100vw; height: 100vh" id="divmap"></div>
<script type="module">
import { LeafletGSI } from "https://js.sabae.cc/LeafletGSI.js";
import {} from "https://code4fukui.github.io/leaflet-kml/L.KML.js";

const map = await LeafletGSI.initMap(divmap);
// map.setView([37, 135], 5); // 日本表示

const kmltext = await (await fetch("assets/example1.kml")).text();
// Create new kml overlay
const parser = new DOMParser();
const kml = parser.parseFromString(kmltext, "text/xml");
const track = new L.KML(kml);
map.addLayer(track);

// Adjust map to show the kml
const bounds = track.getBounds();
map.fitBounds(bounds);
</script>
</body>
</html>
```

## Licence

MIT
