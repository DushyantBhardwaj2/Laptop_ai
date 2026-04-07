# Laptop Price Predictor

## 1) What This Project Does

This project is a machine-learning web application that predicts laptop prices from hardware and software specifications.

The app is built with Streamlit and supports three modes:

- Predict Price: Interactive form-based prediction.
- Explore Data: Charts and comparisons built from the dataset.
- About: Model and project summary.

Primary implementation file: [app.py](app.py)

---

## 2) Core Files And Their Purpose

- [app.py](app.py): Main Streamlit application (UI, model loading, prediction, charts).
- [requirements.txt](requirements.txt): Python dependencies used by local run, Docker, and cloud deploy.
- [runtime.txt](runtime.txt): Target Python runtime for Streamlit Cloud and compatibility.
- [df.pkl](df.pkl): Serialized dataset used for dropdown options, visualization, and similar-laptop lookup.
- [pipe.pkl](pipe.pkl): Primary serialized trained pipeline model.
- [pipe_no_xgb.pkl](pipe_no_xgb.pkl): Fallback serialized model used if primary model fails to load.
- [laptop_data.csv](laptop_data.csv): Source tabular dataset.
- [Dockerfile](Dockerfile): Containerized local run configuration.
- [.dockerignore](.dockerignore): Excludes unnecessary files from Docker build context.
- [.github/workflows/main.yml](.github/workflows/main.yml): CI workflow (install/smoke/build checks).

---

## 3) Detailed Working Of app.py

### 3.1 App Startup

At startup, the app performs:

1. Library imports (Streamlit, NumPy, pandas, matplotlib, seaborn, pickle).
2. NumPy pickle compatibility monkey patch initialization.
3. Streamlit page setup and CSS injection.
4. Cached loading of model and dataset.

### 3.2 Model Compatibility Layer

The code includes robust compatibility for old/new pickle environments:

- Custom constructor hook for NumPy random bit generators.
- Custom unpickler class that remaps numpy internal module path differences.
- Safe loader that first tries native pickle load, then fallback remap logic.
- Model fallback sequence:
  1) Try [pipe.pkl](pipe.pkl)
  2) If loading fails, use [pipe_no_xgb.pkl](pipe_no_xgb.pkl)

This improves reliability across dependency/runtime mismatches.

### 3.3 Cached Resource Loading

The load function is decorated with Streamlit cache resource, so model/data loading occurs once per session/kernel lifecycle rather than every rerun.

This reduces startup and interaction latency.

### 3.4 Sidebar Navigation

Sidebar provides:

- App title and hero image.
- Navigation radio selector:
  - Predict Price
  - Explore Data
  - About
- Creator information and short app description.

### 3.5 Prediction Workflow

In Predict Price mode:

1. User selects laptop specs from structured inputs.
2. App computes derived feature PPI using resolution and screen size.
3. Text fields are sanitized to ASCII-compatible representation.
4. Feature vector is built in expected model order (12 inputs).
5. Pipeline predicts log price, then exponential transform returns price scale.
6. Predicted value is rendered in styled result block.
7. Selected specification summary is shown.
8. Similar laptops are retrieved from dataset by price band (about +-10%).

### 3.6 Explore Data Workflow

In Explore Data mode, charts are generated dynamically:

- Price distribution histogram.
- Price range pie chart.
- Brand-wise boxplot and market share pie.
- Average price by brand/type bar chart.
- RAM vs price scatter plot.
- Touchscreen and OS average price comparisons.

### 3.7 About Section

Contains model context, feature overview, claimed performance context, and usage disclaimer.

---

## 4) Input Specification (Prediction Form)

Model input features used in prediction query:

1. Company
2. TypeName (laptop type)
3. RAM (GB)
4. Weight (kg)
5. Touchscreen (0/1)
6. IPS (0/1)
7. PPI (derived)
8. CPU brand
9. HDD (GB)
10. SSD (GB)
11. GPU brand
12. Operating system

PPI is computed as:

$$
PPI = \frac{\sqrt{(X_{res})^2 + (Y_{res})^2}}{Screen\ Size\ (inches)}
$$

---

## 5) Model Information

The app uses serialized trained regression pipeline artifacts:

- Primary artifact: [pipe.pkl](pipe.pkl)
- Fallback artifact: [pipe_no_xgb.pkl](pipe_no_xgb.pkl)

Observed model behavior in app:

- Pipeline accepts a 12-feature query.
- Output is treated as log-price and transformed by exponential function.
- Fallback strategy ensures app remains usable when one artifact cannot deserialize.

Supporting data artifact:

- [df.pkl](df.pkl) for UI option values, analysis charts, and similar product lookup.

---

## 6) Tools, Libraries, And Platform Stack

### 6.1 Main Python Libraries

- streamlit
- pandas
- numpy
- scikit-learn
- xgboost
- scipy
- matplotlib
- seaborn
- pillow

Current pinned versions are listed in [requirements.txt](requirements.txt).

### 6.2 DevOps And Delivery Tools

- Git and GitHub (source control and remote hosting)
- GitHub Actions workflow in [.github/workflows/main.yml](.github/workflows/main.yml)
- Docker via [Dockerfile](Dockerfile)
- Streamlit Community Cloud for public deployment

---

## 7) Local Run Instructions

### 7.1 Without Docker

```bash
pip install -r requirements.txt
streamlit run app.py
```

Open http://localhost:8501

### 7.2 With Docker

```bash
docker build -t laptop-price-predictor .
docker run --rm -p 8501:8501 laptop-price-predictor
```

Open http://localhost:8501

---

## 8) Streamlit Cloud Deployment Notes

When deploying on Community Cloud:

- Use repository root [requirements.txt](requirements.txt).
- Use [app.py](app.py) as entrypoint.
- Prefer selecting Python 3.11 or 3.12 in Advanced settings if dependency resolution issues appear with newer defaults.

If deployment logs show dependency solver conflicts:

1. Verify exact package pin in [requirements.txt](requirements.txt).
2. Verify selected Python version in Cloud Advanced settings.
3. Reboot or redeploy app after updating settings.

---

## 9) Common Troubleshooting Scenarios

### 9.1 Pickle/NumPy Deserialization Errors

Handled by compatibility unpickler and constructor hook in [app.py](app.py).

### 9.2 Model Load Failure

Automatic fallback from primary model to compatibility model.

### 9.3 Prediction Runtime Errors

Prediction block has exception handling and user-facing fallback guidance.

### 9.4 Schema Differences In Similar Laptop Section

Safe dictionary-style field access is used for alternative column names/fallback values.

---

## 10) Project Structure

```text
.
|-- .github/
|   `-- workflows/
|       `-- main.yml
|-- .streamlit/
|   `-- config.toml
|-- .dockerignore
|-- Dockerfile
|-- README.md
|-- VIVA_QA.md
|-- app.py
|-- requirements.txt
|-- runtime.txt
|-- df.pkl
|-- pipe.pkl
|-- pipe_no_xgb.pkl
|-- laptop_data.csv
|-- create_alternative_model.py
|-- update_app_model.py
`-- jupyter-nb-python-conversion.py
```

---

## 11) Credits

- Kanav Singla (2023UCD3014)
- Utkarsh Dubey (2023UCD3059)
- Dushyant Bhardwaj (2023UCD2163)

---

## 12) License

Educational use only.
