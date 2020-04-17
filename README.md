# tile-server
A modual tile server based heavily upon [switch2osm](https://switch2osm.org/)
docker image and examples.

This project uses the official postgis docker image, a custom
[renderer](https://github.com/wad209/renderer) and a
[osm2pgsql](https://github.com/wad209/osm2pgsql) image that is designed to
import pbf's from e.g. [geofabric's download
server](https://download.geofabrik.de/)

# Quick start
For now, grab the renderer, osm2pgsql, and this repo and put them all in the
same directory.

    git clone https://github.com/wad209/osm2pgsql
    git clone https://github.com/wad209/renderer
    git clone https://github.com/wad209/tile-server

Assuming you have [docker-compose](https://github.com/docker/compose) installed
you should then be able to build the image and import a map

    docker-compose build
    docker-compose up -d
    docker-compose run osm2pgsql run.sh
