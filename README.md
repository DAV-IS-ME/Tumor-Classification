# Tumor Classification
A deep learning project for classifying 9 types of human tissue from H&E‑stained microscopy images. Using a dataset of 32,000 images (28×28×3), we compare Random Forest, MLP, and CNN models to identify the most effective approach for medical image classification.

## Project Overview
This project aims to automate tissue identification to support medical diagnosis and reduce human error. We evaluate three model families and analyze their performance, generalization ability, and computational efficiency.

## Dataset
* 32,000 RGB tissue slice images
* Image size: 28 × 28 × 3
* 9 tissue classes: adipose, background, debris, lymphocyte, mucus, smooth muscle, normal colonic mucosa, stromal, tumour
* H&E staining (Hematoxylin: purple nuclei; Eosin: pink cytoplasm)

## Preprocessing
* Random Forest: flatten → normalize → PCA (20 components)
* MLP & CNN: random rotation, brightness/contrast shift, per‑epoch shuffle
* No class rebalancing (dataset is relatively balanced)

## Models
### Random Forest
* GridSearchCV + 5‑fold CV
* Tuned: n_estimators, max_depth, min_samples_split

### MLP
* Flatten → Dense + BatchNorm + Activation + Dropout (×3) → Softmax
* Tuned: hidden sizes, activation, learning rate

### CNN
* Conv + BatchNorm + Activation
* Two residual-style blocks
* MaxPool → GlobalAvgPool → Dropout → Softmax
* Tuned: filters, kernel size, learning rate

## Results
* Model	Test Accuracy	Notes
* CNN：	0.9814	Best performance; strong spatial feature learning
* MLP：	0.7063	Limited by loss of spatial structure
* Random： Forest	0.7044	Flattening destroys image geometry
* CNN achieves near‑perfect classification across all tissue types, with tumour recall reaching 98.55%.
