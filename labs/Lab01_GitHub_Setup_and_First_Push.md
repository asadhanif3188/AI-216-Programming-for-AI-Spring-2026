# Lab 01: GitHub Setup & First Push

**Week #1**  
**Topic:** Course Toolchain Setup: Git/GitHub + Repository Structure + README  

---

## 1. Objective

- Set up Git and GitHub for the course workflow.
- Create the official course repository with the required folder structure.
- Push a first Python script and a professional README to GitHub using meaningful commits.
- Understand why version control matters for AI programming (reproducibility, collaboration, traceability).

## 2. Background

- Git is a version control tool that tracks changes locally; GitHub hosts Git repositories online for backup and collaboration.
- Version control enables you to safely experiment, collaborate, and revert to prior working states—key habits for data/AI work where code and datasets evolve.

## 3. Tools & Libraries

- Python (installed)
- IDE (VS Code / PyCharm / any preferred editor)
- Git (installed)
- GitHub account

## 4. Tasks

### Task 1 — Install & configure tools

- Install Git (if not already installed).
- Configure Git identity (name + email) on your machine.
- Verify configuration output.

```bash
# Sets your name for all Git commits on your system
git config --global user.name "Your Name"
# Sets your email for all Git commits on your system
git config --global user.email "your.email@example.com"
# Verify
git config --global --list
```

### Task 2 — Create the official AI-216 course repository on GitHub

- On GitHub, create a new repository named: **AI-216-Programming-for-AI** (Public or Private as instructed).
- Do **NOT** initialize with README (you will add it locally).
- Create the required folder structure locally:

```bash
AI-216-Programming-for-AI/
├── labs/
│   └── week01/
├── assignments/
│   └── assignment01/   (create folder; content will come later)
├── project/
└── README.md
```

### Task 3 — Add your first Python script (Week 1)

- Inside `labs/week01/`, create a file named `hello_ai216.py`.
- Script requirements:
  - Prints your name and ID
  - Prints Python version (use `sys.version`)
  - Prints a short 2–3 line message: “What Programming for AI means to me”

```bash
# hello_ai216.py (minimum requirements)
# - print name + id
# - print python version
# - print 2–3 line reflection
```

### Task 4 — Initialize Git, commit, and push to GitHub (first push)

- Open terminal in `AI-216-Programming-for-AI/` and run the standard workflow: init → add → commit → remote → push.
- Use a meaningful commit message (example provided).

```bash
git init
git add .
git commit -m "Lab01: add course repo structure + week01 hello script"

# Add remote (replace <username>)
git remote add origin https://github.com/<username>/AI-216-Programming-for-AI.git
git branch -M main
git push -u origin main
```

### Task 5 — Add a Python/VS Code `.gitignore` (required)

- Create a `.gitignore` in the repository root (same level as `README.md`).
- Include common ignores for:
  - Python cache (`__pycache__/`, `*.pyc`)
  - Virtual environments (`.venv/`, `venv/`)
  - Jupyter checkpoints (`.ipynb_checkpoints/`)
  - VS Code (`.vscode/`)
- Commit and push this as a **separate commit**.

```bash
git add .gitignore
git commit -m "Lab01: add Python/VS Code gitignore"
git push
```

### Task 6 — Branch workflow: improve README and merge (required)

- Create a new branch named: `week01-readme-improve`
- Edit **only** `labs/week01/README.md` to improve clarity (e.g., add better structure, clearer learning bullets, AI/ML relevance).
- Commit on the branch, then merge back into `main`, and push.

```bash
git checkout -b week01-readme-improve
# edit labs/week01/README.md
git add labs/week01/README.md
git commit -m "Lab01: improve week01 README"
git checkout main
git merge week01-readme-improve
git push
```

### Task 7 — Second commit: improve script formatting + docstring (required)

- Update `labs/week01/hello_ai216.py`:
  - Add a module-level docstring (1–3 lines).
  - Improve output formatting (clean labels, consistent spacing, readable lines).
- Commit and push this as a **separate commit** (different from the `.gitignore` and README commits).

```bash
git add labs/week01/hello_ai216.py
git commit -m "Lab01: improve hello script formatting + docstring"
git push
```

### Task 8 — Write a professional README for the Week 1 folder

- Ensure `labs/week01/README.md` includes:
  - Brief description of what you did
  - Key Git commands used
  - What you learned (3 bullets)
  - How this supports AI/ML workflows (reproducibility + collaboration)

```md
# Lab 01 – GitHub Setup & First Push

## What this lab does
...

## Key commands used
- git init
- git add .
- git commit -m "..."
- git push
- git checkout -b ...
- git merge ...

## What I learned
- ...
- ...
- ...

## AI/ML relevance
...
```

## 5. GitHub Submission Checklist

- Repository name matches the course standard.
- Folder structure exists: `labs/week01`, `assignments/assignment01`, `project`.
- `labs/week01/hello_ai216.py` exists and runs.
- `labs/week01/README.md` exists and is meaningful.
- A root-level `.gitignore` exists (Python + VS Code appropriate).
- Branch `week01-readme-improve` was created and merged back to `main`.
- There are **at least 3 meaningful commits** (example: initial push, `.gitignore`, README improvement merge, script improvement).
- All work is pushed to GitHub (verify by opening the repo in a browser).

## 6. LinkedIn Reflection (If Required)

- Post a short 3–5 line reflection (or submit written reflection if you prefer not to post publicly):
- What you learned (Git/GitHub habit).
- How it relates to AI/ML workflows (reproducibility, collaboration).
- One challenge you faced and how you solved it.

## 7. Expected Learning Outcomes

- Configure Git and perform basic repository operations (init, add, commit, push).
- Create and maintain the required course repository structure.
- Use `.gitignore` to avoid committing unnecessary files.
- Use a feature-branch workflow (create branch, commit, merge).
- Document work using a professional README.
- Explain how version control supports AI programming workflows (reproducibility, collaboration, traceability).

<!-- ## 8. Evaluation Criteria

| Component | Weight |
|---|---:|
| Task completion (all required files + structure + `.gitignore`) | 40% |
| Correct GitHub usage (commits, push, branch + merge; meaningful messages) | 30% |
| Documentation quality (README clarity + completeness) | 20% |
| Reflection (LinkedIn or written alternative) | 10% | -->
