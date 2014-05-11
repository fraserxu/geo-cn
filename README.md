geo-cn
=======

### Why?

I wanted to build a map with [d3.js](http://d3js.org/), and I followed up this post [Let’s Make a Map](http://bost.ocks.org/mike/map/). But after get started, I finded it hard to get the needed map data for me, especially for a country like China.

In the post Mike provided lots of good resources to find geographic data, here I just took a step way further and prepared the target data for me to use.

The source data is converted from [Natural Earth](http://www.naturalearthdata.com/).

You can download the complete file from [Admin 0 - Details - map subunits](http://www.naturalearthdata.com/http://www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_map_subunits.zip)

### Tooling

* gdal([Geospatial Data Abstraction Library](http://www.gdal.org/))
  `brew install gdal`
* topjson([TopoJSON](https://github.com/mbostock/topojson))
  `npm install -g topjson`

### Converting Data

* create `subunits.json` GeoJSON file(here including **Hongkong**, **Taiwan** and **Macau**):
  ```
  ogr2ogr \
    -f GeoJSON \
    -where "ADM0_A3 IN ('CHN', 'HKG', 'TWN', 'MAC')" \
    subunits.json \
    ne_10m_admin_0_map_subunits.shp
  ```
* create `places.json`
  ```
ogr2ogr \
  -f GeoJSON \
  -where "ISO_A2 = 'CN' AND SCALERANK < 8" \
  places.json \
  ne_10m_populated_places.shp
  ```

