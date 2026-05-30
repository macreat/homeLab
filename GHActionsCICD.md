# GitHub Actions CI/CD: Guide for ANE Project {#ghActionsCICD}

## 1. Introduction to CI/CD in ANE
This guide establishes the strategic framework for implementing **Continuous Integration (CI)** and **Continuous Deployment (CD)** using GitHub Actions within the ANE (RF Monitoring API) ecosystem. 

By automating repetitive tasks, we eliminate human error during deployment, ensure that documentation is always synchronized with the code, and guarantee that new contributions meet our quality standards before merging.

### Why GH Actions for ANE?
- **Automated Docs:** Ensure `Doxygen` and `/docs` are always up-to-date with every push to `main`.
- **Schema Validation:** Automatically verify that CSV data follows the rules defined in `DICTIONARY.md`.
- **Code Integrity:** Run Python linting and unit tests on every Pull Request.
- **Security:** Manage API keys and server credentials safely via **GitHub Secrets**.

---

## 2. Core Concepts
A workflow consists of:

1.  **Workflows:** The top-level automated process (stored in `.github/workflows/*.yml`).
2.  **Events:** Triggers like `push`, `pull_request`, or `workflow_dispatch` (manual).
3.  **Jobs:** Groups of steps that run on the same runner (e.g., `ubuntu-latest`).
4.  **Steps:** Individual tasks (running a command or using an "Action").
5.  **Actions:** Reusable extensions (e.g., `actions/checkout@v4`).

---

## 3. Specific Use Cases for our Repository

### Use Case A: Automated Documentation Sync (CD)
**Scenario:** Every time a change is merged into `main`, we want the documentation in `/docs` to be regenerated and pushed so Vercel can reflect it.
- **Trigger:** `push` to `main`.
- **Key Action:** Run a Linux-equivalent of `generataedocs.ps1`.
- **Benefit:** The website is always in sync with the latest Markdown files without manual execution.

### Use Case B: Quality Assurance & Schema Check (CI)
**Scenario:** A contributor opens a PR with new data or code changes.
- **Trigger:** `pull_request` to `main`.
- **Key Action:** Run `pytest` and a custom `dictionary_validator.py`.
- **Benefit:** Prevents broken data or inconsistent naming (per `DICTIONARY.md`) from entering the master branch.

### Use Case C: Secure Deployment to Edge Nodes
**Scenario:** Deploying updated QA modules to the 10 distributed SDR sensors.
- **Trigger:** Release tag (e.g., `v1.0.0`).
- **Key Action:** Use `appleboy/ssh-action` to remote into nodes and pull changes.
- **Benefit:** Mass updates to physical sensors without manual SSH'ing into each one.

---

## 4. Proposed Workflow Structure (Conceptual)

### CI: Validation Workflow (`.github/workflows/ci-validation.yml`)
```yaml
name: ANE Quality Assurance

on:
  pull_request:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
          
      - name: Install dependencies
        run: pip install -r software/requirements.txt
        
      - name: Run Schema Validator
        run: python software/validators/schema.py --dict agentCLI/referenceDoc/collaborativeEnvironment/DICTIONARY.md
        
      - name: Run Tests
        run: pytest software/tests/
```

### CD: Documentation & Deployment (`.github/workflows/cd-deploy.yml`)
```yaml
name: ANE Deployment

on:
  push:
    branches: [ main ]

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Install Doxygen
        run: sudo apt-get install doxygen
        
      - name: Generate Docs
        run: |
          cd agentCLI
          doxygen coWorkEnv
          cp -r ../docs/doxygen/html/* ../docs/
          
      - name: Commit updated docs
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: "docs: auto-generate documentation [skip ci]"
          file_pattern: 'docs/*'
```

---

## 5. Local Testing with `act`
To avoid dozens of "test commits" to debug your YAML files, use **act**.
1. Install Docker on your machine.
2. Install `act` (via `brew`, `choco`, or direct download).
3. Run `act` in your project root:
   - `act pull_request`: Simulates a PR event.
   - `act -s GITHUB_TOKEN=...`: Run with secrets.

---

## 6. Security Best Practices
- **Never hardcode secrets:** Use `${{ secrets.MY_SECRET_NAME }}`.
- **Least Privilege:** Ensure the GITHUB_TOKEN has only the permissions needed (e.g., `contents: write`).
- **Environment Protection:** For production deployments, use GH Environments with "Required Reviewers".

---

## Next Steps for ANE Implementation
1.  **Refine Phase 2 Validators:** Ensure the Python scripts are ready to be called from a headless Linux environment.
2.  **Setup GH Secrets:** Add SSH keys and Vercel tokens to the repository settings.
3.  **Bootstrap `.github`:** Create the folder structure and start with the `ci-validation.yml`.

---
*Created as part of the agentCLI reference documentation.*
