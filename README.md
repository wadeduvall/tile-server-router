# tile-server
A modual tile server based heavily upon [switch2osm](https://switch2osm.org/)
docker image and examples.

This project uses the official postgis docker image, a custom
[renderer](https://github.com/wad209/renderer) and a
[osm2pgsql](https://github.com/wad209/osm2pgsql) image that is designed to
import pbf's from e.g. [geofabric's download
server](https://download.geofabrik.de/)

# Quick start
Assuming you have [docker-compose](https://github.com/docker/compose) installed,
first build the necessary images and start the PostGIS container.

    docker-compose build
    docker-compose up postgis 

Once the initial startup for the postgis container is done, ctr-c the
container. Now you can import any PBF by specifying a URL:

    docker-compose run --rm \
    -e IMPORT=true \
    -e PBF=http://download.geofabrik.de/north-america/us/virginia-latest.osm.pbf \
    -e POLY=http://download.geofabrik.de/north-america/us/virginia.poly \
    import ./import.sh

It's also possible to mount the a PBF and poly files:

    docker-compose run --rm \
    -e IMPORT=true \
    -v virginia-latest.osm.pbf:/data.osm.pbf \
    -v virginia.poly:/data.poly \
    import ./import.sh

Then, you can bring up the whole system:

    docker-compose up -d

# Options for importing

If you wish to append to existing data, simply do:

    docker-compose run --rm \
    -e UPDATE=true \
    -e PBF=http://download.geofabrik.de/north-america/us/virginia-latest.osm.pbf \
    -e POLY=http://download.geofabrik.de/north-america/us/virginia.poly \
    import ./import.sh

# Changing the PostGIS server information

The PostGIS container database configuration information is set in file
database.env. It's possible to change this information if you wish, but you'll
also have to update the information in client.env so the renderer knows were to
look for the data.
