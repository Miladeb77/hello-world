# PanelApp Version & Gene Checker

This tool checks local gene panel data against the official signed-off **PanelApp** data to identify differences in panel versions and gene lists.  
It generates a clear, timestamped report summarising any changes.

---

## Features

- **Version Comparison**  
  Compares your local panel version against the latest signed-off version in PanelApp.

- **Gene List Comparison**  
  - Compares your local gene list against the *same version* in PanelApp.  
  - If your local version is outdated, also compares your gene list against the *most recent* signed-off version.

- **Filtered Gene Retrieval**  
  Fetches only high-confidence genes from PanelApp (marked **Expert Review Green**).

- **Automated Reporting**  
  Generates a timestamped `.txt` report with all findings.

- **Logging**  
  Creates a detailed, timestamped log file for each run in the `logs/` directory.

---

## Setup

### 1. Create a Virtual Environment & Install Dependencies

From the `PanelChecker` directory:

```bash
python -m venv PanelChecker_venv
source PanelChecker_venv/bin/activate
pip install requests coverage
```

### 2. Configure File Paths


Before running the script, update the file paths in Check_panels.py:

```python
# --- Data and Constants ---
LOCAL_VERSION_FILE = '/path/to/your/panel_versions'
LOCAL_GENES_FILE   = '/path/to/your/transcripts'
```

Replace the paths with your local data locations.

---

## Usage 

Run the script with your desired options.

- **Check a single panel** 

```bash
python Check_panels.py --Rcodes R141
```

- **Check multiple panels** 

```bash
python Check_panels.py --Rcodes R141,R384,R156
```

- **Check all panels** 

```bash
python Check_panels.py --Rcodes ALL
```

- **Interactive Mode (prompt for R-codes)** 

```bash
python Check_panels.py
```

---

## Outputs

The script generates two types of output in the PanelChecker directory:

- **Interactive Mode (prompt for R-codes)** 
  A human-readable summary of findings, saved as: panel_check_report_[timestamp].txt

- **Log File**
  A detailed execution log, saved in logs/ as: panel_check_[timestamp].log

---

## Running Tests (Optional)

A test suite is included. To run with coverage:

```bash
coverage run -m unittest test_Check_panels.py
coverage report -m
```
