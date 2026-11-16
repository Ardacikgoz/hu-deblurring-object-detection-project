# Blur Robustness of Object Detection

How much do different types of image blur hurt an off-the-shelf object detector, and can **classical or learned deblurring** recover the lost accuracy?

## Setup

- **Detector:** YOLOv8n pretrained on COCO, evaluated on 1,000 images (7,204 objects).
- **Degradations** (`deBlurDataCreation.ipynb`): Gaussian, motion, defocus, bilateral-filtered and low-light blur.
- **Restoration methods:** Wiener filter, Richardson–Lucy (RL), MPRNet, DeblurGANv2.
- **Evaluation:** detection mAP (`yoloPredictNormalAndBlurred.ipynb`, `deblurYOLOPrediction.ipynb`) and image quality with PSNR / SSIM (`ssımPSNR.ipynb`).

## Results – detection mAP@50

| Condition | Blurred | Wiener | Richardson–Lucy | MPRNet | DeblurGANv2 |
|---|---|---|---|---|---|
| Bilateral filtered | 0.356 | 0.253 | 0.234 | 0.346 | **0.359** |
| Defocus | 0.378 | 0.284 | 0.289 | 0.397 | **0.426** |
| Gaussian | 0.257 | 0.196 | 0.259 | **0.298** | 0.283 |
| Low light | 0.048 | **0.113** | 0.010 | 0.007 | – |
| Motion | 0.132 | 0.178 | 0.040 | **0.317** | – |

Clean images: **0.539** mAP@50. *(Best value per row in bold; "–" = not evaluated.)*

**Takeaways**

- Every blur type hurts detection. Low-light and motion blur are the most damaging (mAP@50 drops from 0.539 to 0.048 and 0.132).
- Learned methods help the most: **MPRNet more than doubles mAP on motion blur (0.132 → 0.317)**, and DeblurGANv2 gives the best results on defocus and bilateral blur.
- Classical filters (Wiener, Richardson–Lucy) often lower detection accuracy even when the images look sharper. Pixel-level restoration does not always translate into better detection.

## Repository structure

```
├── deBlurDataCreation.ipynb          # synthetic blur generation
├── dataExtraction.ipynb, jsontToTxt.ipynb   # COCO subset & YOLO label conversion
├── yoloPredictNormalAndBlurred.ipynb # YOLO on clean vs. blurred images
├── deblurYOLOPrediction.ipynb        # YOLO on deblurred images
├── ssımPSNR.ipynb                    # PSNR / SSIM evaluation
└── *.yaml                            # YOLO dataset configs per setting
```

Images and model weights are not included.

---
Term project for the Computational Photography course at Hacettepe University, Department of Artificial Intelligence Engineering.
