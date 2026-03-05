# Delhi Airshed Land-Use Classification 

This project implements an AI pipeline to classify land-use patterns in the **Delhi Airshed region** using **Sentinel-2 satellite imagery** and **ESA WorldCover land-cover data**. The goal is to identify dominant land-use categories such as Built-up areas, Vegetation, Cropland, Water, and Others using deep learning.

The project was developed as part of the **SRIP 2026 – AI for Sustainability assignment**.

---

# Project Overview

Satellite imagery provides an efficient way to monitor environmental changes and urban expansion. This project combines **geospatial data processing and deep learning** to automatically classify land-use patterns from satellite image patches.

The pipeline includes:

• Spatial filtering of satellite images inside the Delhi NCR boundary
• Land-cover patch extraction from ESA WorldCover raster data
• Automatic label assignment using dominant land-cover class
• CNN-based classification of land-use categories
• Evaluation using standard machine learning metrics

---

# Dataset

The project uses the following datasets:

### Sentinel-2 Satellite Images

* RGB image patches
* Image size: **128 × 128 pixels**
* Resolution: **10 meters per pixel**

Each image represents approximately **1.28 km × 1.28 km** of land area.

### ESA WorldCover 2021

Global land-cover raster dataset used to generate labels for satellite images.

Resolution: **10 meters**

### Delhi NCR Shapefile

Used for spatial filtering and region-based analysis.

---

# Methodology

## 1. Spatial Filtering

Satellite image center coordinates are converted to geographic points and filtered to retain only those inside the **Delhi NCR region**.

## 2. Spatial Gridding

A **60 km × 60 km grid** is generated over the region using the coordinate reference system:

```
EPSG:32644
```

## 3. Land-Cover Patch Extraction

For each satellite image, a **128×128 raster patch** is extracted from the ESA WorldCover dataset using its center coordinate.

## 4. Label Assignment

The label for each image is determined using the **dominant land-cover class (mode)** inside the extracted patch.

Example:

| Class           | Pixel Count |
| --------------- | ----------- |
| Built-up (50)   | 8000        |
| Cropland (40)   | 3000        |
| Tree Cover (10) | 512         |

Final label → **Built-up**

## 5. Model Training

A **ResNet18 convolutional neural network** is trained to classify satellite image patches into land-use categories.

## 6. Evaluation

Model performance is evaluated using:

• Accuracy
• F1-Score
• Confusion Matrix

---

# Technologies Used

Python
GeoPandas
Rasterio
NumPy
PyTorch
Scikit-learn
Matplotlib
Shapely
geemap

---

# Project Structure

```
SRIP-Delhi-Airshed-LandUse-Classification
│
├── sustainibility.py
├── README.md
├── requirements.txt
```

---

# Results

The trained CNN model successfully learns spatial patterns from satellite imagery and predicts land-use categories across the Delhi Airshed region.

The evaluation metrics demonstrate the effectiveness of combining **remote sensing data and deep learning for land-use classification**.
