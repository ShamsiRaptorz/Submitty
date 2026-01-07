# Submitty DevOps Project - Docker Setup Guide

## Project Structure

```
Submitty/
│
├── docker-compose.yaml
├── Jenkinsfile
│
├── docker/
│   ├── web/
│   │   ├── Dockerfile
│   │   └── index.html
│   │
│   └── worker/
│       └── Dockerfile
```

## Files Overview

### 1. docker-compose.yaml
- Defines two services: `web` and `worker`
- Web service runs on port 8080 (mapped to container port 80)
- Worker service runs on port 9090
- Both services are connected via `submitty_network` bridge network

### 2. docker/web/Dockerfile
- Based on PHP 8.1 Apache image
- Installs PostgreSQL extensions (pdo, pdo_pgsql)
- Serves index.html from `/var/www/html/`

### 3. docker/worker/Dockerfile
- Based on Python 3.10 slim image
- Runs a simple HTTP server on port 9090

### 4. docker/web/index.html
- Simple HTML page confirming successful deployment

### 5. Jenkinsfile
- Jenkins CI/CD pipeline configuration
- Uses `bat` commands for Windows compatibility
- Stages:
  - Checkout Code
  - Build Docker Images
  - Stop Old Containers
  - Run Containers
  - Smoke Test

## Running the Setup

### Manual Docker Commands

1. **Build the images:**
   ```powershell
   docker compose -f docker-compose.yaml build
   ```

2. **Start the containers:**
   ```powershell
   docker compose -f docker-compose.yaml up -d
   ```

3. **Check running containers:**
   ```powershell
   docker ps
   ```

4. **Stop the containers:**
   ```powershell
   docker compose -f docker-compose.yaml down
   ```

### Access the Services

- **Web Service:** http://localhost:8080
- **Worker Service:** http://localhost:9090

## Jenkins Pipeline Setup

### Prerequisites
- Jenkins installed and running
- Docker installed and accessible from Jenkins
- Git plugin installed in Jenkins

### Setting up the Pipeline

1. **Create a new Pipeline job in Jenkins:**
   - Go to Jenkins Dashboard
   - Click "New Item"
   - Enter name: "Submitty-DevOps"
   - Select "Pipeline"
   - Click OK

2. **Configure the Pipeline:**
   - In "Pipeline Definition", select "Pipeline script from SCM"
   - SCM: Git
   - Repository URL: `https://github.com/ShamsiRaptorz/Submitty.git`
   - Branch: `main`
   - Script Path: `Jenkinsfile`
   - Click Save

3. **Run the Pipeline:**
   - Click "Build Now" on the job page
   - Monitor the build progress in the console output

### Pipeline Stages

1. **Checkout Code:** Clones the repository from GitHub
2. **Build Docker Images:** Builds both web and worker Docker images
3. **Stop Old Containers:** Gracefully stops any existing containers
4. **Run Containers:** Starts the containers in detached mode
5. **Smoke Test:** Lists running containers to verify deployment

## Verification

After running the pipeline or starting containers manually:

1. Check containers are running:
   ```powershell
   docker ps
   ```

2. Verify web service (in browser or PowerShell):
   ```powershell
   Invoke-WebRequest -Uri http://localhost:8080 -UseBasicParsing
   ```

3. Verify worker service:
   ```powershell
   Invoke-WebRequest -Uri http://localhost:9090 -UseBasicParsing
   ```

## Troubleshooting

### Docker Compose Version Warning
If you see a warning about the `version` field being obsolete, you can remove it from `docker-compose.yaml`. Modern Docker Compose doesn't require it, but it's kept for compatibility.

### Port Conflicts
If ports 8080 or 9090 are already in use:
- Change the port mappings in `docker-compose.yaml`
- Update the Jenkinsfile if needed

### Jenkins Pipeline Issues
- Ensure Docker is accessible from Jenkins
- Check Jenkins has permissions to run Docker commands
- Verify Git plugin is installed
- Check Jenkins logs for detailed error messages

## Notes

- The worker Dockerfile copies the entire repository context, which is fine for this demo but could be optimized for production
- The web service uses PHP 8.1 with Apache and PostgreSQL extensions
- Both services are on the same Docker network and can communicate with each other

