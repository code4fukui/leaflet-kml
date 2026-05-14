# leaflet-kml
[
![npm version](https://img.shields.io/npm/v/leaflet-kml.svg)
](https://www.npmjs.com/package/leaflet-kml)
[
![license](https://img.shields.io/npm/l/leaflet-kml.svg)
](LICENSE)

A Leaflet plugin to parse and display KML data on a map. It handles various KML elements, including Placemarks, Lines, Polygons, and GroundOverlays, and applies styling information from the KML file.

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

## Demo
A live demo is available at:
*   **Windy.com Uploader:** https://www.windy.com/uploader

## Features
- **Parses KML Geometries:** Displays Points, LineStrings, Polygons, and Tracks.
- **Handles Complex Structures:** Supports Folders, MultiGeometry, and GroundOverlays.
- **Applies KML Styling:** Renders styles defined in `<Style>` and `<StyleMap>` tags, including colors, line widths, and icons.
- **Informative Popups:** Creates popups for Placemarks using `<name>` and `<description>` tags, preserving HTML content.

## Requirements
- Leaflet 1.0+

## Usage
1.  Include Leaflet's CSS and JavaScript files in your HTML.
2.  Include the `leaflet-kml` plugin script.
3.  Fetch your KML data, parse it as XML, and pass it to the `L.KML` layer.

Here is a complete, runnable example:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>leaflet-kml Demo</title>
  
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

  <!-- leaflet-kml Plugin -->
  <script type="module">
    // The example uses a helper for map initialization, but you can use standard Leaflet:
    // const map = L.map('map').setView([47.5, 13.0], 5);
    // L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
    import { LeafletGSI } from "https://js.sabae.cc/LeafletGSI.js";
    import {} from "https://code4fukui.github.io/leaflet-kml/L.KML.js";

    // Initialize the map
    const map = await LeafletGSI.initMap(map);

    // Load KML file
    const kmltext = await (await fetch("assets/example1.kml")).text();
    const parser = new DOMParser();
    const kml = parser.parseFromString(kmltext, "text/xml");

    // Create a new KML layer and add it to the map
    const track = new L.KML(kml);
    map.addLayer(track);

    // Adjust map to show the KML content
    const bounds = track.getBounds();
    if (bounds.isValid()) {
      map.fitBounds(bounds);
    }
  </