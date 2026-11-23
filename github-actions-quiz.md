# Batch 10 - GitHub Actions Quiz

## Day 1 - GitHub Actions Fundamentals

**1. What are GitHub Actions primarily used for?**

A) To manage database architectures
B) To automate tasks, set up CI/CD, and deploy code directly from repositories
C) To act as a primary web hosting service
D) To manually review code errors

**Ans: B) To automate tasks, set up CI/CD, and deploy code directly from repositories**

---

**2. A job in GitHub Actions consists of**

A) Only one step
B) Multiple workflows
C) Series of individual steps executed sequentially
D) Only environment variables

**Ans: C) Series of individual steps executed sequentially**

---

**3. Where are workflow files stored in a repository?**

A) /github/workflows
B) github/workflow
C) .github/workflows
D) /workflows

**Ans: C) .github/workflows**

---

**4. If a workflow runs a job on Ubuntu, Windows, and macOS simultaneously, how are the runners provisioned by default?**

A) In series
B) In parallel
C) Alphabetically
D) Manually

**Ans: B) In parallel**

---

**5. What is a "Runner" in GitHub Actions?**

A) A script that checks for syntax errors
B) A directory where workflows are stored
C) A set of pre-defined objects
D) A VM responsible for executing workflows upon triggering

**Ans: D) A VM responsible for executing workflows upon triggering**

---

**6. Which of the following is true of GitHub-hosted runners?**

A) You must manage the infrastructure yourself
B) They allow you to run multiple jobs on the same clean machine indefinitely
C) They provide a new clean instance for each and every job execution
D) You can install system-level changes to the base OS

**Ans: C) They provide a new clean instance for each and every job execution**

---

**7. When would you use a "Workflow dispatch" event?**

A) When a pull request is created
B) When you want to manually run the workflow
C) When an issue is updated
D) When code is merged to the main branch

**Ans: B) When you want to manually run the workflow**

---

**8. When does a push event in GitHub Actions trigger a workflow?**

A) When a pull request is merged
B) When commit or tag is pushed to the repository
C) When an issue is created
D) When workflow is deleted

**Ans: B) When commit or tag is pushed to the repository**

---

**9. In GitHub Actions, what does the schedule event with cron syntax actually control?**

A) It runs the workflow only when code is pushed
B) It triggers the workflow at specified time intervals
C) It runs the workflow continuously
D) It triggers the workflow only once when created

**Ans: B) It triggers the workflow at specified time intervals**

---

**10. What typically happens when you push code to a repository that has a workflow configured with on: push?**

A) The workflow is automatically triggered
B) GitHub deletes the previous workflow runs
C) The repository is forked automatically
D) Nothing happens unless triggered manually

**Ans: A) The workflow is automatically triggered**

> ⚠️ Correction: the original sheet showed "B) GitHub deletes the previous workflow runs" as the answer. That is wrong; the correct answer is A.

---

**11. What is the role of Steps within a job?**

A) They define the operating system for the job
B) They trigger other workflows automatically
C) They are individual tasks executed sequentially within a job
D) They manage repository permissions

**Ans: C) They are individual tasks executed sequentially within a job**

---

**12. Which of the following statements correctly describes advantages of GitHub Actions?**

A) You must manually set up and scale servers for your workflows
B) GitHub Actions only works on local machines, not in virtual environments
C) You cannot get reports or job status from GitHub Actions
D) GitHub manages infrastructure, executes jobs and provide reports

**Ans: D) GitHub manages infrastructure, executes jobs and provide reports**

---

**13. What is the advantage of self-hosted runners?**

A) You are responsible for updating the VM
B) You can install any software & fully control the environment
C) You cannot run multiple jobs on the same machine
D) macOS runners are hosted on GitHub's servers

**Ans: B) You can install any software & fully control the environment**

---

**14. Where are GitHub-hosted runners for Linux, Windows, and macOS hosted?**

A) Linux & Windows on Azure, macOS on GitHub macOS cloud
B) Linux & Windows on GitHub cloud, macOS on Azure
C) All runners on self-managed servers
D) All runners on AWS EC2

**Ans: A) Linux & Windows on Azure, macOS on GitHub macOS cloud**

---

**15. Which of the following is allowed on self-hosted runners but NOT on GitHub-hosted runners?**

