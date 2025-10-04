# Mineral-Prospectivity-Mapping-Using-ML-Workflows
This repository contains the end-to-end GeoAI workflow used to produce gold prospectivity maps for Kakamega County. The workflow is ArcGIS-centric and integrates remote sensing indices, terrain derivatives, structural proxies, and geochemical pathfinders into machine-learning models.Outputs feed directly into an ArcGIS Hub “Prospectivity Portal,” Dashboards for insights, and Survey123/StoryMaps for ground-truthing and storytelling.

# Core notebooks (run in this order):
PointExtraction.ipynb — builds the training table by extracting raster covariate values to labelled points.
ML_Algorithms.ipynb — trains/evaluates multiple models (e.g., Random Forest, SVM), with spatially aware validation and model comparison.
SVM.ipynb — focuses the pipeline on a tuned SVM and produces final probability rasters for deployment.

# What this project does
Aggregates multi-source geoscience data (lithology proxies, structure, DEM derivatives, RS indices, geochem) into a consistent modeling table.
Trains and compares ML models with grouped cross-validation to reduce spatial leakage.
Generates prospectivity probability rasters and diagnostics (ROC-AUC, PR-AUC, classification reports) for portal publication and field verification.

# Data requirements
Training points (feature class): e.g., TrainingPts in a file/enterprise geodatabase
## Required fields:
label (1 = mineralization/occurrence; 0 = background/negative)
Optional/used by notebooks: block_id (spatial groups for CV; can be generated)
Covariate rasters (aligned): stored in a single folder with common cell size, extent, and projection
Typical layers:
Remote sensing indices: Fe-oxide (iron oxide), ferrous, Clay (Al–OH), ratio rasters (e.g., Red/Blue, SWIR/NIR, ferric/ferrous);
Topography: DEM, slope, curvature;
Structure: distance-to-faults/lineaments;
Geochemistry: pathfinder/alteration elements (if available).
Projection: a projected CRS suitable for Kenya (e.g., UTM Zone 37S). All rasters must be aligned (snap raster & cell size set in ArcGIS).

# Environment & prerequisites
ArcGIS Pro (with Spatial Analyst extension and the default arcgispro-py3 conda environment)
Python packages (typically present or installable in the ArcGIS Pro environment):
arcpy, numpy, pandas, scikit-learn
Hardware: modeling on 10–30 covariates works comfortably on a modern laptop; very large rasters may benefit from tiled processing.
Tip: manage packages via Python Package Manager in ArcGIS Pro or conda from the ArcGIS Pro Python Command Prompt.
