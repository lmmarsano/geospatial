# [Geospatial Analysis][nb]
An exercise in data science.
[View the notebook online][nb].

## Data Sources
- [Meteorite Landings](https://data.nasa.gov/resource/y77d-th95.geojson) from [NASA](http://data.nasa.gov/)
- [UFO sightings](https://www.kaggle.com/NUFORC/ufo-sightings) from [kaggle](https://www.kaggle.com/), based on data from [NUFORC](http://www.nuforc.org/)

### Usage
- From both data-sets, I used geographic coordinates.
- To practice SQL, I cleansed, type coerced & normalized all fields into relational tables where sensible.

## Overview
Initial plots of the data show highly similar spatial arrangements clustered around populated areas with technological access.
The main question to answer is: are the data correlated?

To analyze the data, I draw some plots to show frequency, then researched some [GIS][GIS] technologies & [concepts](http://www.spatialanalysisonline.com/) (though nothing too sophisticated), to appropriately/efficiently handle geospatial relations, operations, and measurements between coordinate systems & projections.
This resulted in devising a method to divide the globe's surface into simple, equal-area polygons that should preserve well across coordinate transformations in software restricted to straight edge representations.
With this method, I calculate frequencies over sections to yield variables we can correlate.
The correlation is weak, and the analysis shows why.

Geometric operations are largely performed with SQLite's [GIS][GIS] extension, [SpatiaLite][SpatiaLite].
In particular, [SpatiaLite][SpatiaLite] is used to
- [generate tessellations/geometric grids](https://www.gaia-gis.it/fossil/libspatialite/wiki?name=tesselations-4.0) and [extract their constituent shapes into tables](https://www.gaia-gis.it/fossil/libspatialite/wiki?name=VirtualElementary)
- [load coordinate systems](https://www.gaia-gis.it/fossil/libspatialite/wiki?name=switching-to-4.0) & transform between them
- [perform fast geospatial joins with spatial indexing](https://www.gaia-gis.it/fossil/libspatialite/wiki?name=SpatialIndex).

## Setup & Running
1. Clone the project and change into it
   ```sh
   git clone --depth 1 https://github.com/lmmarsano/geospatial.git
   cd geospatial
   ```
2. Extract data
   ```sh
   tar -xaf data.txz
   ```
2. [Install conda](https://conda.io/docs/user-guide/install/index.html) and run
   ```sh
   conda env create -f environment.yml
   ```
3. Activate the environment
   ```sh
   . activate geospatial
   ```
4. Install custom packages
   ```sh
   pip install -r requirements.txt
   ```
5. Run
   ```sh
   jupyter lab
   ```

A web browser should launch to the application containing the notebook.

## Inspired Pull Requests
Producing this notebook unearthed some bugs in dependencies and inspired pull requests to fix them.
- [sqlalchemy-views](https://github.com/jklukas/sqlalchemy-views/pull/6)
- [geopandas](https://github.com/geopandas/geopandas/pull/856)
- [geoplot](https://github.com/ResidentMario/geoplot/pull/65)

[nb]: https://nbviewer.jupyter.org/github/lmmarsano/geospatial/blob/master/geospatial.ipynb
[GIS]: https://en.wikipedia.org/wiki/Geographic_information_system
[SpatiaLite]: https://www.gaia-gis.it/fossil/libspatialite/index
