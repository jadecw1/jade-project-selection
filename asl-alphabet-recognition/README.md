# Static ASL Alphabet Recognition

A computer-vision project comparing four ResNet-18 training strategies for **static American Sign Language (ASL) alphabet classification**.

**Team:** Maddie Bird, Sydney Flake, and Jade Winebright  
**Course:** DAEN 429

## Project overview

The project uses the 29-class ASL Alphabet dataset containing the letters A–Z plus `del`, `nothing`, and `space`. The training dataset contains 87,000 images. An 80/20 stratified train/validation split was used, and training-only augmentation included horizontal flips, rotations, translations, color/brightness adjustments, and Gaussian blur.

Four training policies were compared:

- **T-A:** train the classification head only
- **T-B:** train the final ResNet block plus the classification head
- **T-C:** progressive unfreezing
- **S-A:** train ResNet-18 from scratch

## Results

| Policy | Validation Loss | Validation Accuracy | Validation Macro-F1 |
|---|---:|---:|---:|
| T-A | 0.5344 | 0.8228 | 0.8225 |
| T-B | 0.0096 | 0.9975 | 0.9975 |
| T-C | **0.0012** | **0.9998** | **0.9998** |
| S-A | 0.0444 | 0.9872 | 0.9872 |

**T-C (progressive unfreezing)** was the strongest model overall.

On the original Kaggle test set, T-C achieved:

- **Accuracy:** 1.0000
- **Macro-F1:** 1.0000

On the team's custom test set, performance dropped to:

- **Accuracy:** 0.5926
- **Macro-F1:** 0.4943

The gap between the original and custom test sets highlighted the model's sensitivity to differences in lighting, viewing angle, background, and signer variation.

## Repository structure

```text
asl-alphabet-recognition/
├── README.md
├── requirements.txt
├── code/
│   └── asl_resnet18_ablation.ipynb
├── custom_test_set/
├── figures/
└── report/
    ├── Project Report.pdf
```

## Running the notebook

The notebook was developed for a Kaggle environment and uses `kagglehub` to download the ASL Alphabet dataset and the custom test dataset.

Install dependencies with:

```bash
pip install -r requirements.txt
```

Then open:

```text
code/asl_resnet18_ablation.ipynb
```

A CUDA-capable GPU is strongly recommended because the notebook trains multiple ResNet-18 models on the full 87,000-image training dataset.

## Key takeaway

Transfer learning with progressive unfreezing produced the strongest validation and benchmark-test performance, while the custom-image evaluation showed that near-perfect benchmark performance did not fully translate to more realistic images.
