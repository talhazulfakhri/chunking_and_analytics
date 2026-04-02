# 📦 Data Engineering Portfolio

> A hands-on, notebook-driven learning portfolio covering the four core skills every data engineer needs: chunking, encryption/masking, data quality, and batch processing.

---

## 🎯 Learning Objectives

By completing all four modules you will be able to:

| # | Module | What you will learn |
|---|--------|---------------------|
| 01 | **Data Chunking** | Split large datasets safely; tune `chunk_size` and `overlap`; profile memory vs throughput tradeoffs |
| 02 | **Data Encryption & Masking** | Apply partial mask, full redaction, tokenisation, and hashing; map strategies to GDPR / PCI-DSS / PDPA requirements |
| 03 | **Data Quality** | Handle nulls (drop / fill / flag), deduplicate on composite keys, validate schemas, and measure completeness |
| 04 | **Batch Processing** | Tune batch size, worker count, and commit intervals; benchmark DB write throughput; avoid connection saturation |

---

## 🗂️ Project Structure

```
de_portfolio/
│
├── README.md                    ← you are here
├── requirements.txt             ← all pip dependencies
│
├── notebooks/
│   ├── 01_data_chunking.ipynb
│   ├── 02_data_encryption.ipynb
│   ├── 03_data_quality.ipynb
│   └── 04_batch_processing.ipynb
│
└── data/                        ← auto-generated sample datasets
    └── (created by notebooks on first run)
```

---

## ⚙️ Quick Setup

### 1 — Clone / download this portfolio

```bash
git clone https://github.com/your-username/de-portfolio.git
cd de-portfolio
```

### 2 — Create a virtual environment (recommended)

```bash
python -m venv .venv

# macOS / Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

### 3 — Install all dependencies

```bash
pip install -r requirements.txt
```

> **Tip:** If you only want the core modules without the database driver:
> ```bash
> pip install pandas numpy jupyter ipywidgets matplotlib seaborn faker cryptography tqdm
> ```

### 4 — Enable notebook widgets

```bash
jupyter nbextension enable --py widgetsnbextension
```

### 5 — Launch Jupyter

```bash
jupyter notebook
# or for JupyterLab
jupyter lab
```

Open the `notebooks/` folder and start with `01_data_chunking.ipynb`.

---

## 📓 Module Overview

### Module 01 — Data Chunking
**File:** `notebooks/01_data_chunking.ipynb`

Learn how to break a large CSV / DataFrame into smaller pieces for memory-efficient processing. Covers:
- Fixed-size chunking with `pandas`
- Overlap-aware chunking for context-sensitive pipelines
- `pd.read_csv(chunksize=...)` for true streaming reads
- Memory profiling with `memory_profiler`
- Interactive widget: tune `chunk_size` and `overlap` and watch the metrics update live

**Key parameters to tune:**
| Parameter | Effect | Recommended range |
|-----------|--------|-------------------|
| `chunk_size` | Records per chunk | 1 000 – 50 000 |
| `overlap` | Shared rows between chunks | 0 – 10 % of chunk_size |
| `chunksize` (pd) | Rows read per IO call | 5 000 – 100 000 |

---

### Module 02 — Data Encryption & Masking
**File:** `notebooks/02_data_encryption.ipynb`

Protect customer PII in compliance with data regulations. Covers:
- Partial masking (email, phone, credit card)
- Full redaction
- Reversible tokenisation (lookup table)
- One-way hashing (`SHA-256`, `bcrypt`)
- AES-256 field-level encryption with `cryptography.Fernet`
- Regulation mapping: GDPR, PCI-DSS, HIPAA, PDPA

**Masking strategy comparison:**
| Strategy | Reversible | Format-preserving | Use case |
|----------|-----------|-------------------|----------|
| Partial mask | ✅ (original kept) | ✅ | Display in UI |
| Full redact | ❌ | ❌ | Audit logs |
| Tokenisation | ✅ (via lookup) | ✅ | Analytics joins |
| Hashing | ❌ | ❌ | Deduplication |
| AES Encryption | ✅ (with key) | ❌ | Storage at rest |

---

### Module 03 — Data Quality
**File:** `notebooks/03_data_quality.ipynb`

Build a reusable cleaning pipeline. Covers:
- Null detection and three handling strategies
- Duplicate detection on single and composite keys
- Type coercion and schema validation
- Data profiling (completeness, uniqueness, validity)
- `great-expectations` for automated quality checks

**Null handling strategies:**
| Strategy | Output rows | Data loss | When to use |
|----------|------------|-----------|-------------|
| `dropna` | Fewer | Yes | High-quality source, nulls are errors |
| Fill mean/mode | Same | No | Analytics, ML feature prep |
| Flag & keep | Same + cols | No | Audit trails, downstream flexibility |

---

### Module 04 — Batch Processing
**File:** `notebooks/04_batch_processing.ipynb`

Optimise pipeline write performance against a simulated database. Covers:
- Single-threaded vs multi-threaded batch writes
- `ThreadPoolExecutor` and `ProcessPoolExecutor`
- SQLAlchemy bulk insert with connection pooling
- Benchmarking: throughput (records/s) vs memory
- Tuning `batch_size`, `max_workers`, `commit_every`

**Tuning rules of thumb:**
| Lever | Increase when... | Decrease when... |
|-------|-----------------|------------------|
| `batch_size` | CPU/network is idle | Memory pressure or DB lock errors |
| `max_workers` | IO-bound pipeline | CPU-bound or DB connections limited |
| `commit_every` | Low latency needed | Memory / crash recovery matters |

---

## 🛡️ Regulation Quick Reference

| Regulation | Region | Key requirement |
|------------|--------|----------------|
| GDPR | EU / EEA | Pseudonymisation, right to erasure |
| PDPA | Indonesia / Thailand | Explicit consent, data minimisation |
| PCI-DSS | Global (payments) | Mask PAN, encrypt cardholder data |
| HIPAA | United States | PHI encryption, access controls |

---

## 🔗 Further Reading

- [pandas chunking docs](https://pandas.pydata.org/docs/user_guide/io.html#io-chunking)
- [cryptography library docs](https://cryptography.io/en/latest/)
- [Great Expectations docs](https://docs.greatexpectations.io)
- [SQLAlchemy connection pooling](https://docs.sqlalchemy.org/en/20/core/pooling.html)
- [Python concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html)

---

## 📄 License

MIT — free to use, adapt, and share for learning purposes.
