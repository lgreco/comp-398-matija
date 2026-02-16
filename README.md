# Matija's COMP 398 Independent Study - Spring 2026



# Analyzing the Chicago 311 Service Requests Dataset

*A Structured Plan for a Senior-Level CS Project*

---

## Phase 0: Project Framing and Research Questions

Before touching code, define:

1. **Problem Statement**

   * Are we analyzing service efficiency?
   * Detecting geographic inequities?
   * Forecasting workload?
   * Identifying anomaly patterns?

2. **Hypotheses**

   * Certain neighborhoods experience longer resolution times.
   * Specific request types cluster spatially.
   * Seasonal patterns affect service response.

3. **Evaluation Criteria**

   * Statistical significance?
   * Predictive accuracy?
   * Clustering quality (e.g., silhouette score)?


---

## Phase 1: Environment Setup & Data Acquisition

### 1. Reproducible Development Environment

* Use:

  * Jupyter Notebook (exploration)
  * Python virtual environment or Conda
* Track dependencies (`requirements.txt`)
* Version control via Git

### 2. API-Based Data Retrieval (SODA API)

* Identify dataset ID from the Chicago Data Portal.
* Use:

  * `requests` (basic)
  * `sodapy` (preferred wrapper)
* Implement:

  * Pagination
  * Rate-limit handling
  * Incremental pulls for large datasets

Example concerns:

* API limits
* Authentication for high-volume queries
* Filtering at the API level (use `$select`, `$where`, `$limit`)

This is where you show API literacy, not just “download CSV.”

---

## Phase 2: Data Engineering & Cleaning

### 1. Schema Inspection

* Identify:

  * Request type
  * Status
  * Created date
  * Closed date
  * Location fields
  * Department/Agency

### 2. Data Cleaning

* Handle:

  * Missing geocoordinates
  * Inconsistent request types
  * Invalid timestamps
* Convert:

  * Strings → datetime
  * Derived fields:

    * `time_to_close`
    * `day_of_week`
    * `month`
    * `hour`

### 3. Data Normalization

* Standardize categorical labels
* Possibly encode categories
* Remove obvious outliers (justify criteria)

At this level, justify every transformation.

---

## Phase 3: Exploratory Data Analysis (EDA)

### 1. Univariate Analysis

* Distribution of request types
* Distribution of resolution times
* Volume over time

### 2. Temporal Analysis

* Requests per month (seasonality)
* Time-to-close trends over years
* Weekend vs weekday behavior

### 3. Geographic Analysis

* Requests per neighborhood
* Normalized by population (if census data available)
* Heatmaps

Visualization tools:

* Matplotlib
* Seaborn
* Plotly (interactive)
* Folium (map-based visualization)

The key is: **derive insight, not just produce plots.** The plots illustrate a narrative, the narrative tells a story.

---

## Phase 4: Geospatial Visualization

I think option B may be better but I see a lot of folium and geopandas work done in the field, so worth trying them out for an hour or two.

### Option A: Python-Based Mapping

* `folium`
* `geopandas`
* `contextily`

### Option B: Google Maps API (External)

* Feed cleaned coordinate data
* Build:

  * Heatmaps
  * Marker clustering
  * Time-slider visualizations



---

## Phase 5: Statistical & Machine Learning Analysis


### 1. Clustering

**Geospatial Clustering**

* K-Means on (lat, lon)
* DBSCAN (better for density-based hotspots)

Evaluate:

* Silhouette score
* Cluster interpretability

---

### 2. Predictive Modeling

Predict:

* Time to close (regression)
* Likelihood of escalation (classification)

Features:

* Request type
* Time of day
* Neighborhood
* Historical backlog

Models:

* Linear regression
* Random forest
* Gradient boosting


---

### 3. Equity / Bias Analysis

Investigate:

* Do certain neighborhoods have systematically longer resolution times?
* Control for request type.

Use:

* Statistical tests (t-test, ANOVA)
* Confidence intervals

We move from visualization to story telling.

---

## Phase 6: Reproducibility & Reporting

* Organize notebook:

  * Data loading
  * Cleaning
  * EDA
  * Modeling
  * Conclusions
* Provide:

  * README
  * Requirements file
  * Clear explanation of assumptions
* Optional:

  * Interactive dashboard (Streamlit or Dash)

---

## Deliverable 

1. Clear research question
2. API-driven data ingestion
3. Thoughtful feature engineering
4. Statistical or ML analysis with evaluation
5. Discussion of limitations
6. Ethical considerations
7. Reproducible codebase
