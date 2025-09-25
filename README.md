# Air Quality Sensor QA/QC and Validation  

## 📌 Project Overview  
This project analyses data from 20 Zephyr-like low-cost air quality sensors measuring **NO₂ (ppb), PM₂.₅ (µg/m³), temperature (°C), and relative humidity (%)**. The goal is to:  

1. Perform **QA/QC (Quality Assurance & Control)** to clean raw sensor data.  
2. Validate sensor performance by comparing against a **reference station** and neighbouring sensors.  
3. Detect issues such as **drift, step-changes (e.g., firmware updates), and humidity-related PM₂.₅ inflation**.  
4. Generate outputs including tables, plots, and dashboards for reporting.  

---

## 📂 Dataset Description  
The data pack (hourly, ~6.5 weeks) contains four files:  

- `earthsense_measurements.csv` → Sensor measurements (NO₂, PM₂.₅, Temp, RH, firmware, status).  
- `earthsense_reference.csv` → Trusted reference site (NO₂, PM₂.₅, Temp, RH).  
- `earthsense_metadata.csv` → Sensor metadata (lat/lon, siting class, install date, elevation).  
- `earthsense_changelog.csv` → Known events (firmware update, Saharan dust episode, clock-shift bug).  

---
## 📂 Repository Structure  

### 1. `Analysis_Report/`  
- Contains the **main report** of the task.  
- Summarises methodology, results, and key findings (QA/QC, validation, drift detection).  

### 2. `data/`  
- **Raw data** (`earthsense_measurements.csv`, `earthsense_reference.csv`, `earthsense_metadata.csv`, `earthsense_changelog.csv`).  
- **Cleaned datasets** (e.g., `df_hourly.csv`, `df_valid.csv`, `df_hourly_firmware_status.csv`).  
- Used as inputs for analysis and validation.  

### 3. `figures/`  
- Contains all the **plotted figures** generated during analysis.  
- Includes sensor-reference scatter plots, time series comparisons, correlation heatmaps, drift detection plots, and outlier visualisations.  

### 4. `notebooks/`  
- Jupyter notebooks (`.ipynb`) containing the full workflow:  
  - **Task 1:** QA/QC (timestamp alignment, outlier detection, resampling with flags).  
  - **Task 2:** Validation vs reference and neighbour sensors.  
  - **Task 3:** Drift, step-change, and humidity-related PM inflation analysis.  

---

## ⚙️ How to Use  
1. Open the notebooks in the `notebooks/` folder.  
2. Ensure the `data/` folder is available in the working directory.  
3. Run the notebooks step by step to reproduce the results.  
4. Plots and outputs will be saved in the `figures/` folder.  
## ⚙️ Methods  

### Task 1: QA/QC  
- Aligned timestamps (UTC, DST, duplicates, clock drift).  
- Flagged and removed outliers (e.g., PM₂.₅ < 0, RH > 100%).  
- Handled missing values and flatlines.  
- Resampled to **hourly averages** with quality flags.  

### Task 2: Validation vs Reference & Neighbours  
- Computed performance metrics per sensor: **R², Bias, RMSE** for NO₂ and PM₂.₅.  
- Identified **good vs poor-performing sensors**.  
- Correlation analysis across June–July to spot drift and consistency.  

### Task 3: Event & Firmware Analysis  
- Analysed the **July 10, 2025 firmware update** (1.4.2 → 1.5.0).  
- Compared bias before vs after update to detect step-changes.  
- Confirmed ~40% of sensors showed +3 to +9 ppb NO₂ shifts (consistent with changelog).  
- Detected drift and anomalies for individual units (e.g., ZEPHYR_015 timestamp shift bug).  

---

## 📊 Key Outputs  
- **Tables:**  
  - Record counts per sensor.  
  - Outlier counts by parameter.  
  - Validation metrics (R², Bias, RMSE).  
  - Firmware impact on NO₂ bias.  

- **Figures:**  
  - QA/QC pipeline diagram (Bronze → Silver → Gold).  
  - Correlation plots (sensor vs reference).  
  - Bias shift bar charts (firmware impact).  
  - Drift detection plots (rolling residuals).  

---

## ▶️ How to Run  
1. Create and activate a virtual environment:  
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate   # macOS/Linux
   .venv\Scripts\activate      # Windows


