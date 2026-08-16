# Urban Heat VulnMapping

Urban heat vulnerability mapping for Kochi, India — built for the **GIS Mapathon hosted by NEST Digital**.

## Overview

This project identifies **Priority Intervention Zones** in Kochi: areas where residents face the highest combined risk from urban heat, based on four overlapping factors:

- High land surface temperature
- Low vegetation cover (NDVI)
- Poor access to hospitals (distance-based)
- Low access to cooling/community infrastructure

By layering these datasets, the analysis flags neighborhoods where heat exposure and lack of supporting infrastructure compound each other — the places that should be prioritized for interventions like tree cover, shaded public spaces, and improved emergency access.

## Methodology

1. **Boundary data** — Kochi's administrative boundary extracted from [GADM](https://gadm.org/).
2. **Points of interest** — Hospital, school, and park locations pulled via **QuickOSM** (QGIS plugin) within the Kochi boundary.
   - Where OSM returned polygons (e.g. school/park footprints) instead of points, centroids were computed using the QGIS Processing Toolbox and merged with existing point layers.
3. **Vegetation index** — NDVI computed to represent vegetative cover across the city.
4. **Hospital accessibility** — Distance-to-hospital raster generated to represent proximity to emergency medical care.
5. **Composite scoring** — Heat, vegetation, and hospital-distance layers combined into a single raster to derive Priority Intervention Zones.

All spatial processing was done in **QGIS**.

## Data Sources

| Layer | Source |
|---|---|
| Administrative boundary | GADM |
| Hospitals, schools, parks | OpenStreetMap (via QuickOSM) |
| Vegetation index | NDVI (satellite-derived) |
| Building footprints | *Not included — see Limitations* |

## Repository Structure

```
prfvl-urban-heat-vulnmapping/
├── README.md
└── data/
    └── processed/
        ├── hospital_distance.tif       # Distance-to-hospital raster
        └── hospitals_raster.tif        # Hospital point raster
```

## Limitations & Future Work

- **Building footprints** were planned as an additional layer (finer-grained proxy for built-up density and heat retention) using Geofabrik's Kerala OSM extract, but the file size was too large to process within the competition's time and hardware constraints. This is earmarked as a future improvement.
- Parks and vegetation layers were finalized under time pressure and could benefit from further refinement and validation.
- Priority zone scoring is currently a simple layer overlay; future iterations could explore weighted scoring or machine learning-based classification.

## Team

Built as part of a team effort for the GIS Mapathon (NEST Digital). GIS/spatial analysis pipeline built by [prfvl]; StoryMap, presentation and frontend built by [merin-07], [sarj29] and [lakshmisiju1111git].

## Tools Used

- QGIS (QuickOSM, Processing Toolbox)
- GADM (administrative boundaries)
- OpenStreetMap data
