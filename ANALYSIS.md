# Geospatial MCP landscape: strategic overview

Snapshot of the catalog on 2026-10-29: 113 servers, health checked 2026-10-29.
The tables in `README.md` are generated and stay current. This file is a hand-written analysis and does not update itself, so re-run the numbers before relying on them later.

## Summary

The catalog shows a market that is broad but uneven. Everyday location tasks (geocoding, routing, place search, weather) are well covered, mostly by open-source servers over OpenStreetMap and public data. Commercial value is concentrating in two places: hosted servers run by data vendors, and the large mapping platforms, which now publish their own servers. Analysis-heavy work (spatial databases, desktop GIS, geoprocessing) has fewer servers and almost no vendor involvement. Some capability areas have no servers in the catalog at all.

| Measure | Value |
| --- | --- |
| Servers | 113 across 12 categories |
| Access | 48 open · 4 free · 53 commercial · 8 paywalled |
| Published by the vendor (`official`) | 47 (42%) |
| Health | 64 active · 27 hosted · 18 stale · 3 pending · 1 archived |
| Deployment | 54 local · 30 hosted · 15 local+hosted · 5 self-hosted · 1 add-in · 8 unknown |
| Usable from web clients (hosted or local+hosted) | 45 (40%) |
| Implementation language, where known | Python 39 · TypeScript 25 · JavaScript/Node 4 · other 5 |

## Coverage by category

| Category | Servers | Open or free | Commercial or paywalled | Official | Stale or archived |
| --- | ---: | ---: | ---: | ---: | ---: |
| Maps, tiles & commercial platforms | 19 | 0 | 19 | 13 | 6 |
| Geocoding & place search | 18 | 9 | 9 | 6 | 5 |
| Remote sensing (STAC / EO) | 17 | 6 | 11 | 9 | 1 |
| Weather & climate | 12 | 12 | 0 | 1 | 2 |
| Desktop & enterprise GIS | 10 | 5 | 5 | 0 | 3 |
| Geospatial data access & catalogs | 10 | 6 | 4 | 8 | 0 |
| GIS / geoprocessing toolkits | 7 | 6 | 1 | 2 | 0 |
| Aviation & maritime tracking | 6 | 3 | 3 | 1 | 0 |
| Parcels & property | 5 | 0 | 5 | 4 | 0 |
| Other (IP geolocation, misc) | 4 | 1 | 3 | 2 | 1 |
| Spatial databases | 3 | 2 | 1 | 1 | 0 |
| Routing, isochrones & navigation | 2 | 2 | 0 | 0 | 1 |

The category counts understate some capabilities. Routing is the clearest case: only 2 servers sit in the routing category, but 15 servers carry the `routing` tag, because most mapping platforms bundle routing with geocoding and search.

## Patterns

### Commodity location services are saturated

