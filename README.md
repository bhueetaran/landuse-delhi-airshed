Delhi Airshed Land-Use Classification using Satellite Imagery

This project builds an end-to-end AI pipeline to analyze land-use patterns in the Delhi Airshed using Sentinel-2 satellite imagery and ESA WorldCover land-cover data. The objective is to automatically classify land-use categories such as Built-up, Vegetation, Cropland, Water, and Others using deep learning.

The project was developed as part of the SRIP 2026 – AI for Sustainability assignment.

Project Overview

Rapid urbanization in the Delhi NCR region leads to significant environmental challenges, including pollution and land-use changes. Satellite imagery combined with machine learning can help identify patterns in land use and support environmental monitoring.

This project implements a complete workflow including:

• Spatial filtering of satellite images within the Delhi NCR boundary
• Extraction of land-cover patches from ESA WorldCover raster data
• Automatic label assignment using dominant land-cover class
• Training a Convolutional Neural Network (CNN) for classification
• Evaluation using accuracy, F1-score, and confusion matrix

Dataset

The project uses multiple geospatial datasets.

Sentinel-2 Satellite Images

RGB image patches

Image size: 128 × 128 pixels

Resolution: 10 meters per pixel

Each image covers approximately 1.28 km × 1.28 km of land area.

ESA WorldCover 2021

Raster land-cover dataset used to assign labels.

Resolution: 10 meters

Delhi NCR Shapefile

Used to filter satellite images within the region of interest.

Methodology
1. Spatial Filtering

Satellite image filenames contain center coordinates (latitude and longitude).
These coordinates are converted into geographic points and filtered to keep only the images located inside the Delhi NCR region.

2. Spatial Gridding

A 60 km × 60 km uniform grid is generated over the Delhi NCR region.

The shapefile is converted to the coordinate system:

EPSG:32644 (UTM Zone 44N)

This allows correct distance-based grid calculations.

3. Land-Cover Patch Extraction

For every valid satellite image, a 128×128 pixel patch is extracted from the ESA WorldCover raster centered on the image coordinate.

The extraction is performed using Rasterio.

4. Label Assignment

The land-use label is assigned based on the dominant land-cover class inside the extracted raster patch.

Example:

Land-Cover Class	Pixel Count
Built-up (50)	8000
Cropland (40)	3000
Tree Cover (10)	512

Assigned label → Built-up

5. Label Simplification

ESA land-cover classes are mapped to simplified categories:

ESA Class	Category
50	Built-up
10, 20, 30	Vegetation
40	Cropland
80	Water
Others	Other
6. Dataset Preparation

Each satellite image is paired with its assigned land-use label to build a supervised machine learning dataset.

Example dataset format:

Image	Latitude	Longitude	Label
img_01.png	28.63	77.21	Built-up
img_02.png	28.72	77.10	Cropland
7. Model Training

A ResNet18 Convolutional Neural Network is trained to classify satellite image patches into land-use categories.

The training pipeline includes:

• Image preprocessing
• Train-test split (60/40)
• CNN training using PyTorch

8. Evaluation Metrics

Model performance is evaluated using:

• Accuracy
• F1-score
• Confusion Matrix

These metrics measure how well the CNN predicts land-use classes from satellite imagery.

Technologies Used

The project uses the following Python libraries:

• Python
• GeoPandas
• Rasterio
• NumPy
• PyTorch
• Scikit-learn
• Matplotlib
• Shapely
• geemap (visualization)

The notebook performs the following steps:

Load satellite image patches

Load shapefile and create spatial grid

Filter images inside Delhi NCR

Extract land-cover patches from raster

Assign dominant land-cover labels

Train CNN model

Evaluate classification performance

Project Structure
SRIP-Delhi-Airshed-LandUse-Classification
│
├── sustainibility.ipynb
├── README.md
├── requirements.txt
Results

The trained CNN model successfully learns spatial patterns in satellite imagery and predicts land-use categories for the Delhi Airshed.

Evaluation metrics include:

• Accuracy score
• F1-score
• Confusion matrix visualization

These results demonstrate the feasibility of using deep learning for automated land-use classification.
