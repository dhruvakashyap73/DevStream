# DevStream: Cloud-native, End-to-End CI/CD

## Overview
**DevStream** is a cloud-native, end-to-end CI/CD project built using AWS DevOps services. It demonstrates the complete lifecycle of a web application from cloud-based development setup to automated build, deployment, infrastructure provisioning, and continuous delivery using a fully orchestrated pipeline.

This project is divided into **7 structured parts**, where each part focuses on one critical stage of CI/CD implementation and automation.

---

## Architecture Diagram
![DevStream Architecture Diagram](Documentation/architecture-complete.png)

---

## Part 1: Set Up a Web App in the Cloud

### Objective
Set up a cloud-based development environment and generate a Java web application using Maven.

### Implementation
- Launched an **Amazon EC2 instance** to act as a cloud development server.
- Configured secure access using:
  - Key Pair authentication (`.pem`)
  - SSH connection through terminal and VS Code
- Installed required build tools:
  - Java 8 (Amazon Corretto)
  - Apache Maven
  - Git
- Generated a Maven-based Java web application using archetypes:
  - Created a standard Maven web application structure
  - Prepared the project for CI/CD integration
- Updated and verified the application UI:
  - Modified `index.jsp` to validate that the application structure and deployment output are correct

### Key Outputs
- EC2 development instance created and accessible via SSH
- Maven and Java environment configured successfully
- Web application generated and validated in the instance

### Read More (Comprehensive Report - PDF)
- [Part 1 Report (PDF)](Documentation/Day1-DevOps.pdf)

---

## Part 2: Connect a GitHub Repo with AWS

### Objective
Connect the web application to GitHub for version control and enable remote repository tracking.

### Implementation
- Created a dedicated **GitHub repository** for the application codebase.
- Initialized Git inside the EC2-hosted project directory:
  - Enabled version tracking for all source files
- Connected the local repository to GitHub remote origin:
  - Configured remote URL for push and fetch operations
- Pushed application code into GitHub:
  - Staged files, committed changes, and pushed to the `master` branch
- Configured GitHub authentication securely using a **Personal Access Token (PAT)**:
  - Replaced password authentication with token-based access
  - Improved repository security and compatibility with automation workflows
- Verified repository sync:
  - Ensured all project files were visible and updated in GitHub

### Key Outputs
- GitHub repository linked successfully with the EC2 project directory
- Source code version history established and trackable
- PAT-based secure authentication enabled for future CI/CD stages

### Read More (Comprehensive Report - PDF)
- [Part 2 Report (PDF)](Documentation/Day2-DevOps.pdf)