Geocoding, reverse geocoding, place search and routing appear in more servers than any other capability: 21 servers carry the `geocoding` tag. Seven of the 18 geocoding servers wrap OpenStreetMap services (Nominatim or Overpass), and they overlap heavily. Five of the 18 are stale. A new geocoding server adds little unless it brings different data or a different way of working, such as Overture places (PlaceRoot), US address verification and postal enrichment (Smarty, Zip-Codes.com) or fully offline lookups from a local file (GridPin, the catalog's first offline geocoder).

### The major platforms have arrived, with gaps

13 of the 19 mapping-platform servers are official, including Mapbox, TomTom, MapQuest, CARTO, Felt, Geobble, Cesium and an Esri beta. Two large ecosystems still depend on community work:

- **Google Maps** has four entries and none is official. The reference server has been archived, and the remaining three are community wrappers.
- **Esri / ArcGIS** has seven entries across categories. One is an official beta (ArcGIS Location Services). The rest are community servers or third-party platforms, including both ArcGIS Pro integrations.

Being official does not guarantee upkeep. The Baidu, Foursquare and Stadia Maps servers are official but stale.

Vendors are also starting to replace community wrappers of their own APIs. Geoapify now publishes an official hosted server, which sits beside the older community server for the same API. That community server is stale.

### Data vendors prefer hosted servers

Of the 30 hosted servers, nearly all come from vendors selling data or a platform: parcel and zoning data (Regrid, LandRecords.us, MAIA, Pluia), imagery (Vexcel, Planet, Planetary Computer Pro, SkyWatch), address and postal data (Smarty, Zip-Codes.com), location services (Geoapify), mobility and foot-traffic data (Factori), mineral-exploration data (geoDB), geotagged photos (Fotoshi) and cloud GIS (CARTO, Felt, GIS Cloud, Geobble). A hosted server keeps the vendor's data and API keys on their side and lets them update tools without users reinstalling anything. We expect this to become the default delivery model for commercial geodata, and recent additions bear that out: six of the seven servers added between 2026-10-16 and 2026-10-29 are hosted servers published by the vendor. It also changes what the catalog can check: a hosted server has no source code to scan, so trust rests on the vendor's domain.

### Where servers run

Every entry records a `deployment` value: where the server runs and who runs it.

| Deployment | Servers | Official | Community | What it means for the user |
| --- | ---: | ---: | ---: | --- |
| Local | 54 | 12 | 42 | Install it; your client starts it on your machine. Needs a desktop client. |
| Hosted | 30 | 28 | 2 | Connect to the vendor's URL. Works from web clients; queries go to the vendor. |
| Local + hosted | 15 | 5 | 10 | Run it yourself, or use a public endpoint someone else runs. |
| Self-hosted | 5 | 0 | 5 | Deploy it as an HTTP service yourself. |
| Add-in | 1 | 0 | 1 | Runs inside a desktop application (ArcGIS Pro). |
| Unknown | 8 | 2 | 6 | The README does not say. |

Vendors host and the community ships local servers. Six in ten official servers (28 of 47) are hosted, while nearly two thirds of the community servers (42 of 66) run locally. Only 45 servers, 40% of the catalog, can be used from a web client such as claude.ai without installing anything.

The public endpoints in the local + hosted group mostly come from two community operators, not from the data vendors. Pipeworx runs gateway endpoints for six servers (MapTiler, Nominatim, what3words, OSRM, ATTOM and EarthScope), and cyanheads runs public instances of four (OpenStreetMap, Open-Meteo, OpenAQ and NOAA Marine). These are convenient, but a user's queries then go to a third party that is neither the user nor the data provider.

Maintenance follows the same split. 13 of the 18 stale servers are local, and all 15 local + hosted servers are active, because someone has to keep a public endpoint running.

By category, the pattern follows the work. Desktop GIS and geoprocessing toolkits are almost entirely local, because they drive software or data on the user's machine. Parcels and property data is entirely remote, because the value is the vendor's dataset.

### Earth observation is the most commercially varied area

Remote sensing has the widest spread of access models in the catalog: open STAC and NASA/ESA access, Earth Engine wrappers, imagery marketplaces (SkyFi, SkyWatch), and paid-only vendor platforms. Three of the catalog's eight paywalled servers are here. Newer entries go beyond search and download to embeddings and similarity search (LGND) and array-data queries over Zarr (Arraylake), which suggests the area is moving from data access towards analysis. Discovery is improving too: AWS now publishes an official server for its Registry of Open Data, which finds datasets with STAC endpoints and previews public S3 buckets.

### Weather is open and US-heavy

All 12 weather servers are open or free. Most of them draw on NOAA and the US National Weather Service, or on Open-Meteo for global coverage. Outside the US, only Canada has a national service in the catalog. European services such as ECMWF open data, DWD and the Met Office do not appear, except through Open-Meteo's ERA5 data. A search for European options on 2026-10-15 found no official servers: Rainbow.ai offers a precipitation nowcasting API but no MCP server, and the one Buienradar server is a small, unmaintained community project.

### Analysis tools are thin and community-built

Spatial databases (3 servers), desktop GIS (10) and geoprocessing toolkits (7) together make up less than a fifth of the catalog. No desktop GIS server is official: all five QGIS servers and both ArcGIS Pro servers come from the community. The newest, gis-agent-bridges, is a single community project with bridges for nine desktop packages, including SuperMap, GeoScene and MapGIS, which the catalog did not cover before; by its own account, most of those bridges have not yet been tested against the real software. For agents that do GIS analysis beyond lookups, this is the least mature part of the market and the most open to new work.

## Gaps

These capabilities have no dedicated server in the catalog. Some may exist but not be listed yet, so each gap is a prompt to search before it is a conclusion.

| Capability | What the catalog has today |
| --- | --- |
| Public transit (GTFS, schedules, real-time) | Nothing |
| Fleet and logistics optimisation (vehicle routing, dispatch) | Trip optimisation inside OSRM MCP only |
| Cloud warehouse spatial SQL (BigQuery, Snowflake, Databricks) | Wherobots (Apache Sedona), plus warehouse access through CARTO and Felt |
| Natural hazards (wildfire, flood, earthquake) as a focus | Natural-risk lookups inside TerraLab; wildfire inside weather-mcp; earthquakes inside God's Eye View and the EarthScope server |
| Demographics and census data | Census tract demographics in Zip-Codes.com, population estimates in TerraLab, mobility-derived demographics in Factori (paid), and census enrichment inside Smarty |
| Elevation and terrain as a service | Spread across MapTiler, TerraLab, MapSmith and Open-Meteo |
| 3D, point clouds and digital twins | Cesium and one module of the Kiro power pack |
| Parcels and property outside the US and Canada | French zoning rules (Pluia) and French cadastral parcels (TerraLab); no ownership or valuation data |
| National weather services outside North America | Nothing (see above) |

## Implications

For someone choosing servers: commodity lookups are a solved problem, so choose on data quality, licence and vendor support rather than features. Prefer official or actively maintained servers. Check `deployment` first: if you work in a web client, only the hosted and local + hosted servers are open to you, and for any public endpoint, check who runs the domain.

For someone building servers: the open opportunities are in analysis and in under-served data. Desktop GIS automation, cloud warehouse spatial SQL, transit and hazard data have the clearest demand and the least supply. Another OSM geocoder does not.
