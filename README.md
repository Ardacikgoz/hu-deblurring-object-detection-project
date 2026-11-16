# Blur Robustness of Object Detection

How different blur types affect YOLO detection, and whether classical and learned deblurring restores performance – term project for the Computational Photography course at Hacettepe University, Department of Artificial Intelligence Engineering.

## Contents

- Synthetic blur generation: Gaussian, motion, defocus, bilateral, low-light (`deBlurDataCreation.ipynb`)
- Deblurring methods: Wiener filter, Richardson–Lucy, DeblurGANv2, MPRNet
- YOLO detection on clean vs. blurred vs. deblurred images (`yoloPredictNormalAndBlurred.ipynb`, `deblurYOLOPrediction.ipynb`)
- Image quality evaluation with SSIM / PSNR (`ssımPSNR.ipynb`)
- `*.yaml` – YOLO dataset configs for each blur / deblur setting

> Datasets and large model files are not included. Outputs of very large notebooks were cleared to stay within GitHub's file size limits.