A) Running jobs automatically on push events
B) Using YAML-based workflow configuration
C) Installing system-level software
D) Receiving job logs and artifacts

**Ans: C) Installing system-level software**

---

## Day 2 - GitHub Actions Advanced

**1. In workflow_dispatch, why do we define inputs?**

A) To auto-detect the deployment environment
B) To allow users to select a predefined option when manually running the workflow
C) To permanently set repository environment variables
D) To restrict branch creation

**Ans: B) To allow users to select a predefined option when manually running the workflow**

---

**2. In a GitHub Actions workflow, what is the purpose of using actions/checkout@v4?**

A) Installs dependencies required for the project
B) Creates a new branch automatically before deployment
C) Action checks-out repo under $GITHUB_WORKSPACE, so workflow can access
D) Deploys the application to the production server

**Ans: C) Action checks-out repo under $GITHUB_WORKSPACE, so workflow can access**

---

**3. What are artifacts in GitHub Actions commonly used for?**

A) To permanently store source code in the repository
B) To share files (build outputs, logs, or reports) between jobs and access them after the job completes
C) To trigger another workflow automatically
D) To automatically merging branches

**Ans: B) To share files (build outputs, logs, or reports) between jobs and access them after the job completes**

---

**4. What is the primary purpose of GitHub Environments?**

A) To create new branches automatically
B) To run workflows on different operating systems
C) To protect deployments with environment-specific secrets
D) To cache dependencies between workflow runs

**Ans: C) To protect deployments with environment-specific secrets**

---

**5. What is the main purpose of the lint job?**

A) Run code quality checks before testing
B) Build Docker image
C) Run unit tests
D) Deploy application

**Ans: A) Run code quality checks before testing**

---

**6. Why are `if` conditional expressions used in a job or step?**

A) To permanently remove a step from the workflow
B) To speed up workflow execution automatically
C) To encrypt secrets inside the workflow
D) To control whether a job or step runs based on a condition

**Ans: D) To control whether a job or step runs based on a condition**

---

**7. What is the role of Matrix Strategy in GitHub Actions?**

A) To run single job across predefined combinations of variables
B) To manually create separate jobs for each operating system
C) To reduce the number of workflow runs
D) To deploy applications to multiple servers

**Ans: A) To run single job across predefined combinations of variables**

---

**8. What is the main purpose of using OIDC with AWS in GitHub Actions?**

A) To permanently store AWS access keys in the repository
B) To authenticate securely with AWS without storing long-term credentials
C) To increase Docker build speed
D) To create IAM users automatically

**Ans: B) To authenticate securely with AWS without storing long-term credentials**

---

**9. In GitHub Actions, why is the Fan-Out / Fan-In pattern used?**

A) To run workflows only on one branch
B) To run multiple jobs in parallel & then run a final job
C) To automatically merge pull requests
D) To store secrets securely

**Ans: B) To run multiple jobs in parallel & then run a final job**

---

**10. Which trigger is used to create a reusable workflow?**

A) push
B) workflow_dispatch
C) workflow_call
D) pull_request

**Ans: C) workflow_call**

---

**11. What's the purpose of the concurrency key in a workflow?**

A) Stores workflow logs securely
B) Speeds up Docker image builds
C) Runs multiple workflows in parallel without restriction
D) Limits or cancels in-progress workflow runs to prevent conflicts

**Ans: D) Limits or cancels in-progress workflow runs to prevent conflicts**

---

**12. How do you target a self-hosted runner in a workflow?**

A) runs-on: ubuntu-latest
B) runs-on: github-hosted
C) runs-on: self-hosted
D) runs-on: ec2

**Ans: C) runs-on: self-hosted**

---

**13. What is the main function of the env context?**

A) Store encrypted sensitive values
B) Store environment variables for workflows, jobs, or steps
C) Automatically rotate tokens
D) Store AWS credentials securely

**Ans: B) Store environment variables for workflows, jobs, or steps**

---

**14. What is a common reason jobs are not assigned to a self-hosted runner?**

A) Docker not installed
B) Ubuntu not updated
C) SSH key expired
D) Incorrect runs-on label mismatch

**Ans: D) Incorrect runs-on label mismatch**

---

**15. What is the aim of the secrets context?**

A) Store sensitive data like tokens & passwords
B) Store public configuration values
C) Store workflow outputs
D) Store temporary build variables

**Ans: A) Store sensitive data like tokens & passwords**
