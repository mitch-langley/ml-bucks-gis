<h1>BUCKS COUNTY, PA - GIS DATASET REPOSITORY</h1>

<h2>OVERVIEW</h2>

<p>
This repository contains a curated collection of vector GIS datasets for <b>Bucks County, Pennsylvania</b>. 
The datasets are organized by subject area and are intended for local planning, land use, transportation, 
property, environmental, and spatial analysis.
</p>

<p>
Most datasets are stored as OGC GeoPackage (<code>.gpkg</code>) files. Large countywide property datasets, 
including parcels and site addresses, are divided by municipality to make them easier to manage, query, 
and load in GIS software.
</p>

<p>
  <b>Primary format:</b> OGC GeoPackage (<code>.gpkg</code>)<br>
  <b>Recommended working CRS:</b> NAD83 / Pennsylvania South (ftUS), <code>EPSG:2272</code><br>
  <b>Geographic coverage:</b> Bucks County, Pennsylvania<br>
  <b>Primary use:</b> QGIS, GeoPandas, GDAL/OGR, spatial databases, and other GIS applications
</p>

<h2>REPOSITORY STRUCTURE</h2>

<pre>
bucks_co_gis/
│
├── 01_admin/
│   ├── municipalities.gpkg
│   │   └── Municipal boundaries
│   └── school_districts.gpkg
│       └── School district boundaries
│
├── 02_property/
│   ├── parcels/
│   │   └── Parcel boundaries split by municipality
│   └── site_addresses/
│       └── Site/address points split by municipality
│
├── 03_planning/
│   ├── proposed_developments.gpkg
│   │   └── Proposed land development projects
│   └── zoning.gpkg
│       └── Municipal zoning classifications
│
├── 04_preservation/
│   ├── agricultural_preservation.gpkg
│   │   └── Agricultural conservation easements
│   ├── land_trust_owned.gpkg
│   │   └── Land trust property boundaries
│   ├── natural_areas.gpkg
│   │   └── Natural inventory and resource areas
│   ├── parks_open_space.gpkg
│   │   └── Public parks and open space areas
│   └── preserved_parcels.gpkg
│       └── Preserved land parcels
│
├── 05_environment/
│   ├── streams_nhd.gpkg
│   │   └── Streams and surface water features from the NHD
│   └── watersheds.gpkg
│       └── Watershed boundaries
│
├── 07_transportation/
│   ├── bridges.gpkg
│   │   └── Bridge locations
│   ├── major_roads.gpkg
│   │   └── Major transportation corridors
│   ├── penndot_roadway_segments.gpkg
│   │   └── PennDOT roadway network segments
│   ├── rail_lines.gpkg
│   │   └── Active and inactive rail lines
│   ├── railroad_crossings.gpkg
│   │   └── At-grade railroad crossings
│   ├── road_centerlines.gpkg
│   │   └── County road centerline network
│   ├── traffic.gpkg
│   │   └── Traffic count and volume locations
│   ├── transportation_projects_lines.gpkg
│   │   └── Linear transportation projects
│   └── transportation_projects_points.gpkg
│       └── Point-based transportation projects
│
└── 08_environmental_regulatory/
    ├── air_emission_plants.gpkg
    │   └── Permitted air emission facilities
    ├── captive_hazardous_waste.gpkg
    │   └── Hazardous waste facilities
    ├── industrial_mineral_mining.gpkg
    │   └── Industrial mineral mining sites
    └── land_recycling_cleanup_sites.gpkg
        └── Act 2 land recycling and cleanup sites
</pre>

<h2>DATA ORGANIZATION</h2>

<h3>Countywide Layers</h3>

<p>
Most thematic datasets are stored as a single countywide GeoPackage. These files can normally be loaded 
directly into QGIS or accessed programmatically without additional preprocessing.
</p>

<h3>Municipality-Level Property Layers</h3>

<p>
The datasets in <code>02_property/parcels/</code> and <code>02_property/site_addresses/</code> are divided 
into separate files by municipality. This avoids working with unnecessarily large countywide files when 
analysis only concerns one or several municipalities.
</p>

<p>
Municipality-level files can be analyzed independently or merged when countywide coverage is required.
</p>

<h2>USING THE DATA IN QGIS</h2>

<h3>OPTION A: Drag and Drop</h3>

<ol>
  <li>Open QGIS.</li>
  <li>Open File Explorer on Windows or Finder on macOS.</li>
  <li>Navigate to the local copy of this repository.</li>
  <li>Drag a <code>.gpkg</code> file directly into the QGIS map canvas or <b>Layers</b> panel.</li>
  <li>If the GeoPackage contains more than one layer, QGIS will prompt you to select the layer or layers to add.</li>
</ol>

<h3>OPTION B: QGIS Browser Panel</h3>

<ol>
  <li>Open the <b>Browser</b> panel in QGIS.</li>
  <li>Browse to the local <code>bucks_co_gis</code> directory.</li>
  <li>Optionally add the repository directory to <b>Favorites</b> for easier access.</li>
  <li>Expand a directory such as <code>02_property/parcels/</code>.</li>
  <li>Expand or double-click a GeoPackage to inspect its layers.</li>
  <li>Drag the desired layer onto the map canvas.</li>
