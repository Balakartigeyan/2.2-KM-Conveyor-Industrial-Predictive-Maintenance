# 2.2-KM-Conveyor-Industrial-Predictive-Maintenance

[![Status](https://img.shields.io/badge/status-proof%20of%20concept-blue.svg)](https://github.com/)
[![Python](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](LICENSE)

Project repository containing an end-to-end exploratory analysis and anomaly detection pipeline built from one month of conveyor monitoring telemetry captured in an industrial mining environment.

## Project Objective
Deliver actionable anomaly detection and predictive maintenance insights for a 2.2 km conveyor system. The goal is to surface abnormal operating conditions that can indicate incipient faults and to recommend next steps toward a production-ready failure prediction pipeline.

## Summary
- Data: 1 month of conveyor sensor telemetry (temperature, vibration, load, current, speed, etc.)
- Use cases: early anomaly detection, operational monitoring, and maintenance prioritization
- Outcome: Data quality and signal are sufficient for anomaly detection; additional fault/failure labels are required to build robust supervised failure-prediction models.

## Sample Analysis Output
![Anomaly Detection](eda_plot.png)

## Key Findings
- Identified distinct abnormal vibration spikes that correlate with specific time windows and load events.
- Detected gradual temperature drift associated with increasing conveyor load—suggests thermal stress under heavy operation.
- The dataset contains useful signals for anomaly detection but lacks sufficient labeled failure events for reliable supervised failure-prediction models.

## Tools & Libraries
- Python 3.9+
- pandas, numpy
- scikit-learn
- matplotlib, seaborn
- (Optional) statsmodels, scikit-learn-contrib for extended anomaly methods

## Data
- Source: Onboard conveyor monitoring system (one-month window)
- Typical fields: timestamp, motor_temp_C, vibration_rms_mm_s, motor_current_A, load_percent, shaft_speed_rpm, ambient_temp
- Notes:
  - Ensure consistent timestamp alignment and sampling frequency prior to analysis.
  - Missing values and sensor dropouts were observed and handled via interpolation / forward-fill where appropriate.

## Analysis & Methods
- Exploratory Data Analysis (time series plots, distribution checks, seasonality)
- Unsupervised anomaly detection:
  - Threshold-based detection on vibration and temperature
  - Isolation Forest and statistical outlier detection for multi-variate anomalies
- Feature engineering:
  - Rolling statistics (mean, std), derivative (slope), and event windows
- Evaluation:
  - Visual inspection and domain expert validation of flagged anomalies
  - Limited labeled failures prevented robust supervised evaluation metrics

## Recommendations & Next Steps
1. Increase labeled failure/maintenance-event data (logs from CMMS or maintenance tickets) to enable supervised failure prediction.  
2. Add richer feature extraction:
   - Frequency-domain vibration features (FFT / spectral energy)
   - Time-lagged features and cross-correlations
   - Operational context (shift, load profile, material type)
3. Implement continuous ingestion and real-time anomaly scoring (streaming with Kafka / MQTT + lightweight inference).  
4. Deploy alerting and dashboards for operations with contextual explanations for each anomaly.  
5. Add model monitoring: data drift, concept drift, and regular retraining plans.

## How to run (quickstart)
1. Create virtual environment and install deps:
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   pip install -r requirements.txt
   ```
2. Inspect the notebook and plots:
   - Open notebooks/analysis.ipynb (or the main notebook) in JupyterLab / Jupyter Notebook.
3. Run anomaly detection script (example):
   ```bash
   python scripts/run_anomaly_detection.py --input data/conveyor_month.csv --output outputs/anomalies.csv
   ```

(Adjust script names and arguments as needed to match repository layout.)

## Caveats
- Results are exploratory and intended to inform next-phase engineering work.
- Supervised failure prediction requires more labeled positive failure events; otherwise, models risk overfitting to noise or operational shifts.

## Contributing
Contributions and domain feedback are welcome:
1. Fork the repository
2. Create a feature branch
3. Add tests and documentation for new analysis or ingestion modules
4. Open a Pull Request outlining the purpose and validation steps

## License
MIT — see LICENSE file.

## Contact
Maintainer: Balakartigeyan  
GitHub: https://github.com/Balakartigeyan
