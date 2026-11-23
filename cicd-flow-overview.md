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
