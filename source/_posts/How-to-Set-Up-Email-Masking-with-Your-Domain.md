---
title: How to Set Up Email Masking with Your Domain
date: 2024-11-26 16:36:26
tags:
- Privacy and Security
- Email Masking
category:
- Server Management
---

Email masking is a method of creating alternative email addresses (aliases) that redirect emails to a primary address. These masked emails act as intermediaries, keeping your main email address private. For instance, if your primary email is `personal@main.tld`, you could use aliases like `info@domain.tld` or `sales@domain.tld` to receive messages while maintaining privacy.

## Why Use Email Masking?

### Benefits

- **Privacy Protection**: Keeps your primary email address hidden, reducing spam and phishing risks.
- **Organization**: Use different aliases for specific purposes (e.g., work, subscriptions, support).
- **Easy Revocation**: Disable or delete an alias without impacting your main email.
- **Professionalism**: Using a custom domain email looks more credible and professional.

### Disadvantages

- **Management Overhead**: Requires additional setup and periodic maintenance.
- **Dependence on Mail Server Reliability**: Aliases depend on your mail server’s forwarding functionality.
- **Potential Spam Forwarding**: If an alias is compromised, spam may still reach your primary inbox.

## How to Create Email Masking

There are multiple ways to set up email masking, depending on your tools and preferences:

1. **Using a Custom Domain with a Mail Server**:

This involves owning a domain like `domain.tld` and setting up email forwarding through a mail server (e.g., **aaPanel**, **cPanel**, or services like **Zoho Mail**).

2. **Using Email Hosting Services**:

Providers like **Google Workspace**, **ProtonMail**, and **Zoho Mail** offer alias creation and forwarding options.

3. **Using Specialized Masking Services**:

Services like **SimpleLogin** and **AnonAddy** allow users to create and manage masked emails that forward to a primary account.

## Example Usage

Imagine you’ve set up `info@domain.tld` as your masked email to forward to `personal@main.tld`.

- Someone sends an email to `info@domain.tld `with the subject line “Inquiry.”
- The mail server forwards this message to personal@main.tld.
- You can now read the email in your primary inbox, keeping `info@domain.tld` as the public-facing address.

## Step-by-Step: Create Email Masking with a Custom Domain and Mail Server

For this tutorial, I’ll demonstrate how to set up email masking using **aaPanel** on an **Ubuntu 24.04 VPS**. The mail server will use **Mail Server 5.4.8**, installed from the **aaPanel** app store. We’ll configure a domain `domain.tld` to forward emails to **personal@main.tld**.

Here’s how to set up email masking for **domain.tld** and forward messages to **personal@main.tld**:

### Prerequisites
- A VPS running Ubuntu 24.04 with aaPanel installed.
- Mail Server 5.4.8 installed via aaPanel.
- Your domain (`domain.tld`) is already set up on the mail server, and at least one user email is ready (e.g., `user@domain.tld`).

### Step

1. Access the Mail Forwarding Feature

- Log in to **aaPanel**.
- Open the **Mail Server** app from the dashboard.
- Navigate to the **Mail Forward** section.

2. Add a Forwarding Rule

- Click on the **Add Forward** button.
- Fill out the form with the following details:
    - **Forwarded users**: Enter the email address you want to use as the masked email (e.g., `info@domain.tld`).
    - **Domain**: Select the domain of the forwarded user (e.g., **domain.tld**).
    - **Receiving user**: Enter the actual email address where emails should be forwarded (e.g., `personal@main.tld`). You can include multiple recipients by separating them with a new line.
- Save the configuration.

3. Test the Setup

- Send an email to the masked email address, e.g., `info@domain.tld`.
- Check your main email (`personal@main.tld`) to confirm the forwarded message is received.
