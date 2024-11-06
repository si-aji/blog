---
title: Add Command Aliases in Windows PowerShell
date: 2024-11-06 11:08:23
tags:
- PowerShell
- Windows
- Herd
category:
- Configuration
---

Unlike macOS or Linux environments, customizing terminal configuration on Windows can be a bit tricky. However, PowerShell provides a simple way to create command aliases using the `Set-Alias` cmdlet.

## Why Use Command Aliases?

Command aliases are shortcuts that allow you to use a simpler version of a command, saving time and effort, especially for long or repetitive commands. For example, instead of typing:

```bash
herd php -v
```

You could create a much shorter alias:

```bash
php -v
```

This way, you only need to type `php` instead of the full `herd php` command, improving your productivity by reducing the amount of typing for frequently used commands.

## Step 1: Open PowerShell as Administrator

Before adding aliases in PowerShell, you need to open it with administrative privileges.

1. Press `Win + X` and choose **PowerShell (Admin)**. (The exact option may vary depending on your system configuration.)

2. In the PowerShell window, type the following command to check your current execution policy:

```bash
Get-ExecutionPolicy
```

If the result is Restricted, you will need to change the execution policy to allow script execution. Run the following command to do this:

```bash
Set-ExecutionPolicy RemoteSigned
```

3. Confirm the change by typing Y and pressing Enter.

This will allow you to run local scripts and command aliases.

## Step 2: Add Aliases

PowerShell aliases are created using the `Set-Alias` cmdlet. For example, if you want to create an alias for `herd php` as `php`, you can use this command:

```bash
Set-Alias --Name php -Value "$HOME\Documents\php.bat"
```

### Why use `$HOME`?

The `$HOME` variable points to your user’s home directory, typically `C:\Users\{user}`. This ensures that the alias will work no matter where your profile is stored, making it a flexible choice.

### What is `php.bat`?

The `php.bat` file will execute the herd php command. Here’s what the contents of the `php.bat` file should look like:

```bash
@echo off
herd php %*
```

The `%*` allows you to pass any additional arguments to the `herd php` command, just like the original command would.

## Step 3: Verify the Alias

After executing the alias command, you can verify it by running:

```bash
Get-Command php
```

This will display the details of the `php` command, confirming that it’s now an alias pointing to the `herd php` command.

## Conclusion

Creating command aliases in Windows PowerShell can save you time and effort, especially when you frequently use long or complex commands. By following the simple steps above, you can easily add your own aliases to streamline your workflow and reduce repetitive typing.