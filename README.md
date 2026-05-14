# Flask CI/CD Pipeline — GHCR

A CI/CD pipeline using **GitHub Actions** that builds a Flask Docker image, pushes it to **GitHub Container Registry (GHCR)**, runs it, and verifies the app is live — all on every push to `main`.

---

## Pipeline Steps

| Step                  | Description                                              |
|-----------------------|----------------------------------------------------------|
| Checkout Code         | Clones the repository                                    |
| GHCR Login            | Authenticates to GitHub Container Registry               |
| Build Image           | Builds the Flask Docker image                            |
| Push to GHCR          | Pushes `ghcr.io/<username>/flaskp:latest`               |
| Run Container         | Starts the container on port `5000`                      |
| Health Check          | Polls `http://localhost:5000` until app responds         |
| Check Containers      | Runs `docker ps` to verify container state               |
| Check Logs            | Prints container logs for debugging                      |
| Remove Container      | Cleans up the test container                             |

---

## Run Locally

```bash
# Build the image
docker build -t flaskp .

# Run the container
docker run -d -p 5000:5000 flaskp

# Test
curl http://localhost:5000
```

---

## Secrets Required

Add these in **GitHub → Settings → Secrets → Actions**:

| Secret          | Description                        |
|-----------------|------------------------------------|
| `GITH_USERNAME` | Your GitHub username               |
| `GHCR_TOKEN`    | GitHub Personal Access Token (PAT) with `write:packages` scope |

---

## Tech Stack

- Python / Flask
- Docker
- GitHub Actions
- GitHub Container Registry (GHCR)

---
