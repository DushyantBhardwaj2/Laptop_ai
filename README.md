# Laptop Price Predictor - DevOps Edition (Localhost)

## Project Overview

This is a Streamlit-based ML web app that predicts laptop prices from user-selected specifications. The project has been upgraded with essential DevOps practices for local deployment and academic demonstration.

## Tech Stack

- Python 3.11
- Streamlit
- scikit-learn
- xgboost
- pandas, numpy, scipy
- matplotlib, seaborn
- Docker
- GitHub Actions

## DevOps Implementation

### Docker (Local Containerization)

- Added a Dockerfile for localhost execution.
- App runs on port 8501 inside the container.
- Added .dockerignore to reduce build context size.

### CI/CD (GitHub Actions)

- Added workflow at .github/workflows/main.yml.
- Pipeline steps:
  - Checkout code
  - Setup Python 3.11
  - Install dependencies
  - Run smoke test
  - Build Docker image for validation (no push)

## How To Run Locally

### Normal Run (Without Docker)

```bash
pip install -r requirements.txt
streamlit run app.py
```

Open: <http://localhost:8501>

## Deploy Online (Easiest Way)

Use Streamlit Community Cloud.

1. Push this repo to GitHub.
2. Sign in to Streamlit Community Cloud.
3. Select this repository and set `app.py` as the main file.
4. Deploy using `requirements.txt` and `runtime.txt`.
5. Share the public URL once deployment completes.

Notes:

- Docker is not required for this route.
- `runtime.txt` pins Python 3.11 for better compatibility.
- If a package mismatch appears, update `requirements.txt` and redeploy.

### Docker Run

```bash
docker build -t laptop-price-predictor .
docker run --rm -p 8501:8501 laptop-price-predictor
```

Open: <http://localhost:8501>

## Final Clean Structure

```text
.
|-- .github/
|   `-- workflows/
|       `-- main.yml
|-- .dockerignore
|-- Dockerfile
|-- README.md
|-- VIVA_QA.md
|-- app.py
|-- requirements.txt
|-- df.pkl
|-- pipe.pkl
|-- pipe_no_xgb.pkl
|-- laptop_data.csv
|-- create_alternative_model.py
|-- update_app_model.py
`-- jupyter-nb-python-conversion.py
```

## Notes

- This project is localhost-only by design.
- No cloud deployment or Kubernetes is used.

## License

Educational use only.
