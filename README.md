# DAT-103: Land Use Land Cover (LULC) Classification

This repository contains the code, report, and visualizations for the DAT-103 course project on Land Use Land Cover (LULC) classification.

The project uses multi-spectral Landsat satellite imagery and deep learning (U-Net) to classify terrain in a 50 km² Area of Interest (AOI) located in Cape Town, South Africa.

---

## Repository Structure

- Final DAT-103.ipynb  
  Main Kaggle notebook containing the complete pipeline:
  - USGS M2M API data fetching  
  - Preprocessing  
  - U-Net model training  
  - Test-time augmentation inference  
  - Metric evaluation  

- Project Report.docx  
  Detailed academic report covering methodology, results, and analysis  

- Images/  
  Contains generated visual outputs:
  - True Color composites and NDVI maps  
  - Train/validation/test splits  
  - ROC curves and confusion matrix  
  - F1 score and IoU comparisons  
  - Sample predictions (input vs ground truth vs output)  

---

## Dataset

Input Imagery:
- Landsat 8/9 Collection 2 Level-2 Surface Reflectance  
- Cloud-free scene (0% cloud cover), December 2024  

Input Channels (10 total):
- Spectral bands: B2, B3, B4, B5, B6, B7  
- Derived indices: NDVI, NDWI, NDBI, SAVI  

Ground Truth:
- ESRI 10 m Annual Land Cover dataset  

Target Classes:
- Water  
- Flooded Vegetation  
- Crops  
- Built Area  
- Bare Ground  
- Rangeland  

---

## Methodology

Architecture:
- U-Net semantic segmentation network  
- EfficientNet-B3 encoder (ImageNet pretrained)  

Data Processing:
- 64 x 64 non-overlapping patches  
- Patches with >30% invalid pixels removed  

Loss Function:
- Dice Loss (60%) + Focal Loss (40%)  
- Invalid pixel masking applied  

Optimization:
- AdamW optimizer  
- Differential learning rates (encoder vs decoder)  
- Cosine annealing with warm restarts  
- Mixed precision training (AMP)  

---

## Results

The model converged after approximately 85 epochs and showed strong spatial pattern recognition.

- Weighted F1 Score: 0.852  
- Weighted mIoU: 0.832  
- Macro F1 Score (excluding Bare Ground): 0.564  

Note: Bare Ground represents approximately 0.06% of test pixels, leading to low metric support.

---

## Requirements

The project was developed using a Kaggle GPU environment (T4/P100).

Required libraries:

pip install torch segmentation-models-pytorch rasterio albumentations scikit-learn geopandas matplotlib

---

## Usage

1. Open Kaggle and create a new notebook  
2. Upload "Final DAT-103.ipynb"  
3. Enable GPU (Settings → Accelerator → GPU)  
4. Run all cells  

Note: USGS M2M API credentials are required to download Landsat data.

---

## Team Members

- Rachit Tusharbhai Jani (24125030)  
- Rathore Rahul (24125032)  
- Kritarth (24125026)  
- Ankit Kumar (24117013)  
- Amit Khedar (24125004)  

---

## Notes

This is an academic course project. The pipeline is designed to be reproducible and can be extended to other regions and datasets.
