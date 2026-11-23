# Notes - GitHub Actions

Complete course notes: CI/CD basics, workflows, runners, triggers, secrets, caching, matrix builds, artifacts, deployments, Docker, AWS OIDC, self-hosted runners, best practices and debugging.

## Table of Contents
1. [What is CI/CD](#1-what-is-cicd)
2. [What is GitHub Actions](#2-what-is-github-actions)
3. [How GitHub Actions works](#3-how-github-actions-works)
4. [Workflow, Jobs, and Steps](#4-workflow-jobs-and-steps)
5. [Runners (GitHub-hosted vs self-hosted)](#5-runners-github-hosted-vs-self-hosted)
6. [Events & Triggers (push, pull_request, workflow_dispatch)](#6-events--triggers-push-pull_request-workflow_dispatch)
7. [YAML workflow file structure](#7-yaml-workflow-file-structure)
8. [Using Actions from Marketplace](#8-using-actions-from-marketplace)
9. [Secrets & environment variables](#9-secrets--environment-variables)
10. [Caching dependencies](#10-caching-dependencies)
11. [Matrix builds](#11-matrix-builds)
12. [Artifacts](#12-artifacts)
13. [Deploying applications using GitHub Actions](#13-deploying-applications-using-github-actions)
14. [Integrating with Docker](#14-integrating-with-docker)
15. [Integrating with cloud (AWS example, high-level)](#15-integrating-with-cloud-aws-example-high-level)
16. [Self-hosted runners (concept)](#16-self-hosted-runners-concept)
17. [Best practices for production workflows](#17-best-practices-for-production-workflows)
18. [Debugging GitHub Actions workflows](#18-debugging-github-actions-workflows)

---

## 1. What is CI/CD

### Simple Explanation
Continuous Integration (CI) and Continuous Delivery/Deployment (CD) form the backbone of modern software development. Think of it like an assembly line in a factory. CI is the automated quality check station that inspects every new part (code change) as it is added to the product. CD is the delivery truck that automatically takes the finished, tested product and delivers it to the customer (production environment).

### Why This Matters in DevOps
In the real world, developers push code multiple times a day. Manual testing and manual server uploads are slow and error-prone. CI/CD automates the software delivery process, enabling teams to deliver changes frequently and reliably, reducing deployment risk, and catching bugs early.

### Key Concepts
- **Continuous Integration (CI):** Automatically integrating code changes from multiple contributors into a shared repository, verified by automated builds and tests.
- **Continuous Delivery (CD):** Automating the delivery of applications to selected environments (like staging), ensuring code can be reliably released at any time.
- **Continuous Deployment:** Automating the deployment of every change that passes tests directly to production without human intervention.

### Visual / Workflow Explanation
Modern DevOps workflow (CI/CD pipeline):

```
Developer commits code  →  Trigger CI pipeline  →  Build application      →  Run automated tests          →  Deployment stage         →  Live application
(changes made & saved)     (commit & push)         (compilation/assembly)    (unit, integration, linting)    (release management)        (on cloud infrastructure)
                           └──────────────── CI ───────────────────────────────────────────┘             └──────────── CD ────────────┘
```

### Real-World Example
A web developer finishes a new feature and pushes the code to the main branch. The CI/CD system automatically runs unit tests. Because the tests pass, the system packages the app into a Docker container and deploys it to AWS, making the feature live in minutes.

### Common Beginner Mistakes
- **Mistake:** Thinking CI and CD are the exact same thing.
  **Correction:** CI is about testing and merging code; CD is about releasing and deploying that code to environments.
- **Mistake:** Automating bad processes.
  **Correction:** CI/CD relies on good automated tests; without them, you are just deploying broken code faster.

### Quick Revision Summary
- CI automates code integration and testing.
- CD automates delivery and deployment to environments.
- Reduces bugs and deployment risks.
- Accelerates time-to-market.

---

## 2. What is GitHub Actions

### Simple Explanation
GitHub Actions is a built-in automation tool provided directly inside GitHub. Imagine having a robot assistant living inside your code repository. Whenever you do something (like saving new code), the robot wakes up and follows a to-do list you gave it, like testing the code, sending a Slack message, or publishing a website.

### Why This Matters in DevOps
Traditionally, teams had to set up external CI/CD servers (like Jenkins) to monitor their GitHub repositories. GitHub Actions eliminates this overhead by offering a fully managed continuous integration and continuous delivery (CI/CD) platform directly where the code lives.

### Key Concepts
- **Automation Platform:** It is not just for CI/CD; it can automate almost any repository event (like labeling issues or greeting new contributors).
- **Native Integration:** It is deeply integrated with the GitHub ecosystem, offering a streamlined developer experience.
- **Hosted Infrastructure:** GitHub provides the servers (virtual machines) to run your automation tasks.

### Visual / Workflow Explanation
Automated CI/CD workflow with GitHub Actions:

```
1. GitHub repository event (e.g. Pull Request opened)
2. GitHub Actions detects the event and orchestrates the workflow
3. Provisions a temporary runner server (dynamic, on-demand, ephemeral)
4. Runs automation tasks: Build, Test, Security Scan, Deploy (optional)
5. Reports status back to the Pull Request UI (success or failure outcome)
```

### Real-World Example
An open-source maintainer receives dozens of bug reports daily. They use GitHub Actions to automatically add an "untriaged" label to newly opened issues, and run a security scan whenever someone submits a Pull Request.

### Common Beginner Mistakes
- **Mistake:** Assuming GitHub Actions is only for building and deploying software.
  **Correction:** It is a general-purpose automation tool. You can use it to manage repository chores, automate project management, and handle releases.

### Quick Revision Summary
- Built directly into GitHub.
- Automates CI/CD and repository workflows.
- Removes the need for external CI servers.
- Provides managed execution environments (runners).

---

## 3. How GitHub Actions works

### Simple Explanation
GitHub Actions works on an "Event-Driven" model. Simply put, it means: "When X happens, do Y." You define the X (the trigger) and the Y (the reaction). GitHub acts as the listener, waiting for your specified event, and then spins up the necessary resources to execute your instructions.

### Why This Matters in DevOps
DevOps relies on reacting to code changes instantly. By being event-driven, GitHub Actions ensures pipelines run the millisecond a developer pushes code, maintaining a seamless, continuous feedback loop.

### Key Concepts
- **Event-Driven:** Workflows initiate based on specific triggers (events).
- **Ephemeral Environments:** Every time a workflow runs, GitHub provisions a fresh, temporary virtual machine. Once the task is done, the machine is destroyed, ensuring a clean slate every time.
- **Platform Control Plane:** GitHub handles the complex orchestration, queuing, and scheduling of your jobs in the background.

### Visual / Workflow Explanation: GitHub Actions (Code Push)
```
1. Event (code push)
2. GitHub searches .github/workflows
3. GitHub provisions a fresh VM (runner), spun up in a data center (ephemeral runner)
4. VM executes YAML instructions step-by-step
5. VM is destroyed
6. Logs are displayed in GitHub
```

### YAML Example
```yaml
# A simple representation of "When X, do Y"
on: push        # This is the 'X' (Event)

jobs:
  say_hello:    # This is the 'Y' (Action)
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello World!"
```
- `on: push`: The listener waiting for a code push.
- `runs-on`: Tells GitHub which machine to spin up.
- `run`: The actual command executed on the machine.

### Real-World Example
When a developer pushes code to the `main` branch (Event), GitHub Actions spins up an Ubuntu server (Runner), installs Node.js, runs `npm test` (Execution), and reports if the code is healthy.

### Common Beginner Mistakes
- **Mistake:** Thinking background jobs run on the developer's local machine.
  **Correction:** The jobs execute on GitHub's remote cloud servers (or your own dedicated servers), completely isolated from your laptop.

### Quick Revision Summary
- Operates on an event-driven architecture.
- Workflows live in the `.github/workflows` directory.
- Executes tasks on fresh, ephemeral virtual machines.
- Handles orchestration and queuing automatically.

---

## 4. Workflow, Jobs, and Steps

### Simple Explanation
To build an automation pipeline, GitHub Actions uses a specific hierarchy, like a nesting doll. Think of a recipe book:
- The **Workflow** is the entire recipe book.
- A **Job** is a specific recipe in the book (like "Bake a Cake").
- A **Step** is a single instruction in that recipe (like "Add 2 eggs").
- An **Action** is a pre-packaged tool you can use in a step (like using a store-bought cake mix instead of making it from scratch).

### Why This Matters in DevOps
Structuring pipelines into Workflows, Jobs, and Steps allows DevOps engineers to build complex, highly parallel, and modular pipelines. It keeps automation organized and easy to debug.

### Key Concepts
- **Workflow:** The top-level automated process defined in a YAML file. Contains one or more jobs.
- **Job:** A set of steps executed on the *same* runner. By default, multiple jobs run in parallel unless you tell them to wait for each other.
- **Step:** An individual task within a job. Steps run sequentially (one after another). Because they share the same runner, they can share data via the local file system.
- **Action:** A reusable, standalone unit of code that performs a specific task within a step.

### Visual / Workflow Explanation
Workflow "Release Application":
```
Workflow: Release Application
├── Job 1: build-frontend  (parallel)
│     ├── Step 1: Download code
│     └── Step 2: Run npm run build
└── Job 2: build-backend   (parallel)
      ├── Step 1: Download code
      └── Step 2: Run go build
```

### YAML Example
```yaml
name: Example Workflow
on: push
jobs:
  my_job:                       # This is the Job
    runs-on: ubuntu-latest
    steps:                      # These are the Steps
      - name: Check out code    # Step 1
        uses: actions/checkout@v4   # This is an Action

      - name: Run a script      # Step 2
        run: echo "Code has been downloaded!"   # This is a shell command
```
- `jobs`: defines the grouping of tasks.
- `steps`: lists the sequential tasks.
- `uses`: calls a pre-built Action.
- `run`: executes a standard command-line script.

### Real-World Example
A workflow contains a "Test" job and a "Deploy" job. The "Test" job has steps to install dependencies and run unit tests. The "Deploy" job is configured to only start if the "Test" job succeeds, ensuring broken code is never deployed.

### Common Beginner Mistakes
- **Mistake:** Assuming steps in *different* jobs can share files easily.
  **Correction:** Different jobs run on entirely different virtual machines. To share files between jobs, you must upload and download "Artifacts".
- **Mistake:** Thinking steps run in parallel.
  **Correction:** Jobs run in parallel; steps always run sequentially.

### Quick Revision Summary
- **Workflow:** The overall YAML configuration.
- **Job:** A grouping of steps that run on a single machine.
- **Step:** A sequential command or Action within a job.
- Jobs run in parallel by default; steps run sequentially.

---

## 5. Runners (GitHub-hosted vs self-hosted)

### Simple Explanation
A "Runner" is simply the server (the actual computer) that executes your workflow instructions.
- **GitHub-hosted runners** are computers owned, managed, and maintained by GitHub. You rent them by the minute.
- **Self-hosted runners** are your own computers (like a server in your basement or a VM in your AWS account) that you connect to GitHub to process your jobs.

### Why This Matters in DevOps
Choosing the right compute infrastructure affects pipeline speed, security, and cost. Cloud-native apps often use GitHub-hosted runners for simplicity, while enterprise apps behind strict firewalls use self-hosted runners for security and hardware access.

### Key Concepts
- **GitHub-hosted Runners:** Fully managed VMs (Ubuntu, Windows, macOS). They are ephemeral (destroyed after one job) and require zero maintenance.
- **Larger Runners:** A premium tier of GitHub-hosted VMs with more CPU, RAM, and static IPs.
- **Self-hosted Runners:** Custom infrastructure you manage. They offer complete control over the OS, hardware (like GPUs), and network. They are persistent, meaning files can remain between jobs unless cleaned up.

### Visual / Workflow Explanation
```
GitHub-hosted runner workflow:
GitHub queue → job assigned → fresh Ubuntu VM provisioned (ephemeral) → YAML instructions
→ VM runs job (executes your job/workflow steps) → job completed → VM is immediately destroyed

Self-hosted runner workflow:
GitHub queue → signals runner → custom server/VM (runs locally)
→ runs job (server executes the job locally) → ready → waits (remains active, waiting for next job)
```

### YAML Example
```yaml
jobs:
  hosted_job:
    runs-on: ubuntu-latest      # Uses a standard GitHub-managed Linux VM

  custom_job:
    runs-on: [self-hosted, linux, x64, gpu]   # Routes to your custom server matching these labels
```
- `ubuntu-latest`: Requests GitHub's standard runner.
- `self-hosted`: Instructs GitHub to route the job to your private infrastructure based on labels.

### Real-World Example
A game development studio uses GitHub-hosted Linux runners for quick unit tests, but routes their final heavy 3D rendering jobs to a self-hosted runner that has a powerful physical GPU installed.

### Common Beginner Mistakes
- **Mistake:** Leaving sensitive files on a self-hosted runner.
  **Correction:** Self-hosted runners do not automatically wipe themselves clean after a job. You must manage cleanup to prevent security risks and state pollution.

### Quick Revision Summary
- **Runner:** The VM/server that executes a job.
- **GitHub-hosted:** Managed, ephemeral, zero-maintenance, billed per minute.
- **Self-hosted:** Custom hardware, persistent, runs inside your private network.
- Target runners using the `runs-on` keyword.

---

## 6. Events & Triggers (push, pull_request, workflow_dispatch)

### Simple Explanation
Events and Triggers are the "start buttons" for your workflows. Just as a motion sensor turns on a porch light, an event (like opening a Pull Request) tells GitHub Actions to turn on your workflow.

### Why This Matters in DevOps
DevOps relies on executing the right automation at the right time. You want tests to run when code is proposed, deployments to run when code is merged, and maintenance scripts to run on a nightly schedule.

### Key Concepts
- **`push`:** Triggers when someone pushes commits to a repository branch or tag.
- **`pull_request`:** Triggers when a PR is opened, synchronized (updated), or reopened.
- **`workflow_dispatch`:** Allows you to manually trigger a workflow via the GitHub UI or API. You can even define custom input fields for the manual run.
- **`schedule`:** Triggers at specific times using cron syntax.

### Visual / Workflow Explanation: Pull Request Trigger
```
1. Developer creates PR
2. GitHub detects the `pull_request` event
3. GitHub matches the event to the YAML `on:` block
4. Workflow begins execution: Setup Job → Build App → Run Tests → Lint Code → Deploy (Staging)
```

### YAML Example: Multi-Trigger Workflow
```yaml
name: Multi-Trigger Workflow

on:
  push:
    branches: ["main"]            # Runs when code is pushed to main

  pull_request:
    branches: ["main"]            # Runs when a PR targets main

  workflow_dispatch:
    inputs:                       # Adds a manual button with a user input field
      environment:
        description: 'Target environment'
        required: true
        default: 'staging'
```
- `on:` is the trigger block.
- Branch filters restrict the workflow to only care about the `main` branch.
- `inputs:` defines variables users provide when clicking the manual trigger button.

### Real-World Example
A team configures their testing workflow to trigger automatically on `pull_request` to ensure code quality. They also include a `workflow_dispatch` trigger so QA engineers can manually re-run the tests by clicking a button in the GitHub interface without writing code.

### Common Beginner Mistakes
- **Mistake:** Thinking `push` and `pull_request` triggers will run twice on the same commit if not configured properly.
  **Correction:** If you open a PR and push to it, and your YAML has both triggers without branch filters, it will trigger two duplicate pipeline runs. Use branch filters to control this.

### Quick Revision Summary
- `on:` keyword defines triggers.
- `push` runs on direct repository updates.
- `pull_request` runs on PR lifecycle events.
- `workflow_dispatch` enables manual button clicks with inputs.

---

## 7. YAML workflow file structure

### Simple Explanation
YAML (YAML Ain't Markup Language) is a human-readable data format. In GitHub Actions, you use YAML to write the configuration file that defines your workflow. It uses strict indentation (spaces, not tabs) to represent the hierarchy of your pipeline.

### Why This Matters in DevOps
Modern CI/CD relies on "Configuration as Code." By defining pipelines in YAML and storing them alongside the application code, the pipeline itself is version-controlled, auditable, and collaborative.

### Key Concepts
- **`.github/workflows/`:** The strict directory path where all YAML workflow files must reside.
- **`name:`** The display name of the workflow in the GitHub UI.
- **`on:`** The trigger conditions.
- **`jobs:`** The container for all the tasks.
- **`runs-on:`** The designated runner for a job.
- **`steps:`** The sequence of commands or actions.

### Visual / Workflow Explanation: Directory Structure
```
my-project/
├── src/
├── package.json
└── .github/                 ← GitHub only looks here for workflow configuration (e.g. CI/CD pipelines)
    └── workflows/
        └── ci-pipeline.yml  → 1. Trigger (e.g. push to main) → 2. Build application → 3. Run tests → 4. Deploy (optional)
```

### YAML Example
```yaml
name: Basic CI Pipeline        # Top level: Name
on: push                       # Top level: Trigger
jobs:                          # Top level: Jobs block
  build:                       # Job ID
    runs-on: ubuntu-latest     # Runner configuration
    steps:                     # Steps block
      - name: Check out repo
        uses: actions/checkout@v4

      - name: Run greeting
        run: echo "Hello, YAML!"
```
Notice the indentation: `jobs` contains `build`, which contains `runs-on` and `steps`.

### Real-World Example
A team creates a file named `deploy-prod.yml` in their `.github/workflows` folder. Because it lives in the code repository, when a developer modifies the deployment process, the changes are reviewed in a Pull Request just like regular application code.

### Common Beginner Mistakes
- **Mistake:** Using tabs instead of spaces for indentation.
  **Correction:** YAML strictly requires spaces. A single misplaced tab will break the entire workflow file.
- **Mistake:** Placing the YAML file in the root directory.
  **Correction:** GitHub will completely ignore it unless it is inside the exact `.github/workflows/` folder.

### Quick Revision Summary
- Written in YAML format.
- Must be located in `.github/workflows/`.
- Represents Configuration as Code.
- Relies heavily on proper space-based indentation.

---

## 8. Using Actions from Marketplace

### Simple Explanation
The GitHub Marketplace is like an App Store for your CI/CD pipelines. Instead of writing complex bash scripts to install software, log into cloud providers, or send Slack notifications, you can just "download" pre-written instructions (Actions) created by GitHub or the community.

### Why This Matters in DevOps
Reusability accelerates development. Utilizing Marketplace Actions prevents DevOps engineers from reinventing the wheel, ensuring workflows remain clean, short, and maintainable.

### Key Concepts
- **`uses:` Keyword:** The YAML keyword used to call an action from a step.
- **Action Versioning:** Actions are referenced with a version tag (like `@v3`) or branch (like `@main`) to prevent breaking changes if the author updates the action.
- **`with:` Keyword:** Used to pass input variables/arguments to an action.

### Visual / Workflow Explanation: How `actions/setup-node` Works
```
1. Your step (YAML definition)
2. GitHub downloads the action from the Marketplace
3. The action executes complex background logic (downloads and installs Node.js)
4. Your workflow continues (Node.js environment ready)
```

### YAML Example
```yaml
steps:
  - name: Checkout Code
    uses: actions/checkout@v4        # Essential action to pull your git repository to the runner

  - name: Setup Node.js
    uses: actions/setup-node@v4      # Downloads and installs Node.js
    with:
      node-version: '20'             # Passes an input variable to the action
```
- `actions/checkout@v4`: The standard action required in almost every workflow to download your source code.
- `with:` provides the configuration parameters the action expects.

### Real-World Example
Instead of writing a 50-line shell script to configure AWS credentials safely, a developer simply uses `aws-actions/configure-aws-credentials@v4` from the Marketplace, reducing the setup to just 4 lines of YAML.

### Common Beginner Mistakes
- **Mistake:** Forgetting to use `actions/checkout`.
  **Correction:** A runner starts completely empty. If you don't use the checkout action, your code will not be on the machine, and your build will fail instantly.
- **Mistake:** Binding to the `@main` or `@master` branch of a third-party action.
  **Correction:** Always bind to a specific version tag (like `@v2`) for stability. If the creator pushes a breaking change to their main branch, your pipeline will unexpectedly break.

### Quick Revision Summary
- Pre-built scripts available in the GitHub Marketplace.
- Called using the `uses:` syntax.
- Inputs are passed using the `with:` syntax.
- Always pin actions to specific version tags for stability.

---

## 9. Secrets & environment variables

### Simple Explanation
Workflows often need passwords, API keys, or specific configurations (like deploying to a database). **Secrets** are hidden, encrypted passwords. **Environment Variables** are unhidden configuration settings. GitHub allows you to store both securely and inject them into your workflow.

### Why This Matters in DevOps
Hardcoding passwords directly into your codebase is a massive security risk. GitHub Secrets ensure that sensitive data is encrypted, masked in logs, and only exposed to the runner at the exact moment it is needed.

### Key Concepts
- **Repository / Organization Secrets:** Encrypted variables managed in the GitHub settings UI.
- **Environment Secrets:** Secrets tied to specific deployment targets (e.g., "Production") that can require manual approval to access.
- **Automatic Masking:** If a secret is accidentally printed to the console log during a run, GitHub automatically redacts it (e.g., `***`).
- **`env` Context:** Used to define and access non-sensitive variables.
- **`secrets` Context:** Used to access encrypted secrets.

### Visual / Workflow Explanation: Secure DB Password in GitHub Actions
```
1. Store the database password in GitHub UI (Repository Settings → Secrets > Actions)
2. A defined event ("push" or "pull_request") triggers the workflow
3. The workflow configuration uses the secret syntax: YAML requests ${{ secrets.DB_PASSWORD }}
4. GitHub decrypts the secret and injects it into the runner
5. The code on the runner uses the password to connect to the database server
6. Logs print *** if the password is outputted (GitHub replaces the password with *** to mask it)
```

### YAML Example
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      APP_PORT: 8080                                     # Standard environment variable
    steps:
      - name: Deploy App
        env:
          DB_PASS: ${{ secrets.PROD_DB_PASSWORD }}       # Pulling a secret securely
        run: |
          echo "Deploying on port $APP_PORT"
          ./deploy.sh --password $DB_PASS
```
- `env:` defines variables at the job or step level.
- `${{ secrets.PROD_DB_PASSWORD }}` extracts the secure value.

### Real-World Example
A deployment workflow needs an API token to publish an app to a cloud server. The token is saved in GitHub Repository Secrets. The workflow passes it securely into the deployment script. If an intern accidentally types `echo $API_TOKEN` in the script, GitHub masks it in the public logs to prevent exposure.

### Common Beginner Mistakes
- **Mistake:** Passing secrets to command-line arguments where they might be logged by underlying tools.
  **Correction:** It is safer to pass secrets as Environment Variables to your scripts (as shown in the YAML example) rather than command-line text arguments.

### Quick Revision Summary
- Secrets are encrypted and stored in the GitHub UI.
- Secrets are referenced using `${{ secrets.SECRET_NAME }}`.
- GitHub automatically masks secrets in workflow logs.
- Environment variables (`env`) are used for non-sensitive configuration.

---

## 10. Caching dependencies

### Simple Explanation
When building software, the system often has to download thousands of dependency files (like NPM packages) from the internet. Doing this from scratch every time takes minutes. **Caching** allows the workflow to save those downloaded files on GitHub's servers. Next time the workflow runs, it just grabs the saved files, acting as a high-speed shortcut.

### Why This Matters in DevOps
Time is money. CI/CD pipelines run dozens of times a day. If dependency installation takes 3 minutes, caching can reduce it to 30 seconds. This optimizes performance, provides faster feedback to developers, and lowers cloud compute bills.

### Key Concepts
- **`actions/cache`:** The official Marketplace action used to save and restore cache data.
- **Cache Key:** A unique string identifier. If the key matches an existing cache, it restores it (Cache Hit). If not, it runs the install and saves a new cache (Cache Miss).
- **Hash Files:** Caches are usually keyed to a lockfile (like `package-lock.json`). If the lockfile changes, the hash changes, generating a new cache key and forcing a fresh installation.

### Visual / Workflow Explanation: NPM Caching Workflow (Run 1 vs Run 2)
```
RUN 1: CACHE MISS (the "long way")
  Start workflow & check cache → empty cache (MISS)
  → download NPM packages (est. ~3 mins) → save packages to cache (cache updated)
  → Build complete. Total time: ~3-10 mins

RUN 2: CACHE HIT (the "fast way")
  Start workflow & check cache → cache found (HIT)
  → restore packages from cache (~10 secs) → SKIP download step
  → Build complete. Total time: ~10 secs
```

### YAML Example
```yaml
steps:
  - uses: actions/checkout@v4

  - name: Cache node modules
    uses: actions/cache@v4
    id: cache-npm
    with:
      path: node_modules
      # The key generates a unique string based on the OS and the lockfile
      key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}

  - name: Install dependencies
    if: steps.cache-npm.outputs.cache-hit != 'true'   # Only run if cache missed
    run: npm ci
```
- `path:` The folder to save (e.g., `node_modules`).
- `key:` Uses `hashFiles` to track changes.
- `if:` Condition prevents re-installing if the cache was successfully restored.

### Real-World Example
A team using a massive JavaScript "monorepo" notices their CI takes 10 minutes, with 4 minutes just downloading dependencies. Implementing the cache action drops dependency installation to 20 seconds, drastically speeding up their development loop.

### Common Beginner Mistakes
- **Mistake:** Caching the wrong directories or making the cache key too generic (like just `key: my-cache`).
  **Correction:** Always incorporate the hash of your dependency lockfile in the key (`hashFiles('package-lock.json')`). This guarantees the cache invalidates and updates when you add new dependencies.

### Quick Revision Summary
- Caching saves downloaded dependencies between runs.
- Implemented using the `actions/cache` action.
- Relies on unique `key`s (usually hashed lockfiles).
- Significantly reduces build times and compute costs.

---

## 11. Matrix builds

### Simple Explanation
Imagine you wrote a program and need to test it on Linux, Windows, and macOS, using three different versions of Python. Instead of copying and pasting your job 9 times, a **Matrix** allows you to define the job once and provide a list of variables. GitHub Actions will automatically multiply the job and run all combinations simultaneously.

### Why This Matters in DevOps
Software must run reliably across different environments. Matrix builds improve continuous integration coverage by testing multiple configurations in parallel. Because they run simultaneously, you get extensive testing without increasing the total workflow time.

### Key Concepts
- **`strategy: matrix:`** The YAML block where you define the arrays of variables.
- **Parallel Execution:** GitHub spawns a separate runner for every combination in the matrix simultaneously.
- **Fail-fast:** By default, if one job in the matrix fails, GitHub instantly cancels all other running matrix jobs to save resources.

### Visual / Workflow Explanation: Automatic Parallel Job Expansion
```
Define matrix:  os: [ubuntu, windows]   node: [18, 20]

→ Parallel Job 1: Ubuntu  + Node 18
→ Parallel Job 2: Ubuntu  + Node 20
→ Parallel Job 3: Windows + Node 18
→ Parallel Job 4: Windows + Node 20
   (each on its own VM, all running at the same time)
```

### YAML Example
```yaml
jobs:
  test:
    runs-on: ${{ matrix.os }}            # Dynamically injects the OS
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]
        node-version: [18, 20]
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}   # Dynamically injects the Node version

      - run: npm test
```
- `${{ matrix.os }}`: Pulls the current value from the matrix context.

### Real-World Example
An open-source library developer wants to ensure their code works for all users. They use a matrix build to test their library against Python 3.9, 3.10, and 3.11 across Mac, Linux, and Windows, generating 9 parallel test runs on every Pull Request.

### Common Beginner Mistakes
- **Mistake:** Unintentionally running hundreds of jobs by adding too many variables to the matrix arrays, burning through billing minutes.
  **Correction:** Optimize combinations. Use the `exclude` keyword in the matrix to omit combinations that don't make sense or aren't supported.

### Quick Revision Summary
- Matrix strategies run tests across multiple configurations automatically.
- Defined under `strategy: matrix:`.
- Variables are accessed using `${{ matrix.variable_name }}`.
- Jobs execute in parallel, reducing overall wait times.

---

## 12. Artifacts

### Simple Explanation
When a GitHub Actions runner finishes its job, the virtual machine is destroyed. Any files created during that job (like a compiled app, a PDF report, or log files) are deleted forever. **Artifacts** are the mechanism to upload and save these files before the machine shuts down, so you can download them later or pass them to another job.

### Why This Matters in DevOps
In a CI/CD pipeline, the "Build" job compiles the code, and the "Deploy" job uploads it to the server. Because these are separate jobs running on different machines, you must use Artifacts to pass the compiled code from the Build job to the Deploy job.

### Key Concepts
- **`actions/upload-artifact`:** Action used to save files to GitHub's storage.
- **`actions/download-artifact`:** Action used to retrieve saved files in a subsequent job.
- **Retention Period:** Artifacts are not stored forever; they have a retention limit (default is 90 days) and consume account storage quotas.

### Visual / Workflow Explanation: CI/CD Artifact Transfer
```
Job 1 (Build) - compiles code on BUILD VM
  → creates .zip file (ci_artifact.zip)
  → Job 1 uploads .zip as an artifact to Artifact Storage
  → Job 1 VM is destroyed

Job 2 (Deploy) - starts on a new VM (DEPLOY VM)
  → Job 2 downloads the .zip artifact
  → Job 2 deploys code to the server (unzipping & deploying to the cloud platform / production server)
```

### YAML Example
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "compiled binary" > my-app.bin

      - name: Upload Artifact
        uses: actions/upload-artifact@v4
        with:
          name: application-binary    # Name of the artifact
          path: my-app.bin            # File to upload

  deploy:
    needs: build                      # Tells Deploy job to wait for Build job to finish
    runs-on: ubuntu-latest
    steps:
      - name: Download Artifact
        uses: actions/download-artifact@v4
        with:
          name: application-binary    # Must match the upload name

      - run: cat my-app.bin
```

### Real-World Example
A mobile app developer uses a macOS runner to compile an iOS `.ipa` file. The workflow uploads the `.ipa` file as an artifact. Once the workflow finishes, the QA team navigates to the GitHub Actions UI, clicks on the artifact, and downloads the app to test on their phones.

### Common Beginner Mistakes
- **Mistake:** Using Caching instead of Artifacts to pass data between jobs.
  **Correction:** Caching is for speeding up future workflow runs (like saving dependencies). Artifacts are for saving the output results of a build or passing data *between jobs* in the same run.

### Quick Revision Summary
- Artifacts preserve files after the runner VM is destroyed.
- Use `upload-artifact` to save data.
- Use `download-artifact` to retrieve data in downstream jobs.
- They consume storage billing and have expiration dates.

---

## 13. Deploying applications using GitHub Actions

### Simple Explanation
After code is tested and built, it needs to be sent to a live server so users can interact with it. This process is called deployment. GitHub Actions automates this final step, securely taking your compiled application and transferring it to cloud providers like AWS, Azure, or generic web servers.

### Why This Matters in DevOps
Automated deployment (Continuous Deployment) eliminates the manual "drag-and-drop" release process. It ensures that deployments are highly repeatable and less prone to human error, and can happen rapidly multiple times a day.

### Key Concepts
- **Environments:** GitHub allows you to define environments (e.g., `production`, `staging`). Jobs can be tied to these environments.
- **Environment Protection Rules:** You can configure rules requiring a human to click "Approve" before a deployment job targeting `production` is allowed to execute.
- **Deployment Actions:** The Marketplace contains hundreds of vendor-specific actions (e.g., Azure Login, AWS ECS Deploy) that handle the heavy lifting of cloud deployments.

### Visual / Workflow Explanation: CI/CD Pipeline with Human Approval Gate
```
1. Developer merges code to main branch
2. CI build & test job succeeds
3. Workflow pauses for human approval (environment gate) - Manager approves
4. CD deploy job authenticates with the cloud provider (secure authentication)
5. CD pushes new code to the live server
```

### YAML Example
```yaml
jobs:
  deploy_prod:
    runs-on: ubuntu-latest
    environment: production     # Triggers environment protection rules/approvals
    steps:
      - uses: actions/checkout@v4

      - name: Deploy to Server
        env:
          API_KEY: ${{ secrets.PROD_API_KEY }}
        run: ./deploy.sh --key $API_KEY
```
- `environment: production`: Hooks into GitHub's environment settings, pausing the workflow if approvals are required.

### Real-World Example
A team sets up an environment called `Production`. They configure a protection rule requiring the Lead Engineer's approval. When a workflow reaches the deploy job, it pauses. The Lead Engineer gets an email, reviews the changes, and clicks "Approve" in the GitHub UI, allowing the code to deploy securely to the live web server.

### Common Beginner Mistakes
- **Mistake:** Deploying directly without separating the build and deploy jobs.
  **Correction:** Always split testing/building from deployment into separate jobs. Use the `needs:` keyword so the deploy job *only* runs if the build job passes.

### Quick Revision Summary
- Automates pushing code to live servers.
- Use the `environment` keyword to tie jobs to specific stages.
- Enables manual approval gates for secure releases.
- Relies on Marketplace actions for seamless cloud integration.

---

## 14. Integrating with Docker

### Simple Explanation
Docker wraps your application and all its dependencies into a neat, standardized box called a container. GitHub Actions works exceptionally well with Docker, allowing you to automatically build these boxes and push them to storage registries (like Docker Hub or GitHub Container Registry) whenever you update your code.

### Why This Matters in DevOps
Containerization is the industry standard for modern software delivery. Automating the creation of Docker images ensures that the exact same container tested in CI is the exact same container deployed to production, eliminating "it works on my machine" bugs.

### Key Concepts
- **Service Containers:** You can run detached Docker containers (like a temporary PostgreSQL database) alongside your runner to execute integration tests.
- **Build and Push:** The process of creating the Docker image and uploading it to an image registry.
- **Docker Buildx:** An advanced Docker feature supported in Actions that enables building multi-architecture images and advanced layer caching to speed up builds.

### Visual / Workflow Explanation: CI/CD to Docker
```
1. Checkout code        - CI/CD system retrieves latest source code from repository
2. Authenticate         - System logs in securely to the central image registry
3. Run `docker build`   - Builds a new application container image using instructions in the Dockerfile
4. Run `docker push`    - The updated image is pushed and stored in the registry
5. Server pulls new image - Production server detects update and pulls the new image
6. Deploy & start       - Server starts the new container, deploying the updated application
```

### YAML Example
```yaml
jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: myusername/myapp:latest
```
- `docker/login-action`: Securely logs into the registry.
- `docker/build-push-action`: Handles compiling the Dockerfile and uploading the result.

### Real-World Example
An engineering team uses GitHub Actions to build a Docker image for their Python web app every time a PR is merged. The workflow authenticates to Amazon ECR (Elastic Container Registry), builds the image, tags it with the Git commit hash, and pushes it to the cloud so their Kubernetes cluster can serve it.

### Common Beginner Mistakes
- **Mistake:** Building Docker images from scratch every time, resulting in 10+ minute workflows.
  **Correction:** Utilize Docker Layer Caching (passing `cache-from` and `cache-to` arguments in the build action) to drastically reduce build times.

### Quick Revision Summary
- Easily automates `docker build` and `docker push` commands.
- Official Docker actions exist in the Marketplace.
- Can spin up background "Service Containers" (like DBs) for testing.
- Essential for modern Kubernetes and cloud deployments.

---

## 15. Integrating with cloud (AWS example, high-level)

### Simple Explanation
To deploy to a cloud like AWS, GitHub Actions needs a key to open the door. Previously, you had to generate long-lasting passwords and save them in GitHub. Now, using a technology called **OIDC (OpenID Connect)**, GitHub and AWS perform a secure handshake. GitHub says, "I vouch for this workflow," and AWS issues a temporary, short-lived digital key card to let the workflow in.

### Why This Matters in DevOps
Storing static, permanent cloud credentials is a massive security risk (if leaked, hackers own your cloud). OIDC eliminates hardcoded secrets. It issues temporary access tokens that automatically expire in minutes, significantly improving supply chain security.

### Key Concepts
- **OIDC (OpenID Connect):** A protocol allowing GitHub to exchange short-lived access tokens directly with cloud providers.
- **Identity Provider (IdP):** AWS is configured to trust GitHub's OIDC provider.
- **Trust Policy / Claims:** AWS checks the GitHub token claims to verify the specific repository and branch before granting access. This ensures only *your* repo can access your cloud.

### Visual / Workflow Explanation: GitHub to AWS OIDC Workflow & Secure Deployment
```
1. GitHub Actions (workflow) requests an OIDC token from GitHub (OIDC provider)
2. GitHub issues and signs a JSON Web Token (JWT)
3. The workflow sends the JWT to AWS
4. AWS IAM validates the token against the Trust Policy
5. AWS issues a temporary access key (valid ~1 hour)
6. The workflow uses it to deploy to AWS resources (S3, EC2, Lambda function)
```

### YAML Example
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      id-token: write    # REQUIRED: Allows workflow to request the OIDC JWT token
      contents: read
    steps:
      - uses: actions/checkout@v4

      - name: Configure AWS credentials via OIDC
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123456789012:role/my-github-actions-role
          aws-region: us-east-1

      - name: Deploy
        run: aws s3 sync ./dist s3://my-website-bucket
```
- `permissions: id-token: write`: Mandatory for OIDC to work.
- `aws-actions/configure-aws-credentials`: Handles the entire background handshake automatically.

### Real-World Example
A DevOps team configures AWS to only trust tokens originating from `repo:my-company/my-app:environment:production`. When the GitHub Action runs the deployment job, it assumes an IAM Role in AWS securely without any hardcoded passwords, syncing static website files to an S3 bucket.

### Common Beginner Mistakes
- **Mistake:** Forgetting to add `permissions: id-token: write` to the YAML file.
  **Correction:** Without this permission, GitHub will deny the workflow's request to generate the OIDC token, causing the AWS authentication step to fail immediately.

### Quick Revision Summary
- OIDC eliminates the need to store static cloud secrets.
- Provides highly secure, temporary credentials.
- AWS uses IAM Trust Policies to strictly verify the repository and branch.
- Requires explicit `id-token: write` permissions in the YAML.

---

## 16. Self-hosted runners (concept)

### Simple Explanation
While GitHub-hosted runners are convenient, sometimes you need to run tasks on your own computers. A self-hosted runner is a machine you own (a VM in your cloud, an on-premises server, or even a Raspberry Pi) that you install a small GitHub listening program on. This program "calls home" to GitHub, asks if there are any jobs to do, and executes them on your hardware.

### Why This Matters in DevOps
Enterprise compliance often dictates that source code cannot leave a private corporate network. Self-hosted runners operate inside your firewall, allowing workflows to securely access internal databases, active directories, or custom hardware (like specialized GPUs) that GitHub cannot provide.

### Key Concepts
- **Full Customization:** You control the OS, the installed tools, and the hardware specs.
- **Persistent State:** Unlike GitHub's ephemeral runners that are destroyed after one use, self-hosted runners persist. Files left behind from Job A will be there when Job B starts.
- **Actions Runner Controller (ARC):** A Kubernetes operator used by advanced DevOps teams to automatically scale self-hosted runners up and down based on demand.

### Visual / Workflow Explanation: GitHub Job on Private Server
```
GitHub cloud                                      Your private network (behind FIREWALL)
1. Job triggered (workflow run requested, e.g. commit push, scheduled)
2. GitHub adds job to queue
                                                  3. Private server sees the job (constantly listening for job labels)
                                                  4. Pulls job instructions down through the firewall (outbound connection)
                                                  5. Executes job locally (builds, tests, deploys using local resources)
6. Pushes logs back up to GitHub UI  ←────────────
```

### YAML Example
```yaml
jobs:
  secure-build:
    # Routes the job to your private runner using custom tags
    runs-on: [self-hosted, linux, internal-network]
    steps:
      - uses: actions/checkout@v4
      - run: echo "Running securely on corporate hardware!"
```

### Real-World Example
A healthcare company needs to run integration tests against an internal, highly secure patient database. They spin up a self-hosted runner inside their AWS Virtual Private Cloud (VPC). The runner can query the database directly during the CI pipeline without exposing the database to the public internet.

### Common Beginner Mistakes
- **Mistake:** Using self-hosted runners on public repositories.
  **Correction:** Anyone can submit a malicious Pull Request to a public repo. If that runs on your self-hosted runner, the attacker gains code execution access inside your private network. Only use self-hosted runners for private repositories.
- **Mistake:** Ignoring cleanup.
  **Correction:** Because they are persistent, failing to delete temporary files can fill up the runner's hard drive and crash future builds.

### Quick Revision Summary
- Hosted on your own infrastructure.
- Essential for accessing private network resources (behind firewalls).
- Persistent state requires careful file cleanup.
- Should generally be restricted to private repositories for security.

---

## 17. Best practices for production workflows

### Simple Explanation
Writing a workflow that "just works" is easy, but writing one that is secure, fast, and maintainable takes discipline. Best practices are the industry standards DevOps teams follow to ensure their pipelines don't become slow, expensive, or vulnerable to hackers.

### Why This Matters in DevOps
As an application scales, a messy CI/CD setup will cripple developer velocity. Applying best practices reduces compute billing costs, speeds up feedback loops, and prevents catastrophic security breaches.

### Key Concepts
- **Principle of Least Privilege:** Workflows should only have the bare minimum permissions needed to function (e.g., `contents: read`).
- **Reusable Workflows:** Instead of copying and pasting the exact same YAML into 20 repositories, create one centralized "Reusable Workflow" and have the 20 repositories "call" it. This centralizes maintenance.
- **Pinning Action Versions:** Always use specific version tags or commit SHAs for third-party actions to prevent upstream changes from breaking your builds.
- **Artifact Attestations / SLSA:** Cryptographically signing your build artifacts so consumers can verify the code wasn't tampered with during the CI process.

### Visual / Workflow Explanation: Secure CI/CD Supply Chain Using Reusable Workflows
```
Step 1: Local repo YAML (.github/workflows/main.yml) - developer commits config to their local project repository
   ↓ CALLS
Step 2: Centralized organization reusable workflow (org-central/.github/workflows/secure-build.yml)
        - standardized workflow managed centrally by the organization
   ↓
Step 3: Executes with strict least-privilege permissions (scoped permissions, e.g. via OIDC)
        - hardened environment, only temporary, minimal permissions needed for the build task
   ↓ YIELDS
Step 4: Signed & secure artifact - digitally signed, with provenance attestation
```

### YAML Example: Applying Least Privilege and Reusability
```yaml
# Applying Least Privilege and Reusability
jobs:
  call-central-workflow:
    permissions:
      contents: read     # Explicitly restricting token permissions
    uses: my-org/central-repo/.github/workflows/secure-build.yml@v1.2.0   # Pinning version
```

### Real-World Example
An enterprise with 50 microservices manages CI/CD by maintaining a single "Golden Pipeline" reusable workflow in a central repository. When a security update is needed for the deployment process, the DevOps team updates the central file once, and all 50 microservices instantly inherit the fix.

### Common Beginner Mistakes
- **Mistake:** Blindly copying third-party actions from the internet without reviewing their code.
  **Correction:** Third-party actions have full access to your runner and secrets. Always review the source code of actions you use, and pin them to a specific commit SHA for maximum security.

### Quick Revision Summary
- Explicitly define limited permissions (`permissions:` block).
- Use Reusable Workflows to avoid code duplication.
- Pin third-party actions to specific versions or SHAs.
- Utilize caching to optimize speed and cost.

---

## 18. Debugging GitHub Actions workflows

### Simple Explanation
When a pipeline inevitably fails, you need tools to figure out why. Debugging GitHub Actions involves reading logs, inspecting the variables that were passed into the system, and occasionally enabling hidden "verbose" modes to see exactly what the runner is doing behind the scenes.

### Why This Matters in DevOps
CI/CD errors block developers from merging features and releasing code. Rapid troubleshooting is a core DevOps skill. Understanding how to extract contextual information from a failed runner drastically reduces pipeline downtime.

### Key Concepts
- **Contexts:** GitHub provides objects (like `github`, `env`, `runner`, `steps`) that contain massive amounts of data about the current run. You can print these to the log to understand the state of the machine.
- **Step Debug Logging:** A hidden feature that forces the runner to print highly detailed diagnostic information to the console.
- **Job Summaries:** Custom markdown text you can append to the `$GITHUB_STEP_SUMMARY` file to output clean, readable test results directly on the workflow run page.

### Visual / Workflow Explanation: CI/CD Workflow Troubleshooting
```
1. Workflow fails
2. Developer reviews standard UI logs (unhelpful, generic logs)
3. Error is unclear (generic error, missing context: "Status ?")
4. Injects `toJSON(github)` into YAML (adds debug output)
5. Runs again & prints variables (large JSON output of state)
6. Identifies missing input variable (e.g. target = 'dev')
7. Fixes YAML & success (full successful pipeline)
```

### YAML Example: Dump GitHub Context
```yaml
jobs:
  debug_job:
    runs-on: ubuntu-latest
    steps:
      - name: Dump GitHub context
        env:
          # Converts the complex GitHub context object into readable JSON
          GITHUB_CONTEXT: ${{ toJson(github) }}
        run: echo "$GITHUB_CONTEXT"

      - name: Dump Runner OS
        run: echo "The OS is ${{ runner.os }}"
```
- `toJson()`: A function that formats context objects for easy log reading.

### Real-World Example
A workflow triggered by a Pull Request fails because it cannot find the branch name. The engineer adds a step to echo `${{ toJson(github) }}` to the log. They look at the output and discover that in PR events, the branch name is stored under `github.head_ref`, not `github.ref_name`. They update the script, and the pipeline succeeds.

### Common Beginner Mistakes
- **Mistake:** Printing the entire `github` context object to the logs in a public repository without realizing it might contain sensitive token data.
  **Correction:** While GitHub attempts to mask secrets, dumping entire contexts can be risky. Only dump contexts during private troubleshooting, or print specific safe variables (like `github.event_name`).

### Quick Revision Summary
- Use `toJson(context_name)` to print variables to the logs.
- The `github` context contains details about the trigger event (PRs, branch names).
- The `runner` context details the VM OS and temp folders.
- Job summaries provide clean, readable outputs for test results.
