# Web Application Security Monitoring Lab (Splunk + DVWA)
## Overview
This project uses a lab environment for practising **Security Information and Event Management (SIEM)** and **Threat Hunting** skills. It focuses on the detection of **Cross-Site Scripting (XSS)** vulnerabilities through real-time log analysis and visualisation.

The environment is built using Docker Compose and consists of DVWA (Damn Vulnerable Web Application) container and a Splunk SIEM container.
***
## Prerequisites
To run and complete this lab, the user must have the following installed on their machine:

* **Docker:** Required for running the containers and applications.
* **Docker Compose:** Required for defining and managing the multi-container lab environment.
* **Web Browser:** To interact with the DVWA application at `http://localhost:8080` and Splunk at `http://localhost:8000`.
***
## Lab Environment Setup
The lab environment is deployed using a `docker-compose.yml` file configured with shared volumes to enable log forwarding.

### Docker Config File
Download the `docker-compose.yml` file and ensure it includes the volume mapping for `/var/log/apache2` to allow Splunk to access the web log.

### Start the Environment
Navigate to the project directory and execute the following command:
```
docker-compose up -d
```

### Initial Configuration
1. **Access DVWA:** Open browser to `http://localhost:8080` and log in using username: `admin` and password: `password`.
2. **Initalise Database:** Click **"Create/Reset Database"** and set the security level to **"Low"**
3. **Configure Permissions:** Run the following command to allow Splunk to read the generated logs:
```
docker exec -it dvwa-victim chmod 644 /var/log/apache2/access.log
```
4. **Access Splunk:** Navigate to `http://localhost:8000` and configure a **New Data Input** for the file path `/var/log/dvwa-target/access.log`
