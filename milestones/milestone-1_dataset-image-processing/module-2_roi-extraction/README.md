# Module 2 — Contour Detection & ROI Extraction

---

##  Objective

The objective of this module is to extract individual defect regions (ROIs — Regions of Interest) from PCB images using ground-truth annotation files.

These extracted defect samples are used to create a clean dataset for training the CNN-based defect classification model.

---

## Methodology

This module performs **annotation-driven ROI extraction** using XML label files provided in the DeepPCB dataset.

---

### 1️) Dataset Parsing

The DeepPCB dataset provides annotations in **XML format** containing:

* Image filename
* Defect class label
* Bounding box coordinates

Each XML file corresponds to one PCB image.

---

### 2️) XML Annotation Reading

The pipeline uses Python's `xml.etree.ElementTree` to:

* Parse XML files
* Locate defect objects
* Extract bounding box information:

  * xmin
  * ymin
  * xmax
  * ymax

---

### 3️) Image Matching

For each annotation file:

* Corresponding PCB image is loaded.
* Supports both `.jpg` and `.png` image formats.
* Invalid or missing images are safely skipped.

---

### 4️) ROI Extraction

For every detected defect:

* Bounding box region is cropped from the PCB image.
* Small padding is added around defects to preserve context.
* Boundary checks prevent cropping outside image dimensions.

Crop operation:

```
ROI = Image[ymin:ymax, xmin:xmax]
```

---

### 5️) Dataset Organization

Extracted defect regions are saved category-wise:

```
ROI_Output/
   Missing_hole/
   Mouse_bite/
   Open_circuit/
   Short/
   Spur/
   Spurious_copper/
```

Each cropped image represents a **single defect instance**.

---

## Technologies Used

* Python
* OpenCV
* XML Parsing (ElementTree)
* NumPy

---

## Output Description

Generated Output:

✔ Cropped defect images
✔ Label-preserving directory structure
✔ Clean dataset for deep learning training

Example filename:

```
01_image_001_obj0.jpg
01_image_001_obj1.jpg
```

Each file corresponds to one annotated defect.

---

## Sample Results

<img width="387" height="319" alt="image" src="https://github.com/user-attachments/assets/d6a6773c-31d1-41c8-bd59-cd15ebbb6d1e" />
<img width="417" height="288" alt="Screenshot 2026-02-22 001804" src="https://github.com/user-attachments/assets/eeef71ed-8886-47c0-ab51-73cfb49ad6c1" />
<img width="342" height="301" alt="Screenshot 2026-02-22 001828" src="https://github.com/user-attachments/assets/c23f4263-1a9d-47b3-9a5c-bd677fc8a17a" />



Example:

* Individual defect patch
* Multiple defect samples extracted from a single PCB

---

## Evaluation Outcome

✔ Accurate bounding box extraction

✔ Correct defect localization from annotations

✔ Automated dataset generation achieved

✔ CNN training dataset successfully prepared

---

## 🔄 Relation with Previous Module

**Module 1**
→ Detects and visualizes defects using image subtraction.

**Module 2**
→ Extracts ground-truth defect regions for model training.

Together they complete **Milestone 1 — Dataset Preparation & Image Processing**.

---



## Author

Alfiyabi Saiyyad


