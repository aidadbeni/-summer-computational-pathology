# Paper 3: Hover-Net: Simultaneous Segmentation and Classification of Nuclei in Multi-Tissue Histology Images

## Citation

**Authors:** Simon Graham, Quoc Dang Vu, Shan E. Ahmed Raza, Ayesha Azam, Yee Wah Tsang, Jin Tae Kwak, Nasir Rajpoot

**Journal:** Medical Image Analysis

**Year:** 2019

**DOI:** 10.1016/j.media.2019.101563

---

## Research Question

How can nuclei in H&E-stained histology images be accurately segmented and classified using a single deep learning model, especially when nuclei overlap or form dense clusters?

---

## Motivation

Nuclei segmentation is a fundamental step in computational pathology because many downstream analyses, such as cancer grading, prognosis prediction, and tumor microenvironment analysis, depend on accurate nuclei information. Existing methods typically perform segmentation and classification separately and struggle with overlapping nuclei. The authors aim to develop a unified model capable of performing both tasks simultaneously while improving segmentation accuracy in crowded regions.

---

## Contribution

The paper introduces **HoVer-Net**, the first deep learning model that simultaneously performs nuclei instance segmentation and nuclei classification within a single architecture.

Its main contributions are:

- A novel three-branch architecture for simultaneous segmentation and classification.
- Introduction of horizontal and vertical (HoVer) distance maps to separate touching nuclei.
- A new colorectal nuclei dataset (CoNSeP) containing **24,319** exhaustively annotated nuclei.
- A comprehensive evaluation framework using **Panoptic Quality (PQ)** for more reliable segmentation assessment.

---

## Dataset

- **Dataset(s):**
  - CoNSeP (introduced in this paper)
  - Kumar Dataset
  - CPM-15
  - CPM-17
  - TNBC
  - CRCHisto (classification)

- **Number of slides/images:**
  - CoNSeP: 41 image tiles
  - CoNSeP contains **24,319 annotated nuclei**
  - Six independent datasets were used for evaluation.

- **Cancer type / tissue:**
  - Multi-tissue H&E histology images
  - CoNSeP focuses on colorectal adenocarcinoma.

- **Annotation type:**
  - Instance segmentation masks
  - Nuclei class labels
  - Pixel-level annotations

---

## Method

### Overall Pipeline

1. Input H&E image
2. Feature extraction using a shared encoder
3. Three parallel decoder branches:
   - Nuclear Pixel (NP) branch
   - HoVer branch
   - Nuclear Classification (NC) branch
4. Post-processing using predicted HoVer maps
5. Output:
   - Instance segmentation
   - Nuclei classification

---

### Model Architecture

The network uses a **Pre-activated ResNet-50** encoder followed by three decoder branches:

- **NP Branch**
  - Predicts nucleus vs background.

- **HoVer Branch**
  - Predicts horizontal and vertical distances from every nucleus pixel to its center of mass.
  - These distance maps allow the model to separate touching nuclei.

- **NC Branch**
  - Predicts the class of each nucleus.

The encoder is shared across all tasks, allowing end-to-end training while reducing computational cost.

---

### Training Strategy

The model is trained using a multi-task loss consisting of:

- Mean Squared Error (MSE) for HoVer regression.
- Gradient loss on HoVer maps.
- Cross-Entropy loss.
- Dice loss.

Training is performed in two stages:

1. Train decoder branches while freezing the encoder.
2. Fine-tune the entire network.

The encoder is initialized using ImageNet pretrained weights.

---

### Inference

During inference:

1. The NP branch identifies nuclear pixels.
2. The HoVer branch separates touching nuclei through horizontal and vertical distance predictions.
3. Marker-controlled watershed produces individual nuclei instances.
4. The NC branch assigns a class label to each segmented nucleus using majority voting.

---

## Results

### Main Findings

HoVer-Net achieved state-of-the-art performance across multiple benchmark datasets.

Compared with methods such as:

- U-Net
- Mask R-CNN
- Micro-Net
- DCAN
- DIST
- CIA-Net

HoVer-Net consistently achieved the highest or among the highest **Panoptic Quality (PQ)** scores while simultaneously performing nuclei classification.

Additional findings include:

- Better separation of overlapping nuclei.
- Strong generalization across different tissue types.
- Faster inference than Mask R-CNN for whole-slide processing.
- Significant improvement in nuclei classification compared to previous approaches.

---

## Key Takeaways

- HoVer-Net was the first network to jointly perform nuclei instance segmentation and classification.
- Predicting horizontal and vertical distance maps greatly improves separation of touching nuclei.
- Multi-task learning enables better performance than using separate models.
- The introduction of the CoNSeP dataset provided a valuable benchmark for computational pathology.
- Panoptic Quality (PQ) is proposed as a more informative evaluation metric than Dice or AJI alone.
- HoVer-Net became one of the most influential nuclei segmentation models and serves as the basis for many later computational pathology methods.
