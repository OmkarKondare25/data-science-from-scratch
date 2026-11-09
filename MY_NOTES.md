# My Notes — Doubts, Commands and Tips

Everything I asked while learning that the course syllabus doesn't cover: doubts, commands, errors and fixes, tools and career questions.
New doubts are added to the **Doubts & answers log** (newest first); reference sections below get updated when relevant.

Full study notes: [Complete Data Science, ML, DL & NLP Bootcamp — Course Guide](https://claude.ai/artifact/FvZPmcwuutHQX9t5qoM9te)

## Contents

1. [Doubts & answers log](#doubts--answers-log)
2. [Daily quick reference](#daily-quick-reference)
3. [Python environments](#python-environments)
4. [Errors I hit and how I fixed them](#errors-i-hit-and-how-i-fixed-them)
5. [VS Code setup](#vs-code-setup)
6. [Git and GitHub](#git-and-github)
7. [Learning plan decisions](#learning-plan-decisions)

---

## Doubts & answers log

### 2026-11-09 — Can I create multiple venvs?
- **Q:** Can we create more than one virtual environment?
- **A:** Yes — each venv is just a folder with its own Python and libraries. Use one per project (each portfolio repo gets its own), one per Python version, or separate ones for heavy stacks (e.g. TensorFlow vs PyTorch). For course practice, one venv in `D:\Data Science` is enough.
  - Create: `python -m venv venv` (default 3.12) · `py -3.10 -m venv venv310` (needs 3.10 installed) · `python -m venv venv-dl` (any name).
  - Switch: `deactivate` → `venv310\Scripts\activate`. The prompt prefix, e.g. `(venv310)`, shows which is active. In VS Code: Select Interpreter.
  - Keep them out of Git: add `venv*/` to `.gitignore` for custom names.
  - Separate requirements per venv: `pip freeze > requirements-dl.txt`.
  - Delete = delete the folder (`rmdir /s /q venv310`). Never copy or move a venv; rebuild it and reinstall from the requirements file.

### 2026-11-09 — Switched the venv to Python 3.12.3
- **Q:** `python app.py` printed nothing in the 3.10 venv, so I rebuilt the venv with 3.12.3. Is that OK?
- **A:** Yes. Every library in the course supports Python 3.12, so 3.10 isn't required. Keep one version for the whole project. To rebuild a venv: `rmdir /s /q venv` → `python -m venv venv` → `venv\Scripts\activate` → `pip install -r requirements.txt`, then re-select the interpreter in VS Code.
- **To diagnose "no output" next time:** `where python` (first line should be the venv's python.exe; a `...\WindowsApps\python.exe` entry is the Microsoft Store placeholder that does nothing), `python --version`, `python -c "print('hello')"`, `type app.py`.

### 2026-11-09 — My app.py gives no output
- **Q:** `01-python\practice\app.py` contains `print(1+3)` but I don't see any output.
- **A:** The code is fine; the problem is how it's run. Common causes:
  1. **Wrong folder** — from `D:\Data Science`, run `python 01-python\practice\app.py` (or `cd 01-python\practice` then `python app.py`). Error looks like `can't open file ... No such file or directory`.
  2. **Looking in the wrong tab** — the ▶ Run button prints in the **TERMINAL** tab, on the last line after a long command; not OUTPUT or DEBUG CONSOLE.
  3. **File not saved** — a dot on the tab means unsaved; press Ctrl+S or turn on File → Auto Save.
  4. **Typing Python into the Windows prompt** — `print(1+3)` at `D:\Data Science>` doesn't work; type `python` first to get the `>>>` prompt, or run the file.

### 2026-11-09 — Where to keep notes?
- **Q:** Where should I keep notes of my doubts so I can push them to GitHub?
- **A:** In this file (`MY_NOTES.md`) at the root of `D:\Data Science`. It's committed and pushed with everything else. Course-topic notes go in each part's `notes.md`; doubts outside the syllabus go here.

### 2026-11-09 — VS Code doesn't show my venv in "Select Interpreter"
- **Q:** I can't find `.\venv\Scripts\python.exe` in Python: Select Interpreter.
- **A:** Install the Microsoft **Python** extension, open `D:\Data Science` itself via File → Open Folder, check the venv exists (`dir venv\Scripts\python.exe`), or use **Enter interpreter path… → Find…** to pick it manually. See [VS Code setup](#vs-code-setup).

### 2026-11-09 — Can I use Python 3.10 only for this project, without conda?
- **Q:** I want Python 3.10 for this project but don't have conda.
- **A:** Yes. Install Python 3.10 next to 3.12 (leave "Add to PATH" unticked), then `py -3.10 -m venv venv`. Inside the venv, `python` is 3.10; elsewhere it's still 3.12. See [Python environments](#python-environments).

### 2026-11-09 — `conda` is not recognized
- **Q:** `conda create -p venv python==3.10` fails with "'conda' is not recognized". Can I just run `create -p venv python==3.10`?
- **A:** No. `create` is a conda sub-command, not a standalone command, and conda uses `python=3.10` (single `=`). The error means conda isn't installed or this terminal can't find it. Use venv instead, or run conda from **Anaconda Prompt**.

### 2026-11-09 — Can I use GitHub Desktop instead of Git commands?
- **Q:** I have GitHub Desktop. How do I use it?
- **A:** File → Add local repository → `D:\Data Science` → **Publish repository**. Daily: write a summary → **Commit to main** → **Push origin**. See [Git and GitHub](#git-and-github).

### 2026-11-09 — How do I push all my practice code and notes to GitHub?
- **Q:** I'm starting from scratch and want everything on GitHub.
- **A:** One learning repo (`D:\Data Science`) with a folder per course part (`notes.md`, `practice/`, `notebooks/`), plus a separate repo for each portfolio project. A `.gitignore` keeps out secrets, venv, datasets and models.

### 2026-11-09 — Which role should I aim for?
- **Q:** I already know data analysis. I'm aiming for data scientist, ML engineer or GenAI engineer.
- **A:** Learn the shared core once, then specialise. First target: **ML engineer with GenAI skills** ("AI engineer"). About 33 weeks at 2–3 hours/day. See [Learning plan decisions](#learning-plan-decisions).

### 2026-11-09 — Is the course enough to get a job?
- **Q:** Is this course (plus the guide) enough to become job ready?
- **A:** The content covers most entry-level requirements. What gets you hired is proof: 3–5 deployed projects with good READMEs, ~100 SQL + ~100 Python practice problems, domain knowledge, and explaining your work clearly. Domain projects (banking, reconciliation) stand out.

---

## Daily quick reference

Every study session: open the project → activate the environment → study → commit and push.

**Start of session** (VS Code terminal, Command Prompt):

```bash
cd "D:\Data Science"
venv\Scripts\activate
```

`(venv)` appears at the start of the prompt when it's active.

**Installing a new library while studying:**

```bash
pip install <library-name>
pip freeze > requirements.txt
```

**End of session** — GitHub Desktop: write a summary → **Commit to main** → **Push origin**. Or in the terminal:

```bash
git add .
git commit -m "Part 1: loops and list practice"
git push
```

**Leave the environment** (optional): `deactivate`

---

## Python environments

A **virtual environment** is a private box of Python + libraries for one project, so projects don't break each other. This project uses Python's built-in **venv** with **Python 3.12.3** (switched from 3.10 on 2026-11-09). Create it with `python -m venv venv`. The 3.10 steps below are kept for reference in case a project ever needs an older version.

### venv vs conda

| | venv | conda |
| --- | --- | --- |
| Comes with | Python itself | Anaconda / Miniconda (separate install) |
| Create | `py -3.10 -m venv venv` | `conda create -p venv python=3.10 -y` |
| Activate | `venv\Scripts\activate` | `conda activate "D:\Data Science\venv"` |
| Install libraries | `pip install ...` | `pip install ...` or `conda install ...` |
| Python version | Must be installed already (py launcher) | Downloads any version |
| What I use | Yes | Not installed |

### Using Python 3.10 alongside 3.12 (one-time setup)

| Command | What it does |
| --- | --- |
| `winget install Python.Python.3.10` | Installs Python 3.10 (or python.org installer with "Add to PATH" **unticked**) |
| `py --list` | Lists installed Python versions (should show 3.12 and 3.10) |
| `rmdir /s /q venv` | Deletes an old venv, e.g. one made with the wrong version |
| `py -3.10 -m venv venv` | Creates a venv named `venv` using Python 3.10 |
| `venv\Scripts\activate` | Turns the venv on in this terminal |
| `python --version` | Shows the active Python (should be 3.10.x) |
| `python -m pip install --upgrade pip` | Updates pip, the library installer |
| `pip install -r requirements.txt` | Installs every library in requirements.txt |
| `pip freeze > requirements.txt` | Saves installed libraries and exact versions to the file |
| `deactivate` | Turns the venv off |

### Conda commands (reference, if I install Anaconda later)

Run in **Anaconda Prompt**, not plain cmd:

```bash
cd /d "D:\Data Science"
conda create -p venv python=3.10 -y
conda activate "D:\Data Science\venv"
conda init cmd.exe
```

- `-p venv` creates the environment inside the project folder.
- Conda uses a single `=` (`python=3.10`).
- `conda init cmd.exe` lets the normal VS Code terminal find conda (restart VS Code after).

---

## Errors I hit and how I fixed them

| Error / problem | Why | Fix |
| --- | --- | --- |
| `'condacreate' is not recognized...` | Typo: missing space | `conda create` is two words |
| `'conda' is not recognized as an internal or external command` | Anaconda not installed, or terminal can't find it | Use venv (`py -3.10 -m venv venv`), or Anaconda Prompt, or `conda init cmd.exe` then restart VS Code |
| `create -p venv python==3.10` alone doesn't work | `create` belongs to conda; conda uses `=` not `==` | `conda create -p venv python=3.10` or `py -3.10 -m venv venv` |
| "Python: Select Interpreter" missing from Ctrl+Shift+P | Python extension not installed | Ctrl+Shift+X → install **Python** by Microsoft → reload |
| venv not listed in Select Interpreter | Wrong folder open, venv missing, or not detected | Open `D:\Data Science`; check `dir venv\Scripts\python.exe`; or **Enter interpreter path… → Find…** |
| `LF will be replaced by CRLF` on commit | Windows vs Linux line endings | Harmless, ignore |
| `py -3.10` says version not found | 3.10 not installed, or terminal opened before install | Install 3.10, reopen terminal, check `py --list` |
| `python app.py` → `can't open file ... No such file or directory` | Terminal is in a different folder than the file | `cd` into the file's folder, or run with the path: `python 01-python\practice\app.py` |
| Script runs but no output visible | Looking in OUTPUT / DEBUG CONSOLE, or file not saved | Check the **TERMINAL** tab; save with Ctrl+S (or File → Auto Save) |

---

## VS Code setup

1. **Install the Python extension** — Ctrl+Shift+X → "Python" by **Microsoft** (adds Pylance and Jupyter).
2. **Open the project folder** — File → Open Folder… → `D:\Data Science`. Explorer should show `01-python`, `README.md`, `venv` at the top.
3. **Select the interpreter** — Ctrl+Shift+P → `Select Interpreter` → `.\venv\Scripts\python.exe` (3.12.3). Not listed? **Enter interpreter path… → Find…** → `D:\Data Science\venv\Scripts\python.exe`.
4. **Check** — open a `.py` file; bottom-right shows **3.12.3 ('venv')**. Click it to switch.
5. **Terminal** — Terminal → New Terminal (Ctrl+`). VS Code usually activates the venv automatically.

| Shortcut | Does |
| --- | --- |
| Ctrl+Shift+P | Command palette — search any action |
| Ctrl+` | Show / hide terminal |
| Ctrl+Shift+X | Extensions |
| Ctrl+Shift+G | Source Control (Git) panel |
| Shift+Enter | Run notebook cell and move to next |

---

## Git and GitHub

**Setup:** one learning repo (`D:\Data Science`) for all practice and notes, plus a separate repo per portfolio project. Kept apart from the work repo `D:\Bank_Recon`.

### Folder structure

```
D:\Data Science\
├── README.md          ← goal + progress table
├── MY_NOTES.md        ← this file
├── .gitignore         ← files Git must never upload
├── requirements.txt   ← libraries for this project
├── venv\              ← environment (ignored by Git)
├── 01-python\
│   ├── notes.md       ← summary in my own words
│   ├── practice\      ← .py exercises
│   └── notebooks\     ← .ipynb files
├── 02-data-analysis\  … up to 16-career\
```

**.gitignore keeps out:** `venv/`, `.env` (secrets), `__pycache__/`, `.ipynb_checkpoints/`, datasets (`data/`, `*.csv`, `*.xlsx`, `*.parquet`), models (`*.pkl`, `*.joblib`, `*.h5`, `*.pt`, `*.onnx`), `mlruns/`, editor folders.

### Git commands

| Command | What it does | When |
| --- | --- | --- |
| `git --version` | Checks Git is installed | Once |
| `git config --global user.name "Your Name"` | Name on your commits | Once per computer |
| `git config --global user.email "you@example.com"` | Email on commits (GitHub noreply keeps it private) | Once per computer |
| `git init -b main` | Makes a folder a Git repo, branch `main` | Once per project |
| `git status` | Shows changed / new / staged files | Any time |
| `git add .` | Stages all changes | Every session |
| `git commit -m "message"` | Saves a snapshot with a description | Every session |
| `git log --oneline` | Lists past commits | Any time |
| `git remote add origin <url>` | Links local repo to GitHub | Once (not needed with GitHub Desktop Publish) |
| `git branch -M main` | Renames current branch to `main` | Once, if needed |
| `git push -u origin main` | First upload; remembers the target | Once |
| `git push` | Uploads new commits | Every session |
| `git pull` | Downloads changes from GitHub | When working from another computer |

### GitHub Desktop workflow

*One time:*

1. Sign in: File → Options → Accounts.
2. File → **Add local repository…** → `D:\Data Science`.
3. **Publish repository** → name it (e.g. `data-science-journey`) → untick "Keep this code private" so recruiters can see it → Publish.

*Every session:* save in VS Code → changed files appear in GitHub Desktop → type a summary → **Commit to main** → **Push origin**.

*Handy:* Ctrl+Shift+G = view on GitHub · Ctrl+Shift+A = open in VS Code · History tab = past commits · right-click a file → **Ignore file**.

### Safety rules

- Never commit API keys or passwords — keep them in `.env`. If one leaks, revoke it immediately.
- Don't commit datasets; GitHub rejects files over 100 MB. Link to the source instead.
- Clear notebook outputs before committing big notebooks (or install `nbstripout`).
- No company code or data — public or synthetic data only.
- Commit messages say what I learned: `Part 5: logistic regression + ROC practice`.
- Commit daily — it builds a visible activity history.

---

## Learning plan decisions

**Target:** data scientist, ML engineer or GenAI engineer. I already know data analysis, so I only brush up statistics and SQL. First target: **ML engineer with GenAI skills** ("AI engineer").

**Path (about 33 weeks at 2–3 hours/day):**

1. Brush-up — 2 weeks (statistics, advanced SQL)
2. Python for engineers — 3 weeks (OOP, Git, tests)
3. Core ML — 8 weeks → can start applying for data scientist roles
4. MLOps — 4 weeks → can start applying for ML engineer roles
5. Deep learning + NLP — 6 weeks (PyTorch, transformers)
6. GenAI — 6 weeks (LLMs, RAG, agents) → can start applying for GenAI / AI engineer roles
7. Portfolio + interviews — 4 weeks, then ongoing

**Portfolio ideas (banking / reconciliation domain, public or synthetic data only):** smart transaction matching, unusual-transaction detector, cash-flow forecast, production version of the matcher (FastAPI + Docker + CI/CD + MLflow), LLM bank-narration parser, RAG assistant over RBI circulars, exception-investigator agent.
