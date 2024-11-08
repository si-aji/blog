---
title: 'Github CI/CD: `appleboy/ssh-action`'
date: 2024-11-07 14:55:42
tags:
- CI/CD
- Github Action
category:
- Github Action
---

CI/CD stands for Continuous Integration (CI) and Continuous Deployment/Delivery (CD). CI/CD automates integrating code changes, testing, and deployment, helping streamline the process from code to production. It aims to minimize human intervention in the software delivery cycle, leading to faster and more reliable releases.

## Github Action for CI/CD

GitHub provides a powerful automation tool called GitHub Actions that allows developers to create workflows triggered by events (such as pushes, pull requests, or new issues). These workflows can define a CI/CD pipeline to automate build, test, and deployment tasks. GitHub Actions provides flexible workflows written in YAML that can run on GitHub-hosted or self-hosted runners, making it a versatile choice for automating development tasks.

## CI/CD Process Overview

A typical CI/CD pipeline consists of several stages:

1. **Source Control**: Code changes are pushed to a version control repository (like GitHub).
2. **Build**: The CI/CD tool compiles the code, creating build artifacts if necessary.
3. **Test**: Automated tests run to verify code functionality and catch issues early.
4. **Deploy**: After passing tests, the code is deployed to a production or staging environment.

This pipeline enables frequent updates and ensures the reliability of new releases by automating repetitive steps, reducing human error, and increasing speed.

## The benefits

CI/CD offers several key advantages:

- **Faster Deployments**: Automated workflows streamline the path from development to production.
- **Reduced Errors**: Automated tests catch bugs early, resulting in fewer production issues.
- **Consistency**: Standardized workflows produce predictable results, improving overall software quality.
- **Improved Collaboration**: With automation in place, teams can collaborate efficiently without interrupting each other’s workflows.

## Overview of `appleboy/ssh-action`

The `appleboy/ssh-action` is a GitHub Action that allows workflows to connect to remote servers over SSH and run commands. It is particularly useful for deploying code to servers that aren’t directly accessible from GitHub, providing a bridge to custom environments where direct integration isn’t possible.

## How appleboy/ssh-action Works

The `appleboy/ssh-action` is designed to execute commands on a remote server within a GitHub Actions workflow. For example, it can:

- Deploy code to a VPS or dedicated server.
- Restart services like Nginx, Apache, or Docker containers.
- Transfer files between GitHub and the server using SCP.

This action relies on SSH, so you must provide SSH credentials securely. You can store sensitive data (like SSH keys) in GitHub Secrets and reference them in the workflow configuration.

### Example Configuration

Here’s a sample YAML setup that connects to a remote server and runs commands using `appleboy/ssh-action`:

```yaml
name: Deploy to Server

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v2

      - name: Deploy via SSH
        uses: appleboy/ssh-action@v0.1.0
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          port: 22
          script: |
            cd /path/to/deployment/directory
            git pull origin main
            # Restart service if needed
            sudo systemctl restart myapp
```

In this example:

- The workflow triggers whenever there’s a push to the `main` branch.
- `appleboy/ssh-action` connects to the remote server using SSH credentials stored in GitHub Secrets.
- The action runs a series of commands to pull the latest code and restart a service.

## Pros and Cons

### Advantages of using `appleboy/ssh-action`

- **Customized Environments**: Deploy to virtually any server with SSH access, including non-standard setups.
- **Direct Command Execution**: Run specific commands, including system commands, to control server configurations.
- **File Management**: Transfer files and update server resources as part of the deployment.

### Considerations

- `Security`: Since SSH keys are involved, it’s essential to secure your credentials within GitHub Secrets and restrict SSH access.
- `Setup Complexity`: Requires SSH setup on the server, and firewall configurations if needed.