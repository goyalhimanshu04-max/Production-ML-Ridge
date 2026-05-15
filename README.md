# Algerian Forest Fire — FWI Prediction (Ridge Regression)

Simple Flask web app that predicts the Fire Weather Index (FWI) for the
Algerian Forest Fires dataset using a pre-trained Ridge Regression model.

Features
- Web UI for entering weather features and showing a predicted FWI
- Pre-trained `ridge` model and `scaler` for inference (stored in `models/`)
- Notebooks for training and experimentation in `notebooks/`

Repository structure

- `application.py` — Flask application and prediction endpoints
- `requirements.txt` — Python dependencies
- `data/` — dataset files (e.g. `Algerian_forest_fires_dataset_UPDATE.csv`)
- `models/` — model artifacts (pickle files)
- `notebooks/` — training and exploration notebooks
- `templates/` — HTML templates (`index.html`, `home.html`)
- `assets/`, `scripts/` — static assets and helper scripts

Quickstart (Windows)

1. Install Python 3.10+.
2. Create and activate a virtual environment:

```powershell
python -m venv .venv
./.venv/Scripts/Activate.ps1
```

3. Install dependencies:

```powershell
pip install -r requirements.txt
```

4. Ensure the model files `ridge.pkl` and `scaler.pkl` exist under `models/`.
	 The current `application.py` uses absolute paths; you may need to update
	 those paths to the relative `models/` folder if running on a different drive.

5. Run the app locally:

```powershell
python application.py
# or (production) via gunicorn:
gunicorn --bind 0.0.0.0:5000 application:app
```

Usage

- Open a browser and go to `http://localhost:5000` to access the UI.
- Click "Predict Now" or navigate to `/predictdata` to enter feature values
	and get a predicted FWI.

Data and training

- Dataset: `data/Algerian_forest_fires_dataset_UPDATE.csv`.
- Notebooks: `notebooks/Model_Training.ipynb` and
	`notebooks/Ridge_Lasso_Regression.ipynb` contain training and evaluation code.
- To retrain, run the notebook (or the training cells) and export new
	`ridge.pkl` and `scaler.pkl` into `models/`.

Notes & Recommendations

- `application.py` currently loads pickles using an absolute path (`B:/...`).
	For portability change the paths to relative references, e.g.:

```python
ridge_model = pickle.load(open('models/ridge.pkl', 'rb'))
standard_scaler = pickle.load(open('models/scaler.pkl', 'rb'))
```

- Consider not committing large binary model files to Git. Use an artifact
	storage (S3/Git LFS) or export lightweight model metadata only.

Contributing

- Open an issue or submit a PR. Keep changes isolated and include tests
	or a short validation notebook when changing model code.

License

- This repository does not include a license file. Add a `LICENSE` if you
	want to make the project open-source.
