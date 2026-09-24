# Image Quality Feature Extraction Engine

A modular Python pipeline for extracting **34 quantitative image quality features across 8 mathematical domains** from a dataset of **56,000 degraded facial images**.

This module forms the **feature extraction stage** of a pre-enhancement facial image recoverability assessment pipeline. It analyzes degraded facial images using spatial, statistical, spectral, texture, and color-domain measurements and produces a synchronized feature dataset for downstream statistical validation and recoverability analysis.

---

## Overview

The **Image Quality Feature Extraction Engine** is designed to quantify the visual characteristics of degraded facial images before image enhancement.

The extracted features provide measurable information about:

* Image sharpness
* Noise levels
* Brightness and exposure
* Contrast
* Information entropy
* Edge density
* Image resolution
* Texture characteristics
* Color distributions

The pipeline processes a large-scale dataset of **56,000 degraded facial images** and generates a structured **42-column feature dataset** containing both metadata and quantitative image-quality measurements.

### Key Capabilities

* **34 quantitative image quality metrics**
* **8 mathematical feature domains**
* Large-scale processing of **56,000 degraded facial images**
* **Checkpoint and resume functionality**
* Google Drive synchronization
* Local and cloud dataset storage
* Automatic CSV and Excel export
* Automatic Excel column formatting
* Robust handling of `NaN` and `Inf` values
* Progress tracking with `tqdm`
* Designed for downstream statistical validation

---

# Feature Domain Matrix

The extraction engine calculates **34 image-quality features across 8 domains**.

| Domain                         |  Count | Extracted Features                                                                                                                                            |
| ------------------------------ | -----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sharpness**               |      5 | `laplacian_variance`, `gradient_mean`, `gradient_std`, `tenengrad`, `high_frequency_energy`                                                                   |
| **Noise**                   |      2 | `estimated_noise_std`, `estimated_noise_variance`                                                                                                             |
| **Brightness & Statistics** |      8 | `mean_intensity`, `median_intensity`, `min_intensity`, `max_intensity`, `underexposed_ratio`, `overexposed_ratio`, `intensity_skewness`, `intensity_kurtosis` |
| **Contrast**                |      3 | `rms_contrast`, `intensity_std`, `percentile_contrast`                                                                                                        |
| **Entropy**                 |      1 | `image_entropy`                                                                                                                                               |
| **Edge & Resolution**       |      2 | `edge_density`, `image_area`                                                                                                                                  |
| **Texture (GLCM)**          |      4 | `texture_contrast`, `texture_homogeneity`, `texture_energy`, `texture_correlation`                                                                            |
| **Color Spaces**            |      9 | BGR: `mean_blue`, `mean_green`, `mean_red` • HSV: `mean_hue`, `mean_saturation`, `mean_value` • LAB: `mean_lab_l`, `mean_lab_a`, `mean_lab_b`                 |
| **Total**                      | **34** | **Quantitative Image Quality Features**                                                                                                                       |

---

# Feature Categories

## 1. Sharpness Features

Sharpness-related features measure the amount of high-frequency information and edge variation within an image.

| Feature                 | Description                                   |
| ----------------------- | --------------------------------------------- |
| `laplacian_variance`    | Variance of the Laplacian response            |
| `gradient_mean`         | Mean image gradient magnitude                 |
| `gradient_std`          | Standard deviation of gradient magnitude      |
| `tenengrad`             | Gradient-energy based sharpness measure       |
| `high_frequency_energy` | Energy contained in high-frequency components |

These features are particularly useful for identifying degradation caused by **blur and resolution loss**.

---

## 2. Noise Features

Noise features quantify unwanted high-frequency variations introduced into the image.

| Feature                    | Description                                 |
| -------------------------- | ------------------------------------------- |
| `estimated_noise_std`      | Estimated standard deviation of image noise |
| `estimated_noise_variance` | Estimated variance of image noise           |

These measurements are particularly relevant for evaluating **Gaussian noise degradation**.

---

## 3. Brightness & Statistical Features

These features describe the distribution of pixel intensities.

| Feature              | Description                                     |
| -------------------- | ----------------------------------------------- |
| `mean_intensity`     | Mean grayscale intensity                        |
| `median_intensity`   | Median grayscale intensity                      |
| `min_intensity`      | Minimum pixel intensity                         |
| `max_intensity`      | Maximum pixel intensity                         |
| `underexposed_ratio` | Proportion of pixels classified as underexposed |
| `overexposed_ratio`  | Proportion of pixels classified as overexposed  |
| `intensity_skewness` | Skewness of intensity distribution              |
| `intensity_kurtosis` | Kurtosis of intensity distribution              |

These features help characterize **brightness shifts and exposure-related degradation**.

---

## 4. Contrast Features

Contrast features quantify the spread and variation of pixel intensities.

| Feature               | Description                                     |
| --------------------- | ----------------------------------------------- |
| `rms_contrast`        | Root mean square contrast                       |
| `intensity_std`       | Standard deviation of pixel intensity           |
| `percentile_contrast` | Contrast calculated using intensity percentiles |

These measurements are useful for analyzing **contrast adjustment degradation**.

---

## 5. Entropy

