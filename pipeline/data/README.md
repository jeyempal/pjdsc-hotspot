### **Quezon City Barangay Boundaries** (`qc-brgy-boundaries.geojson`)
#### *What is it?*
- `qc-brgy-boundaries.geojson` contains the geographic boundaries of all **142 Quezon City barangays**. It was created by filtering the nationwide `barangay-level-geom.geojson` file to records with Quezon City's `adm3_psgc` code, `1381300000`. The source is from a repository in Github, specifically the AltCoder Philippines PSGC shapefiles project.
* Each record represents one barangay. The file contains its boundary as a `MultiPolygon` and attributes that identify the barangay and describe the size of its geometry. Its coordinate reference system is **EPSG:32651 (UTM Zone 51N)**, so the coordinates are measured in meters rather than longitude and latitude.
#### *Attributes:*

| Attribute   | Meaning                                                                                            |
| ----------- | -------------------------------------------------------------------------------------------------- |
| `adm1_psgc` | PSGC code for the region. All records have `1300000000`, representing the National Capital Region. |
| `adm2_psgc` | PSGC code for the source data's second administrative level. All QC records have `1381300000`.     |
| `adm3_psgc` | PSGC code for the city. All records have `1381300000`, representing Quezon City.                   |
| `adm4_psgc` | Unique 10-digit PSGC code for each barangay. *Barangay ID*                                         |
| `adm4_en`   | Barangay name                                                                                      |
| `geo_level` | Geographic level of the record. Every value is `Bgy`, meaning barangay.                            |
| `len_crs`   | Approximate perimeter of the polygon in meters, stored as a whole number.                          |
| `area_crs`  | Approximate polygon area in square meters, stored as a whole number.                               |
| `len_km`    | Perimeter in whole kilometers, with the fractional part discarded by the source processing code.   |
| `area_km2`  | Area in whole square kilometers, with the fractional part discarded by the source processing code. |
| `geometry`  | The coordinates defining the barangay's `MultiPolygon` boundary.                                   |

### **2024 Quezon City Barangay Population** (`qc-brgy-population-2024.csv`)
#### *What is it?*
- `2024-QC-population.csv` contains a **2024 population count for each of Quezon City's 142 barangays**. Each row represents one barangay, identified by its PSGC code and name.
- The counts align with the PSA population data already reviewed for HOTSPOT: all 142 barangay codes and names match `qc-brgy-geon.geojson`, and the counts sum to **3,084,270 people**. The CSV contains no geographic boundaries; it can be joined to the boundary file using `adm4_psgc`.
#### *Attributes:*

| Attribute   | Meaning                                                                    |
| ----------- | -------------------------------------------------------------------------- |
| `adm4_psgc` | Unique 10-digit PSGC code for the barangay.                                |
| `adm4_en`   | Barangay name                                                              |
| `corr_code` | Nine-digit correspondence code associated with the barangay's PSGC record. |
| `2024_popu` | Number of people in the barangay in 2024.                                  |

### **Quezon City Barangay Mean NDVI, 2023–2025** (`qc-brgy-NDVI-2023-to-2025-comparison.csv`)
#### *What is it?*
- This CSV contains **one row for each of Quezon City's 142 barangays**, with a mean NDVI value for 2023, 2024, and 2025. All 142 barangay codes are unique, and none of the three NDVI columns has a blank value.
- NDVI is a **unitless indicator of vegetation greenness** calculated from Sentinel-2 satellite imagery. In the Earth Engine workflow, images were screened for clouds, a median NDVI image was produced for each calendar year, and the NDVI pixels within each barangay were averaged.
- The file combines the three yearly NDVI CSVs. It contains no map geometry, join it to `qc-brgy-geon.geojson` using `adm4_psgc` to display the values on a barangay map.
- Higher NDVI generally indicates stronger vegetation signals. These values are not percentages of tree cover, available shade, air temperature, or heat index.
#### *Attributes:*

| Attribute             | Meaning                                                             | Use in HOTSPOT                                                                                                   |
| --------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `adm4_psgc`           | Unique 10-digit PSGC code for the barangay. *Barangay ID.*          | **Primary key** for joining the NDVI values to barangay boundaries, population, and other barangay-level tables. |
| `adm4_en`             | Barangay name.                                                      | Labels barangays on maps and in tables, and helps check joins.                                                   |
| `ndvi_2024_mean_ndvi` | Mean NDVI of the barangay's pixels in the 2024 annual median image. | Maps and compares barangay greenness in 2024.                                                                    |
| `ndvi_2023_mean_ndvi` | Mean NDVI of the barangay's pixels in the 2023 annual median image. | Maps and compares barangay greenness in 2023.                                                                    |
| `ndvi_2025_mean_ndvi` | Mean NDVI of the barangay's pixels in the 2025 annual median image. | Maps and compares barangay greenness in 2025.                                                                    |

### **Candidate Cooling and Public Library Locations** (`cooling-centers.csv`)
#### *What is it?*
- `cooling-centers.csv` lists **29 locations** with names and geographic coordinates. Most entries are labeled `QCPL`, and one is labeled as a Book Nook special library.
- The CSV does not state its source, observation date, coordinate reference system, operating hours, or facility capacity.
#### *Attributes:*

| Attribute   | Meaning                                                           | Use in HOTSPOT                                                         |
| ----------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `name`      | Name assigned to the listed facility, such as `QCPL - Masambong`. | Identifies and labels candidate facilities on a map.                   |
| `latitude`  | North–south location in decimal degrees.                          | Helps plot the facility as a point after its coordinates are verified. |
| `longitude` | East–west location in decimal degrees.                            | Helps plot the facility as a point after its coordinates are verified. |
