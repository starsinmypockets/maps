# Carto Maps for NG Frontend

This repository contains config files for configuring map application in [CKAN NG Frontend](#)

## Getting started

1. [Install *CKAN NG Frontend*](#)
2. Enable carto plugin in your *NG Frontend* environment, along with your carto API credentials:

```
GIT_OWNER=starsinmypockets
CARTO_USER=test-user-123
```

Optionally you can provide a `CARTO_APIKEY`. By default carto's `public_default` key which can access all public resources will be used.

3. Create a git repository called maps
4. For each map, add a directory to the repository with the name of your map -- this will be used in the path for frontend. 

For example your repository directory could look like this:
```
./
../
.git/
README.md
accidents/
  config.json
property-value/
  config.json
311-calls-2018/
  config.json
```
Associated maps will be available at:
* `https://NGSITE.com/maps/accidents`
* `https://NGSITE.com/maps/property-value`
* `https://NGSITE.com/maps/311-calls-2018`
5. Add a valid config file to each directory, for example:



## Configuration

One `config.json` per directory.

### Via iframe

To load map via iframe create carto map, publish and copy iframe link into config, as follows:

```json
{
  "type": "iframe",
  "url": "{PASTE URL HERE}"
}
```

### Via cartoVL


```json
{
  "type": "cartoVL",
  "map": {
    "container": "map",
    "style": "https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json",
    "center": [-73.5673, 45.5017],
    "zoom": 12
  },
  "layers": [
    {
      "source": "accidents_2012_2017",
      "viz": "color: ramp(buckets(prop('nb_victimes_total'), [1, 1, 2, 3, 4, 5, 10, 100]), Prism)"
    }
  ]
}
```

#### type

* `cartoVL`

#### map 

mapboxgl [Map options object](https://docs.mapbox.com/mapbox-gl-js/api/#map)  

Some optional attributes include:

- **container** the id of the div to load the map, should be `map` to use the default plugin template
- **style** path to carto basemap style object
- **center** geographic center of map in `[LONG, LAT]` format

##### example

```json
"map": {
  "container": "map",
  "style": "https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json",
  "center": [-73.5673, 45.5017],
  "zoom": 12
},
```

For more detailed options see the [mapboxgl docs](https://docs.mapbox.com/mapbox-gl-js/api/#map)

#### layers

An array of layer objects consisting of:

- **source** - the name of the carto resource
- **viz** a Viz definition based on [carto expressions](https://carto.com/developers/carto-vl/reference/#cartoexpressions) -- **USE STRING SYNTAX NOT JAVASCRIPT SYNTAX**

##### example

```json
"layers": [
  {
    "source": "accidents_2012_2017",
    "viz": "color: ramp(buckets(prop('nb_victimes_total'), [1, 10, 100]), Prism)"
  }
]
```
