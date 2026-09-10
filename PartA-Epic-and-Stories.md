# Final Project – Part A: Epic and User Stories

Tax Calculator modernization (Cloud Native, DevOps, Agile, and NoSQL)

You can paste these into a Kanban board (ZenHub, Trello, GitHub Projects) or keep this file as the text-editor submission the lab allows.

---

## Epic

**Title:** Modernise Tax Calculator

**Description:** The Tax Calculator currently runs as a manually deployed static application and lacks a robust pipeline in place. This epic focuses on modernizing the application to deploy it on IBM Cloud. But the web application will not just be simply lifted and shifted to cloud. The application will be containerized using Docker container. The deployment will be managed through a pipeline, which will also ensure that all unit tests pass before deployment.

**Status:** In Progress  
**Related stories:** Containerizing the application · Deploying on IBM Cloud · Creating a pipeline for packaging and deploying the application

---

## Story 1: Containerizing the application

**As a** developer  
**I need** to validate that each unit of code performs as expected  
**So that** I can deploy the application to a Docker container

**Description:** To ensure that each unit of code performs as expected, run unit tests. And if the unit tests pass, deploy the application to a docker container.

**Acceptance criteria**

- Unit tests run with Jasmine and show 7 specs, 0 failures
- Dockerfile starts with `FROM nginx` and copies `favicon.ico`, `index.html`, `script.js`, `style.css`, and `taxCalculator.js`

**Status:** To Do

---

## Story 2: Deploying on IBM Cloud

**As a** developer  
**I need** the application to be deployed on IBM Cloud, using IBM Cloud Code Engine  
**So that** I avoid self-managed or in-house virtual machines

**Description:** Instead of hosting on self-managed or in-house virtual machines, deploy the application on IBM Cloud, using IBM Cloud Code Engine.

**Acceptance criteria**

- Docker image builds successfully
- App runs locally in a container on port 8080
- Image is tagged and pushed to IBM Cloud Container Registry
- Tax Calculator is deployed on IBM Cloud Code Engine

**Status:** To Do

---

## Story 3: Creating a pipeline for packaging and deploying the application

**As a** developer  
**I need** a Tekton pipeline to automate the build, test, and packaging of the application  
**So that** I reduce many manual steps in the process of packaging and deploying

**Description:** The current process of packaging and deploying involves too many manual steps. Use a Tekton pipeline to automate the build, test, and packaging stages of the application.

**Acceptance criteria**

- `tasks.yaml` defines npm and Jasmine tasks
- `pipeline.yaml` calls npminstall, tests, and build
- `run.yaml` starts the pipeline
- The image built by the pipeline is deployed

**Status:** To Do
