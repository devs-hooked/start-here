# Quickstart Guide for New Team Members at Hooked (behooked.co)

Welcome to the Hooked team! This guide will help you set up your development environment and understand our CI/CD workflow. For any DevOps assistance, please contact Nikhil Mishra.

## 1. GitHub Setup

### Repository Access
1. Add your SSH key to the `devshooked` GitHub account
2. Set up your passkey for authentication
3. If you need a new repository:
   - Create it under the `devshooked` github account
   - Add yourself as a collaborator

## 2. AWS Account Setup

1. Request an IAM user for the devshooked AWS account from Nikhil Mishra
2. After receiving credentials:
   - Sign in to AWS Console
   - Set up Multi-Factor Authentication (MFA)

## 3. Docker Configuration

For Dockerfile or Docker Compose setup:
1. Share your repository with the `.env` file on Discord
2. Contact Nikhil for Docker configuration assistance and proceed with cicd-stuff

## 4. Cloud Infrastructure

We utilize multiple cloud providers:
- AWS (Primary)
- Azure
- GCP

## 5. CI/CD Workflow

### Our CI/CD Pipeline
```mermaid
flowchart LR
    subgraph Pipeline Flow
    A([Code Push]) --> B[GitHub Actions]
    B --> C[Build Docker Image]
    C --> D[Push to DockerHub]
    D --> E[Create Template]
    E --> F([Deploy])
    B -.-> G{Discord}
    C -.-> G
    D -.-> G
    F -.-> G
    end
    
    classDef start fill:#d4ffcc,stroke:#333,stroke-width:2px
    classDef process fill:#fff4db,stroke:#333,stroke-width:2px
    classDef notify fill:#ffd4d4,stroke:#333,stroke-width:2px
    classDef deploy fill:#d4e4ff,stroke:#333,stroke-width:2px
    
    class A start
    class B,C,D,E process
    class G notify
    class F deploy
```

### Deployment Process
```mermaid
sequenceDiagram
    autonumber
    participant D as Developer
    participant G as GitHub
    participant A as Actions
    participant H as DockerHub
    participant E as Endpoint
    participant N as Discord

    rect rgb(240, 245, 255)
    Note over D,G: Code Submission
    D->>G: Push Code
    G->>A: Trigger Workflow
    end

    rect rgb(255, 245, 240)
    Note over A,H: Build & Push
    A->>N: Build Started
    A->>H: Push Docker Image
    A->>N: Build Complete
    end

    rect rgb(245, 255, 240)
    Note over D,E: Deployment
    D->>E: Create Template
    Note over E: Configure Template:<br/>Image Name<br/>Registry Credentials<br/>Environment Variables
    D->>E: Deploy Template
    E->>N: Deployment Status
    end
```

### Step 1: Dockerfile Creation
- Create a Dockerfile in your repository
- This will be built using GitHub Actions

### Step 2: GitHub Actions Integration
- CI/CD configuration file in your repository triggers the build process
- Built Docker image is pushed to our Docker Hub repository (`gethooked`)
- Access Docker Hub using the devshooked Google account credentials

### Step 3: Build Notifications
- Build status and other details are sent to the `build-notifications` channel on Discord
- Notifications are handled via Discord webhook

### Step 4: Secrets Management
1. Store `.env` secrets in two locations:
   - GitHub secrets (for GitHub Actions)
   - Runpod secrets

### Step 5: Template Creation
After successful build and push:
1. Create a template with:
   - Image name
   - Registry credentials
   - Environment variable secrets

### Step 6: Deployment
- Use the created template in your endpoint
- Configure according to your requirements

## Need Help?

For any DevOps-related assistance or questions, contact Nikhil Mishra.

---
