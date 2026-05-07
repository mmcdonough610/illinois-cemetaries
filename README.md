
# Land Cover Context of Illinois Cemeteries



## Project Contents



- [Data Source](#data-source)
- [Project Background](#project-background)
- [Purpose](#purpose)
- [Mapmaking Process](#mapmaking-process)
- [Map Summary](#map-summary)
- [Final Project Link](#final-project-link)

***

### Data Source

State and County data can be found here:
[Link to U.S. Census Bureau](https://www.census.gov/cgi-bin/geo/shapefiles/index.php)

Cemetery data can be found here: 
[Link to Illinois Geospatial Data Clearinghouse](https://clearinghouse.isgs.illinois.edu/data/infrastructure/us-geographic-names-information-system-gnis-illinois)

Land Cover data can be found here: 
[Link to Multi-Resolution Land Characteristics Consortium](https://www.mrlc.gov/data)

* **Initial Data projection: EPSG:4269 - NAD83**
* **Final Map projection: EPSG:26971 - NAD83/Illinois East**

### Project Background

For this map, the goal was to encompass everything I had learned in the course as well as incorporate topics I've learned in my other courses. The land cover classification is derived from a remote sensing fundamentals course and the cemeteries is a main focus within forensic anthropology.

### Purpose

Understanding cemetery locations is important for a number of reasons in forensic anthropology. Knowing where a cemetery is located can help with access, determine if the cemetery is in danger of being destroyed by the environment it resides, or if the area was abandoned. A map like this may also help the contrustion of future cemeteries as if an area is at risk for sinking or another type of environmental hazard, it is less likely another cemetery will be built in that area. 

### Mapmaking Process

Below are the steps taken to create the map that is linked in this file:

1. Find and download data from sources listed above.
2. Within QGIS, upload each of the data files from above. The U.S. Census Bureau files were uploaded as vector layer, the IGDC data was also a vector layer, while the MRLC NLCD was a raster layer. 
3. Filter the NLCD layer to just be Illinois using the 'NAME'="Illinois" query. To obtain proper placement of Illinois cemeteries, in the IGDS layer, using the query builder use 'FEATURE_NA'="Cemetery", this is the same process for the Bureau layers. 
4. Once filtered, the Illinois state outline and county outlines were made transparent with just a border. The NLCD layer was kept the same colors as the original map. The cemeteries needed to be edited.
5. For the cemetery layer, labels needed to be created to show the land cover type of the cemetery. To do this, the attribute table needed to be edited through the Field Calculator. In the calculator's query builder the following was added to connect the land cover types to the cemetery locations:
**CASE**
    **WHEN "sample_1" = 11 THEN 'Water'**
   **WHEN "sample_1" IN (21,22,23,24) THEN 'Developed'**
    **WHEN "sample_1" IN (41,42,43) THEN 'Forest'**
    **WHEN "sample_1" IN (52,71) THEN 'Shrub/Grass'**
    **WHEN "sample_1" IN (81,82) THEN 'Agriculture'**
    **WHEN "sample_1" IN (90,95) THEN 'Wetland'**
    **ELSE 'Other'**
**END**
6. After the values are connected, they were color-coordinated using the Symbology tab and changing the symbol type to Categorized.
7. Map is completed! 


### Map summary

This map illustrates every known cemetery in the state of Illinois and the county that they reside as well as the land cover type that the cemetery was built in. With the second cropped version of the map focusing on the Northeastern part of Illinois as Cook and Will county, two of the largest counties, are in this area, which equated to a lot of marked cemeteries in the "Developed" class for the land cover classification. With that, each land cover type is expressed in a color per the MRLC and the cemeteries are also expressed in a color that relates them to one of the land cover classifications. The values this comes from is within the attribute table of the NLCD layer. For example, if an area has a 'pixel value' of 11, then the area is considered 'Open Water'. So, if a cemetery were in water, the cemetery dot would be orange. This is the same for all cemeteries and cover types. 

## Final Project Link

Here you are linking from the README.md to the index.html.

Please view the [final map online](www.github...)
