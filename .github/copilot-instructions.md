<!-- .github/copilot-instructions.md - guidance for AI coding agents -->
# Repo snapshot & immediate goals

This repository is a small Streamlit-based demo app (Medical_app/index.py) that simulates health monitoring data, preprocesses features, runs an IsolationForest anomaly detector, evaluates results and shows visualizations in a Streamlit UI. There are no tests or CI files discovered.

# What an AI agent should focus on first

- Understand the single main entrypoint: `Medical_app/index.py` — all logic (data sim, preprocessing, modeling, UI) lives in that file. Avoid large-scale refactors unless the scope is agreed upon.
- The app uses these libraries (see `requirements.txt`): `streamlit`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` — keep changes compatible with them.

# Architecture & patterns (short, concrete)

- Single-file Streamlit app: split into logical sections with clearly named functions: `simulate_health_data`, `preprocess_data`, `detect_anomalies`, `evaluate_model`. Use these helpers when modifying behavior.
- Data flow: data -> preprocess -> scale -> IsolationForest -> label -> evaluate/visualize. Any change to features or scaling must propagate through preprocessing, model training, test split, and evaluation steps.
- UI & exports: Streamlit UI displays DataFrames and plots; a sidebar button writes `anomaly_report.csv` to the working directory.

# Developer workflows / useful commands (Windows PowerShell)

- Install dependencies:
```powershell
python -m pip install -r requirements.txt
```
- Run the app (local dev):
```powershell
streamlit run Medical_app/index.py
```
- Quick syntax check (no tests included):
```powershell
python -m pyflakes Medical_app/index.py  # if dev tool installed
```

# Project-specific constraints & guardrails for AI changes

- Do not assume the presence of tests or CI: add tests sparingly and include a simple README note describing how to run them.
- Keep streamlit UI naming/labels intact unless improving clarity (they are part of the UX for reviewers).
- Avoid changing file paths or adding heavy dependencies unless there is a compelling reason.

# Helpful code examples (reference real lines)

- If adding a new feature that uses the simulated dataset, prefer using `simulate_health_data(num_users, minutes)` to keep behavior consistent.
- To change the anomaly detection configuration, update `detect_anomalies(df_scaled, contamination=...)`. Respect the downstream mapping where IsolationForest outputs -1 for anomalies and 1 for normal and the code converts these to 'Anomaly'/'Normal'.

# Suggested small improvements an agent can safely implement

- Factor the long `index.py` into modules (e.g., `data.py`, `models.py`, `ui.py`) but do it in a single PR and preserve current UI behavior.
- Add a small test file that validates `simulate_health_data` produces the expected columns and types.
- Add a minimal README with run instructions if one is requested.

# Where to find things

- Primary app file: `Medical_app/index.py`
- Dependencies: `requirements.txt`

If any parts of the app are inaccurate or you want the agent to expand into automated tests or a CI configuration, tell me which direction you want next and I will iterate. 
