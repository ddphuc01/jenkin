# Jenkins with Docker Compose

This guide will help you set up Jenkins using Docker Compose.

## Prerequisites
- [Docker](https://docs.docker.com/get-docker/) installed on your system.
- [Docker Compose](https://docs.docker.com/compose/install/) installed.

## How to Use

### Step 1: Start Jenkins
1. Save the `docker-compose.yml` file in a directory.
2. Open a terminal and navigate to the directory containing the file.
3. Run the following command to start Jenkins:
   ```bash
   docker-compose up -d
   ```
   - The `-d` flag runs the containers in detached mode.

### Step 2: Access Jenkins
1. Open your browser and navigate to [http://localhost:8080](http://localhost:8080).
2. Retrieve the initial administrator password:
   ```bash
   docker logs jenkins
   ```
   Look for a line in the logs that looks like this:
   ```
   *************************************************************
   Jenkins initial setup is required. An admin user has been created and a password generated.
   Please use the following password to proceed to installation:

   1234567890abcdef1234567890abcdef
   *************************************************************
   ```
3. Copy the password and paste it into the Jenkins setup screen.

### Step 3: Install Plugins
- Follow the setup wizard to install recommended plugins or select plugins manually.

### Step 4: Create Your First Admin User
- After installing plugins, you will be prompted to create your first admin user. Fill out the required fields and continue.

### Step 5: Configure Jenkins
- Set up Jenkins to suit your CI/CD requirements:
  - Install additional plugins as needed.
  - Configure credentials for repositories, servers, or cloud services.
  - Define jobs or pipelines to automate your builds.

### Step 6: Stop Jenkins
To stop Jenkins, run:
```bash
docker-compose down
```

### Additional Notes
1. **Persisted Data**:
   - The Jenkins data is persisted in the `jenkins_home` volume. You can find it on your host machine if needed.

2. **Docker Integration**:
   - By mounting the Docker socket (`/var/run/docker.sock`), Jenkins can interact with Docker on the host machine. This is useful for building and running Docker images directly from Jenkins.

3. **JNLP Agents**:
   - Port `50000` is exposed to allow Jenkins agents to connect using the JNLP protocol.

4. **Security**:
   - Ensure your Jenkins instance is properly secured, especially if it's exposed to the internet. Use HTTPS and strong credentials.

### Troubleshooting
- **Cannot Access Jenkins**:
  - Ensure the container is running: `docker ps`
  - Check logs for errors: `docker logs jenkins`
- **Port Conflicts**:
  - If port `8080` or `50000` is already in use, modify them in the `docker-compose.yml` file.

For more advanced configurations, refer to the [official Jenkins documentation](https://www.jenkins.io/doc/).