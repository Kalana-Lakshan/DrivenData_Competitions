# DrivenData_Competitions

A curated collection of solutions, notebooks, scripts, and experiments for DrivenData competitions. This repository collects competition code, data-handling utilities, experiments, and reproducible pipelines so you can review, re-run, or adapt methods for future data science competitions.

> Note: This repository contains code and notebooks that reference externally hosted datasets. Datasets are not included in this repository — see the Data section below for download and setup instructions.

## Table of Contents

- [Repository goals](#repository-goals)
- [Repository structure](#repository-structure)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Data](#data)
- [How to run experiments](#how-to-run-experiments)
- [Reproducing notebook results](#reproducing-notebook-results)
- [Adding a new competition](#adding-a-new-competition)
- [Best practices and tips](#best-practices-and-tips)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Repository goals

- Keep a reproducible record of approaches tried on DrivenData competitions.
- Provide runnable notebooks and scripts that can be re-used or adapted.
- Store helper utilities for data loading, feature engineering, training, and evaluation.
- Document experiments and results so future work can build on past efforts.

## Repository structure

The repository follows a per-competition layout to keep things organized:

- competitions/
  - <competition-name>/
    - data/                 # data download instructions, local ingestion scripts, data checks
    - notebooks/            # exploratory and modeling notebooks (.ipynb)
    - src/                  # modules and scripts (feature engineering, models, utils)
    - experiments/          # experiment configs, outputs, saved models
    - requirements.txt      # competition-specific dependencies (optional)
    - README.md             # competition-specific notes and instructions
- scripts/                  # top-level helper scripts (run_all, eval, etc.)
- envs/                     # environment files (conda .yml or pip requirements)
- README.md                 # this file
- LICENSE

Example tree:
```
competitions/
└── soil-moisture-prediction/
    ├── data/
    ├── notebooks/
    ├── src/
    ├── experiments/
    └── README.md
```

## Getting started

### Prerequisites

- Python 3.8+ (some competitions may require different versions; check competition-specific README)
- Git
- Recommended: conda for environment management

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/Kalana-Lakshan/DrivenData_Competitions.git
   cd DrivenData_Competitions
   ```

2. Create an environment (example with conda):
   ```
   conda create -n driven-data python=3.10 -y
   conda activate driven-data
   ```

3. Install top-level dependencies (if present):
   ```
   pip install -r envs/requirements.txt
   ```
   or install competition-specific requirements:
   ```
   pip install -r competitions/<competition-name>/requirements.txt
   ```

### Data

- Raw competition datasets are not stored in this repository.
- For each competition folder there is a `data/` README or setup script that explains:
  - Where to download the datasets (DrivenData competition page or public data host).
  - How to place the data locally (expected paths).
  - Any preprocessing steps required to prepare the data for notebooks or scripts.

Example expected local layout for a competition:
```
competitions/<competition-name>/data/raw/
competitions/<competition-name>/data/processed/
```

Use the included data ingestion scripts where available:
```
python competitions/<competition-name>/src/ingest_data.py --input-dir path/to/downloads --output-dir competitions/<competition-name>/data/processed
```

## How to run experiments

Each competition includes scripts and/or notebooks. Typical workflow:

1. Inspect `competitions/<competition-name>/README.md` for competition-specific instructions.
2. Run a preprocessing script (if available):
   ```
   python competitions/<competition-name>/src/preprocess.py --config competitions/<competition-name>/experiments/config.yaml
   ```
3. Train a model:
   ```
   python competitions/<competition-name>/src/train.py --config competitions/<competition-name>/experiments/config.yaml
   ```
4. Evaluate / create submission:
   ```
   python competitions/<competition-name>/src/predict.py --model-path experiments/run_x/model.pkl --output submission.csv
   ```

Scripts usually accept a `--config` or `--run-id` to reproduce experiments from `experiments/`.

## Reproducing notebook results

- Use the exact environment specified in the competition folder (requirements or environment YAML).
- Restart the kernel and run cells top-to-bottom after placing the required data in the `data/` folder.
- For long-running experiments, check `experiments/` for saved model artifacts and logs — notebooks often reference those to avoid retraining.

## Adding a new competition

To add a new competition, follow the repository conventions:

1. Create a new folder: `competitions/<competition-name>/`
2. Add the following minimal files:
   - `README.md` — short description + data download instructions
   - `src/` — place reusable code (data loaders, models, utils)
   - `notebooks/` — exploratory notebooks
   - `experiments/` — include at least one example config
   - `requirements.txt` (optional) — competition-specific dependencies
3. Add ingestion script and a small README in `data/` describing expected file locations.
4. Open a PR describing the competition and how to run the example.

A good `competitions/<competition>/README.md` should include:
- Short competition overview and objective
- How to obtain the data (links)
- Minimum steps to reproduce the main result

## Best practices and tips

- Keep data out of the repository. Use `data/.gitignore` and document expected paths.
- Use config files (YAML/JSON) to capture experiment hyperparameters and random seeds.
- Version your experiments and save trained models under `experiments/<run-id>/`.
- Add small, reproducible scripts for end-to-end runs so others don’t need to run large notebooks.
- Log deterministic dependencies and Python package versions.

## Contributing

Contributions are welcome. Typical contributions:
- Add a new competition or complete an incomplete competition folder.
- Improve documentation and reproducibility.
- Add utilities that are reusable across competitions.

Please open an issue for larger changes or a pull request with a clear title and description. Include relevant metadata:
- Competition name
- Steps to reproduce
- Expected runtime / resource requirements

## Code of conduct

We expect all contributors to follow respectful, constructive, and professional behavior. If you’d like, add a CODE_OF_CONDUCT.md to the repository.

## License

Specify a license (e.g., MIT) in the repository root. If you don’t want to choose one yet, add a TODO and a short note in this README.

Example:
```
LICENSE: MIT
```

## Contact

Repository owner: Kalana-Lakshan

If you have questions about a specific competition or experiment, open an issue in this repository and tag the competition folder in the issue title.