### `image_entropy`

Image entropy is calculated using **Shannon entropy** and represents the amount of information or uncertainty contained within the image's intensity distribution.

Higher or lower entropy values can indicate changes in image information content caused by different degradation processes.

---

## 6. Edge & Resolution Features

| Feature        | Description                                             |
| -------------- | ------------------------------------------------------- |
| `edge_density` | Density of edges detected using the Canny edge detector |
| `image_area`   | Total image area in pixels                              |

These features help identify changes caused by **blur and low-resolution degradation**.

---

## 7. Texture Features — GLCM

Texture characteristics are extracted using the **Gray-Level Co-occurrence Matrix (GLCM)**.

| Feature               | Description                                       |
| --------------------- | ------------------------------------------------- |
| `texture_contrast`    | Local intensity variation                         |
| `texture_homogeneity` | Similarity of neighboring pixel intensities       |
| `texture_energy`      | Uniformity of texture distribution                |
| `texture_correlation` | Correlation between neighboring pixel intensities |

These features provide information about changes in facial texture caused by image degradation.

---

## 8. Color Space Features

Color information is extracted from three different color spaces.

### BGR

* `mean_blue`
* `mean_green`
* `mean_red`

### HSV

* `mean_hue`
* `mean_saturation`
* `mean_value`

### LAB

* `mean_lab_l`
* `mean_lab_a`
* `mean_lab_b`

Using multiple color spaces provides a broader representation of color and luminance characteristics.

---

# Installation & Setup

## Prerequisites

The project requires:

* Python **3.10+**
* Google Colab *(recommended)*
* Jupyter Notebook / JupyterLab *(for local execution)*

---

## Required Dependencies

Install the required Python packages using:

```bash
pip install opencv-python pandas numpy tqdm scikit-image scipy openpyxl matplotlib seaborn
```

### Main Libraries

| Library        | Purpose                                    |
| -------------- | ------------------------------------------ |
| `OpenCV`       | Image processing and computer vision       |
| `NumPy`        | Numerical computation                      |
| `Pandas`       | Dataset and feature management             |
| `SciPy`        | Statistical analysis                       |
| `scikit-image` | GLCM texture analysis and image processing |
| `OpenPyXL`     | Excel generation and formatting            |
| `Matplotlib`   | Data visualization                         |
| `Seaborn`      | Statistical visualization                  |
| `tqdm`         | Progress monitoring                        |

---

```text
Start
  │
  ▼
Load metadata.csv
  │
  ▼
Check existing feature CSV
  │
  ├── Already processed ──► Skip
  │
  └── Not processed
          │
          ▼
    Extract 34 features
          │
          ▼
     Save results
          │
          ▼
  Every 1,000 images
          │
          ▼
     Checkpoint Sync
```
---

# Output Dataset Schema

Each image is represented by **42 columns**:

```text
8 Metadata Columns
        +
34 Quality Features
        =
42 Total Columns
```

---

## Metadata Columns — 8

|  # | Column               | Description                       |
| -: | -------------------- | --------------------------------- |
|  1 | `original_filename`  | Original image filename           |
|  2 | `cropped_filename`   | Cropped facial image filename     |
|  3 | `degraded_filename`  | Degraded image filename           |
|  4 | `degradation_type`   | Type of degradation applied       |
|  5 | `severity_level`     | Severity category                 |
|  6 | `severity_parameter` | Parameter controlling degradation |
|  7 | `parameter_value`    | Numerical degradation parameter   |
|  8 | `drive_path`         | Image storage path                |

---

##  1. Statistical Validation

**Spearman Rank Correlation** is used to measure the monotonic relationship between degradation severity and extracted image-quality features.

The target validation criterion is:

```text
|ρ| ≥ 0.80
p < 0.001
```

where:

* `ρ` = Spearman rank correlation coefficient
* `p` = statistical significance value

Features are examined to determine whether their values change consistently as degradation severity increases.

---

#  2. Visual Validation

Mean feature values are plotted across degradation severity levels.

The visualizations include:

```text
Mean Feature Value
        │
        │       ●
        │     ●
        │   ●
        │ ●
        └──────────────────►
          Degradation Severity
```

Trend curves are accompanied by **±1 standard deviation (σ)** error bands to visualize variation within each severity level.

---

# Expected Feature Behavior

The following table describes the expected response of selected features to different degradation types.

| Degradation                  | Severity Change | Expected Feature Response                               |
| ---------------------------- | --------------- | ------------------------------------------------------- |
| **Gaussian Blur**        | `σ ↑`           | `laplacian_variance ↓`, `tenengrad ↓`, `edge_density ↓` |
| **Gaussian Noise**        | `σ ↑`           | `estimated_noise_std ↑`, `estimated_noise_variance ↑`   |
| **Brightness Adjustment** | `k ↑ / ↓`       | `mean_intensity` shifts systematically                  |
| **Contrast Adjustment**   | `k ↑ / ↓`       | `rms_contrast` changes systematically                   |
| **Low Resolution**        | `R ↓`           | `high_frequency_energy ↓`, `edge_density ↓`             |

These expected relationships provide a basis for determining whether the extracted features meaningfully represent the applied degradation.
 

