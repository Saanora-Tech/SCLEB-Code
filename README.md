# SCLEB – Saanora Comprehensive LLM Evaluation Benchmark

**SCLEB** is a tiny, zero-cost framework that lets you **benchmark any Large-Language-Model locally** – no servers, no Docker, no secrets required.  
Add your own tasks, register any model (OpenAI, Anthropic, local HF endpoint, …), create a run, and evaluate – all from the command line.

---

## ✨ Features

| Feature | Notes |
|---------|-------|
| 🗄️ SQLite DB | auto-created, lives inside `src/database/app.db` |
| 🛠️ Add Model CLI | `add_model.py` |
| 📝 Add Task  CLI | `add_task.py` |
| 🎛️ Create Run CLI | `create_run.py` |
| ⚡ Run Benchmark  | `run_benchmark.py` (single eval **or** full run) |
| 🌱 Demo Data      | `load_sample_data.py` (4 tasks + 3 models) |
| 🌐 Optional UI    | `python src/main.py` starts a tiny Flask site |

---

## 🖥️ Installation

```bash
git clone https://github.com/<your-user>/SCLEB.git
cd SCLEB
python -m venv .venv && source .venv/bin/activate   # optional but recommended
pip install -r requirements.txt

---

## 🚀 Quick Start

# 1) seed demo tasks & models
python load_sample_data.py

# 2) create a run that benchmarks demo models on all tasks
python create_run.py --name demo --models 1 2 3

# 3) execute the run (replace <ID> with the printed id)
python run_benchmark.py --run-id <ID>

---

## ➕ Add YOUR Model

python add_model.py --name "Local-LLaMA" \
                    --provider local \
                    --endpoint http://localhost:8000/generate

or via JSON: python add_model.py --json my_model.json

---

##➕ Add YOUR Task
python add_task.py \
  --category reasoning \
  --subcategory math \
  --type exact_match \
  --title "2+2" \
  --prompt "What is 2 + 2?" \
  --expect 4

or JSON: python add_task.py --json my_task.json

---

##🏃 One-off Single Evaluation
python run_benchmark.py --model 1 --task 5
