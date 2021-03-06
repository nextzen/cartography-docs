# Get started with Mapzen basemaps

_You will need a free Mapzen API key to use the basemaps. Visit https://mapzen.com/developers to get yours now._

_Mapzen basemaps are written in Tangram's scene file syntax. They can be displayed in web maps using [Tangram JS](
https://mapzen.com/documentation/tangram/Javascript-API/) or [mapzen.js](https://mapzen.com/documentation/mapzen-js/) and on [iOS](https://mapzen.com/documentation/ios/) and [Android](https://mapzen.com/documentation/tangram/android-walkthrough/) using [Tangram ES](https://github.com/tangrams/tangram-es)._

## Add a basemap to a project

There are two convenient methods to incorporate Mapzen basemaps into your project:

### mapzen.js

[mapzen.js](https://mapzen.com/documentation/mapzen-js/) is an easy way to embed Mapzen basemaps into web pages. mapzen.js wraps Leaflet, Tangram, and Mapzen basemaps into an general toolkit.

For example:

```
L.Mapzen.apiKey = 'your-mapzen-api-key';

var map = L.Mapzen.map('map', {
  tangramOptions: {
    scene: {
      import: L.Mapzen.BasemapStyles.Refill
    }
  }
})
```

See the mapzen.js [Get Started](https://mapzen.com/documentation/mapzen-js/get-started/) guide for full examples.

**mapzen.js basemap styles**

The [API reference](https://mapzen.com/documentation/mapzen-js/api-reference/#basemap-styles) lists out all named Mapzen basemap styles and is currently:

* **[Bubble Wrap](https://mapzen.com/products/maps/bubble-wrap)**
    * `L.Mapzen.BasemapStyles.BubbleWrap`
    * `L.Mapzen.BasemapStyles.BubbleWrapMoreLabels`
    * `L.Mapzen.BasemapStyles.BubbleWrapNoLabels`
* **[Refill](https://mapzen.com/products/maps/refill/more-labels)**
    * `L.Mapzen.BasemapStyles.Refill`
    * `L.Mapzen.BasemapStyles.RefillMoreLabels`
    * `L.Mapzen.BasemapStyles.RefillNoLabels`
* **[Walkabout](https://mapzen.com/products/maps/walkabout/more-labels)**
    * `L.Mapzen.BasemapStyles.Walkabout`
    * `L.Mapzen.BasemapStyles.WalkaboutMoreLabels`
    * `L.Mapzen.BasemapStyles.WalkaboutNoLabels`
* **[Tron](https://mapzen.com/products/maps/tron/more-labels)**
    * `L.Mapzen.BasemapStyles.Tron`
    * `L.Mapzen.BasemapStyles.TronMoreLabels`
    * `L.Mapzen.BasemapStyles.TronNoLabels`
* **[Cinnabar](https://mapzen.com/products/maps/cinnabar/more-labels)**
    * `L.Mapzen.BasemapStyles.Cinnabar`
    * `L.Mapzen.BasemapStyles.CinnabarMoreLabels`
    * `L.Mapzen.BasemapStyles.CinnabarNoLabels`

_Note: Zinc has been retired as a standalone basemap style but is now available as a Refill color theme._

### Tangram

You can also use Mapzen's GL map renderer, [Tangram](https://mapzen.com/documentation/tangram/) to add basemaps to your project.

Tangram's scene import syntax ([documentation](https://mapzen.com/documentation/tangram/import/)) allows one scene file to import another:

```
import: https://mapzen.com/carto/refill-style/9/refill-style.yaml

global:
    sdk_mapzen_api_key: your-mapzen-api-key
```

Scene files and related assets are available for use in Tangram and Leaflet directly via the Mapzen CDN.

**Template**

* `https://mapzen.com/carto/{stylename}/{stylefile}.{format}`

Where `{stylename}` and `{stylefile}` are generally the same and will likely converge in future versions.

And where `{format}` is mostly `yaml` but Tangram scene file bundles can also be specified as `zip`.

Looking to peg to a specific **version** of a style? We have you covered!

* `https://mapzen.com/carto/{stylename}/{version}/{stylefile}.{format}`

Where {version} is optional and can be major (eg: `1`), major + minor (`1.0`), or major + minor + patch (`1.0.0`).

**Partial listing of Refill versions:**

In this case, these all resolve to the same asset.

* `https://mapzen.com/carto/refill-style/1/refill-style.zip`
* `https://mapzen.com/carto/refill-style/1.0/refill-style.zip`
* `https://mapzen.com/carto/refill-style/1.0.0/refill-style.zip`

**Mapzen CDN basemap styles**

* **Bubble Wrap**
    * `https://mapzen.com/carto/bubble-wrap-style/bubble-wrap.zip`
* **Refill**
    * `https://mapzen.com/carto/refill-style/refill-style.zip`
* **Walkabout**
    * `https://mapzen.com/carto/walkabout-style/walkabout-style.zip`
* **Tron**
    * `https://mapzen.com/carto/tron-style/tron-style.zip`
* **Cinnabar**
    * `https://mapzen.com/carto/cinnabar-style/cinnabar-style.zip`

## Customize basemap

Modify Mapzen basemap styles using the scene file's global properties. See [API reference](api-reference.md) for details.

For example, modify the default labels in Bubble Wrap to show Kannada, an Indian language:

```
import: https://mapzen.com/carto/bubble-wrap-style/bubble-wrap.yaml

global:
    ux_language: kn
```

## Data visualization

Import Mapzen basemaps into your own Tangram project and overlay your own data.

For example:

```
import: https://mapzen.com/carto/refill-style/9/refill-style.yaml

sources:
    polygons_in_polls:
        type: GeoJSON
        url: https://gist.githubusercontent.com/burritojustice/e80e4b55c0fecd6f93cc8dae20ac2686/raw/c350c17d0697a52e73dc39ab261f4d0f14ca1afa/LAC_neightborhoods_polling_places_2014_general.geojson

styles:
    choropleth:
        base: polygons
        blend: multiply

layers:
    my_data_viz:
        data: { source: polygons_in_polls}
        draw:
            choropleth:
                order: global.sdk_order_under_roads_0
                color: |
                    function() {
                        var count = feature.poll_count;
                        var OrRd = ['fef0d9', 'fdcc8a', 'fc8d59', 'e34a33', 'b30000'];
                        var color =
                        count = 0 ? '000' :
                        count < 15 ? OrRd[0] :
                        count < 30 ? OrRd[1] :
                        count < 60 ? OrRd[2] :
                        count < 120 ? OrRd[3] :
                        OrRd[4] ;
                        return "#" + color;
                    }

```

## Tile size

Mapzen basemap styles use `512` pixel sized vector and terrain tiles to reduce API and network requests, overall latency, and improve label placements in Tangram. The following versions introduced `512` pixel tiles:

* Bubble Wrap: `8.0.0` and later
* Cinnabar: `8.0.0` and later
* Refill: `9.0.0` and later
* Tron: `5.0.0` and later
* Walkabout: `6.0.0` and later

Earlier versions of Mapzen basemap styles used `256` tiles before September 2017.
