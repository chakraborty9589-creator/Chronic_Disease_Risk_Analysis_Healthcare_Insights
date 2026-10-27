# Chronic Disease Risk Analysis and Healthcare Insights Using Tableau
**Comprehensive Academic & Professional Project Report**

---

## 1. Project Title & Objective

- **Project Title:** Chronic Disease Risk Analysis & Healthcare Insights
- **Domain:** Healthcare Analytics, Epidemiological Risk Assessment, Clinical Informatics, and Data Visualization.
- **Objective:** Analyze patient demographic, clinical, lifestyle, and symptom-related indicators across 5,000 patient records to identify patterns and prevalence associated with three major chronic conditions:
  - **Heart Disease**
  - **Diabetes**
  - **Stroke**
- **Purpose & Scope:** Provide healthcare practitioners, clinical researchers, and public health planners with an interactive visual exploration tool to investigate population-level health trends, compare risk strata, and evaluate health indicators.
- **Ethical Disclaimer:** This project and dashboard are designed strictly for population-level exploratory research and education. They do not constitute individual medical diagnosis or establish causal links.

---

## 2. Dataset Inspection & Technical Audit

| Metric | Verified Value | Analytical Interpretation |
| :--- | :--- | :--- |
| **Dataset File** | [`smart_healthcare_dataset.csv`](file:///c:/Users/soumadip/Desktop/HEALTH%20WALA/smart_healthcare_dataset.csv) | Primary dataset stored in project workspace |
| **Total Patient Records** | **5,000** | Full population cohort evaluated |
| **Total Features (Columns)** | **16** | Demographic, Clinical, Lifestyle, Symptom, Disease flags |
| **Missing / Null Values** | **0 (0.00%)** | 100% complete dataset across all 16 fields |
| **Duplicate Records** | **0 (0.00%)** | Every record represents a distinct observation |
| **Patient Identifier** | *None* | No synthetic IDs fabricated; entity integrity preserved |
| **Disease Encodings** | `0` (Negative) / `1` (Positive) | Binary integer encoding |

### Field Profiles & Distributions:
1. **Age (Years):** Mean = **48.81 &plusmn; 17.84**, Median = 49.0, Range = [18, 79].
2. **Gender:** Female = **2,506 (50.12%)**, Male = **2,494 (49.88%)**. Perfectly balanced sample.
3. **BMI ($\text{kg/m}^2$):** Mean = **24.97 &plusmn; 5.28**, Range = [15.0, 42.6].
4. **Blood Pressure (Systolic, mmHg):** Mean = **134.45 &plusmn; 26.17**, Range = [90, 179].
5. **Cholesterol (Total, mg/dL):** Mean = **224.62 &plusmn; 43.12**, Range = [150, 299].
6. **Glucose (Fasting, mg/dL):** Mean = **134.50 &plusmn; 37.43**, Range = [70, 199].
7. **Exercise Level:** Sedentary (`0`) = 1,647 (32.9%), Moderate (`1`) = 1,677 (33.5%), Active (`2`) = 1,676 (33.5%).
8. **Smoking:** Non-Smoker (`0`) = 2,462 (49.2%), Smoker (`1`) = 2,538 (50.8%).
9. **Alcohol:** Non-Drinker (`0`) = 2,493 (49.9%), Drinker (`1`) = 2,507 (50.1%).
10. **Symptoms:**
    - Fatigue: 2,576 Present (51.5%), 2,424 Absent (48.5%)
    - Chest Pain: 2,520 Present (50.4%), 2,480 Absent (49.6%)
    - Dizziness: 2,487 Present (49.7%), 2,513 Absent (50.3%)
11. **Health Risk Score Audit:** Min = **100.0**, Max = **100.0**, Mean = **100.0**, Variance = **0.00**.
    > **CRITICAL DATA QUALITY FINDING:** The `health_risk_score` is completely invariant (constant at 100.0) across all 5,000 rows. It possesses zero discriminatory power. Consequently, it cannot be used for clinical risk segmentation. A transparent data quality audit note replaces any misleading ranking charts.

---

## 3. Verified Calculations & Prevalence Metrics

All statistics were calculated from the 5,000 valid records without imputation or fabrication:

### A. Overall Disease Prevalence
- **Diabetes:** **34.92%** (1,746 positive / 3,254 negative) &mdash; *Highest prevalence*
- **Heart Disease:** **29.98%** (1,499 positive / 3,501 negative)
- **Stroke:** **24.86%** (1,243 positive / 3,757 negative)

### B. Disease Prevalence by Age Tier
| Age Group | Cohort Size | Heart Disease Prev. | Diabetes Prev. | Stroke Prev. |
| :--- | :---: | :---: | :---: | :---: |
| **Under 30** | 945 | **0.00%** (0) | **0.00%** (0) | **0.00%** (0) |
| **30–39** | 785 | **0.00%** (0) | **0.00%** (0) | **0.00%** (0) |
| **40–49** | 806 | **0.00%** (0) | **0.00%** (0) | **0.00%** (0) |
| **50–59** | 835 | **8.62%** (72) | **15.21%** (127) | **0.00%** (0) |
| **60–69** | 797 | **74.78%** (596) | **98.75%** (787) | **51.57%** (411) |
| **70 and above** | 832 | **99.88%** (831) | **100.00%** (832) | **100.00%** (832) |

*Key finding:* In this dataset, chronic conditions are strictly absent prior to age 50, emerging in the 50–59 cohort, escalating exponentially in ages 60–69, and saturating at virtually 100% in individuals aged 70 and older.

### C. Disease Prevalence by Gender
- **Female (N = 2,506):** Heart Disease: **30.41%** (762), Diabetes: **35.40%** (887), Stroke: **25.14%** (630)
- **Male (N = 2,494):** Heart Disease: **29.55%** (737), Diabetes: **34.44%** (859), Stroke: **24.58%** (613)
*Finding:* Differences between genders remain within &lt;0.96 percentage points across all three conditions.

### D. Disease Prevalence by BMI Stratum
- **Underweight (&lt;18.5, N = 516):** Heart Disease: **20.54%**, Diabetes: **38.18%**, Stroke: **25.39%**
- **Normal weight (18.5–24.9, N = 2,010):** Heart Disease: **25.97%**, Diabetes: **32.84%**, Stroke: **23.93%**
- **Overweight (25.0–29.9, N = 1,671):** Heart Disease: **32.91%**, Diabetes: **34.71%**, Stroke: **25.01%**
- **Obesity (&ge;30.0, N = 803):** Heart Disease: **39.98%**, Diabetes: **38.48%**, Stroke: **26.53%**
*Finding:* Heart disease risk displays a direct linear ascent from 20.54% up to 39.98% as BMI escalates.

### E. Clinical Measurement Comparison (Positive vs. Negative)
- **Heart Disease:**
  - Blood Pressure: Positive Mean = **136.09 mmHg** vs. Negative Mean = **133.74 mmHg** (&Delta; = +2.35 mmHg)
  - Cholesterol: Positive Mean = **225.85 mg/dL** vs. Negative Mean = **224.09 mg/dL** (&Delta; = +1.76 mg/dL)
  - Glucose: Positive Mean = **133.98 mg/dL** vs. Negative Mean = **134.72 mg/dL**
- **Diabetes:**
  - Fasting Glucose: Positive Mean = **135.97 mg/dL** vs. Negative Mean = **133.70 mg/dL** (&Delta; = +2.27 mg/dL)
- **Stroke:**
  - Blood Pressure: Positive Mean = **136.26 mmHg** vs. Negative Mean = **133.84 mmHg** (&Delta; = +2.42 mmHg)

---

## 4. Calculated Fields Implemented in Tableau

The following calculated fields were developed and integrated into the native Tableau workbook:

1. **`[Calculation_AgeGroup]`**:
   ```sql
   IF [age] < 30 THEN "Under 30"
   ELSEIF [age] <= 39 THEN "30-39"
   ELSEIF [age] <= 49 THEN "40-49"
   ELSEIF [age] <= 59 THEN "50-59"
   ELSEIF [age] <= 69 THEN "60-69"
   ELSE "70 and above"
   END
   ```
2. **`[Calculation_BmiCategory]`**:
   ```sql
   IF [bmi] < 18.5 THEN "Underweight (<18.5)"
   ELSEIF [bmi] < 25.0 THEN "Normal weight (18.5-24.9)"
   ELSEIF [bmi] < 30.0 THEN "Overweight (25.0-29.9)"
   ELSE "Obesity (>=30.0)"
   END
   ```
3. **`[Calculation_HDStatus]`**:
   `IF [heart_disease] = 1 THEN "Positive" ELSEIF [heart_disease] = 0 THEN "Negative" ELSE "Unknown" END`
4. **`[Calculation_DiabetesStatus]`**:
   `IF [diabetes] = 1 THEN "Positive" ELSEIF [diabetes] = 0 THEN "Negative" ELSE "Unknown" END`
5. **`[Calculation_StrokeStatus]`**:
   `IF [stroke] = 1 THEN "Positive" ELSEIF [stroke] = 0 THEN "Negative" ELSE "Unknown" END`
6. **`[Calculation_HDPrev]`**:
   `(SUM([heart_disease]) / COUNT([heart_disease])) * 100`
7. **`[Calculation_DiabetesPrev]`**:
   `(SUM([diabetes]) / COUNT([diabetes])) * 100`
8. **`[Calculation_StrokePrev]`**:
   `(SUM([stroke]) / COUNT([stroke])) * 100`
9. **`[Calculation_ExerciseLabel]`**:
   `IF [exercise_level] = 0 THEN "Sedentary (Level 0)" ELSEIF [exercise_level] = 1 THEN "Moderate (Level 1)" ELSE "Active (Level 2)" END`
10. **`[Calculation_SmokingLabel]`**:
    `IF [smoking] = 1 THEN "Smoker" ELSE "Non-Smoker" END`
11. **`[Calculation_AlcoholLabel]`**:
    `IF [alcohol] = 1 THEN "Drinker" ELSE "Non-Drinker" END`
12. **`[Calculation_FatigueLabel]` / `[Calculation_ChestPainLabel]` / `[Calculation_DizzinessLabel]`**:
    Categorical labels mapping binary indicators to descriptive symptom strings.
13. **`[Calculation_RiskScoreNote]`**:
    `"Data Quality Warning: Health Risk Score is constant at 100.0 across all 5,000 records. Non-discriminative for clinical risk segmentation."`

---

## 5. Worksheets & Visual Structure

The workbook contains **11 dedicated analytical worksheets**:

| Worksheet Name | Chart Type | Analytical Focus |
| :--- | :--- | :--- |
| **WS 1: Overall Disease Prevalence** | Horizontal / Column Bar Chart | Compares prevalence rates across Heart Disease (29.98%), Diabetes (34.92%), Stroke (24.86%). |
| **WS 2: Disease Distribution** | Stacked / Grouped Bar Chart | Positive vs. negative patient counts for each chronic condition. |
| **WS 3: Prevalence by Age Group** | Multi-Line / Grouped Bar Chart | Illustrates the age threshold dynamics across the 6 ordered age tiers. |
| **WS 4: Prevalence by Gender** | Grouped Bar Chart | Female vs. male prevalence rates with consistent denominators. |
| **WS 5: BMI Category Analysis** | Bar Chart with Measure Subgroups | Population distribution and heart disease prevalence scaling with BMI. |
| **WS 6: Clinical Indicators** | Grouped Comparison Bars | Mean Blood Pressure, Cholesterol, and Glucose across positive vs. negative cohorts. |
| **WS 7: Lifestyle Analysis** | Clustered Column Chart | Prevalence across Exercise Tiers (0, 1, 2), Smoking, and Alcohol categories. |
| **WS 8: Symptom Patterns** | Comparative Bar Chart | Rates of chronic diseases in patients presenting with Chest Pain, Fatigue, and Dizziness. |
| **WS 9: Health Risk Score Note** | Formatted Data Quality Callout | Transparent audit of invariant score (100.0) preventing misleading visual artifacts. |
| **WS 10: Demographic Overview** | Donut / Pyramid Distribution | Overall cohort gender balance and age-tier population counts. |
| **WS 11: Key Findings & KPIs** | Summary KPI Cards | Total counts and key rate indicators for executive review. |

---

## 6. Dashboard Architecture & User Personas

The Master Dashboard (`Chronic Disease Risk Analysis Dashboard`) is arranged with an intentional visual hierarchy:

```
+------------------------------------------------------------------------------------------------+
|  HEADER: Chronic Disease Risk Analysis & Healthcare Insights | N = 5,000 Verified Patients     |
+------------------------------------------------------------------------------------------------+
|  KPIs: [Total: 5,000] [Diabetes: 34.92%] [Heart Disease: 29.98%] [Stroke: 24.86%] [Age: 48.8] |
+------------------------------------------------------------------------------------------------+
|  ROW 1: (WS 1) Overall Prevalence  | (WS 2) Disease Distribution | (WS 10) Demographics        |
+------------------------------------------------------------------------------------------------+
|  ROW 2: (WS 3) Age Group Dynamics (0% -> 100%)       | (WS 4) Gender    | (WS 5) BMI Strata   |
+------------------------------------------------------------------------------------------------+
|  ROW 3: (WS 6) Clinical Indicators | (WS 7) Lifestyle Analysis   | (WS 8) Symptom Patterns     |
+------------------------------------------------------------------------------------------------+
|  BOTTOM: (WS 9) Health Risk Score Data Quality Warning | (WS 11) Analytical Findings & Notes   |
+------------------------------------------------------------------------------------------------+
```

### Three User Personas Supported:

1. **Persona 1: Healthcare Professional (Clinician / Physician)**
   - *Needs:* Clinical indicators (systolic BP, cholesterol, fasting glucose), acute symptom reporting, age-stratified prevalence.
   - *Dashboard Value:* Quick identification of high-prevalence demographic cohorts (patients &ge; 50) and BMI risk factors, with explicit reminders that clinical measurements alone do not substitute for comprehensive diagnostic workups.
2. **Persona 2: Healthcare Researcher & Data Analyst**
   - *Needs:* Precise denominators, statistical distributions, data cleanliness audits, and variance verification.
   - *Dashboard Value:* Transparent reporting of cohort counts (5,000 records, 0 nulls), validation that `health_risk_score` is invariant, and clear separation of correlation from clinical causation.
3. **Persona 3: Public Health Planner & Administrator**
   - *Needs:* High-level demographic disease burdens, lifestyle associations, and population health screening priorities.
   - *Dashboard Value:* Provides executive KPI cards, demographic pyramids, and multi-disease comparisons to guide health education and screening outreach for geriatric populations.

---

## 7. Deliverable Artifacts

All deliverables have been created and verified in the workspace:

1. **Tableau Workbook (`.twb`):**
   [`Chronic_Disease_Risk_Analysis_Healthcare_Insights.twb`](file:///c:/Users/soumadip/Desktop/HEALTH%20WALA/Chronic_Disease_Risk_Analysis_Healthcare_Insights.twb)
   - Configured with native XML schema version 18.1 compatible with Tableau Public 2026.2.
   - Verified active and running in Tableau Public Desktop (`tabpublic.exe`).
2. **Tableau Packaged Workbook (`.twbx`):**
   [`Chronic_Disease_Risk_Analysis_Healthcare_Insights.twbx`](file:///c:/Users/soumadip/Desktop/HEALTH%20WALA/Chronic_Disease_Risk_Analysis_Healthcare_Insights.twbx)
   - Self-contained package containing both the workbook XML and the embedded dataset (`Data/smart_healthcare_dataset.csv`).
   - Portable for academic submission, professor evaluation, and portfolio sharing.
3. **Interactive Web Dashboard (`index.html`):**
   [`index.html`](file:///c:/Users/soumadip/Desktop/HEALTH%20WALA/index.html)
   - Full interactive client-side dashboard powered by Chart.js and Tailwind CSS.
   - Features real-time multi-variable filtering, live KPI recalculations, and persona toggles.
4. **Source Dataset (`.csv`):**
   [`smart_healthcare_dataset.csv`](file:///c:/Users/soumadip/Desktop/HEALTH%20WALA/smart_healthcare_dataset.csv)
   - 5,000 verified rows, 16 features.
