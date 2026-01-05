# Livability Score

This project is a **Flask-based web application** designed to help New York City residents analyze urban livability using public 311 complaint data. It provides a comprehensive dashboard for visualizing complaint trends, searching for specific building health scores, and identifying "Ghost Landlords" based on maintenance responsiveness.

---

## Features

### 1. Interactive Livability Map

* **Zip Code & Building Analysis**: Visualize complaint intensity across different NYC neighborhoods.
* **Category Filtering**: Toggle between categories like Public Safety, Health Hazards, Housing Quality, and more to see how they impact specific areas.
* **Heatmaps**: Identify high-density complaint zones.

### 2. Livability Search

* Search for any building by **Address, Building Number, or Zip Code**.
* View a normalized **Livability Score (0–100)** where higher scores indicate fewer complaints and better living conditions.
* Get a detailed breakdown of complaint types (e.g., Heat/Hot Water vs. Rodents) for specific properties.

### 3. Ghost Landlord Detector

* **Responsiveness Tracking**: Analyzes the time between a 311 complaint being "Created" and "Closed."
* **Landlord Labeling**: Categorizes landlord responsiveness into:
* **Speedy**: Under 3 days.
* **Meh**: 3–7 days.
* **Slow**: 7–14 days.
* **Ghosted**: Over 14 days or unresponsive.



### 4. Data Dashboard

* **High-Level Stats**: Total complaints, unique buildings, and covered zip codes.
* **Rankings**: View the "Best" and "Worst" buildings in the city based on real-time data filtering.
* **Temporal Trends**: Yearly trends showing whether neighborhood conditions are improving or declining.

---

## Technical Stack

* **Backend**: Python / Flask
* **Data Processing**: Pandas, NumPy
* **Database**: PostgreSQL (configured via `db_config.py`)
* **Frontend**: HTML5, Jinja2, JavaScript (Leaflet/Chart.js integration)
* **Data Source**: 311 Service Requests (Integrated CSV format)

---

## Project Structure

* `app.py`: The main Flask application containing routing and API endpoints.
* `livability_model.py`: The core logic engine. Handles data normalization, fuzzy address matching, and the livability scoring algorithm.
* `db_config.py`: Database connection parameters and PostgreSQL URI generation.
* `final_integrated.csv`: (Required) The processed dataset containing NYC 311 complaints and BBL identifiers.

---

## 🔧 Installation & Setup

1. **Clone the repository** and ensure you have the `final_integrated.csv` file in the root directory.
2. **Install Dependencies**:
```bash
pip install flask pandas numpy psycopg2-binary

```


3. **Configure Database** (Optional):
Update `db_config.py` with your local PostgreSQL credentials if using the database-driven features.
4. **Run the Application**:
```bash
python app.py

```

5. **Access the Site**:
Open your browser to `http://127.0.0.1:5001`.

---

## Scoring Methodology

The **Livability Score** is calculated based on 311 complaint volume relative to the city-wide 99th percentile.

* **Normalization**: A square-root transform is applied so that initial complaints impact the score more heavily than outliers.
* **Weights**: While the main score is volume-based, specific categories like **Public Safety** and **Housing Quality** are weighted higher in dashboard summaries.
