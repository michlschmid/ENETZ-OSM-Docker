# Installation
1. Download Map-Data
    * Protomaps:
        * AllgäuNetz Region (D/A): https://protomaps.com/extracts/00377668-95f6-45c8-84e5-a1d181fc68bb

    * Geofabrik (Prebuilt):
        * Bayern:         https://download.geofabrik.de/europe/germany/bayern.html
        * Deutschland:    https://download.geofabrik.de/europe/germany.html
        * Österreich:     https://download.geofabrik.de/europe/austria.html

2. Prepare storage containers
    * Create "database" volume container for persistence:
    ```
    docker volume create openstreetmap-data
    ```

    * Create "rendered tiles cache" volume container for persistence:
    ```
    docker volume create openstreetmap-rendered-tiles
    ```

3. Generate "Local-OSM-Server" Docker container and import the downloaded Map-Data
    * And install it and import the data:
    ```
    time docker run -v /htdocs/tramino/OSM-TileServer/data/protomaps-allgaeu.osm.pbf:/data.osm.pbf -v openstreetmap-data:/var/lib/postgresql/12/main overv/openstreetmap-tile-server:1.3.10 import
    ```

4. Startup "Local-OSM-Server" Docker container
    * Start the tile server running:
    ```
    docker-compose up
    ```
    or:
    ```
    docker run -p 80:80 -v openstreetmap-data:/var/lib/postgresql/12/main -d overv/openstreetmap-tile-server:1.3.10 run
    ```

5. Check that everything is working as expected. Browse to:
```
http://localhost/tile/0/0/0.png
```


# Links and Sources
* https://switch2osm.org/serving-tiles/using-a-docker-container/

* https://github.com/Overv/openstreetmap-tile-server/blob/master/README.md

* https://hub.docker.com/r/overv/openstreetmap-tile-server/tags

* https://switch2osm.org/serving-tiles/

* https://switch2osm.org/the-basics/
