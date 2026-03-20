# Data Science Education — Jupyter Notebooks

A complete curriculum covering Data Science, Machine Learning, and Deep Learning as interactive Jupyter notebooks.

## Project Structure

```
workshop_1/
├── notebooks/          # All notebooks (.ipynb)
│   ├── 01_python_basics.ipynb
│   ├── 02_python_intermediate.ipynb
│   ├── 03_python_advanced.ipynb
│   ├── 04_sql_course.ipynb
│   ├── 05_numpy_pandas_course.ipynb
│   ├── 06_statistics_ds_course.ipynb
│   ├── 07_data_visualization_course.ipynb
│   ├── 08_machine_learning_course.ipynb
├── data/               # Data folder (shared between container and host)
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

---

## Option 1 — Docker (recommended)

No Python installation or local dependencies required.

### Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows / macOS / Linux)

### Getting Started

```bash
# 1. Clone / download the repository and navigate to the folder
cd education

# 2. Build the image and start the container
#    (first run takes a few minutes — downloads PyTorch, sklearn, etc.)
docker compose up --build

# 3. Open your browser at
#    http://localhost:8888
```

Subsequent starts (no rebuild needed):

```bash
docker compose up
```

Stop the container:

```bash
docker compose down
```

### Volumes (file synchronisation)

| Host folder | Container path | Description |
|---|---|---|
| `./notebooks/` | `/workspace/notebooks/` | Notebooks — changes are reflected immediately on both sides |
| `./data/` | `/workspace/data/` | Data files — files saved inside the container appear on the host and vice versa |

> All notebook changes are saved directly to your host disk. Nothing is lost after `docker compose down`.

---

## Option 2 — Local Python (virtualenv)

Use this if you already have Python 3.10+ installed and prefer not to use Docker.

### Requirements

- Python 3.10 or newer ([python.org](https://www.python.org/downloads/))

### Installation

```bash
# 1. Navigate to the project folder
cd education

# 2. Create a virtual environment
python -m venv .venv

# 3. Activate the environment
#    macOS / Linux:
source .venv/bin/activate
#    Windows (PowerShell):
.venv\Scripts\Activate.ps1

# 4. Install dependencies
pip install --upgrade pip
pip install -r requirements.txt

# 5. Install PyTorch (CPU build)
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu

# 6. Launch JupyterLab
jupyter lab --notebook-dir=notebooks
```

Your browser will open at `http://localhost:8888`.

### Deactivate the environment

```bash
deactivate
```

---

## Notebooks Overview

| # | Notebook | Topics covered |
|---|---|---|
| 01 | `01_python_basics.ipynb` | Python basics — types, loops, functions |
| 02 | `02_python_intermediate.ipynb` | OOP, exceptions, standard library |
| 03 | `03_python_advanced.ipynb` | Advanced Python — decorators, generators, async |
| 04 | `04_sql_course.ipynb` | SQL — SELECT, JOINs, CTEs, Window Functions, SQLAlchemy |
| 05 | `05_numpy_pandas_course.ipynb` | NumPy (arrays, broadcasting, linalg) + Pandas (DataFrame, groupby, time series) |
| 06 | `06_statistics_ds_course.ipynb` | Statistics, distributions, hypothesis testing, EDA, feature engineering |
| 07 | `07_data_visualization_course.ipynb` | Matplotlib, Seaborn, Plotly — static and interactive charts |
| 08 | `08_machine_learning_course.ipynb` | Scikit-learn, XGBoost, LightGBM, clustering, pipelines, hyperparameter tuning |

---

## Troubleshooting

**Port 8888 is already in use**

Change the port in `docker-compose.yml`:
```yaml
ports:
  - "8889:8888"   # then open http://localhost:8889
```

**Build fails due to insufficient disk space or memory**

The PyTorch CPU build is ~800 MB. Make sure Docker Desktop has at least **4 GB RAM** and **10 GB disk space** allocated.

**Kernel does not start in a notebook**

In JupyterLab select the kernel manually: `Kernel → Change Kernel → Python 3`.
