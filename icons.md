# Icon Library

Mapzen basemap styles include custom icons to display points of interest on a map, ranging from airports to zoos. These can be used interchangeably between the different basemaps or in a custom [Tangram map](https://mapzen.com/documentation/tangram) of your own.

The library has expanded to a several hundred icons. Most, but not all icons, are available in 4 or more styles.

There are no rights restrictions on the icons. The examples below are for Tangram but you are free to use the icons in your favorite mapping library or application. The original Illustrator [vector artwork](https://github.com/tangrams/icons) is also available.

## Using built-in sprites

Icons can be added to a Tangram map using the [sprites property](https://mapzen.com/documentation/tangram/draw/#sprite) of the `mapzen_icon_library` draw style.

### By icon name

Import the Refill basemap style (which includes the Mapzen icon library) and draw user-provided points on the map using the library's **zoo** icon.

```
import:
    - https://mapzen.com/carto/refill-style/9/refill-style.zip

sources:
    my-source:
        type: GeoJSON
        url:  https://example.com/filename.geojson

layers:
    my-layer:
        data:
            source: my-source
        draw:
            mapzen_icon_library:
                sprite: zoo
```

### Data-driven styling

Data-driven styling is supported when your data includes a `kind` property with values matched to the icon names in the table. Data is evaluated on a per-feature basis so you'll end up with a variety of icons shown on the map.

```
import:
    - https://mapzen.com/carto/refill-style/9/refill-style.zip

sources:
    my-source:
        type: GeoJSON
        url:  https://example.com/filename.geojson

layers:
    my-layer:
        data:
            source: my-source
        draw:
            mapzen_icon_library: {}
```

### Bring your own classification

Sprites can be defined with a Javascript function that allows remapping property values to the named icons in the library.

```
import:
    - https://mapzen.com/carto/refill-style/9/refill-style.zip

sources:
    my-source:
        type: GeoJSON
        url:  https://example.com/filename.geojson

layers:
    my-layer:
        data:
            source: my-source
        draw:
            mapzen_icon_library:
                sprite: |
                    function() {
                        var class = feature.class;
                        var kind = class == 'my_airport'   ? 'airport'  :
                                   class == 'my_hospital'  ? 'hospital' :
                                   class == 'my_zoo'       ? 'zoo'      :
                                   'generic';
                        return kind;
                    }
```

## Using Mapzen icons independently

### Tangram

You can use the icons in the Mapzen icon library independent of Mapzen basemap styles by importing just the icon bundle into a Tangram scene. 

* `https://mapzen.com/carto/bubble-wrap-style/8/themes/bubble-wrap-icons.zip`
* `https://mapzen.com/carto/cinnabar-style/8/themes/cinnabar-icons.zip`
* `https://mapzen.com/carto/refill-style/9/themes/refill-icons.zip`
* `https://mapzen.com/carto/tron-style/5/themes/tron-icons.zip`
* `https://mapzen.com/carto/walkabout-style/6/themes/walkabout-icons.zip`
* `https://mapzen.com/carto/sdk-default-style/1/themes/sdk-default-icons.zip`

For example:

```
import:
    - https://mapzen.com/carto/refill-style/9/themes/refill-icons.zip

sources:
    my-source:
        type: GeoJSON
        url:  https://example.com/filename.geojson

layers:
    my-layer:
        data:
            source: my-source
        draw:
            mapzen_icon_library:
                sprite: zoo
```

### Sprites

The Mapzen Icon Library is available for use in your favorite mapping or graphics software as individual sprite images.

Currently only only `png` format at `2x` resolution is supported.

* `https://mapzen.com/carto/bubble-wrap-style/8/icons/{resolution}/{sprite}.{format}`
* `https://mapzen.com/carto/cinnabar-style/8/icons/{resolution}/{sprite}.{format}`
* `https://mapzen.com/carto/refill-style/9/icons/{resolution}/{sprite}.{format}`
* `https://mapzen.com/carto/tron-style/5/icons/{resolution}/{sprite}.{format}`
* `https://mapzen.com/carto/walkabout-style/6/icons/{resolution}/{sprite}.{format}`
* `https://mapzen.com/carto/sdk-default-style/1/icons/{resolution}/{sprite}.{format}`

**For example:**

Load the `adit` sprite in the **Bubble Wrap** style at `2x` in `png` format:

```
https://mapzen.com/carto/bubble-wrap-style/8/icons/2x/adit.png
```

## Customize icon colors

You can customize the icon colors by changing the global color of colorized-icons in styles. Assign the color in the global u_tint. If you would like to color the badge fill area, assign the color in the draw layer. See below:

```
import:
    - https://mapzen.com/carto/refill-style/9/themes/refill-icons.zip

sources:
    my-source:
        type: GeoJSON
        url:  https://example.com/filename.geojson

styles:
    colorized-icons:
        shaders:
            uniforms:
                # color the icon here
                u_tint: [0.925,0.090,0.094]

layers:
    my-layer:
        data:
            source: my-source
        draw:
            mapzen_icon_library:
                # color the badge fill area here
                color: [0.724,1.000,0.893]
                sprite: zoo
```

### Mix and match icon styles

You could even use the Bubble Wrap icons on Refill!

```
import:
    - https://mapzen.com/carto/refill-style/9/refill-style.zip
    - https://mapzen.com/carto/bubble-wrap-style/8/themes/bubble-wrap-icons.zip
```

## Sprites

Sprite names generally match the `kind` values from the [Mapzen vector tiles](https://mapzen.com/documentation/vector-tiles/layers/#points-of-interest) points of interest (pois) layer.

Some exceptions:

- [Populated places](https://mapzen.com/documentation/vector-tiles/layers/#places) that are displayed as point features (capitals, cities, and towns for instance) use the `capital` or `townspot` icons, respectively.
- Icons for sports pitches and religious places of worship are based on `kind_detail`.
- Road shields are generally sourced from the `network` values in the [roads layer](https://mapzen.com/documentation/vector-tiles/layers/#roads-transportation)
- User experience assets are prefixed with `ux-`.


sprite | Bubble Wrap | Walkabout | Tron | Refill | Cinnabar
:----- | :---------: | :-------: | :--: | :----: | :------:
adit | ![adit](img/sprite/bubble-wrap-style/2x/adit.png) | ![adit](img/sprite/walkabout-style/2x/adit.png) | ![adit](img/sprite/tron-style/2x/adit.png) | ![adit](img/sprite/refill-style/2x/adit.png) | ![adit](img/sprite/refill-style/2x/adit.png)
aerodrome | ![aerodrome](img/sprite/bubble-wrap-style/2x/aerodrome.png) | ![aerodrome](img/sprite/walkabout-style/2x/aerodrome.png) | ![aerodrome](img/sprite/tron-style/2x/aerodrome.png) | ![aerodrome](img/sprite/refill-style/2x/aerodrome.png) | ![aerodrome](img/sprite/refill-style/2x/aerodrome.png)
airport | ![airport](img/sprite/bubble-wrap-style/2x/airport.png) | ![airport](img/sprite/walkabout-style/2x/airport.png) | ![airport](img/sprite/tron-style/2x/airport.png) | ![airport](img/sprite/refill-style/2x/airport.png) | ![airport](img/sprite/refill-style/2x/airport.png)
airport-l | | | ![airport-l](img/sprite/tron-style/2x/airport-l.png) | | |
alcohol | ![alcohol](img/sprite/bubble-wrap-style/2x/alcohol.png) | ![alcohol](img/sprite/walkabout-style/2x/alcohol.png) | ![alcohol](img/sprite/tron-style/2x/alcohol.png) | ![alcohol](img/sprite/refill-style/2x/alcohol.png) | ![alcohol](img/sprite/refill-style/2x/alcohol.png)
allotments | | ![allotments](img/sprite/walkabout-style/2x/allotments.png) | | | |
amusement_ride | ![amusement_ride](img/sprite/bubble-wrap-style/2x/amusement_ride.png) | ![amusement_ride](img/sprite/walkabout-style/2x/amusement_ride.png) | ![amusement_ride](img/sprite/tron-style/2x/amusement_ride.png) | ![amusement_ride](img/sprite/refill-style/2x/amusement_ride.png) | ![amusement_ride](img/sprite/refill-style/2x/amusement_ride.png)
apartments | ![apartments](img/sprite/bubble-wrap-style/2x/apartments.png) | ![apartments](img/sprite/walkabout-style/2x/apartments.png) | ![apartments](img/sprite/tron-style/2x/apartments.png) | ![apartments](img/sprite/refill-style/2x/apartments.png) | ![apartments](img/sprite/refill-style/2x/apartments.png)
aquarium | ![aquarium](img/sprite/bubble-wrap-style/2x/aquarium.png) | ![aquarium](img/sprite/walkabout-style/2x/aquarium.png) | ![aquarium](img/sprite/tron-style/2x/aquarium.png) | ![aquarium](img/sprite/refill-style/2x/aquarium.png) | ![aquarium](img/sprite/refill-style/2x/aquarium.png)
archaeological_site | ![archaeological_site](img/sprite/bubble-wrap-style/2x/archaeological_site.png) | ![archaeological_site](img/sprite/walkabout-style/2x/archaeological_site.png) | ![archaeological_site](img/sprite/tron-style/2x/archaeological_site.png) | ![archaeological_site](img/sprite/refill-style/2x/archaeological_site.png) | ![archaeological_site](img/sprite/refill-style/2x/archaeological_site.png)
atm | ![atm](img/sprite/bubble-wrap-style/2x/atm.png) | ![atm](img/sprite/walkabout-style/2x/atm.png) | ![atm](img/sprite/tron-style/2x/atm.png) | ![atm](img/sprite/refill-style/2x/atm.png) | ![atm](img/sprite/refill-style/2x/atm.png)
attraction | | ![attraction](img/sprite/walkabout-style/2x/attraction.png) | | | |
bakery | ![bakery](img/sprite/bubble-wrap-style/2x/bakery.png) | ![bakery](img/sprite/walkabout-style/2x/bakery.png) | ![bakery](img/sprite/tron-style/2x/bakery.png) | ![bakery](img/sprite/refill-style/2x/bakery.png) | ![bakery](img/sprite/refill-style/2x/bakery.png)
bank | ![bank](img/sprite/bubble-wrap-style/2x/bank.png) | ![bank](img/sprite/walkabout-style/2x/bank.png) | ![bank](img/sprite/tron-style/2x/bank.png) | ![bank](img/sprite/refill-style/2x/bank.png) | ![bank](img/sprite/refill-style/2x/bank.png)
bar | ![bar](img/sprite/bubble-wrap-style/2x/bar.png) | ![bar](img/sprite/walkabout-style/2x/bar.png) | ![bar](img/sprite/tron-style/2x/bar.png) | ![bar](img/sprite/refill-style/2x/bar.png) | ![bar](img/sprite/refill-style/2x/bar.png)
baseball | ![baseball](img/sprite/bubble-wrap-style/2x/baseball.png) | ![baseball](img/sprite/walkabout-style/2x/baseball.png) | ![baseball](img/sprite/tron-style/2x/baseball.png) | ![baseball](img/sprite/refill-style/2x/baseball.png) | ![baseball](img/sprite/refill-style/2x/baseball.png)
basketball | ![basketball](img/sprite/bubble-wrap-style/2x/basketball.png) | ![basketball](img/sprite/walkabout-style/2x/basketball.png) | ![basketball](img/sprite/tron-style/2x/basketball.png) | ![basketball](img/sprite/refill-style/2x/basketball.png) | ![basketball](img/sprite/refill-style/2x/basketball.png)
battlefield | ![battlefield](img/sprite/bubble-wrap-style/2x/battlefield.png) | ![battlefield](img/sprite/walkabout-style/2x/battlefield.png) | ![battlefield](img/sprite/tron-style/2x/battlefield.png) | | |
bbq | | ![bbq](img/sprite/walkabout-style/2x/bbq.png) | | | |
beach | ![beach](img/sprite/bubble-wrap-style/2x/beach.png) | ![beach](img/sprite/walkabout-style/2x/beach.png) | ![beach](img/sprite/tron-style/2x/beach.png) | ![beach](img/sprite/refill-style/2x/beach.png) | ![beach](img/sprite/refill-style/2x/beach.png)
beach_resort | | ![beach_resort](img/sprite/walkabout-style/2x/beach_resort.png)| | | |
beacon | ![beacon](img/sprite/bubble-wrap-style/2x/beacon.png) | ![beacon](img/sprite/walkabout-style/2x/beacon.png) | ![beacon](img/sprite/tron-style/2x/beacon.png) | ![beacon](img/sprite/refill-style/2x/beacon.png) | ![beacon](img/sprite/refill-style/2x/beacon.png)
bench | ![bench](img/sprite/bubble-wrap-style/2x/bench.png) | ![bench](img/sprite/walkabout-style/2x/bench.png) | ![bench](img/sprite/tron-style/2x/bench.png) | ![bench](img/sprite/refill-style/2x/bench.png) | ![bench](img/sprite/refill-style/2x/bench.png)
bicycle | ![bicycle](img/sprite/bubble-wrap-style/2x/bicycle.png) | ![bicycle](img/sprite/walkabout-style/2x/bicycle.png) | ![bicycle](img/sprite/tron-style/2x/bicycle.png) | ![bicycle](img/sprite/refill-style/2x/bicycle.png) | ![bicycle](img/sprite/refill-style/2x/bicycle.png)
bicycle_parking | ![bicycle_parking](img/sprite/bubble-wrap-style/2x/bicycle_parking.png) | ![bicycle_parking](img/sprite/walkabout-style/2x/bicycle_parking.png) | ![bicycle_parking](img/sprite/tron-style/2x/bicycle_parking.png) | ![bicycle_parking](img/sprite/refill-style/2x/bicycle_parking.png) | ![bicycle_parking](img/sprite/refill-style/2x/bicycle_parking.png)
bicycle_rental | ![bicycle_rental](img/sprite/bubble-wrap-style/2x/bicycle_rental.png) | ![bicycle_rental](img/sprite/walkabout-style/2x/bicycle_rental.png) | ![bicycle_rental](img/sprite/tron-style/2x/bicycle_rental.png) | ![bicycle_rental](img/sprite/refill-style/2x/bicycle_rental.png) | ![bicycle_rental](img/sprite/refill-style/2x/bicycle_rental.png)
bicycle_rental_station | ![bicycle_rental_station](img/sprite/bubble-wrap-style/2x/bicycle_rental_station.png) | ![bicycle_rental_station](img/sprite/walkabout-style/2x/bicycle_rental_station.png) | ![bicycle_rental_station](img/sprite/tron-style/2x/bicycle_rental_station.png) | ![bicycle_rental_station](img/sprite/refill-style/2x/bicycle_rental_station.png) | ![bicycle_rental_station](img/sprite/refill-style/2x/bicycle_rental_station.png)
biergarten | ![biergarten](img/sprite/bubble-wrap-style/2x/biergarten.png) | ![biergarten](img/sprite/walkabout-style/2x/biergarten.png) | ![biergarten](img/sprite/tron-style/2x/biergarten.png) | ![biergarten](img/sprite/refill-style/2x/biergarten.png) | ![biergarten](img/sprite/refill-style/2x/biergarten.png)
boat_rental | | ![boat_rental](img/sprite/walkabout-style/2x/boat_rental.png) | | | |
books | ![books](img/sprite/bubble-wrap-style/2x/books.png) | ![books](img/sprite/walkabout-style/2x/books.png) | ![books](img/sprite/tron-style/2x/books.png) | ![books](img/sprite/refill-style/2x/books.png) | ![books](img/sprite/refill-style/2x/books.png)
brewery | ![brewery](img/sprite/bubble-wrap-style/2x/brewery.png) | ![brewery](img/sprite/walkabout-style/2x/brewery.png) | ![brewery](img/sprite/tron-style/2x/brewery.png) | ![brewery](img/sprite/refill-style/2x/brewery.png) | ![brewery](img/sprite/refill-style/2x/brewery.png)
bridge | ![bridge](img/sprite/bubble-wrap-style/2x/bridge.png) | ![bridge](img/sprite/walkabout-style/2x/bridge.png) | ![bridge](img/sprite/tron-style/2x/bridge.png) | ![bridge](img/sprite/refill-style/2x/bridge.png) | ![bridge](img/sprite/refill-style/2x/bridge.png)
buddhist | ![buddhist](img/sprite/bubble-wrap-style/2x/buddhist.png) | ![buddhist](img/sprite/walkabout-style/2x/buddhist.png) | ![buddhist](img/sprite/tron-style/2x/buddhist.png) | ![buddhist](img/sprite/refill-style/2x/buddhist.png) | ![buddhist](img/sprite/refill-style/2x/buddhist.png)
building | ![building](img/sprite/bubble-wrap-style/2x/building.png) | ![building](img/sprite/walkabout-style/2x/building.png) | ![building](img/sprite/tron-style/2x/building.png) | ![building](img/sprite/refill-style/2x/building.png) | ![building](img/sprite/refill-style/2x/building.png)
bus_station | ![bus_station](img/sprite/bubble-wrap-style/2x/bus_station.png) | ![bus_station](img/sprite/walkabout-style/2x/bus_station.png) | ![bus_station](img/sprite/tron-style/2x/bus_station.png) | ![bus_station](img/sprite/refill-style/2x/bus_station.png) | ![bus_station](img/sprite/refill-style/2x/bus_station.png)
bus_stop | ![bus_stop](img/sprite/bubble-wrap-style/2x/bus_stop.png) | ![bus_stop](img/sprite/walkabout-style/2x/bus_stop.png) | ![bus_stop](img/sprite/tron-style/2x/bus_stop.png) | ![bus_stop](img/sprite/refill-style/2x/bus_stop.png) | ![bus_stop](img/sprite/refill-style/2x/bus_stop.png)
butcher | ![butcher](img/sprite/bubble-wrap-style/2x/butcher.png) | ![butcher](img/sprite/walkabout-style/2x/butcher.png) | ![butcher](img/sprite/tron-style/2x/butcher.png) | ![butcher](img/sprite/refill-style/2x/butcher.png) | ![butcher](img/sprite/refill-style/2x/butcher.png)
cafe | ![cafe](img/sprite/bubble-wrap-style/2x/cafe.png) | ![cafe](img/sprite/walkabout-style/2x/cafe.png) | ![cafe](img/sprite/tron-style/2x/cafe.png) | ![cafe](img/sprite/refill-style/2x/cafe.png) | ![cafe](img/sprite/refill-style/2x/cafe.png)
camp_site | ![camp_site](img/sprite/bubble-wrap-style/2x/camp_site.png) | ![camp_site](img/sprite/walkabout-style/2x/camp_site.png) | ![camp_site](img/sprite/tron-style/2x/camp_site.png) | ![camp_site](img/sprite/refill-style/2x/camp_site.png) | ![camp_site](img/sprite/refill-style/2x/camp_site.png)
capital-l | ![capital-l](img/sprite/bubble-wrap-style/2x/capital-l.png) | ![capital-l](img/sprite/walkabout-style/2x/capital-l.png) | ![capital-l](img/sprite/tron-style/2x/capital-l.png) | ![capital-l](img/sprite/refill-style/2x/capital-l.png) | ![capital-l](img/sprite/refill-style/2x/capital-l.png)
capital-m | ![capital-m](img/sprite/bubble-wrap-style/2x/capital-m.png) | ![capital-m](img/sprite/walkabout-style/2x/capital-m.png) | ![capital-m](img/sprite/tron-style/2x/capital-m.png) | ![capital-m](img/sprite/refill-style/2x/capital-m.png) | ![capital-m](img/sprite/refill-style/2x/capital-m.png)
capital-s | ![capital-s](img/sprite/bubble-wrap-style/2x/capital-s.png) | ![capital-s](img/sprite/walkabout-style/2x/capital-s.png) | ![capital-s](img/sprite/tron-style/2x/capital-s.png) | ![capital-s](img/sprite/refill-style/2x/capital-s.png) | ![capital-s](img/sprite/refill-style/2x/capital-s.png)
capital-xl | ![capital-xl](img/sprite/bubble-wrap-style/2x/capital-xl.png) | ![capital-xl](img/sprite/walkabout-style/2x/capital-xl.png) | ![capital-xl](img/sprite/tron-style/2x/capital-xl.png) | ![capital-xl](img/sprite/refill-style/2x/capital-xl.png) | ![capital-xl](img/sprite/refill-style/2x/capital-xl.png)
capital-xs | ![capital-xs](img/sprite/bubble-wrap-style/2x/capital-xs.png) | ![capital-xs](img/sprite/walkabout-style/2x/capital-xs.png) | ![capital-xs](img/sprite/tron-style/2x/capital-xs.png) | ![capital-xs](img/sprite/refill-style/2x/capital-xs.png) | ![capital-xs](img/sprite/refill-style/2x/capital-xs.png)
car | ![car](img/sprite/bubble-wrap-style/2x/car.png) | ![car](img/sprite/walkabout-style/2x/car.png) | ![car](img/sprite/tron-style/2x/car.png) | ![car](img/sprite/refill-style/2x/car.png) | ![car](img/sprite/refill-style/2x/car.png)
car_repair | ![car_repair](img/sprite/bubble-wrap-style/2x/car_repair.png) | ![car_repair](img/sprite/walkabout-style/2x/car_repair.png) | ![car_repair](img/sprite/tron-style/2x/car_repair.png) | ![car_repair](img/sprite/refill-style/2x/car_repair.png) | ![car_repair](img/sprite/refill-style/2x/car_repair.png)
car_sharing | ![car_sharing](img/sprite/bubble-wrap-style/2x/car_sharing.png) | ![car_sharing](img/sprite/walkabout-style/2x/car_sharing.png) | ![car_sharing](img/sprite/tron-style/2x/car_sharing.png) | ![car_sharing](img/sprite/refill-style/2x/car_sharing.png) | ![car_sharing](img/sprite/refill-style/2x/car_sharing.png)
caravan_site | ![caravan_site](img/sprite/bubble-wrap-style/2x/caravan_site.png) | ![caravan_site](img/sprite/walkabout-style/2x/caravan_site.png) | | | |
care_home | ![care_home](img/sprite/bubble-wrap-style/2x/care_home.png) | ![care_home](img/sprite/walkabout-style/2x/care_home.png) | ![care_home](img/sprite/tron-style/2x/care_home.png) | ![care_home](img/sprite/refill-style/2x/care_home.png) | ![care_home](img/sprite/refill-style/2x/care_home.png)
castle | ![castle](img/sprite/bubble-wrap-style/2x/castle.png) | ![castle](img/sprite/walkabout-style/2x/castle.png) | ![castle](img/sprite/tron-style/2x/castle.png) | ![castle](img/sprite/refill-style/2x/castle.png) | ![castle](img/sprite/refill-style/2x/castle.png)
category-namespace-do_and_see | ![category-namespace-do_and_see](img/sprite/bubble-wrap-style/2x/category-namespace-do_and_see.png) | ![category-namespace-do_and_see](img/sprite/walkabout-style/2x/category-namespace-do_and_see.png) | ![category-namespace-do_and_see](img/sprite/tron-style/2x/category-namespace-do_and_see.png) | ![category-namespace-do_and_see](img/sprite/refill-style/2x/category-namespace-do_and_see.png) | ![category-namespace-do_and_see](img/sprite/refill-style/2x/category-namespace-do_and_see.png)
category-namespace-eat_and_drink | ![category-namespace-eat_and_drink](img/sprite/bubble-wrap-style/2x/category-namespace-eat_and_drink.png) | ![category-namespace-eat_and_drink](img/sprite/walkabout-style/2x/category-namespace-eat_and_drink.png) | ![category-namespace-eat_and_drink](img/sprite/tron-style/2x/category-namespace-eat_and_drink.png) | ![category-namespace-eat_and_drink](img/sprite/refill-style/2x/category-namespace-eat_and_drink.png) | ![category-namespace-eat_and_drink](img/sprite/refill-style/2x/category-namespace-eat_and_drink.png)
category-namespace-education_and_religion | ![category-namespace-education_and_religion](img/sprite/bubble-wrap-style/2x/category-namespace-education_and_religion.png) | ![category-namespace-education_and_religion](img/sprite/walkabout-style/2x/category-namespace-education_and_religion.png) | ![category-namespace-education_and_religion](img/sprite/tron-style/2x/category-namespace-education_and_religion.png) | ![category-namespace-education_and_religion](img/sprite/refill-style/2x/category-namespace-education_and_religion.png) | ![category-namespace-education_and_religion](img/sprite/refill-style/2x/category-namespace-education_and_religion.png)
category-namespace-health | ![category-namespace-health](img/sprite/bubble-wrap-style/2x/category-namespace-health.png) | ![category-namespace-health](img/sprite/walkabout-style/2x/category-namespace-health.png) | ![category-namespace-health](img/sprite/tron-style/2x/category-namespace-health.png) | ![category-namespace-health](img/sprite/refill-style/2x/category-namespace-health.png) | ![category-namespace-health](img/sprite/refill-style/2x/category-namespace-health.png)
category-namespace-mobility | ![category-namespace-mobility](img/sprite/bubble-wrap-style/2x/category-namespace-mobility.png) | ![category-namespace-mobility](img/sprite/walkabout-style/2x/category-namespace-mobility.png) | ![category-namespace-mobility](img/sprite/tron-style/2x/category-namespace-mobility.png) | ![category-namespace-mobility](img/sprite/refill-style/2x/category-namespace-mobility.png) | ![category-namespace-mobility](img/sprite/refill-style/2x/category-namespace-mobility.png)
category-namespace-other | ![category-namespace-other](img/sprite/bubble-wrap-style/2x/category-namespace-other.png) | ![category-namespace-other](img/sprite/walkabout-style/2x/category-namespace-other.png) | ![category-namespace-other](img/sprite/tron-style/2x/category-namespace-other.png) | ![category-namespace-other](img/sprite/refill-style/2x/category-namespace-other.png) | ![category-namespace-other](img/sprite/refill-style/2x/category-namespace-other.png)
category-namespace-shop_and_service | ![category-namespace-shop_and_service](img/sprite/bubble-wrap-style/2x/category-namespace-shop_and_service.png) | ![category-namespace-shop_and_service](img/sprite/walkabout-style/2x/category-namespace-shop_and_service.png) | ![category-namespace-shop_and_service](img/sprite/tron-style/2x/category-namespace-shop_and_service.png) | ![category-namespace-shop_and_service](img/sprite/refill-style/2x/category-namespace-shop_and_service.png) | ![category-namespace-shop_and_service](img/sprite/refill-style/2x/category-namespace-shop_and_service.png)
category-predicate-addressing | ![category-predicate-addressing](img/sprite/bubble-wrap-style/2x/category-predicate-addressing.png) | ![category-predicate-addressing](img/sprite/walkabout-style/2x/category-predicate-addressing.png) | ![category-predicate-addressing](img/sprite/tron-style/2x/category-predicate-addressing.png) | ![category-predicate-addressing](img/sprite/refill-style/2x/category-predicate-addressing.png) | ![category-predicate-addressing](img/sprite/refill-style/2x/category-predicate-addressing.png)
category-predicate-attraction | ![category-predicate-attraction](img/sprite/bubble-wrap-style/2x/category-predicate-attraction.png) | ![category-predicate-attraction](img/sprite/walkabout-style/2x/category-predicate-attraction.png) | ![category-predicate-attraction](img/sprite/tron-style/2x/category-predicate-attraction.png) | ![category-predicate-attraction](img/sprite/refill-style/2x/category-predicate-attraction.png) | ![category-predicate-attraction](img/sprite/refill-style/2x/category-predicate-attraction.png)
category-predicate-civic | ![category-predicate-civic](img/sprite/bubble-wrap-style/2x/category-predicate-civic.png) | ![category-predicate-civic](img/sprite/walkabout-style/2x/category-predicate-civic.png) | ![category-predicate-civic](img/sprite/tron-style/2x/category-predicate-civic.png) | ![category-predicate-civic](img/sprite/refill-style/2x/category-predicate-civic.png) | ![category-predicate-civic](img/sprite/refill-style/2x/category-predicate-civic.png)
category-predicate-drink | ![category-predicate-drink](img/sprite/bubble-wrap-style/2x/category-predicate-drink.png) | ![category-predicate-drink](img/sprite/walkabout-style/2x/category-predicate-drink.png) | ![category-predicate-drink](img/sprite/tron-style/2x/category-predicate-drink.png) | ![category-predicate-drink](img/sprite/refill-style/2x/category-predicate-drink.png) | ![category-predicate-drink](img/sprite/refill-style/2x/category-predicate-drink.png)
category-predicate-eat | ![category-predicate-eat](img/sprite/bubble-wrap-style/2x/category-predicate-eat.png) | ![category-predicate-eat](img/sprite/walkabout-style/2x/category-predicate-eat.png) | ![category-predicate-eat](img/sprite/tron-style/2x/category-predicate-eat.png) | ![category-predicate-eat](img/sprite/refill-style/2x/category-predicate-eat.png) | ![category-predicate-eat](img/sprite/refill-style/2x/category-predicate-eat.png)
category-predicate-education | ![category-predicate-education](img/sprite/bubble-wrap-style/2x/category-predicate-education.png) | ![category-predicate-education](img/sprite/walkabout-style/2x/category-predicate-education.png) | ![category-predicate-education](img/sprite/tron-style/2x/category-predicate-education.png) | ![category-predicate-education](img/sprite/refill-style/2x/category-predicate-education.png) | ![category-predicate-education](img/sprite/refill-style/2x/category-predicate-education.png)
category-predicate-fun | ![category-predicate-fun](img/sprite/bubble-wrap-style/2x/category-predicate-fun.png) | ![category-predicate-fun](img/sprite/walkabout-style/2x/category-predicate-fun.png) | ![category-predicate-fun](img/sprite/tron-style/2x/category-predicate-fun.png) | ![category-predicate-fun](img/sprite/refill-style/2x/category-predicate-fun.png) | ![category-predicate-fun](img/sprite/refill-style/2x/category-predicate-fun.png)
category-predicate-health | ![category-predicate-health](img/sprite/bubble-wrap-style/2x/category-predicate-health.png) | ![category-predicate-health](img/sprite/walkabout-style/2x/category-predicate-health.png) | ![category-predicate-health](img/sprite/tron-style/2x/category-predicate-health.png) | ![category-predicate-health](img/sprite/refill-style/2x/category-predicate-health.png) | ![category-predicate-health](img/sprite/refill-style/2x/category-predicate-health.png)
category-predicate-industry | ![category-predicate-industry](img/sprite/bubble-wrap-style/2x/category-predicate-industry.png) | ![category-predicate-industry](img/sprite/walkabout-style/2x/category-predicate-industry.png) | ![category-predicate-industry](img/sprite/tron-style/2x/category-predicate-industry.png) | ![category-predicate-industry](img/sprite/refill-style/2x/category-predicate-industry.png) | ![category-predicate-industry](img/sprite/refill-style/2x/category-predicate-industry.png)
category-predicate-mobility | ![category-predicate-mobility](img/sprite/bubble-wrap-style/2x/category-predicate-mobility.png) | ![category-predicate-mobility](img/sprite/walkabout-style/2x/category-predicate-mobility.png) | ![category-predicate-mobility](img/sprite/tron-style/2x/category-predicate-mobility.png) | ![category-predicate-mobility](img/sprite/refill-style/2x/category-predicate-mobility.png) | ![category-predicate-mobility](img/sprite/refill-style/2x/category-predicate-mobility.png)
category-predicate-money | ![category-predicate-money](img/sprite/bubble-wrap-style/2x/category-predicate-money.png) | ![category-predicate-money](img/sprite/walkabout-style/2x/category-predicate-money.png) | ![category-predicate-money](img/sprite/tron-style/2x/category-predicate-money.png) | ![category-predicate-money](img/sprite/refill-style/2x/category-predicate-money.png) | ![category-predicate-money](img/sprite/refill-style/2x/category-predicate-money.png)
category-predicate-nature | ![category-predicate-nature](img/sprite/bubble-wrap-style/2x/category-predicate-nature.png) | ![category-predicate-nature](img/sprite/walkabout-style/2x/category-predicate-nature.png) | ![category-predicate-nature](img/sprite/tron-style/2x/category-predicate-nature.png) | ![category-predicate-nature](img/sprite/refill-style/2x/category-predicate-nature.png) | ![category-predicate-nature](img/sprite/refill-style/2x/category-predicate-nature.png)
category-predicate-religion | ![category-predicate-religion](img/sprite/bubble-wrap-style/2x/category-predicate-religion.png) | ![category-predicate-religion](img/sprite/walkabout-style/2x/category-predicate-religion.png) | ![category-predicate-religion](img/sprite/tron-style/2x/category-predicate-religion.png) | ![category-predicate-religion](img/sprite/refill-style/2x/category-predicate-religion.png) | ![category-predicate-religion](img/sprite/refill-style/2x/category-predicate-religion.png)
category-predicate-service | ![category-predicate-service](img/sprite/bubble-wrap-style/2x/category-predicate-service.png) | ![category-predicate-service](img/sprite/walkabout-style/2x/category-predicate-service.png) | ![category-predicate-service](img/sprite/tron-style/2x/category-predicate-service.png) | ![category-predicate-service](img/sprite/refill-style/2x/category-predicate-service.png) | ![category-predicate-service](img/sprite/refill-style/2x/category-predicate-service.png)
category-predicate-shop | ![category-predicate-shop](img/sprite/bubble-wrap-style/2x/category-predicate-shop.png) | ![category-predicate-shop](img/sprite/walkabout-style/2x/category-predicate-shop.png) | ![category-predicate-shop](img/sprite/tron-style/2x/category-predicate-shop.png) | ![category-predicate-shop](img/sprite/refill-style/2x/category-predicate-shop.png) | ![category-predicate-shop](img/sprite/refill-style/2x/category-predicate-shop.png)
category-predicate-sleep | ![category-predicate-sleep](img/sprite/bubble-wrap-style/2x/category-predicate-sleep.png) | ![category-predicate-sleep](img/sprite/walkabout-style/2x/category-predicate-sleep.png) | ![category-predicate-sleep](img/sprite/tron-style/2x/category-predicate-sleep.png) | ![category-predicate-sleep](img/sprite/refill-style/2x/category-predicate-sleep.png) | ![category-predicate-sleep](img/sprite/refill-style/2x/category-predicate-sleep.png)
category-predicate-transport | ![category-predicate-transport](img/sprite/bubble-wrap-style/2x/category-predicate-transport.png) | ![category-predicate-transport](img/sprite/walkabout-style/2x/category-predicate-transport.png) | ![category-predicate-transport](img/sprite/tron-style/2x/category-predicate-transport.png) | ![category-predicate-transport](img/sprite/refill-style/2x/category-predicate-transport.png) | ![category-predicate-transport](img/sprite/refill-style/2x/category-predicate-transport.png)
cemetery | ![cemetery](img/sprite/bubble-wrap-style/2x/cemetery.png) | ![cemetery](img/sprite/walkabout-style/2x/cemetery.png) | ![cemetery](img/sprite/tron-style/2x/cemetery.png) | ![cemetery](img/sprite/refill-style/2x/cemetery.png) | ![cemetery](img/sprite/refill-style/2x/cemetery.png)
chapel | ![chapel](img/sprite/bubble-wrap-style/2x/chapel.png) | ![chapel](img/sprite/walkabout-style/2x/chapel.png) | ![chapel](img/sprite/tron-style/2x/chapel.png) | ![chapel](img/sprite/refill-style/2x/chapel.png) | ![chapel](img/sprite/refill-style/2x/chapel.png)
chimney | ![chimney](img/sprite/bubble-wrap-style/2x/chimney.png) | ![chimney](img/sprite/walkabout-style/2x/chimney.png) | ![chimney](img/sprite/tron-style/2x/chimney.png) | ![chimney](img/sprite/refill-style/2x/chimney.png) | ![chimney](img/sprite/refill-style/2x/chimney.png)
christian | ![christian](img/sprite/bubble-wrap-style/2x/christian.png) | ![christian](img/sprite/walkabout-style/2x/christian.png) | ![christian](img/sprite/tron-style/2x/christian.png) | ![christian](img/sprite/refill-style/2x/christian.png) | ![christian](img/sprite/refill-style/2x/christian.png)
cinema | ![cinema](img/sprite/bubble-wrap-style/2x/cinema.png) | ![cinema](img/sprite/walkabout-style/2x/cinema.png) | ![cinema](img/sprite/tron-style/2x/cinema.png) | ![cinema](img/sprite/refill-style/2x/cinema.png) | ![cinema](img/sprite/refill-style/2x/cinema.png)
clinic | | ![clinic](img/sprite/walkabout-style/2x/clinic.png) | | | |
clothes | ![clothes](img/sprite/bubble-wrap-style/2x/clothes.png) | ![clothes](img/sprite/walkabout-style/2x/clothes.png) | ![clothes](img/sprite/tron-style/2x/clothes.png) | ![clothes](img/sprite/refill-style/2x/clothes.png) | ![clothes](img/sprite/refill-style/2x/clothes.png)
college | ![college](img/sprite/bubble-wrap-style/2x/college.png) | ![college](img/sprite/walkabout-style/2x/college.png) | ![college](img/sprite/tron-style/2x/college.png) | ![college](img/sprite/refill-style/2x/college.png) | ![college](img/sprite/refill-style/2x/college.png)
company | ![company](img/sprite/bubble-wrap-style/2x/company.png) | ![company](img/sprite/walkabout-style/2x/company.png) | ![company](img/sprite/tron-style/2x/company.png) | ![company](img/sprite/refill-style/2x/company.png) | ![company](img/sprite/refill-style/2x/company.png)
computer | ![computer](img/sprite/bubble-wrap-style/2x/computer.png) | ![computer](img/sprite/walkabout-style/2x/computer.png) | ![computer](img/sprite/tron-style/2x/computer.png) | ![computer](img/sprite/refill-style/2x/computer.png) | ![computer](img/sprite/refill-style/2x/computer.png)
confectionery | ![confectionery](img/sprite/bubble-wrap-style/2x/confectionery.png) | ![confectionery](img/sprite/walkabout-style/2x/confectionery.png) | ![confectionery](img/sprite/tron-style/2x/confectionery.png) | ![confectionery](img/sprite/refill-style/2x/confectionery.png) | ![confectionery](img/sprite/refill-style/2x/confectionery.png)
conservation | ![conservation](img/sprite/bubble-wrap-style/2x/conservation.png) | ![conservation](img/sprite/walkabout-style/2x/conservation.png) | ![conservation](img/sprite/tron-style/2x/conservation.png) | | |
convenience | ![convenience](img/sprite/bubble-wrap-style/2x/convenience.png) | ![convenience](img/sprite/walkabout-style/2x/convenience.png) | ![convenience](img/sprite/tron-style/2x/convenience.png) | ![convenience](img/sprite/refill-style/2x/convenience.png) | ![convenience](img/sprite/refill-style/2x/convenience.png)
county_shield-1char | ![county_shield-1char](img/sprite/bubble-wrap-style/2x/county_shield-1char.png) | ![county_shield-1char](img/sprite/walkabout-style/2x/county_shield-1char.png) | ![county_shield-1char](img/sprite/tron-style/2x/county_shield-1char.png) | ![county_shield-1char](img/sprite/refill-style/2x/county_shield-1char.png) | ![county_shield-1char](img/sprite/refill-style/2x/county_shield-1char.png)
county_shield-2char | ![county_shield-2char](img/sprite/bubble-wrap-style/2x/county_shield-2char.png) | ![county_shield-2char](img/sprite/walkabout-style/2x/county_shield-2char.png) | ![county_shield-2char](img/sprite/tron-style/2x/county_shield-2char.png) | ![county_shield-2char](img/sprite/refill-style/2x/county_shield-2char.png) | ![county_shield-2char](img/sprite/refill-style/2x/county_shield-2char.png)
county_shield-3char | ![county_shield-3char](img/sprite/bubble-wrap-style/2x/county_shield-3char.png) | ![county_shield-3char](img/sprite/walkabout-style/2x/county_shield-3char.png) | ![county_shield-3char](img/sprite/tron-style/2x/county_shield-3char.png) | ![county_shield-3char](img/sprite/refill-style/2x/county_shield-3char.png) | ![county_shield-3char](img/sprite/refill-style/2x/county_shield-3char.png)
county_shield-4char | ![county_shield-4char](img/sprite/bubble-wrap-style/2x/county_shield-4char.png) | ![county_shield-4char](img/sprite/walkabout-style/2x/county_shield-4char.png) | ![county_shield-4char](img/sprite/tron-style/2x/county_shield-4char.png) | ![county_shield-4char](img/sprite/refill-style/2x/county_shield-4char.png) | ![county_shield-4char](img/sprite/refill-style/2x/county_shield-4char.png)
county_shield-5char | ![county_shield-5char](img/sprite/bubble-wrap-style/2x/county_shield-5char.png) | ![county_shield-5char](img/sprite/walkabout-style/2x/county_shield-5char.png) | ![county_shield-5char](img/sprite/tron-style/2x/county_shield-5char.png) | ![county_shield-5char](img/sprite/refill-style/2x/county_shield-5char.png) | ![county_shield-5char](img/sprite/refill-style/2x/county_shield-5char.png)
courthouse | ![courthouse](img/sprite/bubble-wrap-style/2x/courthouse.png) | ![courthouse](img/sprite/walkabout-style/2x/courthouse.png) | ![courthouse](img/sprite/tron-style/2x/courthouse.png) | ![courthouse](img/sprite/refill-style/2x/courthouse.png) | ![courthouse](img/sprite/refill-style/2x/courthouse.png)
dam | | ![dam](img/sprite/walkabout-style/2x/dam.png) | | | |
dentist | | ![dentist](img/sprite/walkabout-style/2x/dentist.png) | | | |
department_store | ![department_store](img/sprite/bubble-wrap-style/2x/department_store.png) | ![department_store](img/sprite/walkabout-style/2x/department_store.png) | ![department_store](img/sprite/tron-style/2x/department_store.png) | ![department_store](img/sprite/refill-style/2x/department_store.png) | ![department_store](img/sprite/refill-style/2x/department_store.png)
dive_centre | | ![dive_centre](img/sprite/walkabout-style/2x/dive_centre.png) | | | |
dock | ![dock](img/sprite/bubble-wrap-style/2x/dock.png) | ![dock](img/sprite/walkabout-style/2x/dock.png) | ![dock](img/sprite/tron-style/2x/dock.png) | ![dock](img/sprite/refill-style/2x/dock.png) | ![dock](img/sprite/refill-style/2x/dock.png)
doctors | | ![doctors](img/sprite/walkabout-style/2x/doctors.png) | | | |
dog_park | | ![dog_park](img/sprite/walkabout-style/2x/dog_park.png) | | | |
doityourself | ![doityourself](img/sprite/bubble-wrap-style/2x/doityourself.png) | ![doityourself](img/sprite/walkabout-style/2x/doityourself.png) | ![doityourself](img/sprite/tron-style/2x/doityourself.png) | ![doityourself](img/sprite/refill-style/2x/doityourself.png) | ![doityourself](img/sprite/refill-style/2x/doityourself.png)
dot-black | | ![dot-black](img/sprite/walkabout-style/2x/dot-black.png) | | | |
dot-white | | ![dot-white](img/sprite/walkabout-style/2x/dot-white.png) | | | |
drinking_water | ![drinking_water](img/sprite/bubble-wrap-style/2x/drinking_water.png) | ![drinking_water](img/sprite/walkabout-style/2x/drinking_water.png) | ![drinking_water](img/sprite/tron-style/2x/drinking_water.png) | ![drinking_water](img/sprite/refill-style/2x/drinking_water.png) | ![drinking_water](img/sprite/refill-style/2x/drinking_water.png)
dry_cleaning | ![dry_cleaning](img/sprite/bubble-wrap-style/2x/dry_cleaning.png) | ![dry_cleaning](img/sprite/walkabout-style/2x/dry_cleaning.png) | ![dry_cleaning](img/sprite/tron-style/2x/dry_cleaning.png) | ![dry_cleaning](img/sprite/refill-style/2x/dry_cleaning.png) | ![dry_cleaning](img/sprite/refill-style/2x/dry_cleaning.png)
electronics | ![electronics](img/sprite/bubble-wrap-style/2x/electronics.png) | ![electronics](img/sprite/walkabout-style/2x/electronics.png) | ![electronics](img/sprite/tron-style/2x/electronics.png) | ![electronics](img/sprite/refill-style/2x/electronics.png) | ![electronics](img/sprite/refill-style/2x/electronics.png)
embassy | ![embassy](img/sprite/bubble-wrap-style/2x/embassy.png) | ![embassy](img/sprite/walkabout-style/2x/embassy.png) | ![embassy](img/sprite/tron-style/2x/embassy.png) | ![embassy](img/sprite/refill-style/2x/embassy.png) | ![embassy](img/sprite/refill-style/2x/embassy.png)
enclosure | | ![enclosure](img/sprite/walkabout-style/2x/enclosure.png) | | | |
estate_agent | ![estate_agent](img/sprite/bubble-wrap-style/2x/estate_agent.png) | ![estate_agent](img/sprite/walkabout-style/2x/estate_agent.png) | ![estate_agent](img/sprite/tron-style/2x/estate_agent.png) | ![estate_agent](img/sprite/refill-style/2x/estate_agent.png) | ![estate_agent](img/sprite/refill-style/2x/estate_agent.png)
factory | ![factory](img/sprite/bubble-wrap-style/2x/factory.png) | ![factory](img/sprite/walkabout-style/2x/factory.png) | ![factory](img/sprite/tron-style/2x/factory.png) | ![factory](img/sprite/refill-style/2x/factory.png) | ![factory](img/sprite/refill-style/2x/factory.png)
fashion | ![fashion](img/sprite/bubble-wrap-style/2x/fashion.png) | ![fashion](img/sprite/walkabout-style/2x/fashion.png) | ![fashion](img/sprite/tron-style/2x/fashion.png) | ![fashion](img/sprite/refill-style/2x/fashion.png) | ![fashion](img/sprite/refill-style/2x/fashion.png)
fast_food | ![fast_food](img/sprite/bubble-wrap-style/2x/fast_food.png) | ![fast_food](img/sprite/walkabout-style/2x/fast_food.png) | ![fast_food](img/sprite/tron-style/2x/fast_food.png) | ![fast_food](img/sprite/refill-style/2x/fast_food.png) | ![fast_food](img/sprite/refill-style/2x/fast_food.png)
ferry | ![ferry](img/sprite/bubble-wrap-style/2x/ferry.png) | ![ferry](img/sprite/walkabout-style/2x/ferry.png) | ![ferry](img/sprite/tron-style/2x/ferry.png) | ![ferry](img/sprite/refill-style/2x/ferry.png) | ![ferry](img/sprite/refill-style/2x/ferry.png)
ferry_terminal | ![ferry_terminal](img/sprite/bubble-wrap-style/2x/ferry_terminal.png) | ![ferry_terminal](img/sprite/walkabout-style/2x/ferry_terminal.png) | ![ferry_terminal](img/sprite/tron-style/2x/ferry_terminal.png) | ![ferry_terminal](img/sprite/refill-style/2x/ferry_terminal.png) | ![ferry_terminal](img/sprite/refill-style/2x/ferry_terminal.png)
fire_station | ![fire_station](img/sprite/bubble-wrap-style/2x/fire_station.png) | ![fire_station](img/sprite/walkabout-style/2x/fire_station.png) | ![fire_station](img/sprite/tron-style/2x/fire_station.png) | ![fire_station](img/sprite/refill-style/2x/fire_station.png) | ![fire_station](img/sprite/refill-style/2x/fire_station.png)
firepit | | ![firepit](img/sprite/walkabout-style/2x/firepit.png) | | | |
fishing | | ![fishing](img/sprite/walkabout-style/2x/fishing.png) | | | |
fishing_area | | ![fishing_area](img/sprite/walkabout-style/2x/fishing_area.png) | | | |
fitness | ![fitness](img/sprite/bubble-wrap-style/2x/fitness.png) | ![fitness](img/sprite/walkabout-style/2x/fitness.png) | ![fitness](img/sprite/tron-style/2x/fitness.png) | ![fitness](img/sprite/refill-style/2x/fitness.png) | ![fitness](img/sprite/refill-style/2x/fitness.png)
fitness_station | ![fitness_station](img/sprite/bubble-wrap-style/2x/fitness_station.png) | ![fitness_station](img/sprite/walkabout-style/2x/fitness_station.png) | ![fitness_station](img/sprite/tron-style/2x/fitness_station.png) | ![fitness_station](img/sprite/refill-style/2x/fitness_station.png) | ![fitness_station](img/sprite/refill-style/2x/fitness_station.png)
florist | ![florist](img/sprite/bubble-wrap-style/2x/florist.png) | ![florist](img/sprite/walkabout-style/2x/florist.png) | ![florist](img/sprite/tron-style/2x/florist.png) | ![florist](img/sprite/refill-style/2x/florist.png) | ![florist](img/sprite/refill-style/2x/florist.png)
forest | ![forest](img/sprite/bubble-wrap-style/2x/forest.png) | ![forest](img/sprite/walkabout-style/2x/forest.png) | ![forest](img/sprite/tron-style/2x/forest.png) | ![forest](img/sprite/refill-style/2x/forest.png) | ![forest](img/sprite/refill-style/2x/forest.png)
fort | ![fort](img/sprite/bubble-wrap-style/2x/fort.png) | ![fort](img/sprite/walkabout-style/2x/fort.png) | ![fort](img/sprite/tron-style/2x/fort.png) | ![fort](img/sprite/refill-style/2x/fort.png) | ![fort](img/sprite/refill-style/2x/fort.png)
fountain | ![fountain](img/sprite/bubble-wrap-style/2x/fountain.png) | ![fountain](img/sprite/walkabout-style/2x/fountain.png) | ![fountain](img/sprite/tron-style/2x/fountain.png) | ![fountain](img/sprite/refill-style/2x/fountain.png) | ![fountain](img/sprite/refill-style/2x/fountain.png)
fuel | ![fuel](img/sprite/bubble-wrap-style/2x/fuel.png) | ![fuel](img/sprite/walkabout-style/2x/fuel.png) | ![fuel](img/sprite/tron-style/2x/fuel.png) | ![fuel](img/sprite/refill-style/2x/fuel.png) | ![fuel](img/sprite/refill-style/2x/fuel.png)
gallery | ![gallery](img/sprite/bubble-wrap-style/2x/gallery.png) | ![gallery](img/sprite/walkabout-style/2x/gallery.png) | ![gallery](img/sprite/tron-style/2x/gallery.png) | ![gallery](img/sprite/refill-style/2x/gallery.png) | ![gallery](img/sprite/refill-style/2x/gallery.png)
garden | ![garden](img/sprite/bubble-wrap-style/2x/garden.png) | ![garden](img/sprite/walkabout-style/2x/garden.png) | ![garden](img/sprite/tron-style/2x/garden.png) | ![garden](img/sprite/refill-style/2x/garden.png) | ![garden](img/sprite/refill-style/2x/garden.png)
gas_canister | | ![gas_canister](img/sprite/walkabout-style/2x/gas_canister.png) | | | |
gate | | ![gate](img/sprite/walkabout-style/2x/gate.png) | | | |
generator | ![generator](img/sprite/bubble-wrap-style/2x/generator.png) | ![generator](img/sprite/walkabout-style/2x/generator.png) | ![generator](img/sprite/tron-style/2x/generator.png) | ![generator](img/sprite/refill-style/2x/generator.png) | ![generator](img/sprite/refill-style/2x/generator.png)
generic | ![generic](img/sprite/bubble-wrap-style/2x/generic.png) | ![generic](img/sprite/walkabout-style/2x/generic.png) | ![generic](img/sprite/tron-style/2x/generic.png) | ![generic](img/sprite/refill-style/2x/generic.png) | ![generic](img/sprite/refill-style/2x/generic.png)
generic_shield-1char | ![generic_shield-1char](img/sprite/bubble-wrap-style/2x/generic_shield-1char.png) | ![generic_shield-1char](img/sprite/walkabout-style/2x/generic_shield-1char.png) | ![generic_shield-1char](img/sprite/tron-style/2x/generic_shield-1char.png) | ![generic_shield-1char](img/sprite/refill-style/2x/generic_shield-1char.png) | ![generic_shield-1char](img/sprite/refill-style/2x/generic_shield-1char.png)
generic_shield-2char | ![generic_shield-2char](img/sprite/bubble-wrap-style/2x/generic_shield-2char.png) | ![generic_shield-2char](img/sprite/walkabout-style/2x/generic_shield-2char.png) | ![generic_shield-2char](img/sprite/tron-style/2x/generic_shield-2char.png) | ![generic_shield-2char](img/sprite/refill-style/2x/generic_shield-2char.png) | ![generic_shield-2char](img/sprite/refill-style/2x/generic_shield-2char.png)
generic_shield-3char | ![generic_shield-3char](img/sprite/bubble-wrap-style/2x/generic_shield-3char.png) | ![generic_shield-3char](img/sprite/walkabout-style/2x/generic_shield-3char.png) | ![generic_shield-3char](img/sprite/tron-style/2x/generic_shield-3char.png) | ![generic_shield-3char](img/sprite/refill-style/2x/generic_shield-3char.png) | ![generic_shield-3char](img/sprite/refill-style/2x/generic_shield-3char.png)
generic_shield-4char | ![generic_shield-4char](img/sprite/bubble-wrap-style/2x/generic_shield-4char.png) | ![generic_shield-4char](img/sprite/walkabout-style/2x/generic_shield-4char.png) | ![generic_shield-4char](img/sprite/tron-style/2x/generic_shield-4char.png) | ![generic_shield-4char](img/sprite/refill-style/2x/generic_shield-4char.png) | ![generic_shield-4char](img/sprite/refill-style/2x/generic_shield-4char.png)
generic_shield-5char | ![generic_shield-5char](img/sprite/bubble-wrap-style/2x/generic_shield-5char.png) | ![generic_shield-5char](img/sprite/walkabout-style/2x/generic_shield-5char.png) | ![generic_shield-5char](img/sprite/tron-style/2x/generic_shield-5char.png) | ![generic_shield-5char](img/sprite/refill-style/2x/generic_shield-5char.png) | ![generic_shield-5char](img/sprite/refill-style/2x/generic_shield-5char.png)
geyser | | ![geyser](img/sprite/walkabout-style/2x/geyser.png) | | | |
gift | ![gift](img/sprite/bubble-wrap-style/2x/gift.png) | ![gift](img/sprite/walkabout-style/2x/gift.png) | ![gift](img/sprite/tron-style/2x/gift.png) | ![gift](img/sprite/refill-style/2x/gift.png) | ![gift](img/sprite/refill-style/2x/gift.png)
golf_course | ![golf_course](img/sprite/bubble-wrap-style/2x/golf_course.png) | ![golf_course](img/sprite/walkabout-style/2x/golf_course.png) | ![golf_course](img/sprite/tron-style/2x/golf_course.png) | ![golf_course](img/sprite/refill-style/2x/golf_course.png) | ![golf_course](img/sprite/refill-style/2x/golf_course.png)
government | ![government](img/sprite/bubble-wrap-style/2x/government.png) | ![government](img/sprite/walkabout-style/2x/government.png) | ![government](img/sprite/tron-style/2x/government.png) | ![government](img/sprite/refill-style/2x/government.png) | ![government](img/sprite/refill-style/2x/government.png)
grass | ![grass](img/sprite/bubble-wrap-style/2x/grass.png) | ![grass](img/sprite/walkabout-style/2x/grass.png) | ![grass](img/sprite/tron-style/2x/grass.png) | ![grass](img/sprite/refill-style/2x/grass.png) | ![grass](img/sprite/refill-style/2x/grass.png)
grave_yard | ![grave_yard](img/sprite/bubble-wrap-style/2x/grave_yard.png) | ![grave_yard](img/sprite/walkabout-style/2x/grave_yard.png) | ![grave_yard](img/sprite/tron-style/2x/grave_yard.png) | ![grave_yard](img/sprite/refill-style/2x/grave_yard.png) | ![grave_yard](img/sprite/refill-style/2x/grave_yard.png)
greengrocer | ![greengrocer](img/sprite/bubble-wrap-style/2x/greengrocer.png) | ![greengrocer](img/sprite/walkabout-style/2x/greengrocer.png) | ![greengrocer](img/sprite/tron-style/2x/greengrocer.png) | ![greengrocer](img/sprite/refill-style/2x/greengrocer.png) | ![greengrocer](img/sprite/refill-style/2x/greengrocer.png)
hairdresser | ![hairdresser](img/sprite/bubble-wrap-style/2x/hairdresser.png) | ![hairdresser](img/sprite/walkabout-style/2x/hairdresser.png) | ![hairdresser](img/sprite/tron-style/2x/hairdresser.png) | ![hairdresser](img/sprite/refill-style/2x/hairdresser.png) | ![hairdresser](img/sprite/refill-style/2x/hairdresser.png)
hangar | ![hangar](img/sprite/bubble-wrap-style/2x/hangar.png) | ![hangar](img/sprite/walkabout-style/2x/hangar.png) | ![hangar](img/sprite/tron-style/2x/hangar.png) | ![hangar](img/sprite/refill-style/2x/hangar.png) | ![hangar](img/sprite/refill-style/2x/hangar.png)
hardware | ![hardware](img/sprite/bubble-wrap-style/2x/hardware.png) | ![hardware](img/sprite/walkabout-style/2x/hardware.png) | ![hardware](img/sprite/tron-style/2x/hardware.png) | ![hardware](img/sprite/refill-style/2x/hardware.png) | ![hardware](img/sprite/refill-style/2x/hardware.png)
historical | ![historical](img/sprite/bubble-wrap-style/2x/historical.png) | ![historical](img/sprite/walkabout-style/2x/historical.png) | ![historical](img/sprite/tron-style/2x/historical.png) | ![historical](img/sprite/refill-style/2x/historical.png) | ![historical](img/sprite/refill-style/2x/historical.png)
hospital | ![hospital](img/sprite/bubble-wrap-style/2x/hospital.png) | ![hospital](img/sprite/walkabout-style/2x/hospital.png) | ![hospital](img/sprite/tron-style/2x/hospital.png) | ![hospital](img/sprite/refill-style/2x/hospital.png) | ![hospital](img/sprite/refill-style/2x/hospital.png)
hostel | ![hostel](img/sprite/bubble-wrap-style/2x/hostel.png) | ![hostel](img/sprite/walkabout-style/2x/hostel.png) | ![hostel](img/sprite/tron-style/2x/hostel.png) | ![hostel](img/sprite/refill-style/2x/hostel.png) | ![hostel](img/sprite/refill-style/2x/hostel.png)
hot_spring | ![hot_spring](img/sprite/bubble-wrap-style/2x/hot_spring.png) | ![hot_spring](img/sprite/walkabout-style/2x/hot_spring.png) | ![hot_spring](img/sprite/tron-style/2x/hot_spring.png) | ![hot_spring](img/sprite/refill-style/2x/hot_spring.png) | ![hot_spring](img/sprite/refill-style/2x/hot_spring.png)
hotel | ![hotel](img/sprite/bubble-wrap-style/2x/hotel.png) | ![hotel](img/sprite/walkabout-style/2x/hotel.png) | ![hotel](img/sprite/tron-style/2x/hotel.png) | ![hotel](img/sprite/refill-style/2x/hotel.png) | ![hotel](img/sprite/refill-style/2x/hotel.png)
hunting | | ![hunting](img/sprite/walkabout-style/2x/hunting.png) | | | |
ice_cream | ![ice_cream](img/sprite/bubble-wrap-style/2x/ice_cream.png) | ![ice_cream](img/sprite/walkabout-style/2x/ice_cream.png) | ![ice_cream](img/sprite/tron-style/2x/ice_cream.png) | ![ice_cream](img/sprite/refill-style/2x/ice_cream.png) | ![ice_cream](img/sprite/refill-style/2x/ice_cream.png)
industrial | ![industrial](img/sprite/bubble-wrap-style/2x/industrial.png) | ![industrial](img/sprite/walkabout-style/2x/industrial.png) | ![industrial](img/sprite/tron-style/2x/industrial.png) | ![industrial](img/sprite/refill-style/2x/industrial.png) | ![industrial](img/sprite/refill-style/2x/industrial.png)
information | ![information](img/sprite/bubble-wrap-style/2x/information.png) | ![information](img/sprite/walkabout-style/2x/information.png) | ![information](img/sprite/tron-style/2x/information.png) | ![information](img/sprite/refill-style/2x/information.png) | ![information](img/sprite/refill-style/2x/information.png)
insurance | ![insurance](img/sprite/bubble-wrap-style/2x/insurance.png) | ![insurance](img/sprite/walkabout-style/2x/insurance.png) | ![insurance](img/sprite/tron-style/2x/insurance.png) | ![insurance](img/sprite/refill-style/2x/insurance.png) | ![insurance](img/sprite/refill-style/2x/insurance.png)
jewelry | ![jewelry](img/sprite/bubble-wrap-style/2x/jewelry.png) | ![jewelry](img/sprite/walkabout-style/2x/jewelry.png) | ![jewelry](img/sprite/tron-style/2x/jewelry.png) | ![jewelry](img/sprite/refill-style/2x/jewelry.png) | ![jewelry](img/sprite/refill-style/2x/jewelry.png)
jewish | ![jewish](img/sprite/bubble-wrap-style/2x/jewish.png) | ![jewish](img/sprite/walkabout-style/2x/jewish.png) | ![jewish](img/sprite/tron-style/2x/jewish.png) | ![jewish](img/sprite/refill-style/2x/jewish.png) | ![jewish](img/sprite/refill-style/2x/jewish.png)
kindergarten | ![kindergarten](img/sprite/bubble-wrap-style/2x/kindergarten.png) | ![kindergarten](img/sprite/walkabout-style/2x/kindergarten.png) | ![kindergarten](img/sprite/tron-style/2x/kindergarten.png) | ![kindergarten](img/sprite/refill-style/2x/kindergarten.png) | ![kindergarten](img/sprite/refill-style/2x/kindergarten.png)
kiosk | ![kiosk](img/sprite/bubble-wrap-style/2x/kiosk.png) | ![kiosk](img/sprite/walkabout-style/2x/kiosk.png) | ![kiosk](img/sprite/tron-style/2x/kiosk.png) | ![kiosk](img/sprite/refill-style/2x/kiosk.png) | ![kiosk](img/sprite/refill-style/2x/kiosk.png)
landmark | ![landmark](img/sprite/bubble-wrap-style/2x/landmark.png) | ![landmark](img/sprite/walkabout-style/2x/landmark.png) | ![landmark](img/sprite/tron-style/2x/landmark.png) | ![landmark](img/sprite/refill-style/2x/landmark.png) | ![landmark](img/sprite/refill-style/2x/landmark.png)
laundry | ![laundry](img/sprite/bubble-wrap-style/2x/laundry.png) | ![laundry](img/sprite/walkabout-style/2x/laundry.png) | ![laundry](img/sprite/tron-style/2x/laundry.png) | ![laundry](img/sprite/refill-style/2x/laundry.png) | ![laundry](img/sprite/refill-style/2x/laundry.png)
library | ![library](img/sprite/bubble-wrap-style/2x/library.png) | ![library](img/sprite/walkabout-style/2x/library.png) | ![library](img/sprite/tron-style/2x/library.png) | ![library](img/sprite/refill-style/2x/library.png) | ![library](img/sprite/refill-style/2x/library.png)
light_rail | ![light_rail](img/sprite/bubble-wrap-style/2x/light_rail.png) | ![light_rail](img/sprite/walkabout-style/2x/light_rail.png) | ![light_rail](img/sprite/tron-style/2x/light_rail.png) | ![light_rail](img/sprite/refill-style/2x/light_rail.png) | ![light_rail](img/sprite/refill-style/2x/light_rail.png)
lighthouse | ![lighthouse](img/sprite/bubble-wrap-style/2x/lighthouse.png) | ![lighthouse](img/sprite/walkabout-style/2x/lighthouse.png) | ![lighthouse](img/sprite/tron-style/2x/lighthouse.png) | ![lighthouse](img/sprite/refill-style/2x/lighthouse.png) | ![lighthouse](img/sprite/refill-style/2x/lighthouse.png)
liquor | ![liquor](img/sprite/bubble-wrap-style/2x/liquor.png) | ![liquor](img/sprite/walkabout-style/2x/liquor.png) | ![liquor](img/sprite/tron-style/2x/liquor.png) | ![liquor](img/sprite/refill-style/2x/liquor.png) | ![liquor](img/sprite/refill-style/2x/liquor.png)
mall | ![mall](img/sprite/bubble-wrap-style/2x/mall.png) | ![mall](img/sprite/walkabout-style/2x/mall.png) | ![mall](img/sprite/tron-style/2x/mall.png) | ![mall](img/sprite/refill-style/2x/mall.png) | ![mall](img/sprite/refill-style/2x/mall.png)
manor | ![manor](img/sprite/bubble-wrap-style/2x/manor.png) | ![manor](img/sprite/walkabout-style/2x/manor.png) | ![manor](img/sprite/tron-style/2x/manor.png) | ![manor](img/sprite/refill-style/2x/manor.png) | ![manor](img/sprite/refill-style/2x/manor.png)
marina | ![marina](img/sprite/bubble-wrap-style/2x/marina.png) | ![marina](img/sprite/walkabout-style/2x/marina.png) | ![marina](img/sprite/tron-style/2x/marina.png) | ![marina](img/sprite/refill-style/2x/marina.png) | ![marina](img/sprite/refill-style/2x/marina.png)
memorial | ![memorial](img/sprite/bubble-wrap-style/2x/memorial.png) | ![memorial](img/sprite/walkabout-style/2x/memorial.png) | ![memorial](img/sprite/tron-style/2x/memorial.png) | ![memorial](img/sprite/refill-style/2x/memorial.png) | ![memorial](img/sprite/refill-style/2x/memorial.png)
mine | | ![mine](img/sprite/walkabout-style/2x/mine.png) | | | |
mineshaft | ![mineshaft](img/sprite/bubble-wrap-style/2x/mineshaft.png) | ![mineshaft](img/sprite/walkabout-style/2x/mineshaft.png) | ![mineshaft](img/sprite/tron-style/2x/mineshaft.png) | ![mineshaft](img/sprite/refill-style/2x/mineshaft.png) | ![mineshaft](img/sprite/refill-style/2x/mineshaft.png)
mobile_phone | ![mobile_phone](img/sprite/bubble-wrap-style/2x/mobile_phone.png) | ![mobile_phone](img/sprite/walkabout-style/2x/mobile_phone.png) | ![mobile_phone](img/sprite/tron-style/2x/mobile_phone.png) | ![mobile_phone](img/sprite/refill-style/2x/mobile_phone.png) | ![mobile_phone](img/sprite/refill-style/2x/mobile_phone.png)
monument | ![monument](img/sprite/bubble-wrap-style/2x/monument.png) | ![monument](img/sprite/walkabout-style/2x/monument.png) | ![monument](img/sprite/tron-style/2x/monument.png) | ![monument](img/sprite/refill-style/2x/monument.png) | ![monument](img/sprite/refill-style/2x/monument.png)
motel | ![motel](img/sprite/bubble-wrap-style/2x/motel.png) | ![motel](img/sprite/walkabout-style/2x/motel.png) | ![motel](img/sprite/tron-style/2x/motel.png) | ![motel](img/sprite/refill-style/2x/motel.png) | ![motel](img/sprite/refill-style/2x/motel.png)
motorcycle | | ![motorcycle](img/sprite/walkabout-style/2x/motorcycle.png) | | | |
museum | ![museum](img/sprite/bubble-wrap-style/2x/museum.png) | ![museum](img/sprite/walkabout-style/2x/museum.png) | ![museum](img/sprite/tron-style/2x/museum.png) | ![museum](img/sprite/refill-style/2x/museum.png) | ![museum](img/sprite/refill-style/2x/museum.png)
music | ![music](img/sprite/bubble-wrap-style/2x/music.png) | ![music](img/sprite/walkabout-style/2x/music.png) | ![music](img/sprite/tron-style/2x/music.png) | ![music](img/sprite/refill-style/2x/music.png) | ![music](img/sprite/refill-style/2x/music.png)
muslim | ![muslim](img/sprite/bubble-wrap-style/2x/muslim.png) | ![muslim](img/sprite/walkabout-style/2x/muslim.png) | ![muslim](img/sprite/tron-style/2x/muslim.png) | ![muslim](img/sprite/refill-style/2x/muslim.png) | ![muslim](img/sprite/refill-style/2x/muslim.png)
national_park | ![national_park](img/sprite/bubble-wrap-style/2x/national_park.png) | ![national_park](img/sprite/walkabout-style/2x/national_park.png) | ![national_park](img/sprite/tron-style/2x/national_park.png) | | |
natural_forest | ![natural_forest](img/sprite/bubble-wrap-style/2x/natural_forest.png) | ![natural_forest](img/sprite/walkabout-style/2x/natural_forest.png) | ![natural_forest](img/sprite/tron-style/2x/natural_forest.png) | ![natural_forest](img/sprite/refill-style/2x/natural_forest.png) | ![natural_forest](img/sprite/refill-style/2x/natural_forest.png)
nature_reserve | ![nature_reserve](img/sprite/bubble-wrap-style/2x/nature_reserve.png) | ![nature_reserve](img/sprite/walkabout-style/2x/nature_reserve.png) | ![nature_reserve](img/sprite/tron-style/2x/nature_reserve.png) | ![nature_reserve](img/sprite/refill-style/2x/nature_reserve.png) | ![nature_reserve](img/sprite/refill-style/2x/nature_reserve.png)
newspaper | ![newspaper](img/sprite/bubble-wrap-style/2x/newspaper.png) | ![newspaper](img/sprite/walkabout-style/2x/newspaper.png) | ![newspaper](img/sprite/tron-style/2x/newspaper.png) | ![newspaper](img/sprite/refill-style/2x/newspaper.png) | ![newspaper](img/sprite/refill-style/2x/newspaper.png)
nursing_home | ![nursing_home](img/sprite/bubble-wrap-style/2x/nursing_home.png) | ![nursing_home](img/sprite/walkabout-style/2x/nursing_home.png) | ![nursing_home](img/sprite/tron-style/2x/nursing_home.png) | ![nursing_home](img/sprite/refill-style/2x/nursing_home.png) | ![nursing_home](img/sprite/refill-style/2x/nursing_home.png)
observatory | ![observatory](img/sprite/bubble-wrap-style/2x/observatory.png) | ![observatory](img/sprite/walkabout-style/2x/observatory.png) | ![observatory](img/sprite/tron-style/2x/observatory.png) | ![observatory](img/sprite/refill-style/2x/observatory.png) | ![observatory](img/sprite/refill-style/2x/observatory.png)
office | ![office](img/sprite/bubble-wrap-style/2x/office.png) | ![office](img/sprite/walkabout-style/2x/office.png) | ![office](img/sprite/tron-style/2x/office.png) | ![office](img/sprite/refill-style/2x/office.png) | ![office](img/sprite/refill-style/2x/office.png)
optician | ![optician](img/sprite/bubble-wrap-style/2x/optician.png) | ![optician](img/sprite/walkabout-style/2x/optician.png) | ![optician](img/sprite/tron-style/2x/optician.png) | ![optician](img/sprite/refill-style/2x/optician.png) | ![optician](img/sprite/refill-style/2x/optician.png)
outdoor | | ![outdoor](img/sprite/walkabout-style/2x/outdoor.png) | | | |
painter | ![painter](img/sprite/bubble-wrap-style/2x/painter.png) | ![painter](img/sprite/walkabout-style/2x/painter.png) | ![painter](img/sprite/tron-style/2x/painter.png) | ![painter](img/sprite/refill-style/2x/painter.png) | ![painter](img/sprite/refill-style/2x/painter.png)
park | ![park](img/sprite/bubble-wrap-style/2x/park.png) | ![park](img/sprite/walkabout-style/2x/park.png) | ![park](img/sprite/tron-style/2x/park.png) | ![park](img/sprite/refill-style/2x/park.png) | ![park](img/sprite/refill-style/2x/park.png)
park-l | ![park-l](img/sprite/bubble-wrap-style/2x/park-l.png) | | ![park-l](img/sprite/tron-style/2x/park-l.png) | | |
parking | ![parking](img/sprite/bubble-wrap-style/2x/parking.png) | ![parking](img/sprite/walkabout-style/2x/parking.png) | ![parking](img/sprite/tron-style/2x/parking.png) | ![parking](img/sprite/refill-style/2x/parking.png) | ![parking](img/sprite/refill-style/2x/parking.png)
peak | ![peak](img/sprite/bubble-wrap-style/2x/peak.png) | ![peak](img/sprite/walkabout-style/2x/peak.png) | ![peak](img/sprite/tron-style/2x/peak.png) | ![peak](img/sprite/refill-style/2x/peak.png) | ![peak](img/sprite/refill-style/2x/peak.png)
pet | ![pet](img/sprite/bubble-wrap-style/2x/pet.png) | ![pet](img/sprite/walkabout-style/2x/pet.png) | ![pet](img/sprite/tron-style/2x/pet.png) | ![pet](img/sprite/refill-style/2x/pet.png) | ![pet](img/sprite/refill-style/2x/pet.png)
pharmacy | ![pharmacy](img/sprite/bubble-wrap-style/2x/pharmacy.png) | ![pharmacy](img/sprite/walkabout-style/2x/pharmacy.png) | ![pharmacy](img/sprite/tron-style/2x/pharmacy.png) | ![pharmacy](img/sprite/refill-style/2x/pharmacy.png) | ![pharmacy](img/sprite/refill-style/2x/pharmacy.png)
photographer | ![photographer](img/sprite/bubble-wrap-style/2x/photographer.png) | ![photographer](img/sprite/walkabout-style/2x/photographer.png) | ![photographer](img/sprite/tron-style/2x/photographer.png) | ![photographer](img/sprite/refill-style/2x/photographer.png) | ![photographer](img/sprite/refill-style/2x/photographer.png)
photographic_laboratory | ![photographic_laboratory](img/sprite/bubble-wrap-style/2x/photographic_laboratory.png) | ![photographic_laboratory](img/sprite/walkabout-style/2x/photographic_laboratory.png) | ![photographic_laboratory](img/sprite/tron-style/2x/photographic_laboratory.png) | ![photographic_laboratory](img/sprite/refill-style/2x/photographic_laboratory.png) | ![photographic_laboratory](img/sprite/refill-style/2x/photographic_laboratory.png)
picnic_site | | ![picnic_site](img/sprite/walkabout-style/2x/picnic_site.png) | | | |
picnic_table | | ![picnic_table](img/sprite/walkabout-style/2x/picnic_table.png) | | | |
pier | ![pier](img/sprite/bubble-wrap-style/2x/pier.png) | ![pier](img/sprite/walkabout-style/2x/pier.png) | ![pier](img/sprite/tron-style/2x/pier.png) | ![pier](img/sprite/refill-style/2x/pier.png) | ![pier](img/sprite/refill-style/2x/pier.png)
pitch | ![pitch](img/sprite/bubble-wrap-style/2x/pitch.png) | ![pitch](img/sprite/walkabout-style/2x/pitch.png) | ![pitch](img/sprite/tron-style/2x/pitch.png) | ![pitch](img/sprite/refill-style/2x/pitch.png) | ![pitch](img/sprite/refill-style/2x/pitch.png)
place_of_worship | ![place_of_worship](img/sprite/bubble-wrap-style/2x/place_of_worship.png) | ![place_of_worship](img/sprite/walkabout-style/2x/place_of_worship.png) | ![place_of_worship](img/sprite/tron-style/2x/place_of_worship.png) | ![place_of_worship](img/sprite/refill-style/2x/place_of_worship.png) | ![place_of_worship](img/sprite/refill-style/2x/place_of_worship.png)
plant | ![plant](img/sprite/bubble-wrap-style/2x/plant.png) | ![plant](img/sprite/walkabout-style/2x/plant.png) | ![plant](img/sprite/tron-style/2x/plant.png) | ![plant](img/sprite/refill-style/2x/plant.png) | ![plant](img/sprite/refill-style/2x/plant.png)
playground | ![playground](img/sprite/bubble-wrap-style/2x/playground.png) | ![playground](img/sprite/walkabout-style/2x/playground.png) | ![playground](img/sprite/tron-style/2x/playground.png) | ![playground](img/sprite/refill-style/2x/playground.png) | ![playground](img/sprite/refill-style/2x/playground.png)
police | ![police](img/sprite/bubble-wrap-style/2x/police.png) | ![police](img/sprite/walkabout-style/2x/police.png) | ![police](img/sprite/tron-style/2x/police.png) | ![police](img/sprite/refill-style/2x/police.png) | ![police](img/sprite/refill-style/2x/police.png)
post_office | ![post_office](img/sprite/bubble-wrap-style/2x/post_office.png) | ![post_office](img/sprite/walkabout-style/2x/post_office.png) | ![post_office](img/sprite/tron-style/2x/post_office.png) | ![post_office](img/sprite/refill-style/2x/post_office.png) | ![post_office](img/sprite/refill-style/2x/post_office.png)
protected_area | ![protected_area](img/sprite/bubble-wrap-style/2x/protected_area.png) | ![protected_area](img/sprite/walkabout-style/2x/protected_area.png) | ![protected_area](img/sprite/tron-style/2x/protected_area.png) | | |
pub | ![pub](img/sprite/bubble-wrap-style/2x/pub.png) | ![pub](img/sprite/walkabout-style/2x/pub.png) | ![pub](img/sprite/tron-style/2x/pub.png) | ![pub](img/sprite/refill-style/2x/pub.png) | ![pub](img/sprite/refill-style/2x/pub.png)
public | ![public](img/sprite/bubble-wrap-style/2x/public.png) | ![public](img/sprite/walkabout-style/2x/public.png) | ![public](img/sprite/tron-style/2x/public.png) | ![public](img/sprite/refill-style/2x/public.png) | ![public](img/sprite/refill-style/2x/public.png)
quarry | ![quarry](img/sprite/bubble-wrap-style/2x/quarry.png) | ![quarry](img/sprite/walkabout-style/2x/quarry.png) | ![quarry](img/sprite/tron-style/2x/quarry.png) | ![quarry](img/sprite/refill-style/2x/quarry.png) | ![quarry](img/sprite/refill-style/2x/quarry.png)
ranger_station | | ![ranger_station](img/sprite/walkabout-style/2x/ranger_station.png) | | | |
recreation_ground | ![recreation_ground](img/sprite/bubble-wrap-style/2x/recreation_ground.png) | ![recreation_ground](img/sprite/walkabout-style/2x/recreation_ground.png) | ![recreation_ground](img/sprite/tron-style/2x/recreation_ground.png) | ![recreation_ground](img/sprite/refill-style/2x/recreation_ground.png) | ![recreation_ground](img/sprite/refill-style/2x/recreation_ground.png)
recreation_track | | ![recreation_track](img/sprite/walkabout-style/2x/recreation_track.png) | | | |
recycling | ![recycling](img/sprite/bubble-wrap-style/2x/recycling.png) | ![recycling](img/sprite/walkabout-style/2x/recycling.png) | ![recycling](img/sprite/tron-style/2x/recycling.png) | ![recycling](img/sprite/refill-style/2x/recycling.png) | ![recycling](img/sprite/refill-style/2x/recycling.png)
restaurant | ![restaurant](img/sprite/bubble-wrap-style/2x/restaurant.png) | ![restaurant](img/sprite/walkabout-style/2x/restaurant.png) | ![restaurant](img/sprite/tron-style/2x/restaurant.png) | ![restaurant](img/sprite/refill-style/2x/restaurant.png) | ![restaurant](img/sprite/refill-style/2x/restaurant.png)
retail | ![retail](img/sprite/bubble-wrap-style/2x/retail.png) | ![retail](img/sprite/walkabout-style/2x/retail.png) | ![retail](img/sprite/tron-style/2x/retail.png) | ![retail](img/sprite/refill-style/2x/retail.png) | ![retail](img/sprite/refill-style/2x/retail.png)
ruin | ![ruin](img/sprite/bubble-wrap-style/2x/ruin.png) | ![ruin](img/sprite/walkabout-style/2x/ruin.png) | ![ruin](img/sprite/tron-style/2x/ruin.png) | ![ruin](img/sprite/refill-style/2x/ruin.png) | ![ruin](img/sprite/refill-style/2x/ruin.png)
ruins | ![ruins](img/sprite/bubble-wrap-style/2x/ruins.png) | ![ruins](img/sprite/walkabout-style/2x/ruins.png) | ![ruins](img/sprite/tron-style/2x/ruins.png) | ![ruins](img/sprite/refill-style/2x/ruins.png) | ![ruins](img/sprite/refill-style/2x/ruins.png)
school | ![school](img/sprite/bubble-wrap-style/2x/school.png) | ![school](img/sprite/walkabout-style/2x/school.png) | ![school](img/sprite/tron-style/2x/school.png) | ![school](img/sprite/refill-style/2x/school.png) | ![school](img/sprite/refill-style/2x/school.png)
scuba_diving | | ![scuba_diving](img/sprite/walkabout-style/2x/scuba_diving.png) | | | |
shoemaker | ![shoemaker](img/sprite/bubble-wrap-style/2x/shoemaker.png) | ![shoemaker](img/sprite/walkabout-style/2x/shoemaker.png) | ![shoemaker](img/sprite/tron-style/2x/shoemaker.png) | ![shoemaker](img/sprite/refill-style/2x/shoemaker.png) | ![shoemaker](img/sprite/refill-style/2x/shoemaker.png)
shower | | ![shower](img/sprite/walkabout-style/2x/shower.png) | | | |
ski | ![ski](img/sprite/bubble-wrap-style/2x/ski.png) | ![ski](img/sprite/walkabout-style/2x/ski.png) | ![ski](img/sprite/tron-style/2x/ski.png) | ![ski](img/sprite/refill-style/2x/ski.png) | ![ski](img/sprite/refill-style/2x/ski.png)
ski_jumping | | ![ski_jumping](img/sprite/walkabout-style/2x/ski_jumping.png) | | | |
ski_rental | | ![ski_rental](img/sprite/walkabout-style/2x/ski_rental.png) | | ![ski_rental](img/sprite/refill-style/2x/ski_rental.png) | ![ski_rental](img/sprite/refill-style/2x/ski_rental.png)
ski_school | | ![ski_school](img/sprite/walkabout-style/2x/ski_school.png) | | ![ski_school](img/sprite/refill-style/2x/ski_school.png) | ![ski_school](img/sprite/refill-style/2x/ski_school.png)
skiing | | ![skiing](img/sprite/walkabout-style/2x/skiing.png) | | | |
slipway | ![slipway](img/sprite/bubble-wrap-style/2x/slipway.png) | ![slipway](img/sprite/walkabout-style/2x/slipway.png) | ![slipway](img/sprite/tron-style/2x/slipway.png) | ![slipway](img/sprite/refill-style/2x/slipway.png) | ![slipway](img/sprite/refill-style/2x/slipway.png)
soccer | ![soccer](img/sprite/bubble-wrap-style/2x/soccer.png) | ![soccer](img/sprite/walkabout-style/2x/soccer.png) | ![soccer](img/sprite/tron-style/2x/soccer.png) | ![soccer](img/sprite/refill-style/2x/soccer.png) | ![soccer](img/sprite/refill-style/2x/soccer.png)
sports | ![sports](img/sprite/bubble-wrap-style/2x/sports.png) | ![sports](img/sprite/walkabout-style/2x/sports.png) | ![sports](img/sprite/tron-style/2x/sports.png) | ![sports](img/sprite/refill-style/2x/sports.png) | ![sports](img/sprite/refill-style/2x/sports.png)
sports_centre | ![sports_centre](img/sprite/bubble-wrap-style/2x/sports_centre.png) | ![sports_centre](img/sprite/walkabout-style/2x/sports_centre.png) | ![sports_centre](img/sprite/tron-style/2x/sports_centre.png) | ![sports_centre](img/sprite/refill-style/2x/sports_centre.png) | ![sports_centre](img/sprite/refill-style/2x/sports_centre.png)
spring | ![spring](img/sprite/bubble-wrap-style/2x/spring.png) | ![spring](img/sprite/walkabout-style/2x/spring.png) | ![spring](img/sprite/tron-style/2x/spring.png) | ![spring](img/sprite/refill-style/2x/spring.png) | ![spring](img/sprite/refill-style/2x/spring.png)
stadium | ![stadium](img/sprite/bubble-wrap-style/2x/stadium.png) | ![stadium](img/sprite/walkabout-style/2x/stadium.png) | ![stadium](img/sprite/tron-style/2x/stadium.png) | ![stadium](img/sprite/refill-style/2x/stadium.png) | ![stadium](img/sprite/refill-style/2x/stadium.png)
station | ![station](img/sprite/bubble-wrap-style/2x/station.png) | ![station](img/sprite/walkabout-style/2x/station.png) | ![station](img/sprite/tron-style/2x/station.png) | ![station](img/sprite/refill-style/2x/station.png) | ![station](img/sprite/refill-style/2x/station.png)
store | ![store](img/sprite/bubble-wrap-style/2x/store.png) | ![store](img/sprite/walkabout-style/2x/store.png) | ![store](img/sprite/tron-style/2x/store.png) | ![store](img/sprite/refill-style/2x/store.png) | ![store](img/sprite/refill-style/2x/store.png)
substation | ![substation](img/sprite/bubble-wrap-style/2x/substation.png) | ![substation](img/sprite/walkabout-style/2x/substation.png) | ![substation](img/sprite/tron-style/2x/substation.png) | ![substation](img/sprite/refill-style/2x/substation.png) | ![substation](img/sprite/refill-style/2x/substation.png)
subway_entrance | ![subway_entrance](img/sprite/bubble-wrap-style/2x/subway_entrance.png) | ![subway_entrance](img/sprite/walkabout-style/2x/subway_entrance.png) | ![subway_entrance](img/sprite/tron-style/2x/subway_entrance.png) | ![subway_entrance](img/sprite/refill-style/2x/subway_entrance.png) | ![subway_entrance](img/sprite/refill-style/2x/subway_entrance.png)
summer_camp | ![summer_camp](img/sprite/bubble-wrap-style/2x/summer_camp.png) | ![summer_camp](img/sprite/walkabout-style/2x/summer_camp.png) | ![summer_camp](img/sprite/tron-style/2x/summer_camp.png) | ![summer_camp](img/sprite/refill-style/2x/summer_camp.png) | ![summer_camp](img/sprite/refill-style/2x/summer_camp.png)
supermarket | ![supermarket](img/sprite/bubble-wrap-style/2x/supermarket.png) | ![supermarket](img/sprite/walkabout-style/2x/supermarket.png) | ![supermarket](img/sprite/tron-style/2x/supermarket.png) | ![supermarket](img/sprite/refill-style/2x/supermarket.png) | ![supermarket](img/sprite/refill-style/2x/supermarket.png)
swimming_area | | ![swimming_area](img/sprite/walkabout-style/2x/swimming_area.png) | | ![swimming_area](img/sprite/refill-style/2x/swimming_area.png) | ![swimming_area](img/sprite/refill-style/2x/swimming_area.png)
swimming_pool | ![swimming_pool](img/sprite/bubble-wrap-style/2x/swimming_pool.png) | ![swimming_pool](img/sprite/walkabout-style/2x/swimming_pool.png) | ![swimming_pool](img/sprite/tron-style/2x/swimming_pool.png) | ![swimming_pool](img/sprite/refill-style/2x/swimming_pool.png) | ![swimming_pool](img/sprite/refill-style/2x/swimming_pool.png)
tailor | ![tailor](img/sprite/bubble-wrap-style/2x/tailor.png) | ![tailor](img/sprite/walkabout-style/2x/tailor.png) | ![tailor](img/sprite/tron-style/2x/tailor.png) | ![tailor](img/sprite/refill-style/2x/tailor.png) | ![tailor](img/sprite/refill-style/2x/tailor.png)
taqueria | ![taqueria](img/sprite/bubble-wrap-style/2x/taqueria.png) | | | | |
telescope | | ![telescope](img/sprite/walkabout-style/2x/telescope.png) | | | |
tennis | ![tennis](img/sprite/bubble-wrap-style/2x/tennis.png) | ![tennis](img/sprite/walkabout-style/2x/tennis.png) | ![tennis](img/sprite/tron-style/2x/tennis.png) | ![tennis](img/sprite/refill-style/2x/tennis.png) | ![tennis](img/sprite/refill-style/2x/tennis.png)
theatre | ![theatre](img/sprite/bubble-wrap-style/2x/theatre.png) | ![theatre](img/sprite/walkabout-style/2x/theatre.png) | ![theatre](img/sprite/tron-style/2x/theatre.png) | ![theatre](img/sprite/refill-style/2x/theatre.png) | ![theatre](img/sprite/refill-style/2x/theatre.png)
theme_park | ![theme_park](img/sprite/bubble-wrap-style/2x/theme_park.png) | ![theme_park](img/sprite/walkabout-style/2x/theme_park.png) | ![theme_park](img/sprite/tron-style/2x/theme_park.png) | ![theme_park](img/sprite/refill-style/2x/theme_park.png) | ![theme_park](img/sprite/refill-style/2x/theme_park.png)
toilets | ![toilets](img/sprite/bubble-wrap-style/2x/toilets.png) | ![toilets](img/sprite/walkabout-style/2x/toilets.png) | ![toilets](img/sprite/tron-style/2x/toilets.png) | ![toilets](img/sprite/refill-style/2x/toilets.png) | ![toilets](img/sprite/refill-style/2x/toilets.png)
tower | ![tower](img/sprite/bubble-wrap-style/2x/tower.png) | ![tower](img/sprite/walkabout-style/2x/tower.png) | ![tower](img/sprite/tron-style/2x/tower.png) | ![tower](img/sprite/refill-style/2x/tower.png) | ![tower](img/sprite/refill-style/2x/tower.png)
townhall | ![townhall](img/sprite/bubble-wrap-style/2x/townhall.png) | ![townhall](img/sprite/walkabout-style/2x/townhall.png) | ![townhall](img/sprite/tron-style/2x/townhall.png) | ![townhall](img/sprite/refill-style/2x/townhall.png) | ![townhall](img/sprite/refill-style/2x/townhall.png)
townspot-l | ![townspot-l](img/sprite/bubble-wrap-style/2x/townspot-l.png) | ![townspot-l](img/sprite/walkabout-style/2x/townspot-l.png) | ![townspot-l](img/sprite/tron-style/2x/townspot-l.png) | ![townspot-l](img/sprite/refill-style/2x/townspot-l.png) | ![townspot-l](img/sprite/refill-style/2x/townspot-l.png)
townspot-l-rev | ![townspot-l-rev](img/sprite/bubble-wrap-style/2x/townspot-l-rev.png) | ![townspot-l-rev](img/sprite/walkabout-style/2x/townspot-l-rev.png) | ![townspot-l-rev](img/sprite/tron-style/2x/townspot-l-rev.png) | ![townspot-l-rev](img/sprite/refill-style/2x/townspot-l-rev.png) | ![townspot-l-rev](img/sprite/refill-style/2x/townspot-l-rev.png)
townspot-m | ![townspot-m](img/sprite/bubble-wrap-style/2x/townspot-m.png) | ![townspot-m](img/sprite/walkabout-style/2x/townspot-m.png) | ![townspot-m](img/sprite/tron-style/2x/townspot-m.png) | ![townspot-m](img/sprite/refill-style/2x/townspot-m.png) | ![townspot-m](img/sprite/refill-style/2x/townspot-m.png)
townspot-m-rev | ![townspot-m-rev](img/sprite/bubble-wrap-style/2x/townspot-m-rev.png) | ![townspot-m-rev](img/sprite/walkabout-style/2x/townspot-m-rev.png) | ![townspot-m-rev](img/sprite/tron-style/2x/townspot-m-rev.png) | ![townspot-m-rev](img/sprite/refill-style/2x/townspot-m-rev.png) | ![townspot-m-rev](img/sprite/refill-style/2x/townspot-m-rev.png)
townspot-s | ![townspot-s](img/sprite/bubble-wrap-style/2x/townspot-s.png) | ![townspot-s](img/sprite/walkabout-style/2x/townspot-s.png) | ![townspot-s](img/sprite/tron-style/2x/townspot-s.png) | ![townspot-s](img/sprite/refill-style/2x/townspot-s.png) | ![townspot-s](img/sprite/refill-style/2x/townspot-s.png)
townspot-s-rev | ![townspot-s-rev](img/sprite/bubble-wrap-style/2x/townspot-s-rev.png) | ![townspot-s-rev](img/sprite/walkabout-style/2x/townspot-s-rev.png) | ![townspot-s-rev](img/sprite/tron-style/2x/townspot-s-rev.png) | ![townspot-s-rev](img/sprite/refill-style/2x/townspot-s-rev.png) | ![townspot-s-rev](img/sprite/refill-style/2x/townspot-s-rev.png)
townspot-xl | ![townspot-xl](img/sprite/bubble-wrap-style/2x/townspot-xl.png) | ![townspot-xl](img/sprite/walkabout-style/2x/townspot-xl.png) | ![townspot-xl](img/sprite/tron-style/2x/townspot-xl.png) | ![townspot-xl](img/sprite/refill-style/2x/townspot-xl.png) | ![townspot-xl](img/sprite/refill-style/2x/townspot-xl.png)
townspot-xl-rev | ![townspot-xl-rev](img/sprite/bubble-wrap-style/2x/townspot-xl-rev.png) | ![townspot-xl-rev](img/sprite/walkabout-style/2x/townspot-xl-rev.png) | ![townspot-xl-rev](img/sprite/tron-style/2x/townspot-xl-rev.png) | ![townspot-xl-rev](img/sprite/refill-style/2x/townspot-xl-rev.png) | ![townspot-xl-rev](img/sprite/refill-style/2x/townspot-xl-rev.png)
townspot-xs | ![townspot-xs](img/sprite/bubble-wrap-style/2x/townspot-xs.png) | ![townspot-xs](img/sprite/walkabout-style/2x/townspot-xs.png) | ![townspot-xs](img/sprite/tron-style/2x/townspot-xs.png) | ![townspot-xs](img/sprite/refill-style/2x/townspot-xs.png) | ![townspot-xs](img/sprite/refill-style/2x/townspot-xs.png)
townspot-xs-rev | ![townspot-xs-rev](img/sprite/bubble-wrap-style/2x/townspot-xs-rev.png) | ![townspot-xs-rev](img/sprite/walkabout-style/2x/townspot-xs-rev.png) | ![townspot-xs-rev](img/sprite/tron-style/2x/townspot-xs-rev.png) | ![townspot-xs-rev](img/sprite/refill-style/2x/townspot-xs-rev.png) | ![townspot-xs-rev](img/sprite/refill-style/2x/townspot-xs-rev.png)
toys | ![toys](img/sprite/bubble-wrap-style/2x/toys.png) | ![toys](img/sprite/walkabout-style/2x/toys.png) | ![toys](img/sprite/tron-style/2x/toys.png) | ![toys](img/sprite/refill-style/2x/toys.png) | ![toys](img/sprite/refill-style/2x/toys.png)
traffic_signals | ![traffic_signals](img/sprite/bubble-wrap-style/2x/traffic_signals.png) | ![traffic_signals](img/sprite/walkabout-style/2x/traffic_signals.png) | ![traffic_signals](img/sprite/tron-style/2x/traffic_signals.png) | ![traffic_signals](img/sprite/refill-style/2x/traffic_signals.png) | ![traffic_signals](img/sprite/refill-style/2x/traffic_signals.png)
trailhead | | ![trailhead](img/sprite/walkabout-style/2x/trailhead.png) | | | |
train | ![train](img/sprite/bubble-wrap-style/2x/train.png) | | ![train](img/sprite/tron-style/2x/train.png) | ![train](img/sprite/refill-style/2x/train.png) | ![train](img/sprite/refill-style/2x/train.png)
train_station | | | ![train_station](img/sprite/tron-style/2x/train_station.png) | | |
train_station-l | ![train_station-l](img/sprite/bubble-wrap-style/2x/train_station-l.png) | ![train_station-l](img/sprite/walkabout-style/2x/train_station-l.png) | ![train_station-l](img/sprite/tron-style/2x/train_station-l.png) | ![train_station-l](img/sprite/refill-style/2x/train_station-l.png) | ![train_station-l](img/sprite/refill-style/2x/train_station-l.png)
tram_stop | ![tram_stop](img/sprite/bubble-wrap-style/2x/tram_stop.png) | ![tram_stop](img/sprite/walkabout-style/2x/tram_stop.png) | ![tram_stop](img/sprite/tron-style/2x/tram_stop.png) | ![tram_stop](img/sprite/refill-style/2x/tram_stop.png) | ![tram_stop](img/sprite/refill-style/2x/tram_stop.png)
tree | | ![tree](img/sprite/walkabout-style/2x/tree.png) | | | |
tree-s | | ![tree-s](img/sprite/walkabout-style/2x/tree-s.png) | | | |
university | ![university](img/sprite/bubble-wrap-style/2x/university.png) | ![university](img/sprite/walkabout-style/2x/university.png) | ![university](img/sprite/tron-style/2x/university.png) | ![university](img/sprite/refill-style/2x/university.png) | ![university](img/sprite/refill-style/2x/university.png)
US:CA-1char | ![US:CA-1char](img/sprite/bubble-wrap-style/2x/US-CA-1char.png) | ![US:CA-1char](img/sprite/walkabout-style/2x/US-CA-1char.png) | ![US:CA-1char](img/sprite/tron-style/2x/US-CA-1char.png) | ![US:CA-1char](img/sprite/refill-style/2x/US-CA-1char.png) | ![US:CA-1char](img/sprite/refill-style/2x/US-CA-1char.png)
US:CA-2char | ![US:CA-2char](img/sprite/bubble-wrap-style/2x/US-CA-2char.png) | ![US:CA-2char](img/sprite/walkabout-style/2x/US-CA-2char.png) | ![US:CA-2char](img/sprite/tron-style/2x/US-CA-2char.png) | ![US:CA-2char](img/sprite/refill-style/2x/US-CA-2char.png) | ![US:CA-2char](img/sprite/refill-style/2x/US-CA-2char.png)
US:CA-3char | ![US:CA-3char](img/sprite/bubble-wrap-style/2x/US-CA-3char.png) | ![US:CA-3char](img/sprite/walkabout-style/2x/US-CA-3char.png) | ![US:CA-3char](img/sprite/tron-style/2x/US-CA-3char.png) | ![US:CA-3char](img/sprite/refill-style/2x/US-CA-3char.png) | ![US:CA-3char](img/sprite/refill-style/2x/US-CA-3char.png)
US:CA-4char | ![US:CA-4char](img/sprite/bubble-wrap-style/2x/US-CA-4char.png) | ![US:CA-4char](img/sprite/walkabout-style/2x/US-CA-4char.png) | ![US:CA-4char](img/sprite/tron-style/2x/US-CA-4char.png) | ![US:CA-4char](img/sprite/refill-style/2x/US-CA-4char.png) | ![US:CA-4char](img/sprite/refill-style/2x/US-CA-4char.png)
US:CA-5char | ![US:CA-5char](img/sprite/bubble-wrap-style/2x/US-CA-5char.png) | ![US:CA-5char](img/sprite/walkabout-style/2x/US-CA-5char.png) | ![US:CA-5char](img/sprite/tron-style/2x/US-CA-5char.png) | ![US:CA-5char](img/sprite/refill-style/2x/US-CA-5char.png) | ![US:CA-5char](img/sprite/refill-style/2x/US-CA-5char.png)
US:I-1char | ![US:I-1char](img/sprite/bubble-wrap-style/2x/US-I-1char.png) | ![US:I-1char](img/sprite/walkabout-style/2x/US-I-1char.png) | ![US:I-1char](img/sprite/tron-style/2x/US-I-1char.png) | ![US:I-1char](img/sprite/refill-style/2x/US-I-1char.png) | ![US:I-1char](img/sprite/refill-style/2x/US-I-1char.png)
US:I-2char | ![US:I-2char](img/sprite/bubble-wrap-style/2x/US-I-2char.png) | ![US:I-2char](img/sprite/walkabout-style/2x/US-I-2char.png) | ![US:I-2char](img/sprite/tron-style/2x/US-I-2char.png) | ![US:I-2char](img/sprite/refill-style/2x/US-I-2char.png) | ![US:I-2char](img/sprite/refill-style/2x/US-I-2char.png)
US:I-3char | ![US:I-3char](img/sprite/bubble-wrap-style/2x/US-I-3char.png) | ![US:I-3char](img/sprite/walkabout-style/2x/US-I-3char.png) | ![US:I-3char](img/sprite/tron-style/2x/US-I-3char.png) | ![US:I-3char](img/sprite/refill-style/2x/US-I-3char.png) | ![US:I-3char](img/sprite/refill-style/2x/US-I-3char.png)
US:I-4char | ![US:I-4char](img/sprite/bubble-wrap-style/2x/US-I-4char.png) | ![US:I-4char](img/sprite/walkabout-style/2x/US-I-4char.png) | ![US:I-4char](img/sprite/tron-style/2x/US-I-4char.png) | ![US:I-4char](img/sprite/refill-style/2x/US-I-4char.png) | ![US:I-4char](img/sprite/refill-style/2x/US-I-4char.png)
US:I-5char | ![US:I-5char](img/sprite/bubble-wrap-style/2x/US-I-5char.png) | ![US:I-5char](img/sprite/walkabout-style/2x/US-I-5char.png) | ![US:I-5char](img/sprite/tron-style/2x/US-I-5char.png) | ![US:I-5char](img/sprite/refill-style/2x/US-I-5char.png) | ![US:I-5char](img/sprite/refill-style/2x/US-I-5char.png)
US:NY-1char | ![US:NY-1char](img/sprite/bubble-wrap-style/2x/US-NY-1char.png) | ![US:NY-1char](img/sprite/walkabout-style/2x/US-NY-1char.png) | ![US:NY-1char](img/sprite/tron-style/2x/US-NY-1char.png) | ![US:NY-1char](img/sprite/refill-style/2x/US-NY-1char.png) | ![US:NY-1char](img/sprite/refill-style/2x/US-NY-1char.png)
US:NY-2char | ![US:NY-2char](img/sprite/bubble-wrap-style/2x/US-NY-2char.png) | ![US:NY-2char](img/sprite/walkabout-style/2x/US-NY-2char.png) | ![US:NY-2char](img/sprite/tron-style/2x/US-NY-2char.png) | ![US:NY-2char](img/sprite/refill-style/2x/US-NY-2char.png) | ![US:NY-2char](img/sprite/refill-style/2x/US-NY-2char.png)
US:NY-3char | ![US:NY-3char](img/sprite/bubble-wrap-style/2x/US-NY-3char.png) | ![US:NY-3char](img/sprite/walkabout-style/2x/US-NY-3char.png) | ![US:NY-3char](img/sprite/tron-style/2x/US-NY-3char.png) | ![US:NY-3char](img/sprite/refill-style/2x/US-NY-3char.png) | ![US:NY-3char](img/sprite/refill-style/2x/US-NY-3char.png)
US:NY-4char | ![US:NY-4char](img/sprite/bubble-wrap-style/2x/US-NY-4char.png) | ![US:NY-4char](img/sprite/walkabout-style/2x/US-NY-4char.png) | ![US:NY-4char](img/sprite/tron-style/2x/US-NY-4char.png) | ![US:NY-4char](img/sprite/refill-style/2x/US-NY-4char.png) | ![US:NY-4char](img/sprite/refill-style/2x/US-NY-4char.png)
US:NY-5char | ![US:NY-5char](img/sprite/bubble-wrap-style/2x/US-NY-5char.png) | ![US:NY-5char](img/sprite/walkabout-style/2x/US-NY-5char.png) | ![US:NY-5char](img/sprite/tron-style/2x/US-NY-5char.png) | ![US:NY-5char](img/sprite/refill-style/2x/US-NY-5char.png) | ![US:NY-5char](img/sprite/refill-style/2x/US-NY-5char.png)
US:PA-1char | ![US:PA-1char](img/sprite/bubble-wrap-style/2x/US-PA-1char.png) | ![US:PA-1char](img/sprite/walkabout-style/2x/US-PA-1char.png) | ![US:PA-1char](img/sprite/tron-style/2x/US-PA-1char.png) | ![US:PA-1char](img/sprite/refill-style/2x/US-PA-1char.png) | ![US:PA-1char](img/sprite/refill-style/2x/US-PA-1char.png)
US:PA-2char | ![US:PA-2char](img/sprite/bubble-wrap-style/2x/US-PA-2char.png) | ![US:PA-2char](img/sprite/walkabout-style/2x/US-PA-2char.png) | ![US:PA-2char](img/sprite/tron-style/2x/US-PA-2char.png) | ![US:PA-2char](img/sprite/refill-style/2x/US-PA-2char.png) | ![US:PA-2char](img/sprite/refill-style/2x/US-PA-2char.png)
US:PA-3char | ![US:PA-3char](img/sprite/bubble-wrap-style/2x/US-PA-3char.png) | ![US:PA-3char](img/sprite/walkabout-style/2x/US-PA-3char.png) | ![US:PA-3char](img/sprite/tron-style/2x/US-PA-3char.png) | ![US:PA-3char](img/sprite/refill-style/2x/US-PA-3char.png) | ![US:PA-3char](img/sprite/refill-style/2x/US-PA-3char.png)
US:PA-4char | ![US:PA-4char](img/sprite/bubble-wrap-style/2x/US-PA-4char.png) | ![US:PA-4char](img/sprite/walkabout-style/2x/US-PA-4char.png) | ![US:PA-4char](img/sprite/tron-style/2x/US-PA-4char.png) | ![US:PA-4char](img/sprite/refill-style/2x/US-PA-4char.png) | ![US:PA-4char](img/sprite/refill-style/2x/US-PA-4char.png)
US:PA-5char | ![US:PA-5char](img/sprite/bubble-wrap-style/2x/US-PA-5char.png) | ![US:PA-5char](img/sprite/walkabout-style/2x/US-PA-5char.png) | ![US:PA-5char](img/sprite/tron-style/2x/US-PA-5char.png) | ![US:PA-5char](img/sprite/refill-style/2x/US-PA-5char.png) | ![US:PA-5char](img/sprite/refill-style/2x/US-PA-5char.png)
US:US-1char | ![US:US-1char](img/sprite/bubble-wrap-style/2x/US-US-1char.png) | ![US:US-1char](img/sprite/walkabout-style/2x/US-US-1char.png) | ![US:US-1char](img/sprite/tron-style/2x/US-US-1char.png) | ![US:US-1char](img/sprite/refill-style/2x/US-US-1char.png) | ![US:US-1char](img/sprite/refill-style/2x/US-US-1char.png)
US:US-2char | ![US:US-2char](img/sprite/bubble-wrap-style/2x/US-US-2char.png) | ![US:US-2char](img/sprite/walkabout-style/2x/US-US-2char.png) | ![US:US-2char](img/sprite/tron-style/2x/US-US-2char.png) | ![US:US-2char](img/sprite/refill-style/2x/US-US-2char.png) | ![US:US-2char](img/sprite/refill-style/2x/US-US-2char.png)
US:US-3char | ![US:US-3char](img/sprite/bubble-wrap-style/2x/US-US-3char.png) | ![US:US-3char](img/sprite/walkabout-style/2x/US-US-3char.png) | ![US:US-3char](img/sprite/tron-style/2x/US-US-3char.png) | ![US:US-3char](img/sprite/refill-style/2x/US-US-3char.png) | ![US:US-3char](img/sprite/refill-style/2x/US-US-3char.png)
US:US-4char | ![US:US-4char](img/sprite/bubble-wrap-style/2x/US-US-4char.png) | ![US:US-4char](img/sprite/walkabout-style/2x/US-US-4char.png) | ![US:US-4char](img/sprite/tron-style/2x/US-US-4char.png) | ![US:US-4char](img/sprite/refill-style/2x/US-US-4char.png) | ![US:US-4char](img/sprite/refill-style/2x/US-US-4char.png)
US:US-5char | ![US:US-5char](img/sprite/bubble-wrap-style/2x/US-US-5char.png) | ![US:US-5char](img/sprite/walkabout-style/2x/US-US-5char.png) | ![US:US-5char](img/sprite/tron-style/2x/US-US-5char.png) | ![US:US-5char](img/sprite/refill-style/2x/US-US-5char.png) | ![US:US-5char](img/sprite/refill-style/2x/US-US-5char.png)
ux-current-location | ![ux-current-location](img/sprite/bubble-wrap-style/2x/ux-current-location.png) | ![ux-current-location](img/sprite/walkabout-style/2x/ux-current-location.png) | ![ux-current-location](img/sprite/tron-style/2x/ux-current-location.png) | ![ux-current-location](img/sprite/refill-style/2x/ux-current-location.png) | ![ux-current-location](img/sprite/refill-style/2x/ux-current-location.png)
ux-locate-off | ![ux-locate-off](img/sprite/bubble-wrap-style/2x/ux-locate-off.png) | ![ux-locate-off](img/sprite/walkabout-style/2x/ux-locate-off.png) | ![ux-locate-off](img/sprite/tron-style/2x/ux-locate-off.png) | ![ux-locate-off](img/sprite/refill-style/2x/ux-locate-off.png) | ![ux-locate-off](img/sprite/refill-style/2x/ux-locate-off.png)
ux-locate-on | ![ux-locate-on](img/sprite/bubble-wrap-style/2x/ux-locate-on.png) | ![ux-locate-on](img/sprite/walkabout-style/2x/ux-locate-on.png) | ![ux-locate-on](img/sprite/tron-style/2x/ux-locate-on.png) | ![ux-locate-on](img/sprite/refill-style/2x/ux-locate-on.png) | ![ux-locate-on](img/sprite/refill-style/2x/ux-locate-on.png)
ux-route-arrow | ![ux-route-arrow](img/sprite/bubble-wrap-style/2x/ux-route-arrow.png) | ![ux-route-arrow](img/sprite/walkabout-style/2x/ux-route-arrow.png) | ![ux-route-arrow](img/sprite/tron-style/2x/ux-route-arrow.png) | ![ux-route-arrow](img/sprite/refill-style/2x/ux-route-arrow.png) | ![ux-route-arrow](img/sprite/refill-style/2x/ux-route-arrow.png)
ux-route-start | ![ux-route-start](img/sprite/bubble-wrap-style/2x/ux-route-start.png) | ![ux-route-start](img/sprite/walkabout-style/2x/ux-route-start.png) | ![ux-route-start](img/sprite/tron-style/2x/ux-route-start.png) | ![ux-route-start](img/sprite/refill-style/2x/ux-route-start.png) | ![ux-route-start](img/sprite/refill-style/2x/ux-route-start.png)
ux-route-stop | ![ux-route-stop](img/sprite/bubble-wrap-style/2x/ux-route-stop.png) | ![ux-route-stop](img/sprite/walkabout-style/2x/ux-route-stop.png) | ![ux-route-stop](img/sprite/tron-style/2x/ux-route-stop.png) | ![ux-route-stop](img/sprite/refill-style/2x/ux-route-stop.png) | ![ux-route-stop](img/sprite/refill-style/2x/ux-route-stop.png)
ux-search-active | ![ux-search-active](img/sprite/bubble-wrap-style/2x/ux-search-active.png) | ![ux-search-active](img/sprite/walkabout-style/2x/ux-search-active.png) | ![ux-search-active](img/sprite/tron-style/2x/ux-search-active.png) | ![ux-search-active](img/sprite/refill-style/2x/ux-search-active.png) | ![ux-search-active](img/sprite/refill-style/2x/ux-search-active.png)
ux-search-inactive | ![ux-search-inactive](img/sprite/bubble-wrap-style/2x/ux-search-inactive.png) | ![ux-search-inactive](img/sprite/walkabout-style/2x/ux-search-inactive.png) | ![ux-search-inactive](img/sprite/tron-style/2x/ux-search-inactive.png) | ![ux-search-inactive](img/sprite/refill-style/2x/ux-search-inactive.png) | ![ux-search-inactive](img/sprite/refill-style/2x/ux-search-inactive.png)
ux-transit-stop | ![ux-transit-stop](img/sprite/bubble-wrap-style/2x/ux-transit-stop.png) | ![ux-transit-stop](img/sprite/walkabout-style/2x/ux-transit-stop.png) | ![ux-transit-stop](img/sprite/tron-style/2x/ux-transit-stop.png) | ![ux-transit-stop](img/sprite/refill-style/2x/ux-transit-stop.png) | ![ux-transit-stop](img/sprite/refill-style/2x/ux-transit-stop.png)
veterinary | ![veterinary](img/sprite/bubble-wrap-style/2x/veterinary.png) | ![veterinary](img/sprite/walkabout-style/2x/veterinary.png) | ![veterinary](img/sprite/tron-style/2x/veterinary.png) | ![veterinary](img/sprite/refill-style/2x/veterinary.png) | ![veterinary](img/sprite/refill-style/2x/veterinary.png)
viewpoint | ![viewpoint](img/sprite/bubble-wrap-style/2x/viewpoint.png) | ![viewpoint](img/sprite/walkabout-style/2x/viewpoint.png) | ![viewpoint](img/sprite/tron-style/2x/viewpoint.png) | ![viewpoint](img/sprite/refill-style/2x/viewpoint.png) | ![viewpoint](img/sprite/refill-style/2x/viewpoint.png)
vineyard | ![vineyard](img/sprite/bubble-wrap-style/2x/vineyard.png) | ![vineyard](img/sprite/walkabout-style/2x/vineyard.png) | ![vineyard](img/sprite/tron-style/2x/vineyard.png) | ![vineyard](img/sprite/refill-style/2x/vineyard.png) | ![vineyard](img/sprite/refill-style/2x/vineyard.png)
volcano | ![volcano](img/sprite/bubble-wrap-style/2x/volcano.png) | ![volcano](img/sprite/walkabout-style/2x/volcano.png) | ![volcano](img/sprite/tron-style/2x/volcano.png) | ![volcano](img/sprite/refill-style/2x/volcano.png) | ![volcano](img/sprite/refill-style/2x/volcano.png)
wastewater_plant | ![wastewater_plant](img/sprite/bubble-wrap-style/2x/wastewater_plant.png) | ![wastewater_plant](img/sprite/walkabout-style/2x/wastewater_plant.png) | ![wastewater_plant](img/sprite/tron-style/2x/wastewater_plant.png) | ![wastewater_plant](img/sprite/refill-style/2x/wastewater_plant.png) | ![wastewater_plant](img/sprite/refill-style/2x/wastewater_plant.png)
water_park | ![water_park](img/sprite/bubble-wrap-style/2x/water_park.png) | ![water_park](img/sprite/walkabout-style/2x/water_park.png) | ![water_park](img/sprite/tron-style/2x/water_park.png) | ![water_park](img/sprite/refill-style/2x/water_park.png) | ![water_park](img/sprite/refill-style/2x/water_park.png)
water_slide | | ![water_slide](img/sprite/walkabout-style/2x/water_slide.png) | | | |
water_tower | | ![water_tower](img/sprite/walkabout-style/2x/water_tower.png) | | | |
water_works | ![water_works](img/sprite/bubble-wrap-style/2x/water_works.png) | ![water_works](img/sprite/walkabout-style/2x/water_works.png) | ![water_works](img/sprite/tron-style/2x/water_works.png) | ![water_works](img/sprite/refill-style/2x/water_works.png) | ![water_works](img/sprite/refill-style/2x/water_works.png)
waterfall | | ![waterfall](img/sprite/walkabout-style/2x/waterfall.png) | | | |
wayside_shrine | ![wayside_shrine](img/sprite/bubble-wrap-style/2x/wayside_shrine.png) | ![wayside_shrine](img/sprite/walkabout-style/2x/wayside_shrine.png) | ![wayside_shrine](img/sprite/tron-style/2x/wayside_shrine.png) | ![wayside_shrine](img/sprite/refill-style/2x/wayside_shrine.png) | ![wayside_shrine](img/sprite/refill-style/2x/wayside_shrine.png)
wine | ![wine](img/sprite/bubble-wrap-style/2x/wine.png) | ![wine](img/sprite/walkabout-style/2x/wine.png) | ![wine](img/sprite/tron-style/2x/wine.png) | ![wine](img/sprite/refill-style/2x/wine.png) | ![wine](img/sprite/refill-style/2x/wine.png)
winery | ![winery](img/sprite/bubble-wrap-style/2x/winery.png) | ![winery](img/sprite/walkabout-style/2x/winery.png) | ![winery](img/sprite/tron-style/2x/winery.png) | ![winery](img/sprite/refill-style/2x/winery.png) | ![winery](img/sprite/refill-style/2x/winery.png)
winter_sports | ![winter_sports](img/sprite/bubble-wrap-style/2x/winter_sports.png) | ![winter_sports](img/sprite/walkabout-style/2x/winter_sports.png) | ![winter_sports](img/sprite/tron-style/2x/winter_sports.png) | ![winter_sports](img/sprite/refill-style/2x/winter_sports.png) | ![winter_sports](img/sprite/refill-style/2x/winter_sports.png)
works | ![works](img/sprite/bubble-wrap-style/2x/works.png) | ![works](img/sprite/walkabout-style/2x/works.png) | ![works](img/sprite/tron-style/2x/works.png) | ![works](img/sprite/refill-style/2x/works.png) | ![works](img/sprite/refill-style/2x/works.png)
zoo | ![zoo](img/sprite/bubble-wrap-style/2x/zoo.png) | ![zoo](img/sprite/walkabout-style/2x/zoo.png) | ![zoo](img/sprite/tron-style/2x/zoo.png) | ![zoo](img/sprite/refill-style/2x/zoo.png)


## Versions

The following Mapzen basemap styles support the `mapzen_icon_library` style defaults and named icon assets:

* Bubble Wrap: `8.0.0` and later
* Cinnabar: `8.0.0` and later
* Refill: `9.0.0` and later
* Tron: `5.0.0` and later
* Walkabout: `6.0.0` and later

Earlier versions of Mapzen basemap styles did not support all icons in the table above or the style defaults.
