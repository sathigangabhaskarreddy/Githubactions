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

# 🚀 **GitHub Actions Events

---

## ✅ **1. push**

**Simple words:** Runs when you push (upload) code to a branch.

**Syntax:**

```yaml
on:
  push:
    branches:
      - main
```

---

## ✅ **2. pull_request**

**Simple words:** Runs when someone opens or updates a pull request.

**Syntax:**

```yaml
on:
  pull_request:
    branches:
      - main
```

---

## ✅ **3. workflow_dispatch**

**Simple words:** You click a button to run it manually.

**Syntax:**

```yaml
on:
  workflow_dispatch:
```

---

## ✅ **4. schedule**

**Simple words:** Runs automatically at specific times (cron job).

**Syntax:**

```yaml
on:
  schedule:
    - cron: "0 1 * * *" # Runs every day at 1 AM
```

---

## ✅ **5. issues**

**Simple words:** Runs when an issue is opened, edited, or closed.

**Syntax:**

```yaml
on:
  issues:
    types: [opened, edited, closed]
```

---

## ✅ **6. release**

**Simple words:** Runs when you publish a new version.

**Syntax:**

```yaml
on:
  release:
    types: [published]
```

---

## ✅ **7. fork**

**Simple words:** Runs when someone makes a copy of your repo.

**Syntax:**

```yaml
on:
  fork:
```

---

## ✅ **8. create**

**Simple words:** Runs when a branch or tag is created.

**Syntax:**

```yaml
on:
  create:
```

---

## ✅ **9. delete**

**Simple words:** Runs when a branch or tag is deleted.

**Syntax:**

```yaml
on:
  delete:
```

---

## ✅ **10. pull_request_review**

**Simple words:** Runs when someone approves or comments on a PR.

**Syntax:**

```yaml
on:
  pull_request_review:
    types: [submitted]
```

---

## ✅ **11. workflow_run**

**Simple words:** Runs when another workflow finishes.

**Syntax:**

```yaml
on:
  workflow_run:
    workflows: ["Build"]
    types: [completed]
```

---

## ✅ **12. workflow_call**

**Simple words:** Workflow is called from another workflow (reusable workflow).

**Syntax:**

```yaml
on:
  workflow_call:
```

---

## ✅ **13. registry_package**

**Simple words:** Runs when a package is added, changed, or deleted.

**Syntax:**

```yaml
on:
  registry_package:
    types: [published]
```

---

## 🎉 **Summary Table**

| Event               | Simple Meaning             | Syntax                    |
| ------------------- | -------------------------- | ------------------------- |
| push                | Code pushed                | `on: push`                |
| pull_request        | PR opened/updated          | `on: pull_request`        |
| workflow_dispatch   | Manual run                 | `on: workflow_dispatch`   |
| schedule            | Runs on timer              | `on: schedule`            |
| issues              | Issue opened/updated       | `on: issues`              |
| release             | Release created            | `on: release`             |
| fork                | Repo forked                | `on: fork`                |
| create              | Branch/tag created         | `on: create`              |
| delete              | Branch/tag deleted         | `on: delete`              |
| pull_request_review | PR reviewed                | `on: pull_request_review` |
| workflow_run        | Workflow finished          | `on: workflow_run`        |
| workflow_call       | Called by another workflow | `on: workflow_call`       |
| registry_package    | Package published          | `on: registry_package`    |