</ol>

<h3>OPTION C: Add Vector Layer</h3>

<ol>
  <li>Go to <b>Layer</b> &gt; <b>Add Layer</b> &gt; <b>Add Vector Layer...</b>.</li>
  <li>For the source type, select <b>File</b>.</li>
  <li>Click the browse button next to <b>Vector Dataset(s)</b>.</li>
  <li>Select one or more <code>.gpkg</code> files.</li>
  <li>Click <b>Add</b>.</li>
</ol>

<h2>WORKING WITH PARCELS AND ADDRESSES</h2>

<p>
Because parcel and address data are stored by municipality, multiple files may need to be combined for 
cross-municipal or countywide analysis.
</p>

<h3>Merge Layers in QGIS</h3>

<ol>
  <li>Load the desired municipal parcel or address layers.</li>
  <li>Go to <b>Vector</b> &gt; <b>Data Management Tools</b> &gt; <b>Merge Vector Layers...</b>.</li>
  <li>Select the municipal layers to combine.</li>
  <li>Confirm that the coordinate reference systems are compatible.</li>
  <li>Choose an output GeoPackage or use a temporary layer.</li>
  <li>Click <b>Run</b>.</li>
</ol>

<h3>Python / GeoPandas</h3>

<p>
GeoPackage files can also be read directly with GeoPandas:
</p>

<pre><code>import geopandas as gpd

gdf = gpd.read_file(
    "02_property/parcels/doylestown_borough.gpkg"
)

print(gdf.crs)
print(gdf.columns)
print(gdf.head())
</code></pre>

<p>
Multiple municipal datasets can be combined with <code>pandas.concat()</code> or processed individually 
depending on the analysis.
</p>

<h2>COORDINATE REFERENCE SYSTEMS</h2>

<p>
For local analysis in Bucks County, the recommended projected coordinate reference system is:
</p>

<pre><code>EPSG:2272
NAD83 / Pennsylvania South (ftUS)
</code></pre>

<p>
This CRS is appropriate for local measurements and spatial analysis where U.S. survey feet are useful.
</p>

<p>
Other coordinate systems may be useful depending on the application:
</p>

<ul>
  <li>
    <b>EPSG:2272, NAD83 / Pennsylvania South (ftUS):</b>
    recommended for local and regional GIS analysis.
  </li>
  <li>
    <b>EPSG:4326, WGS 84:</b>
    useful for geographic coordinates, GPS data, and general data interchange.
  </li>
  <li>
    <b>EPSG:3857, WGS 84 / Pseudo-Mercator:</b>
    commonly used by web mapping and online basemap services.
  </li>
</ul>

<p>
QGIS performs on-the-fly reprojection, so individual layers do not need to be permanently converted simply 
to display them together.
</p>

<h3>Set the Project CRS in QGIS</h3>

<ol>
  <li>Click the CRS indicator in the lower-right corner of the QGIS window.</li>
  <li>Search for <code>EPSG:2272</code>.</li>
  <li>Select <b>NAD83 / Pennsylvania South (ftUS)</b>.</li>
  <li>Click <b>OK</b>.</li>
</ol>

<h2>DATA SOURCES AND CURRENCY</h2>

<p>
The repository consolidates datasets obtained from multiple public GIS and government sources. Depending 
on the layer, source agencies may include Bucks County, the Commonwealth of Pennsylvania, PennDOT, 
Pennsylvania DEP, and federal geospatial programs.
</p>

<p>
Datasets represent snapshots of the source data at the time they were obtained or processed. They should 
not be assumed to represent current legal, regulatory, ownership, zoning, environmental, or infrastructure 
conditions without verification against the authoritative source.
</p>

<h2>NOTES</h2>

<ul>
  <li>This repository is a <b>curated analytical dataset</b>, not a complete mirror of every available Bucks County GIS layer.</li>
  <li>Directory numbering is intentionally thematic. Unused numbers may be reserved for categories not currently included in the repository.</li>
  <li>GeoPackage attribute schemas vary because the datasets originate from different agencies and source systems.</li>
  <li>Geometry types, field names, update dates, and source CRS may therefore differ between datasets.</li>
  <li>When performing measurements or geometric operations, use an appropriate projected CRS rather than Web Mercator.</li>
  <li>For legal, engineering, surveying, permitting, or regulatory decisions, verify information against the responsible government agency or authoritative record.</li>
</ul>

<h2>SOFTWARE COMPATIBILITY</h2>

<p>
The GeoPackage format used throughout the repository is supported by most modern GIS software and libraries, including:
</p>

<ul>
  <li>QGIS</li>
  <li>ArcGIS Pro</li>
  <li>GDAL / OGR</li>
  <li>GeoPandas</li>
  <li>Pyogrio</li>
  <li>Fiona</li>
  <li>SQLite / SpatiaLite-compatible workflows</li>
</ul>
