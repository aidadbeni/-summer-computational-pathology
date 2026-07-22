# summer-computational-pathology
Literature review and reproducibility work on pathology foundation models, with a focus on Prov-GigaPath.

## Overview

This repository documents my summer project on computational pathology
and pathology foundation models.

The assigned materials include:

- HoVer-Net
- UNI
- Prov-GigaPath
- Supporting research papers

The main practical objective is to reproduce the official Prov-GigaPath
demo using a compressed whole-slide pathology image.

## Current progress

- [x] Started the assigned literature review
- [x] Read three assigned papers
- [x] Reviewed the purpose of HoVer-Net
- [ ] Reviewed the purpose of UNI
- [ ] Inspected the Prov-GigaPath repository
- [ ] Configure the computational environment
- [ ] Obtain access to the Prov-GigaPath model weights
- [ ] Download the sample whole-slide image
- [ ] Run tile-level feature extraction
- [ ] Run slide-level feature extraction
- [ ] Document the demo outputs
- [ ] Complete the remaining papers

## Models

### HoVer-Net

HoVer-Net performs nucleus instance segmentation and classification in
histopathology images.

### UNI

UNI extracts feature representations from individual pathology image
patches.

### Prov-GigaPath

Prov-GigaPath represents an entire whole-slide image. It first extracts
features from individual image tiles and then combines the tile features
and their spatial coordinates using a slide-level encoder.

## Prov-GigaPath pipeline

1. Load a whole-slide image.
2. Identify tissue-containing regions.
3. Divide the tissue into smaller tiles.
4. Extract an embedding from each tile.
5. retain the coordinates of every tile.
6. Pass the tile embeddings and coordinates into the slide encoder.
7. Generate a whole-slide representation.

## Repository status

This repository is under active development. The current stage focuses
on literature review, environment configuration, and reproduction of
the official Prov-GigaPath demo.
