# IronHack Final Project: Improving the Recreational Landscape of a Berlin Municipality

## Objective
Develop a dashboard mapping sporting facilities in one region of Berlin, using municipal recreational data and incorporating local health/social data, with goal of facilitating data-driven decision-making regarding resource allocation.

## Data Sources
- Municipal Recreational Data (various excel tables)
- "Life-World-Oriented" Map, geojson - [Lebensweltlich orientierte Räume (LOR)](https://daten.odis-berlin.de/de/dataset/lor_planungsgraeume/)
- Berlin Health and Social Atlas/Index 2022 - [Gesundheits- und Sozialstrukturatlas Berlin 2022](https://daten.berlin.de/datensaetze/gesundheits-und-sozialstrukturatlas-berlin-2022-indexwerte-auf-ebene-der-prognoseräume)

## Approach
### Data Cleaning
3 excel tables with data collected regarding recreational facilities were used: informal outdoor, formal outdoor/uncovered and formal indoor/covered. Several columns were removed, for lack of relevance. For the most part, NaNs were left in place, as it was generally not necessary to remove them. The attributes used for the scoring system were later on converted into binary values.

### Converting  Geocoordinate System
Tableau did not seem to natively support UTM (Universal Transverse Mercator) coordinates for mapping, and works primarily with latitude and longitude coordinates. To use UTM coordinates in Tableau, you would typically need to convert them to latitude and longitude. The conversion from UTM coordinates to latitude and longitude coordinates was performed using the Pyproj library's transform function. The UTM coordinates were transformed from the UTM projection to the WGS84 (World Geodetic System 1984) projection, resulting in latitude and longitude values.

### Scoring Outdoor Formal Facilities
Weights were assigned to attributes of outdoor/formal sports facilities (BZR level) to evaluate their quality. The other two tables could not be used in this case, as they did not contain the same attributes as descriptors for sporting facilities. 

Attributes were transformed into binary values, with higher scores indicating better quality. Taken into account was: security, proper lining, lighting, sound system, irrigation, containment fence, drainage, coach-zone. For the example run, "security" was given a higher weight, to indicate importance and urgency. This can be tweaked later, to suit the needs of the stakeholders. First, LabelEncoder from the scikit-learn library was used to convert categorical columns into binary values (1 or 0), and specifically encoded "security deficiency" as 1 for "No" and 0 for "Yes" (since this column would be negative if ticked, and all others would be positive). Then, an additional column called 'quality_score' was created, where a weighted scoring system was applied. This process ensures that each informal outdoor/uncovered facility's quality is assessed using a standardized scoring system.

### Bringing Social/Health Data into Planning Zones

## Visualization

## Next Steps
### Fine Tuning Map Features
adding dyanmic zone, improving relationships between dataframes
### Adding a third regional map layer
### Responding to needs/reality of municipality



