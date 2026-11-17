# Deep learning for healthcare: a Responsible AI view

Five 80-minute sessions that open the neural network black box and translate what it means for clinical decisions. Every notebook is self-contained, runs on a laptop processor (no graphics card needed) and also runs in Google Colab.

| Session | Notebook | Data | Question |
|---|---|---|---|
| 1 | `01_DL_from_neuron_to_black_box.ipynb` | PhysioNet 2012 ICU | What changes when we replace a readable model with one we cannot read? |
| 2 | `02_DL_does_the_network_earn_its_place.ipynb` | PhysioNet 2012 ICU | Does a neural network beat Cox and random forest from notebook 03? |
| 3 | `03_DL_images_and_the_test_set_trap.ipynb` | DermaMNIST (original and corrected) | Where does deep learning earn its place, and is the test honest? |
| 4 | `04_DL_explanations_and_shortcuts.ipynb` | DermaMNIST corrected | Can explanation maps be trusted, and do they catch shortcuts? |
| 5 | `05_DL_trust_referral_and_decision.ipynb` | DermaMNIST corrected | Calibration, referral, robustness, subgroups, model card, regulation |

## Run locally

Start Jupyter **inside this folder**: the notebooks use relative paths (`data/`, `models/`, `../ICU_Survival_analysis/`).

```bash
conda env create -f environment.yml
conda activate deep-learning-rai
jupyter lab
```

In Jupyter, select the Python kernel from the `deep-learning-rai` environment. The environment uses the CPU version of PyTorch.

Session 2, section 6 uses the TabPFN-2 tabular foundation model (installed by `environment.yml` through pip; in Colab run `%pip install tabpfn`). Its first run downloads the weights from Hugging Face, so it needs internet once; TabPFN-2 needs no account or login. Run that section once before class: on a laptop processor it is the slowest cell. If it fails, the rest of the notebook still runs.

Run session 3 before sessions 4 and 5: it saves `models/cnn_corrected_seed0.pt` (trained on `dermamnist_corrected_28.npz`, seed 0). If the file is missing, sessions 4 and 5 retrain the model automatically (under a minute).

The Conda environment was tested on Windows with Python 3.13.18, PyTorch 2.14.1, NumPy 2.5.5, scikit-learn 1.9.1, pandas 3.1.1, Matplotlib 3.11.2, SciPy 1.18.1 and lifelines 0.30.0. All five notebooks ran from start to finish. The environment file does not lock exact package versions, so a new installation may use different versions.

Earlier measured run times on a 2-core cloud processor: session 1 about 20 s, session 2 about 45 s, session 3 about 2 min, session 4 about 30 s, session 5 about 30 s. Rehearse once on the teaching laptop before class; saved outputs are a fallback if a cell fails live.

## Data sources and licences

- ICU: PhysioNet Computing in Cardiology Challenge 2012, set A, as prepared in the course repository `IE-ML-for-Healthcare/ICU_Survival_analysis`. Sessions 1 and 2 read `../ICU_Survival_analysis/PhysionetChallenge2012-set-a.csv.gz` if present, otherwise download it from GitHub
- Skin lesions: DermaMNIST and DermaMNIST corrected, from [Abhishek et al., 2025, Scientific Data](https://doi.org/10.1038/s41597-025-04382-5), files in [kakumarabhishek/Corrected-Skin-Image-Datasets](https://github.com/kakumarabhishek/Corrected-Skin-Image-Datasets). The repository's Apache 2.0 licence covers its code; the images come from HAM10000 ([Tschandl et al., 2018](https://doi.org/10.1038/sdata.2018.161)) and keep that dataset's non-commercial terms. A copy is in `data/`; if absent, the notebooks download it (about 40 MB)
