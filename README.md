# Healthcare Operations & Patient Risk Analytics

### Business Problem
Hospital leadership faces two critical operational and clinical challenges: **Emergency Department (ED) patient flow bottlenecks** and **Intensive Care Unit (ICU) sepsis morbidity**. Prolonged ED wait times compromise patient safety, while delayed sepsis recognition in the ICU drives preventable mortality and extended bed occupancy.

This project analyzes ED operational logs and ICU patient records to uncover root-cause bottlenecks, build interpretable baseline predictive models, and deliver evidence-based recommendations for hospital management.

### Key Findings
1. Emergency Department Operations (01_ED_Analysis.ipynb)
- Primary Bottleneck: Average total ED visit duration was 71 minutes, with Provider Wait Time averaging 42 minutes (59%)—far exceeding triage (8 mins), registration (6 mins), and consultation (15 mins).
- Triage Integrity: Clinical triage worked effectively across all departments, prioritizing life-threatening Priority 1 cases (5 mins) over non-urgent Priority 5 cases (67 mins).
- Night-Shift Staffing Deficit: Even with 0 patients in queue, wait times averaged 44 minutes. Filtering by zero-queue arrivals revealed that staffing reductions during 21:00–05:00 (7–9 staff vs. 11–12 during daytime shifts) caused wait times to spike to 36–59 minutes. Increasing provider staffing cuts average wait times by over half (from 64 mins at 2 staff to 25–29 mins at 15–16 staff).
2. ICU Sepsis Risk (02_ICU_Sepsis_Analysis.ipynb)
- High Clinical Burden: Out of 180 ICU admissions, 27.8% (50 patients) developed sepsis.
- Extended Length of Stay: Sepsis shifted ICU length of stay from short discharges (20–40 hours) toward prolonged stays of 45–75 hours, straining ICU bed capacity.
- Early Onset Peak: Over 50% of sepsis cases developed within the first 10–20 hours of ICU admission, indicating many patients entered the ICU already incubating infection.
- Demographic Profile: Sepsis split nearly evenly by gender (26 males vs. 24 females) and clustered among adults aged 40–70 (mirroring overall ICU admission demographics), underscoring the need for physiological screening over demographic profiling alone.
  
### Modeling & Evaluation Summary
- ED Waiting Time Prediction (Regression): Trained Linear Regression, Decision Tree, and Random Forest models evaluated via MAE, RMSE, and R2 to quantify prediction error in clinical minutes.
- ICU Sepsis Prediction (Classification): Trained Logistic Regression, Decision Tree, and Random Forest classifiers using stratified train/test splits and strictly pre-onset clinical features (excluding post-outcome variables like total LOS, antibiotics administered etc). Evaluated using Confusion Matrices, Precision, Recall, F1-Score, and ROC-AUC, prioritizing Recall to minimize the severe mortality cost of False Negatives.
  
### Strategic Recommendations
- Reallocate ED Overnight Staffing (21:00–05:00): Shift 2–3 provider slots to cover late-night/early-morning arrivals and mitigate the 44-minute zero-queue baseline delay.
- Enforce Mandatory First-24-Hour ICU Sepsis Screening: Implement automatic serum lactate checks and infection screening upon ICU admission to catch early-onset cases within the critical 10–20 hour window.
- Prioritize High-Recall Alert Thresholds: Tune clinical decision-support models to minimize False Negatives while pairing alerts with rapid nurse verification.

### Limitations
- ICU_Sepsis_Patient_Data.xlsx contains synthetic educational clinical features intended for portfolio modeling and requires live EHR recalibration before clinical deployment.
- The ICU dataset is limited to 180 patient admissions, constraining deep multi-variable subgroup analysis.
- ED logs do not capture diagnostic lab/imaging turnaround times or inpatient bed boarding delays.
  
### How to Reproduce Project
### 1. Clone the repository
git clone <your-repo-url>
cd healthcare-analytics-capstone

### 2. Install required packages
pip install -r requirements.txt

### 3. Launch Jupyter and run notebooks in order
jupyter notebook


