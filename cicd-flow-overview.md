# CI/CD Flow: From Code Push to End User

## Simple Explanation
A developer pushes code to GitHub. The code must be **built**, then **tested** to confirm it works as expected. Only if the tests pass is it **deployed** to a server, and end users access the application through that server.

No single tool does everything. Each stage has its own tool, and **GitHub Actions** is the automation that connects them into one pipeline.

## Pipeline Stages

| Stage | What happens | Tool |
|---|---|---|
| 1. Code push | Developer runs `git push` | Git + GitHub |
| 2. Pipeline trigger | The push automatically starts the pipeline | **GitHub Actions** (runs the whole pipeline) |
| 3. Build | Code is compiled or packaged | Language build tool: `npm run build`, `mvn package`, `go build`, `pip install` |
| 3b. Docker image | The app is packed into a container image | **Docker** (`docker build`) |
| 4. Test | Checks that the app behaves as expected | Test tools: `pytest`, Jest, JUnit (lint runs here too) |
| 5. Push image | The image is stored in a registry | Docker Hub / AWS ECR |
| 6. Deploy | If tests pass, code is released to a server | AWS (EC2, Elastic Beanstalk, ECS) or any server |
| 7. End user access | Users open the server URL/IP and use the app | Server, usually with a domain and load balancer |

## Flow Diagram
```
git push → GitHub Actions → build (+ docker build) → test → pass? → deploy to server → end users access
                                                              └─ fail? → stop here, notify developer
```

## Key Concepts
- **GitHub Actions** is the orchestrator. It runs the pipeline and decides the order: build first, then test, then deploy.
- **Docker is not the pipeline.** Docker only packages the app and its dependencies into a container image.
- **Why Docker?** The exact same container that was tested is the one deployed to production, which avoids "it works on my machine" bugs.
- **Docker is optional for building.** A build can run without Docker, but containers make results consistent across environments.
- **Test gate:** If tests fail, deployment must not happen.

## YAML Idea: Deploy Only If Tests Pass
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t myapp .

  test:
    needs: build            # runs only after build succeeds
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pytest

  deploy:
    needs: test             # runs only if tests pass
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to server..."
```
`needs:` is what stops a deploy when the previous job fails.

## Real-World Example
A developer pushes a new feature. GitHub Actions builds the app and creates a Docker image. The test job runs automated tests. Because they pass, the image is pushed to the registry and deployed to the server (for example, AWS Elastic Beanstalk). Users now see the new feature at the app's URL.

## Common Beginner Mistakes
- **Mistake:** Thinking Docker runs the whole pipeline.
  **Correction:** GitHub Actions runs the pipeline; Docker only builds the container image.
- **Mistake:** Deploying without a test stage.
  **Correction:** Always put tests before deploy and use `needs:` so a failed test blocks the release.

## Quick Revision Summary
- Push → Build → Test → Deploy → Users access.
- GitHub Actions automates the whole flow.
- Docker packages the app into an image.
- Tests act as a gate: fail means no deployment.


 GitHub Actions: Workflow, Jobs, Steps and Actions
 
## Simple Explanation
GitHub Actions is the platform. Inside it, a **workflow** defines the whole pipeline. Each stage of the pipeline (build, test, deploy) is a **job**. Inside each job there are **steps**, and a step can use a **prebuilt action**.
 
## Hierarchy
```
GitHub Actions (platform)
└── Workflow            = one YAML file; the entire pipeline is defined here
    ├── on:             = trigger (push, pull_request, ...)
    ├── Job: build      = one stage
    │     ├── Step 1: checkout code   (uses: actions/checkout@v4)   ← prebuilt Action
    │     └── Step 2: docker build    (run: docker build ...)       ← your own command
    ├── Job: test       = next stage
    │     └── Steps ...
    └── Job: deploy     = next stage
          └── Steps ...
```
 
## Key Concepts
- **Workflow:** A YAML file stored in `.github/workflows/`. The complete pipeline is defined inside it.
- **Job:** Each stage (build, test, deploy) is a job. Every job runs on its own separate runner (VM).
- **Step:** A small task inside a job. Steps run one after another, sequentially.
- **Action (prebuilt):** A ready-made, reusable step called with `uses:`, for example `actions/checkout@v4`. To run your own command instead, use `run:`.
## Execution Rules
- Jobs run in **parallel** by default.
- Use `needs:` to set the order (build, then test, then deploy).
- Steps always run **sequentially** within a job.
- Jobs run on different machines, so files are shared between them using **artifacts**.
## YAML Example
```yaml
name: CI/CD Pipeline            # Workflow
on: push                        # Trigger
 
jobs:
  build:                        # Job 1
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4          # Prebuilt action
      - name: Build Docker image
        run: docker build -t myapp .       # Your own command
 
  test:                         # Job 2
    needs: build                # Runs only after build succeeds
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pytest
 
  deploy:                       # Job 3
    needs: test                 # Runs only if tests pass
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to server..."
```
 
## Quick Revision Summary
- Workflow = the whole pipeline (one YAML file).
- Job = one stage of the pipeline.
- Step = a single task inside a job.
- Action = a prebuilt, reusable step (`uses:`); `run:` is for your own commands.
- Jobs are parallel by default; use `needs:` for order.
 
