# Githubactions

**What is GITHB actions **
  GitHub Actions are packaged scripts to automate tasks in a software-development workflow in GitHub
  You can configure GitHub Actions to trigger complex workflows that meet your organization's needs.
  The trigger can happen each time developers check new source code into a specific branch, at timed intervals, or manually.

**Types of GitHub actions**
  1. Container Actions
  2. Javascript actions
  3. Composit actions

**Type	                Runs In	                        Best For	                          Example**
Container Action	    Docker container	              Full control of environment	        Python + ffmpeg job
JavaScript Action	    Node.js on GitHub runner	      Fast reusable logic	                Validate PR titles
Composite Action	    Shell steps on runner	          Combining multiple steps	          Setup + install + test

**GitHub Actions Workflow Architecture**
   → Workflow 
      → Jobs
        → Steps
            → Actions / Commands

**Workflows**
    1.Defined in **.github/workflows/*.yml**
    2.Triggers based on events
    (push, pull_request, schedule, manual, etc.)
    3.Can contain one or **multiple jobs**

    **Example: workflow.yml**
      name: CI Pipeline
      on: push
      jobs: ...
**Jobs**
    A job is a group of steps that run on the same machine (runner).
    Each job runs on a runner (Ubuntu, Windows, Mac)
    Jobs can run:
        in parallel (default)
        in sequence (using needs:)
    Example: jobs.yml
    jobs:
      build:
        runs-on: ubuntu-latest
      test:
        runs-on: ubuntu-latest
        needs: build
**Steps**
    Steps are individual tasks inside a job.
    Run in order (top to bottom)
    A step can:
      run a shell command (run:)
      use an action (uses:)
    Example: steps.yml
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
    
      - name: Install dependencies
        run: npm install
**Actions**
  Actions are reusable components used inside steps.
    1. Container Actions
    2. Javascript actions
    3. Composit actions
    Example:
      - uses: actions/setup-node@v4

**Runners**
    A runner is a machine that executes your job.
    GitHub provides:

      ubuntu-latest
      windows-latest
      macos-latest


    


  
