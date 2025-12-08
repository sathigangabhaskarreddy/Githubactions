# 🚀 GitHub Actions

## 📌 What are GitHub Actions?
GitHub Actions are **automated workflows** that help you build, test, and deploy your code directly inside GitHub.

They allow you to:
- Automate software development tasks  
- Trigger workflows when:
  - Code is pushed  
  - Pull requests are created  
  - On schedule  
  - Manually  
- Build complete CI/CD pipelines for your applications

---

## 📦 Types of GitHub Actions

### 1. **Container Actions**
- Run inside a **Docker container**
- Best for: custom environments, system dependencies  
- Example: Python + FFmpeg build job

### 2. **JavaScript Actions**
- Run directly on GitHub runners using Node.js  
- Best for: fast, reusable logic  
- Example: PR title validation

### 3. **Composite Actions**
- Combine multiple shell steps or existing actions  
- Best for: grouping repeated steps  
- Example: Setup → Install → Test pipeline

### 📋 Comparison Table

| Type              | Runs In             | Best For                       | Example                  |
|-------------------|---------------------|--------------------------------|--------------------------|
| Container Action  | Docker container    | Full control of environment    | Python + FFmpeg job      |
| JavaScript Action | Node.js runner      | Fast reusable logic            | PR title validation      |
| Composite Action  | Shell steps runner  | Combine multiple steps         | Setup → Install → Test   |

---

## 🏛️ GitHub Actions Workflow Architecture

```

Workflow
→ Jobs
→ Steps
→ Actions / Commands

````

---

## ⚙️ Workflows

- Located in **`.github/workflows/*.yml`**
- Triggered by:
  - push  
  - pull_request  
  - schedule  
  - manual dispatch  
- Can contain **one or multiple jobs**

### Example: `workflow.yml`

```yaml
name: CI Pipeline

on: push

jobs:
  build:
    runs-on: ubuntu-latest
````

---

## 🧩 Jobs

A **job** is a group of steps that run on the same runner.

Jobs can run:

* **In parallel** (default)
* **In sequence** using `needs:`

### Example: `jobs.yml`

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  test:
    runs-on: ubuntu-latest
    needs: build
```

---

## 🔧 Steps

Steps are **individual tasks** inside a job.

A step can:

* Run a shell command (`run:`)
* Use a GitHub action (`uses:`)

### Example: `steps.yml`

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v4

  - name: Install dependencies
    run: npm install
```

---

## 🧱 Actions

Actions are reusable components used inside steps.

### Types:

* Container Actions
* JavaScript Actions
* Composite Actions

### Example:

```yaml
- uses: actions/setup-node@v4
```

---

## 🖥️ Runners

A **runner** is a machine that executes your job.

GitHub provides:

* `ubuntu-latest`
* `windows-latest`
* `macos-latest`

You can also use **self-hosted runners** for custom environments.
