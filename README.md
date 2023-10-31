# IronHack Final Project: Improving the Recreational Landscape of a Berlin Municipality

## Objective
Develop a dashboard mapping sporting facilities in one region of Berlin, using municipal recreational data and incorporating local health/social data, with goal of facilitating data-driven decision-making regarding resource allocation.

## Data Sources
- Municipal Recreational Data (various excel tables)
- "Life-World-Oriented" Map, geojson - [Lebensweltlich orientierte Räume (LOR)](https://daten.odis-berlin.de/de/dataset/lor_planungsgraeume/)
- Berlin Health and Social Atlas/Index 2022 - [Gesundheits- und Sozialstrukturatlas Berlin 2022](https://daten.berlin.de/datensaetze/gesundheits-und-sozialstrukturatlas-berlin-2022-indexwerte-auf-ebene-der-prognoseräume)

## Approach
### Data Cleaning
Three tables containing data related to recreational facilities were utilized: informal outdoor, formal outdoor/uncovered, and formal indoor/covered. Unnecessary columns were removed, while NaNs (missing values) were retained, as they were generally not considered essential for removal. Attributes used in the scoring system were subsequently converted into binary values. Many values, particularly those related to sport facility types, were grouped to simplify filtering on the dashboard by reducing the number of distinct values. Since the three dataframes did not contain a large number of rows, they were eventually combined, facilitating a simpler upload to Tableau.

### Converting  Geocoordinate System
Tableau did not seem to natively support UTM (Universal Transverse Mercator) coordinates for mapping, and works primarily with latitude and longitude coordinates. To use UTM coordinates in Tableau, you would typically need to convert them to latitude and longitude. The conversion from UTM coordinates to latitude and longitude coordinates was performed using the Pyproj library's transform function. The UTM coordinates were transformed from the UTM projection to the WGS84 (World Geodetic System 1984) projection, resulting in latitude and longitude values.

### Scoring Outdoor Formal Facilities
Weights were assigned to attributes of outdoor/formal sports facilities (BZR level) to evaluate their quality. The other two tables could not be used in this case, as they did not contain the same attributes as descriptors for sporting facilities. 

Attributes were transformed into binary values, with higher scores indicating better quality. Taken into account was: security, proper lining, lighting, sound system, irrigation, containment fence, drainage, coach-zone. For the example run, "security" was given a higher weight, to indicate importance and urgency. This can be tweaked later, to suit the needs of the stakeholders. First, LabelEncoder from the scikit-learn library was used to convert categorical columns into binary values (1 or 0), and specifically encoded "security deficiency" as 1 for "No" and 0 for "Yes" (since this column would be negative if ticked, and all others would be positive). Then, an additional column called 'quality_score' was created, where a weighted scoring system was applied. This process ensures that each informal outdoor/uncovered facility's quality is assessed using a standardized scoring system.

### Bringing Social/Health Data into Planning Zones
In QGIS, data obtained from the "Health and Social Atlas 2022" was appended to the attribute table of a GeoJSON file containing regional polygons, establishing a spatial connection between the HSA 2022 dataset and the map.

## Visualization
The new Sports Facilities dataframe and two GeoJSON files containing the different regional polygon data were imported into Tableau, where relationships were created to associate them. Subsequently, filters were selected based on their potential value for future decision-makers.
![Screenshot 2023-10-31 at 22 40 50](https://github.com/JaydaBubel/IronHack_FinalProject/assets/129682724/d1e033a2-bfaa-4d84-937f-64b94feac21f)

## Next Steps
### Fine Tuning Map Features
- adding dyanmic zoom
- improving relationships between dataframes in tableau, resulting in a more seamless dashboard
  
### Adding a third regional map layer
- adding the third layer of LOR regions, relevant to decision-making
  
### Responding to needs/reality of municipality
- consulting stakeholders on their needs/wants for a dashboard, and making necessary changes


