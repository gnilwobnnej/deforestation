# deforestation

This project uses satellite imagery to detect deforestation by computing the **Normalized Difference Vegetation Index (NDVI)** before and after a suspected deforestation event. It highlights areas with significant vegetation loss and visualizes them using image masks and plots.

---

## Project Overview

**Goal:** Identify areas of deforestation by comparing pre- and post-event satellite imagery using NDVI.

**Tools used:**
- `rasterio` for geospatial raster image processing
- `numpy` for numerical operations
- `matplotlib` for visualization
- `scikit-learn` for evaluation (F1 score)

---

## Dataset and Files

The notebook expects the following GeoTIFF files:

- `before_RED.tiff` – Red band of the satellite image *before* deforestation
- `before_NIR.tiff` – Near-infrared (NIR) band *before*
- `after_RED.tiff` – Red band *after*
- `after_NIR.tiff` – NIR band *after*

You must also have ground truth data or use the sample manual annotation provided in the notebook.

---


## How It Works (Step-by-Step)

1. **Load Satellite Bands**  
   RED and NIR bands are loaded from satellite images using `rasterio`.

2. **Compute NDVI**  
   NDVI is calculated using the formula:NDVI = NIR - RED / NIR + RED


   This helps identify how healthy the vegetation is.

3. **Compare Before vs. After**  
   We subtract the NDVI after the event from the NDVI before to see where vegetation has declined.

4. **Threshold for Deforestation**  
   A threshold (like 0.2) is applied to highlight areas with major NDVI drops, likely signs of deforestation.

5. **Visualize Results**  
   Show:
   - NDVI before
   - NDVI after
   - Areas detected as deforested (highlighted in red)

6. **Create Ground Truth Mask (Optional)**  
   If you want to test your results, you can manually mark a region as "deforested" and save it as a reference GeoTIFF.

7. **Evaluation**  
   Using your ground truth, you can measure how accurate the detection is using:
   - F1 Scores
   - Intersection over Union (IoU)

---

## Evaluation Metrics

- **Intersection over Union (IoU)** – Measures how much your detected deforestation overlaps with the actual deforested area.
- **F1 Score** – Balances precision and recall to tell you how accurate your mask is.

---

## Example Output

- **NDVI Before:** Greener areas show healthy vegetation
- **NDVI After:** Less green = vegetation loss
- **Deforestation Detected:** Areas flagged with significant NDVI drop are highlighted in red

---


## 🛠 Future Improvements

- Automate the ground truth labeling using ML models
- Add support for more complex/multispectral imagery
- Export results to interactive web maps using tools like Folium or GeoJSON

