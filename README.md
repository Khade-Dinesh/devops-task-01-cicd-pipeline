# Node.js CI/CD Pipeline with GitHub Actions and Docker

## Project Overview

This project demonstrates an automated CI/CD pipeline for a Node.js web application using GitHub Actions and Docker. Whenever code is pushed to the `main` branch, the workflow checks the application, builds a Docker image, and publishes it to Docker Hub.

## Objectives

- Automate application checks using GitHub Actions.
- Package the Node.js application using Docker.
- Publish the Docker image to Docker Hub.
- Manage credentials securely using GitHub Actions Secrets.

## Technologies Used

- Ubuntu 24.04 LTS
- Node.js 22
- npm
- Express.js
- Git and GitHub
- GitHub Actions
- Docker Engine
- Docker Hub

## CI/CD Workflow

1. Developer pushes code to the `main` branch.
2. GitHub Actions checks out the repository.
3. Node.js is configured on the runner.
4. Dependencies are installed using `npm ci`.
5. The application syntax check runs using `npm test`.
6. Docker Buildx prepares the image build.
7. GitHub Actions authenticates with Docker Hub using repository secrets.
8. The Docker image is built and pushed to Docker Hub with the `latest` tag.

## Project Structure

```text
nodejs-demo-app/
├── .github/
│   └── workflows/
│       └── main.yml
├── .gitignore
├── Dockerfile
├── package.json
├── package-lock.json
├── server.js
└── README.md
```

## Run Locally

Install the dependencies:

```bash
npm ci
```

Run the application:

```bash
node server.js
```

Open `http://localhost:3000` in a browser.

Health endpoint:

```text
http://localhost:3000/health
```

## Run with Docker

Build the Docker image:

```bash
docker build -t nodejs-demo-app:1.0 .
```

Run the container:

```bash
docker run -d --name nodejs-demo -p 3000:3000 nodejs-demo-app:1.0
```

Test the application:

```bash
curl http://localhost:3000
curl http://localhost:3000/health
```

## Docker Hub

The GitHub Actions workflow publishes the image to Docker Hub using this naming convention:

```text
<DOCKERHUB_USERNAME>/nodejs-demo-app:latest
```

Pull the published image:

```bash
docker pull <DOCKERHUB_USERNAME>/nodejs-demo-app:latest
```

Replace `<DOCKERHUB_USERNAME>` with your Docker Hub username.

## GitHub Actions Secrets

The workflow uses these repository secrets:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

The access token is stored as a GitHub Secret rather than being hardcoded in the workflow or application files.

## Verification

- [x] Node.js application created
- [x] Docker image built and tested locally
- [x] GitHub Actions workflow configured
- [x] Workflow completed successfully
- [x] Docker Hub `latest` image tag verified

## Troubleshooting

During initial setup, the Docker image push failed with a `401 Unauthorized` error because the Docker Hub access token had insufficient permissions. The issue was resolved by updating the token permissions and rerunning the workflow.

## Key Learnings

- Configuring a CI/CD workflow with GitHub Actions
- Using Docker to containerize a Node.js application
- Publishing container images to Docker Hub
- Managing credentials with GitHub Actions Secrets
- Troubleshooting CI/CD pipeline failures

## Future Improvements

- Add automated HTTP integration tests.
- Add image version tags based on Git commits.
- Add vulnerability scanning for container images.
- Extend the workflow with a deployment stage.

## Screenshots

### GitHub Actions Pipeline Success
![GitHub Actions Success](screenshots/01-github-actions-success.png)

### Docker Hub Image
![Docker Hub Image](screenshots/02-dockerhub-image.png)

### Local Application Test
![Local App Test](screenshots/03-local-app-test.png)

