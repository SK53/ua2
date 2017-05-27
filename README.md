# ua2
Urban Areas (2nd attempt)

This repository contains Geojson files purporting to represent urban areas across the world. The data are created from OpenStreetMap (and are therefore licensed according to OdBL) using a fairly simple algorthim, first described by vlasvlasvlas at State of the Map 2014 in Buenos Aires. I accidentally rediscovered a similar algorithm and discussed the pros and cons of various ways of identifying urban areas from OSM data on my blog, Maps Matter.

The algorithm simply takes all public motorable highways (motorway, primary, trunk, secondary, tertiary, unclassified and residential) which are less than 2000 metres in length (either in Popular Mercator projection or using PostGIS geography type). The network of such roads is analysed to find discrete graphs of connected ways, these are then buffered by about 100 metres and then negatively buffered by a similar amount to fill small holes. Individual polygons are then further buffered, tested for interconnectivity and merged (for instance to handle areas split by small waterways) to create the final results.

There are undoubtedly false positives (for instance many roads in isolated industrial or military areas; or where rural roads have been split into small sections), and in countries where the road network is less well mapped there will be false negatives. Ultimately I plan to add various metrics to each polygon: area in sq km, number of holes (very holey ones are probably dubious), length of residential road, total road length, number of certain pois etc. The hope is that the metrics might be useful for identifying false positives, however, in practice I suspect human visual inspection will be just as fruitful and speedy.

Data are tiled either in 10, 5 or 2.5 degree tiles: mainly to make it easier to manage on github. It is envisaged that shape files will be prepared for formal releases.

Envisaged potential uses:

* Cartographic, for instance as an alternative to Natural Earth (filtering on size & generalisation will be needed)
* For analytical purposes
* As an aid for routing (e.g., offering default speed limits)
* As an aid for improving OSM (ratios of street lengths etc). Buffering distances have been chosen to accomodate places where not all urban streets have been mapped on OSM.
