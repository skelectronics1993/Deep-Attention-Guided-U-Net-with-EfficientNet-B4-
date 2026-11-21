# Deep Attention-Guided U-Net with EfficientNet-B4 Encoder for Post-Wildfire Burned-Area Segmentation

Code for the paper **"Deep Attention-Guided U-Net with EfficientNet-B4 Encoder for Post-Wildfire Burned-Area Segmentation."**

This repository provides the training, evaluation, and ablation code for a dual-attention U-Net that segments burned areas / fire regions from UAV wildfire imagery. The proposed model pairs an **EfficientNet-B4** encoder with a U-Net decoder and **channel + spatial attention**, trained with a combined loss (**BCE–Dice + Focal + Tversky**).

## Notebooks

| File | Status | Notes |
|---|---|---|
| `sujeeth_code_corrected.ipynb` | **Current / verified** | Use this version. Baselines (ResNet50, DenseNet121) and the proposed model's test metrics are genuinely executed and reproducible from this notebook. Unverified ablation/statistics cells present in earlier drafts have been removed. |
| `sujeeth_code_10-09_26 updated.ipynb` | Superseded | Kept for history only. Some cells in this version (attention ablation, loss ablation, bootstrap statistics) contain stale/hardcoded outputs that do not match a re-run of the current code — do not cite numbers from this file. |

## Datasets

- **BurnedAreaUAV** (Portugal) — UAV RGB imagery with pixel-level burned/unburned masks
- **Boreal-Forest-Fire Subset-C** (Finland) — UAV RGB imagery; manual and SAM-generated mask subsets

## Verified test-set results

| Model | IoU | Dice | Precision | Recall | F1 |
|---|---|---|---|---|---|
| **Proposed (Dual-Attention EfficientNet-B4 U-Net)** | 0.9056 | 0.9505 | 0.9464 | 0.9546 | 0.9505 |
| ResNet50-U-Net | 0.8496 | 0.9123 | 0.9017 | 0.9238 | 0.9123 |
| DenseNet121-U-Net | 0.8558 | 0.9157 | 0.9052 | 0.9266 | 0.9157 |

*Test-label provenance: ground-truth masks are a mix of manually annotated and SAM-generated (pseudo-)masks; see the paper's Data Description section for the exact split.*

## Code and Data Availability

- Datasets: BurnedAreaUAV and Boreal-Forest-Fire Subset-C (see citations in the paper)
- Code: this repository
- Trained weights: [add link if/when released]

## Citation

If you use this code, please cite the paper (full citation to be added upon acceptance/publication).
