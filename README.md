# 🔥 Full Guide: Building a Reliable AI/DS Environment with Anaconda, Conda & UV

> _“In Data Science, controlling your environment is controlling your outcome.”_

---

## 📌 Overview

Dalam proyek AI dan Data Science, banyak orang terjebak pada masalah yang sebenarnya bukan masalah modeling atau data, melainkan:

- Konflik dependency package
- Perbedaan versi library
- Project tidak bisa direplikasi di mesin lain
- Setup yang butuh waktu berjam-jam hanya untuk menyiapkan tools

**Masalah utamanya sederhana: environment management.**

Pada tutorial ini, saya akan membahas:

- Mengapa environment isolation itu krusial.
- Bagaimana membangun environment yang solid dengan Anaconda, Conda, dan UV.
- Best practice setup yang scalable, reliable, dan siap untuk project production-level.

---

## 🧠 Konsep Dasar: Environment Is King 👑

### Analoginya:

Bayangkan environment itu seperti *laboratorium eksperimen*.  
Setiap eksperimen AI kamu butuh:

- Suhu tertentu (Python version)
- Alat tertentu (packages)
- Bahan baku (dataset, dependency)
- Petunjuk prosedur (config versioning)

**Satu kesalahan kecil, eksperimen gagal.**

Itulah kenapa isolasi environment adalah prosedur wajib. Bukan sekedar "biar bisa jalan", tapi *agar project tetap reproducible kapanpun dan dimanapun*.

---

## 🔧 Tools Stack

### 1️⃣ **Anaconda**  
Distribusi Python + Data Science toolkit yang sudah pre-packed.  
Memberikan kenyamanan one-stop installation:  
Python, Jupyter, NumPy, Pandas, SciKit-Learn, Matplotlib, dll langsung tersedia.

### 2️⃣ **Conda (Environment Manager)**  
Engine utama untuk environment management:

- Create isolated environment
- Manage multiple Python versions
- Install packages & resolve dependencies secara otomatis

### 3️⃣ **UV (Ultra Fast Package Installer)**  
UV adalah generation-next package manager, jauh lebih cepat & deterministic dibanding pip:

- Resolusi dependency lebih cepat
- Build reproducible lockfiles
- Sangat optimal untuk CI/CD & cloud-based AI development

---

## 🚀 Full Setup Guide

---

### 🟠 Step 1 — Install Anaconda

- Download installer sesuai OS dari [https://www.anaconda.com/products/distribution](https://www.anaconda.com/products/distribution)
- Jalankan installer
- Pada opsi PATH, centang **Add Anaconda to PATH** (saya menyarankan aktifkan untuk CLI access)

#### Verifikasi:

```bash
conda --version
python --version
```

### 🟠  Step 2 — Membuat Environment Isolated

Misalnya saya ingin membuat environment AI untuk project sentiment analysis:
```bash
conda create --name ai-sentiment python=3.11
```

Aktifkan:
```bash
conda activate ai-sentiment
```

Cek environment aktif:
```bash
conda info --envs
```

### 🟠 Step 4 — Install UV (UltraFast Pip)
Option A — via pip (jika cepat)
```bash
pip install uv
```

Option B — via installer (stabil & disarankan)
```bash
curl -Ls https://astral.sh/uv/install.sh | sh
```

Verifikasi:
```bash
uv --version
```

🟠 Step 5 — Install Additional Packages via UV
Contoh:

```bash
uv pip install seaborn xgboost nltk lightgbm
```

Hasilnya:
- Proses install jauh lebih cepat
- Dependency resolution jauh lebih stabil

🟠 Step 6 — Testing Environment via Jupyter
Buka:

```bash
jupyter notebook
```

Lakukan import testing:
```python
import numpy as np
import pandas as pd
import tensorflow as tf
import torch
import seaborn as sns
import lightgbm as lgb
```
Jika tidak error: Environment Fully Operational.

✅ Best Practices (Do & Don’ts)
Do:
- Isolasi setiap project dalam environment terpisah.
- Export environment untuk reproducibility:

```bash
conda env export > ai-sentiment.yml
```
Import environment jika deploy ulang:

```bash
conda env create -f ai-sentiment.yml
```
Gunakan UV untuk optimasi speed saat install package pip-based.

Don’t:
- Install semua package di base environment.
- Campur-campur pip dan conda tanpa kontrol.
- Abaikan documentation dependency tiap project.
