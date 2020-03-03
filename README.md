# Designing custom map styles for your OpeStreetMap vector tiles

OpenStreetMap is a collaborative project to create a free editable map of the world. Designing a style for your custom OSM vector tiles can be a bit confusing for a newcomer to GIS or to somebody just getting started with maps. This workshop focuses on creating a map style using Maputnik visual editor and applying it to your custom vector tiles (rest assured - we’ll provide the OSM tiles)

## 1. Style your map with maputnik and export your json

https://maputnik.github.io/editor

## 2. Update tiles datasource and style settings and export

Change the TileJSON URL from Maputnik Data Sources to `http://localhost:8080/data/v.json`
Change the Glyphs URL from Maputnik Style Settings to `https://api.maptiler.com/fonts/{fontstack}/{range}.pbf?key=kZiXT98mXBUn4Sw0HMPv`
Export Style

## 3. Download MBTiles

We have pregenerated vector tiles for Cluj-Napoca city. To genereate your own vector tiles refer to https://github.com/MapDev-OSM/Generating-Vector-Tiles-from-OpenStreetMap-data

You can download pregenerated tiles inside the `./tiles` folder of this repo. - [Cluj-Napoca vector tiles](./tiles/cluj-napoca.mbtiles)

## 4. Host the tiles on a local server

To serve your vector tiles you need a server that reads the MBTiles and exposes an api for clients. Clients requyest the tiles and displays them on the client browser. For this workshop we will use [tileserver-gl](https://github.com/maptiler/tileserver-gl) .

A list of other tile servers that you can use to serve your tiles can be found here: https://github.com/mapbox/awesome-vector-tiles#servers

Start cmd/bash in the folder where you downloaded the tiles

Bash

```
docker run --rm -it -v $(pwd):/data -p 8080:80 klokantech/tileserver-gl
```

Cmd

```
docker run --rm -it -v %CD%:/data -p 8080:80 klokantech/tileserver-gl
```

## 5. Prepare the mbtiles-custom-style repo

```
git clone https://github.com/MapDev-OSM/mbtiles-custom-style.git
```

Save your json style inside `mbtiles-custom-style/build/styles`
Edit `mbtiles-custom-style/src/config.js` to include your custom style

## 6.a Run mbtiles-custom-style website using docker

Bash

```
docker run --rm -v $(pwd):/web --name mbtiles-custom-style --entrypoint /web/start.sh -p 9090:9090 -w="/web" node:13.8.0
```

Cmd

```
docker run --rm -v %CD%:/web --name mbtiles-custom-style --entrypoint /web/start.sh -p 9090:9090 -w="/web" node:13.8.0
```

## 6.b Run mbtiles-custom-style website using npm

```
npm install
npm run dev
```

Visit http://localhost:9090 and select your style from the dropdown
