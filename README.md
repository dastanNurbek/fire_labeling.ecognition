# Labeled Sample Creator for Fire Classification in eCognition

This eCognition Architect application streamlines the creation of fire classification training data by guiding the user through three main steps:

- Creating spectral indices
- Threshold-based classification
- Generating labeled sample patches
  
The end result is a set of image patches labeled as burned, ready for use in machine learning model training.

## How It Works

### Creating Indices

The application first generates two common fire-detection indices:

- NDVI (Normalized Difference Vegetation Index) — measures vegetation health and greenness.
- NBR (Normalized Burn Ratio) — detects burned areas by comparing near-infrared and shortwave infrared reflectance.

These indices are added as new image layers and serve as the input for the classification step.

### Threshold Classification

The classification process runs in two stages:

- Multi-threshold on NBR — separates burned from unburned areas using a user-defined NBR threshold.
- Refinement with NDVI — further adjusts the classification by filtering based on mean NDVI values, helping remove false positives.

A manual editing mode is included so the user can visually inspect and correct classification results before proceeding.

### Generating Labeled Samples
Once classification is finalized, the application generates sample image patches for the 'burned' class.

Patch size, output location, and sample counts are controlled via the patch parameters.

Patches are saved as .tif images, each labeled according to its class.

## Installation

1. Fork this repository
2. In eCognition, under ```Architect``` window, choose ```Open Action Library```. Select the ```ActionLibrary``` folder.
3. Open ```Architect``` window again. Click on ```Load Solution``` and select the ```User_interaction.dax``` file.

## Example

### Step 1: Creating Indices
We begin with the original post-fire RGB image:

<img src="https://github.com/dastanNurbek/fire_labeling.ecognition/blob/main/Example/rgb.jpg" alt="drawing" width="300"/>

*Original post-fire Sentinel-2 imagery visualized in RGB.*

From this, by selecting the Red, NIR, and SWIR layers, the application generates:
- **NBR** (Normalized Burn Ratio) — sensitive to burn severity:
  
  <img src="https://github.com/dastanNurbek/fire_labeling.ecognition/blob/main/Example/nbr.jpg" alt="drawing" width="300"/>
  
  *Darker areas indicate higher burn severity.*
- **NDVI** (Normalized Difference Vegetation Index) — measures vegetation greenness:
  
  <img src="https://github.com/dastanNurbek/fire_labeling.ecognition/blob/main/Example/ndvi.jpg" alt="drawing" width="300"/>
  
  *Brighter green values indicate healthier vegetation.*

---

### Step 2: Threshold Classification
The application applies thresholds to classify **burned** (brown) vs **unburned** (green) areas:

- **NBR Threshold Result:**
  
  <img src="https://github.com/dastanNurbek/fire_labeling.ecognition/blob/main/Example/nbr_threshold.jpg" alt="drawing" width="300"/>
  
  *Initial burned/unburned separation based on NBR.*

- **NDVI Threshold Refinement:**
  
  <img src="https://github.com/dastanNurbek/fire_labeling.ecognition/blob/main/Example/ndvi_threshold.jpg" alt="drawing" width="300"/>
  
  *Refines classification using NDVI to reduce false positives.*

At this point, the user can manually edit the classification to correct any mistakes before generating patches.

---

### Step 3: Generating Labeled Samples
After classification:
- **Burned area patches** (*positive samples*) are created.
- **Unburned area patches**.

These patches are exported as `.tif` files with given parameters into the **`Samples/`** folder in your project directory, each labeled according to its class.

---
