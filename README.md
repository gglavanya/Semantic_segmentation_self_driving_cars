# Semantic_segmentation_self_driving_cars


---

# 🚗 **Semantic Segmentation on Cityscapes Using Improved U-Net with Attention**

This repository presents an end-to-end semantic segmentation system built using multiple U-Net–based architectures and an improved attention-augmented U-Net model.
The project explores **several deep learning models**, evaluates their performance on the **Cityscapes** dataset, and implements a custom U-Net variant enhanced with **hybrid attention (channel + spatial)** and **multi-scale feature fusion** to achieve better segmentation quality.

---

## 📌 **Models Explored**

This project experiments with a range of segmentation architectures:

* **U-Net (Baseline)**
* **U-Net++**
* **U-Net + Channel Attention (SE)**
* **U-Net + Spatial + Channel Attention (CBAM)**
* **DeepLabv3+**
* **Improved U-Net (Final Model)** → Hybrid Attention + Multi-scale Fusion

Each model was trained and evaluated to compare segmentation accuracy and understand architectural strengths and limitations.

---

## 🗂️ **Dataset: Cityscapes**

Cityscapes is a large-scale benchmark dataset for urban scene understanding.

* **5,000 fine-annotated images** from 50 European cities
* Includes objects like roads, buildings, vehicles, pedestrians, vegetation
* Original **34 classes** remapped to **19 training classes**
* Augmentations applied: horizontal flip, color jitter
* make sure to download in the cityscape dataset channel

A custom dataset class (`Cityscapes19`) handles:

* 34 → 19 class remapping
* Nearest-neighbor mask resizing
* Normalization (ImageNet mean/std)
* Data augmentation for improved generalization

---

## 🧠 **Improved U-Net Architecture (Final Model)**

The final model is an enhanced U-Net designed for improved feature extraction and segmentation accuracy.

### ✔ **Hybrid Attention (Channel + Spatial)**

* *Channel Attention* learns **what** features are important
* *Spatial Attention* learns **where** important regions are located
* Applied to encoder skip connections to refine features before decoding

### ✔ **Multi-Scale Feature Fusion**

* Combines features from bottleneck and encoder stages
* Improves segmentation of objects of varying sizes

### ✔ **Decoder Enhancement**

* DoubleConv blocks reconstruct spatial detail
* Attention-refined skip connections improve boundary accuracy

### ✔ **Output Layer**

* 1×1 convolution producing logits for **19 semantic classes**

---

## 🧮 **Loss Function & Optimization**

* **Combined Loss:**

  * CrossEntropyLoss (with ignore_index=255)
  * Dice Loss for region-level consistency
* **Optimizer:** AdamW (lr = 5e-4, weight decay = 1e-4)
* **Scheduler:** CosineAnnealingLR
* **Metrics:** Per-class IoU and mean IoU (mIoU)

Training was conducted for **up to 100 epochs** with:

* Batch size: 8 (training)
* Batch size: 4 (validation)

---

## 📊 **Results**

| Model                      | Train Loss | Val Loss   | mIoU      |
| -------------------------- | ---------- | ---------- | --------- |
| U-Net                      | –          | –          | –         |
| U-Net++                    | 0.34       | 0.84       | 0.30      |
| U-Net + SE                 | 0.33       | 0.43       | 0.29      |
| U-Net + CBAM               | 0.70       | 0.56       | 0.339     |
| DeepLabv3+                 | 0.05       | 0.45       | 0.50      |
| **Improved U-Net (Final)** | **0.0949** | **0.5433** | **0.336** |

The improved U-Net demonstrated strong performance and balanced accuracy with efficiency.

---

## 🎥 **Visualization**

The project includes utilities to:

* Convert predicted masks into RGB images using Cityscapes palette
* Run inference on single images
* Generate video overlays for real-time segmentation visualization

---

## 🏋️ **Training**

Run training with:

```bash
semseg.ipynb

unet.ipynb```

Model checkpoints are automatically saved when validation mIoU improves.


---

## 🌱 **Future Work**

* Integrate Transformer-based modules for long-range feature learning
* Add ASPP or pyramid pooling for stronger multi-scale context
* Improve segmentation in rural, low-light, and heavy-traffic scenarios
* Enhance multi-object separation in overlapping regions
* Optimize model for real-time use through quantization/pruning
* Explore ConvLSTMs or video transformers for temporal consistency

---

## 🤝 **Contributing**

Pull requests and suggestions are welcome!
Feel free to open an issue for discussions or improvements.

---


