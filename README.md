# 💻 Laptop Price Predictor

An interactive web application that predicts laptop prices based on user-selected specifications using a machine learning model. Built with Streamlit, this project enables users to estimate laptop prices, explore data insights, and understand feature impacts on pricing.

---

## 🚀 Features

- **Price Prediction**: Enter laptop specs (brand, RAM, CPU, GPU, storage, etc.) to get an instant price estimate.
- **Data Exploration**: Visualize price distributions, brand comparisons, and feature importance with interactive charts.
- **Similar Laptops**: See real examples from the dataset that match your predicted price range.
- **Modern UI**: Enhanced with custom CSS for a visually appealing and user-friendly experience.

---

## 🏗️ Project Structure

```
├── app.py                  # Streamlit web app
├── create_alternative_model.py  # Script to build a fallback ML model
├── df.pkl                  # Preprocessed DataFrame (used by app)
├── laptop_data.csv         # Raw laptop dataset
├── pipe.pkl                # Main trained ML pipeline
├── Procfile                # For deployment (e.g., Render, Heroku)
├── render_setup.sh         # Render deployment setup
├── requirements.txt        # Python dependencies
├── setup.sh                # Environment setup script
├── update_app_model.py     # Script to update/patch the app model
```

---

## 🖥️ Usage

### 1. **Install Requirements**
```bash
pip install -r requirements.txt
```

### 2. **Run the App Locally**
```bash
streamlit run app.py
```

### 3. **Web Interface**
- Open your browser at [http://localhost:8501](http://localhost:8501)
- Use the sidebar to navigate between:
  - **Predict Price**: Input specs and get a price prediction
  - **Explore Data**: Visualize price trends, brand stats, and feature impacts
  - **About**: Learn about the app, model, and team

---

## 📊 Data & Model
- **Dataset**: `laptop_data.csv` (over 1,300 laptops, various brands and specs)
- **Features Used**: Brand, Type, RAM, Storage (HDD/SSD), CPU, GPU, Screen Size, Resolution, OS, Weight, Touchscreen, IPS
- **Model**: Trained regression pipeline (scikit-learn, OneHotEncoder, RandomForest/GradientBoosting)
- **Performance**: R² ≈ 0.86 (explains ~86% of price variance)

---

## 🛠️ Deployment
- **Procfile** and **setup.sh** provided for easy deployment on Render, Heroku, or similar platforms.
- Example Render build command:
  ```sh
  sh setup.sh && streamlit run app.py
  ```

---

## 👨‍💻 Authors
- Kanav Singla (2023UCD3014)
- Utkarsh Dubey (2023UCD3059)

---

## 📚 Technologies Used
- Streamlit
- scikit-learn
- pandas, numpy
- matplotlib, seaborn

---

## ⚠️ Disclaimer
> The predictions are for reference only and may not reflect real-time market prices. Use at your own discretion.

---

## 📄 License
This project is for educational purposes.
