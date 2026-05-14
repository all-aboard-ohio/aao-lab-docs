---
title: Datasets & Tools Reference
excerpt: A curated reference of open datasets and Python/GIS tools relevant to transit analysis, rail advocacy, and spatial data work at the AAO Data Lab.
---

# Datasets & Tools Reference

This document catalogs open datasets and analysis tools that are well-suited to the kinds of work AAO Data Lab produces — transit network analysis, ridership and demand modeling, station area analysis, equity mapping, and building the public case for passenger rail investment in Ohio.

Entries are grouped by type. Each entry includes a brief description, its primary use case at AAO, and a link to the source.

---

## Open Geospatial Datasets

### Overture Maps Foundation
**Source:** [overturemaps.org](https://overturemaps.org) | **License:** CDLA Permissive 2.0  
A collaborative, openly licensed map dataset backed by Amazon, Microsoft, Meta, and TomTom. Overture provides globally consistent, deduplicated data across four themes: **places** (businesses and POIs), **buildings** (global footprints), **transportation** (road and rail network segments), and **base** (land use, water, administrative boundaries). Released as GeoParquet files queryable with DuckDB or GeoPandas. Particularly valuable for station area analysis at scale — Overture's transportation schema includes segment-level attributes that outperform raw OSM for routing.

### Microsoft Global ML Building Footprints
**Source:** [GitHub — microsoft/GlobalMLBuildingFootprints](https://github.com/microsoft/GlobalMLBuildingFootprints) | **License:** ODbL  
Machine-learning-derived building footprints for over 1.4 billion buildings globally, generated from Bing satellite imagery using semantic segmentation models. Covers the contiguous US at very high completeness. At the station area level, building footprints are essential for density analysis, transit-oriented development (TOD) assessments, and parking lot quantification (large impervious surface clusters with no footprint = structured parking). Available as GeoJSON and GeoParquet by region.

### Google Open Buildings
**Source:** [sites.research.google/open-buildings](https://sites.research.google/open-buildings) | **License:** CC BY 4.0  
A complementary global building footprint dataset derived from Google's satellite imagery pipeline. Covers approximately 2 billion buildings across Africa, Asia, Latin America, and parts of Europe. For US-focused AAO work, this is most useful as a cross-reference against Microsoft's dataset or for international rail comparison studies. Includes a confidence score per footprint, which is useful for filtering.

### GTFS Feeds (General Transit Feed Specification)
**Source:** [Transitland](https://www.transit.land), [Mobility Database](https://mobilitydatabase.org) | **License:** varies by agency  
The GTFS standard defines the format for public transit schedules published by transit agencies — stops, routes, trips, stop times, calendar, and fare information. The GTFS Realtime extension adds live vehicle positions and service alerts. For Ohio, the relevant agencies include COTA (Columbus), RTA (Cleveland), SORTA (Cincinnati), DARTA (Dayton), and others. Aggregated GTFS catalogs like Transitland allow you to pull feeds for any agency in one query. GTFS feeds are the foundation of any service frequency analysis, headway mapping, or accessibility isochrone study.

### OpenAddresses
**Source:** [openaddresses.io](https://openaddresses.io) | **License:** varies by country/state (mostly ODbL or CC)  
A global, community-assembled dataset of address points sourced from government open data portals (county auditors, city GIS departments, state DOTs). Covering hundreds of millions of address points in the US alone, OpenAddresses is more granular and authoritative than OSM-derived addresses. At AAO, it's useful for population-weighted catchment analysis around proposed or existing stations — instead of approximating from census blocks, you can geocode directly to address points and compute walking distance distributions.

### WSF Evolution (World Settlement Footprint Evolution)
**Source:** [DLR / ESA — WSF Evolution](https://www.dlr.de/eoc/en/desktopdefault.aspx/tabid-9628/16557_read-40454) | **License:** CC BY 4.0  
A satellite-derived global dataset mapping the growth of human settlements from 1985 to 2015, produced by the German Aerospace Center (DLR) using Landsat and Sentinel imagery. Each pixel is a 10-meter binary classification of settled vs. unsettled land for each year in the series. For transit advocacy, this is uniquely powerful for visualizing how settlement patterns have sprawled in Ohio metro areas over four decades — creating the visual argument that car-dependent development and transit disinvestment are directly linked. Deployable as raster overlays in Folium or deck.gl.

---

## Python Geospatial Libraries

### OSMnx
**Source:** [github.com/gboeing/osmnx](https://github.com/gboeing/osmnx) | **Install:** `pip install osmnx`  
A Python library for downloading, modeling, analyzing, and visualizing street networks and other geospatial features from OpenStreetMap. OSMnx wraps the OSM Overpass API and returns NetworkX graph objects directly — meaning you can go from "download the pedestrian network for downtown Columbus" to "compute all 10-minute walking isochrones from Union Station" in under 20 lines of Python. Also handles building footprints, amenities, and transit stops from OSM. Pairs naturally with GeoPandas for spatial joins and with Folium or Matplotlib for visualization.

### GeoPandas
**Source:** [geopandas.org](https://geopandas.org) | **Install:** `pip install geopandas`  
The foundational Python library for vector geospatial data analysis. GeoPandas extends Pandas DataFrames with a `geometry` column, enabling spatial operations (unions, intersections, buffers, spatial joins) directly on tabular data. Reading and writing Shapefiles, GeoJSON, GeoParquet, and GPKG is built-in via `fiona`. At AAO, GeoPandas is the workhorse for nearly any station area analysis: buffer stops, join census demographics, compute area statistics, export GeoJSON for web maps. Works seamlessly with the rest of this stack — OSMnx outputs GeoPandas GeoDataFrames, PySAL accepts them, and Folium/Matplotlib render them.

### NetworkX
**Source:** [networkx.org](https://networkx.org) | **Install:** `pip install networkx`  
Python's standard library for creating, manipulating, and analyzing graphs and networks. For transit work, NetworkX underpins OSMnx's network analysis (shortest paths, centrality, connectivity) but is also independently useful for modeling transit networks as graphs — stops as nodes, routes as edges — and running analyses like betweenness centrality (which stops carry the most transfers?), Dijkstra pathfinding, or network resilience modeling. Critical for any project that needs to quantify the structural importance of a proposed rail line to a regional network.

### PySAL (Python Spatial Analysis Library)
**Source:** [pysal.org](https://pysal.org) | **Install:** `pip install pysal` (or individual submodules)  
A federation of Python libraries for spatial statistics and econometrics. PySAL is split into several subpackages: `esda` (exploratory spatial data analysis — Moran's I, spatial autocorrelation), `libpysal` (spatial weights matrices), `inequality` (spatial inequality measures), `mgwr` (multiscale geographically weighted regression), and `segregation` (dissimilarity indices and spatial segregation metrics). For AAO work, `esda` is most immediately applicable — mapping spatial clusters of transit access, identifying statistically significant concentrations of transit-dependent populations, and supporting equity arguments with rigorous spatial statistics.

### Matplotlib
**Source:** [matplotlib.org](https://matplotlib.org) | **Install:** `pip install matplotlib`  
Python's foundational 2D plotting library and the rendering backend for most geospatial visualization in this stack. While not GIS-specific, Matplotlib is how GeoPandas `.plot()` renders maps, and how most static figures suitable for reports and PDFs are produced. For AAO publications and the Scioto Analysis-style reports that commission projects intend to produce, Matplotlib generates print-quality figures. Pair with `contextily` to add basemap tiles (OpenStreetMap, Stamen Terrain) behind GeoPandas plots. Seaborn wraps Matplotlib for statistical chart types (box plots, heatmaps, distribution charts).

### Folium
**Source:** [python-visualization.github.io/folium](https://python-visualization.github.io/folium) | **Install:** `pip install folium`  
A Python wrapper around the Leaflet.js mapping library, producing interactive HTML maps from Python data objects. Folium maps can be embedded directly in Jupyter notebooks or exported as standalone HTML files suitable for publication on the AAO Data Lab site. Supports choropleth layers from GeoJSON/GeoPandas, marker clusters, heatmaps, and custom tile layers. For AAO, Folium is the right tool when you want stakeholders and the public to interact with a map (zoom, click for details, toggle layers) without building a full React + Mapbox application.

---

## Additional Datasets Identified for AAO Data Lab Needs

Beyond the libraries above, the following datasets and tools address specific research needs common to Ohio transit and rail advocacy work.

---

### National Transit Database (NTD)
**Source:** [transit.dot.gov/ntd](https://www.transit.dot.gov/ntd) | **Agency:** FTA  
The FTA's primary national database of transit system performance, finances, and ridership. Every transit agency receiving federal funds reports here annually. NTD data enables direct comparison of Ohio systems against peer metros, tracking ridership trends over time, and making the case that chronic underfunding (not low demand) drives poor performance. Particularly useful for Commission-type deliverables where the ask is a ridership and investment benchmarking study.

### Bureau of Transportation Statistics — National Transportation Atlas Database (NTAD)
**Source:** [bts.gov/ntad](https://www.bts.gov/ntad) | **Agency:** USDOT  
The BTS maintains a comprehensive geospatial dataset of national transportation infrastructure: rail lines, Amtrak routes and stations, highway networks, intermodal terminals, and aviation assets. Rail geometry here is authoritative for routing and station-placement analysis. Updated annually.

### Amtrak GTFS & Performance Data
**Source:** [data.amtrak.com](https://data.amtrak.com) | [Transitland](https://www.transit.land/feeds/f-9q9-amtrak)  
Amtrak publishes a GTFS feed covering all intercity routes. On-time performance data is separately available via the Amtrak API and has been compiled historically by researchers. For Ohio rail analysis, the Cardinal and Capitol Limited routes are the primary operative services — analyzing their on-time rates, dwell times, and ridership by segment is essential groundwork for any Ohio intercity rail advocacy deliverable.

### LEHD Origin-Destination Employment Statistics (LODES)
**Source:** [lehd.ces.census.gov](https://lehd.ces.census.gov/data) | **Agency:** US Census Bureau  
Census-derived data mapping where workers live and where they work at the census block level. LODES produces the most granular commute flow data available in the US: you can show exactly how many workers commute from a given neighborhood to a downtown employment center, and whether that corridor has transit service. Directly supports the economic-access argument for new rail and BRT corridors.

### American Community Survey (ACS) — Transportation Tables
**Source:** [census.gov/programs-surveys/acs](https://www.census.gov/programs-surveys/acs.html) | **Access:** `pip install census` or Census API  
The ACS 5-year estimates include Table B08301 (Means of Transportation to Work) and B08303 (Travel Time to Work), broken down by census tract. These are the standard equity-mapping inputs: percent of households without a vehicle, transit commute share by neighborhood, and time poverty (workers spending 45+ minutes commuting). The `censusdata` or `pygris` Python packages make it straightforward to pull these directly into a GeoPandas workflow.

### EPA Smart Location Database (SLD)
**Source:** [epa.gov/smartgrowth/smart-location-mapping](https://www.epa.gov/smartgrowth/smart-location-mapping) | **Agency:** EPA  
A nationwide census-block-group-level dataset with over 90 measures of built environment, accessibility, and transit service. Key fields include: employment and housing density, intersection density (walkability proxy), distance to nearest transit stop, job accessibility by auto and transit, and bicycle network density. The SLD is the empirical backbone for transit-oriented development arguments — it can show, with statistical rigor, that areas near rail stations have measurably different built environments and transit outcomes than similar areas without service.

### OpenStreetMap via Overpass API
**Source:** [overpass-api.de](https://overpass-api.de) | **Access:** OSMnx, `pip install overpy`  
Beyond what OSMnx wraps, the Overpass API allows direct querying of any OSM feature by tag. For AAO, this means extracting rail infrastructure (tracks, stations, platforms, signals), cycling infrastructure, and pedestrian paths with full attribute data. OSM's `railway=*` tag schema covers heavy rail, light rail, subway, tram, monorail, and preserved railways — useful for mapping Ohio's existing and former rail corridors. The `overpy` library provides a lower-level interface when custom queries are needed.

### H3 — Uber Hexagonal Hierarchical Spatial Index
**Source:** [h3geo.org](https://h3geo.org) | **Install:** `pip install h3`  
A hierarchical hexagonal grid system developed by Uber for geographic analysis. H3 divides the world into equal-area hexagons at multiple resolution levels (0–15). For transit work, H3 is useful for aggregating point data (stops, ridership, demographics) to a consistent spatial unit that doesn't inherit the arbitrary shape problems of census tracts or ZIP codes. Hexagonal binning also produces more visually intuitive density maps than square grids. Pairs well with GeoPandas and deck.gl.

### Replica (Travel Demand Data)
**Source:** [replicahq.com](https://replicahq.com) | **License:** Commercial (academic/nonprofit tiers available)  
Replica synthesizes travel demand data from anonymized mobile location data, producing estimates of daily trip volumes, mode shares, and origin-destination flows at the census block level. For Ohio, it can answer "How many people currently make trips between Cleveland and Columbus?" and disaggregate them by travel mode, purpose, and time of day. Particularly well-suited to the demand analysis phase of Commission-type projects. Academic and nonprofit access may be available at reduced cost.

### TIGER/Line Shapefiles
**Source:** [census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html) | **Access:** `pip install pygris`  
The Census Bureau's authoritative geospatial boundaries for all US administrative and statistical geographies: states, counties, census tracts, block groups, blocks, ZIP Code Tabulation Areas (ZCTAs), congressional districts, and more. The `pygris` Python package wraps the Census TIGER API and returns GeoPandas GeoDataFrames directly — no file downloads needed. Essential for any analysis that needs to join demographic data to geography or clip datasets to Ohio.

### Transitland
**Source:** [transit.land](https://www.transit.land) | **Access:** REST API (free tier available)  
An open, aggregated registry of GTFS feeds from transit agencies worldwide, maintained by Interline Technologies. Transitland provides a single API endpoint to query routes, stops, operators, and feed history across thousands of agencies without managing individual GTFS file downloads. Especially useful for multi-system comparisons (e.g., comparing Ohio metro bus frequency to Pittsburgh, Louisville, or Indianapolis) and for historical service analysis when an agency no longer publishes older feeds.

### Socrata Open Data APIs (Ohio and Local Governments)
**Source:** varies — [data.ohio.gov](https://data.ohio.gov), [data.columbus.gov](https://data.columbus.gov), [data.census.gov](https://data.census.gov)  
Ohio and its largest cities publish datasets through Socrata-powered open data portals. Relevant datasets include ODOT crash records by location, Columbus traffic counts, Cuyahoga County parcel data, and ODOT project funding tables. The `sodapy` Python client library provides a uniform interface to any Socrata portal. Cross-referencing ODOT project spending with transit investment gaps is a compelling data narrative for rail advocacy.

---

## Quick-Reference Tool Matrix

| Tool / Dataset | Type | Primary AAO Use Case |
|---|---|---|
| Overture Maps | Dataset | Station area base layers, routing network |
| MS Global Buildings | Dataset | Density / TOD / parking analysis |
| Google Open Buildings | Dataset | Cross-reference, international comparisons |
| GTFS Feeds | Dataset | Service frequency, headway, accessibility |
| OpenAddresses | Dataset | Population-weighted catchment analysis |
| WSF Evolution | Dataset | Settlement sprawl & TOD visual arguments |
| OSMnx | Python library | Street network + walkability analysis |
| GeoPandas | Python library | All vector spatial data wrangling |
| NetworkX | Python library | Transit network graph modeling |
| PySAL | Python library | Spatial statistics & equity analysis |
| Matplotlib | Python library | Static print-quality figures and maps |
| Folium | Python library | Interactive web-embeddable maps |
| NTD | Dataset | System performance & investment benchmarking |
| BTS NTAD | Dataset | Rail line geometry, national infrastructure |
| Amtrak GTFS | Dataset | Ohio intercity route analysis |
| LODES | Dataset | Commute flow origin-destination analysis |
| ACS Transportation Tables | Dataset | Car-free households, transit commute shares |
| EPA Smart Location DB | Dataset | TOD built-environment metrics |
| H3 | Python library | Uniform hexagonal spatial aggregation |
| Replica | Dataset (commercial) | Travel demand + mode share estimates |
| TIGER/Line / pygris | Dataset + library | Census geography boundaries for Ohio |
| Transitland | Dataset / API | Multi-agency GTFS aggregation |
| Socrata (Ohio portals) | Dataset / API | ODOT crash, traffic, parcel, project data |

---

## Getting Help

Questions about using any of these datasets or tools in an AAO Data Lab project? Ask in the `#data-resources` channel in the [AAO Slack](https://join.slack.com/t/lab-allaboardohio/shared_invite/zt-3x7cyvl53-0IQMjvljmA64iNCZvhaP1w) or open a discussion on the [aao-dev-docs](https://github.com/all-aboard-ohio/aao-dev-docs) repository.
