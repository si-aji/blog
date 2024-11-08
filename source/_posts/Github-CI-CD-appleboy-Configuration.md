---
title: 'Github CI/CD: `appleboy/ssh-action` Configuration'
date: 2024-11-08 10:31:44
tags:
- CI/CD
- Github Action
- appleboy/ssh-action
category:
- Github Action
---

If you're interested in deploying code with GitHub Actions, appleboy/ssh-action is a flexible tool for running commands on remote servers over SSH. As outlined on the GitHub page, this action can be used with SSH keys, passwords, and other methods. In this post, I'll demonstrate how to configure appleboy/ssh-action with an SSH private key for secure, streamlined deployments.

## Prerequisites

Before getting started, ensure you have access to the following:

- **SSH Access** to the target server
- **GitHub Repository Access** where you'll configure the workflow

SSH access means you can connect to the server via SSH, and you’ll either generate a new SSH key or use an existing one to store securely in GitHub Secrets.

## Configuration Steps

Follow these steps to set up `appleboy/ssh-action` with SSH key authentication.

1. SSH Access to the Target Server

Ensure you have SSH access to the target server and that your user account has sufficient permissions to execute deployment commands.

2. Generate an SSH Key (Optional)

If you don’t already have an SSH key, generate one using:

```shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This creates a public and private key pair in your ~/.ssh directory. The private key will be used as a secret in GitHub, and the public key will be added to the server.

3. Copy the SSH Private Key to Clipboard

Copy the content of the private key file (~/.ssh/id_rsa):

```shell
cat ~/.ssh/id_rsa | pbcopy  # MacOS
cat ~/.ssh/id_rsa | xclip   # Linux
```

Or open the file and copy it manually.

4. Add the SSH Public Key to Your Server Profile

To allow SSH access, add the public key (~/.ssh/id_rsa.pub) to the ~/.ssh/authorized_keys file on the server. This step is essential for passwordless SSH access.

5. Add GitHub Secrets to Your Repository

Now, in your GitHub repository, go to Settings > Secrets and Variables > Actions and add the following secrets:

- **`SSH_HOST`**: The IP address or hostname of the server. For example, if your SSH command is ssh `root@192.168.0.1`, your **`SSH_HOST`** value will be `192.168.0.1`.

- **`SSH_USERNAME`**: The SSH username. Based on the example above, this value would be `root`.

- **`SSH_PORT`**: The port used for SSH connections. The default is `22`, but check if your server uses a custom port.

- **`SSH_PRIVATE_KEY`**: The contents of the private SSH key (`~/.ssh/id_rsa`). Paste the raw content of the key here (without line breaks).

With these secrets in place, your SSH connection information is securely stored in GitHub.

---

## Example Workflow Configuration

Here’s an example of a GitHub Actions YAML file using appleboy/ssh-action with the SSH key setup:

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
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Deploy via SSH
        uses: appleboy/ssh-action@v0.1.8
        with:
          host: ${{ secrets.SSH_HOST }}
          username: ${{ secrets.SSH_USERNAME }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          port: ${{ secrets.SSH_PORT }}
          script: |
            cd /path/to/your/app
            git pull origin main
            npm install
            npm run build
            pm2 restart all
```

### Breakdown of Configuration
- **host**: Points to your server's IP address or hostname.
- **username**: Specifies the user account for SSH access.
- **key**: Uses your SSH private key from GitHub Secrets for authentication.
- **port**: Connects through the specified SSH port.
- **script**: Runs deployment commands on the server, such as pulling code and restarting the app.

## Known Issue

If you encounter the following error:

> ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain

This typically indicates an issue with SSH key authentication. To resolve this:

- Make sure your SSH public key is added to the `~/.ssh/authorized_keys` file on the server.