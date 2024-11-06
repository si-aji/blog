---
title: 'Valet: Isolate PHP Version for Each Projects'
date: 2024-11-06 10:49:21
tags:
- Valet
- PHP
category:
- Development Tools
- Valet
---

When working with multiple Project, sometime we need different PHP version for each project. Just like when we are working for older project that still use older Laravel version, we need to change our PHP version to match with the project requirement. Fortunately, Laravel Valet makes it easy to isolate PHP versions for each project, ensuring that your development environment stays flexible and compatible with your projects' requirements.

## Prerequisites
- You should have **Laravel Valet** installed on your system. If you haven’t installed it yet, follow the official [Valet installation guide](https://laravel.com/docs/11.x/valet).
- You’ll need Homebrew and PHP versions installed on your machine.

## Step 1: Install Multiple PHP Versions
Before you can switch between php version, you'll need the PHP version it's self. You can use Homebrew to install PHP versions.

```bash
brew install php@7.4
brew install php@8.0
brew install php@8.1
```

Once installed, you can check the available PHP versions by running:

```bash
brew list | grep php
```

## Step 2: Switch PHP Versions Globally
To set a global PHP version (for Valet), you can use the following command:

```bash
valet use php@8.0
```

This command sets PHP 8.0 as the default PHP version for Valet.

## Step 3: Isolate PHP Version for a Specific Project
Now, let’s isolate a different PHP version for a specific project.

1. Navigate to the project’s root directory.

```bash
cd ~/Sites/my-project
```

2. Run the following command to isolate the project’s PHP version:

```bash
valet use php@7.4
```
This will switch the PHP version to 7.4 just for that project, while other projects will continue to use the globally set version.

## Step 4: Verify the PHP Version
You can verify the PHP version that Valet is using for a project by running:

```bash
php -v
```

This should output the PHP version currently in use for that project. However, sometimes running php -v might not show the correct PHP version, especially if it’s still pointing to the default PHP version installed on your system, not the one used by Valet. Let’s see how to resolve that.

## Fixing the `php -v` Version Output
If `php -v` shows the wrong PHP version (the default PHP version instead of the Valet PHP version), it’s because the terminal is still using the system's default PHP command. To resolve this, we need to add an alias to ensure the correct PHP command is used by Valet.

1. Open your shell configuration file (e.g., `.bash_profile`, `.zshrc`, `.bashrc`):
```bash
nano ~/.zshrc  # or ~/.bash_profile for bash users
```

2. Add the following alias command to your file:
```bash
alias php='valet php'
```
This ensures that every time you type php, the command will use the PHP version managed by Valet, rather than the system’s default PHP version.

3. Save the file and restart your terminal or reload the shell configuration:
```bash
source ~/.zshrc  # or source ~/.bash_profile for bash users
```

4. Now, run `php -v` again, and it should display the correct PHP version being used by Valet for the current project.

You can always check which PHP version is active by using the php -v command and verify the project’s PHP version.