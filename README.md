# Deep Attention-Guided U-Net with EfficientNet-B4 Encoder for Post-Wildfire Burned-Area Segmentation

Code for the paper **"Deep Attention-Guided U-Net with EfficientNet-B4 Encoder for Post-Wildfire Burned-Area Segmentation."**

This repository provides the training, evaluation, and ablation code for a dual-attention U-Net that segments burned areas / fire regions from UAV wildfire imagery. The proposed model pairs an **EfficientNet-B4** encoder with a **U-Net** decoder and **channel + spatial attention**, trained with a **combined loss** (BCE–Dice + Focal + Tversky).

---

## Highlights

- **Encoder:** EfficientNet-B4 (ImageNet-pretrained)
- **Decoder:** U-Net with skip connections
- **Attention:** channel attention + spatial attention on decoder features
- **Loss:** combined BCE–Dice + Focal + Tversky (for severe class imbalance)
- **Baselines compared:** DenseNet121-U-Net, ResNet50-U-Net, and a plain EfficientNet-B4-U-Net
- **Reproducible:** fixed seed, per-epoch checkpointing, and resume support

---

## Results (test set)

| Model | IoU | Dice | Precision | Recall | F1 |
|---|---|---|---|---|---|
| **Proposed (EfficientNet-B4 + Dual Attention)** | **0.9056** | **0.9505** | **0.9464** | **0.9546** | **0.9505** |
| EfficientNet-B4 U-Net (baseline) | 0.8807 | 0.9325 | 0.9443 | 0.9522 | 0.9482 |
| DenseNet121 U-Net | 0.8558 | 0.9157 | 0.9052 | 0.9266 | 0.9157 |
| ResNet50 U-Net | 0.8496 | 0.9123 | 0.9017 | 0.9238 | 0.9123 |

> Numbers are from the notebook's test-set evaluation. Please re-run to reproduce on your own environment.

---

## Repository contents

```
.
├── DA_UNet_EfficientNetB4.ipynb   # main training + evaluation + ablation notebook
└── README.md
```
> Rename the notebook line above to match the actual file in your repo.

---

## Datasets

This work uses publicly available UAV wildfire datasets (obtain from their original sources):

- **BurnedAreaUAV** — UAV burned-area segmentation imagery.
- **Boreal Forest Fire** — Pesonen et al., *Scientific Data* **12**, 1419 (2025). DOI: 10.1038/s41597-025-05634-0

No new data were created in this study. Download the datasets from their sources and update the dataset paths in the notebook's configuration cell.

---

## Requirements

- Python 3.10+
- PyTorch (CUDA recommended)
- `segmentation-models-pytorch`, `albumentations`, `opencv-python`, `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `scipy`

Install:

```bash
pip install torch torchvision segmentation-models-pytorch albumentations opencv-python numpy pandas matplotlib scikit-learn scipy
```

---

## How to run

1. Open the notebook in **Google Colab** (GPU runtime) or a local Jupyter environment.
2. Mount/point to your dataset directory and set the paths in the configuration cell.
3. Run the cells top to bottom:
   - data loading and augmentation,
   - build the proposed model and baselines,
   - train (per-epoch checkpoints are saved for resume),
   - evaluate on the test set and generate metrics/figures.

Checkpoints and results are written to the output directory set in the notebook.

---

## Method summary

- **Backbone:** EfficientNet-B4 encoder extracts multi-scale features; a U-Net decoder reconstructs the segmentation map through skip connections.
- **Attention:** channel attention reweights feature channels; spatial attention highlights informative regions — together sharpening burned-area boundaries.
- **Loss:** `L = BCE-Dice + Focal + Tversky`, chosen to handle the strong foreground/background imbalance typical of aerial fire imagery.

---

## Reproducibility notes

- A fixed random seed is set for repeatability.
- Training supports checkpoint-and-resume, so interrupted runs continue from the last saved epoch.
- All reported metrics come directly from the notebook's evaluation cells; re-running on the same data should reproduce them within normal run-to-run variance.

---

## Citation

If you use this code, please cite the paper (details to be added on publication):

```bibtex
@article{kumar_daeunet_wildfire,
  title   = {Deep Attention-Guided U-Net with EfficientNet-B4 Encoder for Post-Wildfire Burned-Area Segmentation},
  author  = {Kumar, Sujeet and Bhattacharya, Rajarshi},
  note    = {Manuscript},
  year    = {2026}
}
```

---

## Contact

**Sujeet Kumar** — Department of Electronics and Communication Engineering, National Institute of Technology Patna, India
Email: sujeetk.phd24.ec@nitp.ac.in

---

## License

Add a license of your choice (e.g., MIT) as a `LICENSE` file. The datasets retain their original licenses.
