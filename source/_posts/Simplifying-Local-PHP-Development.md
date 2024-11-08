---
title: Simplifying Local PHP Development
date: 2024-11-06 10:05:24
tags:
- Valet
- Herd
- XAMPP
- Laragon
- Development Tools
category:
- Development Tools
---

When it comes to local development, especially for PHP and Laravel projects, choosing the right tools will make our life easier. There are a lot of options out there, from classic choice like XAMPP or even Laragon, to newer Laravel focused solution like Valet and Herd. We will try to dive even further to compare the development tools.

## XAMPP
XAMPP has been around for years as go-to solution for setting up Apache, MySql, PHP and Perl. It's been used by many developer out there, or even many school when teaching to the students. It’s a general-purpose local development tool, suitable for various environments.

### Key Features
- **Apache-Based**: Runs on the Apache server, which is useful for projects that need to mimic typical production environments.
- **Cross Platform**: Available on Windows, macOS, and Linux, making it versatile.
- **GUI Interface**: Offers a control panel for managing services like MySQL, FTP, and SMTP.

### Pros
- Flexible and cross-platform, so it’s easy to move projects between operating systems.
- Offers a full server environment, which is useful for non-Laravel or mixed-stack projects.

### Cons
- Can be resource-heavy, especially if you only need a lightweight PHP environment.
- Setting up individual projects with virtual hosts and routing can be more cumbersome compared to modern tools like Laragon, Herd or Valet.

---

## Laragon
Somewhat like XAMPP, but more modern. It's only available on Windows, and provides a complete local development stack

### Key Features
- **Auto routing**: Laragon can automatically create local domains for your projects (only applied to specified directory), similar to Herd and Valet
- **Multi-Environment Support**: Supports PHP, Apache, Nginx, MySQL, and even Node.js, making it suitable for multi-stack development.
- **PHP Switching**: Easily switch between different PHP versions for compatibility testing.

### Pros
- Lightweight and fast, with less overhead than XAMPP.
- Perfect for Windows users needing a flexible but modern development tool.

### Cons
- Windows-only, so not suitable for macOS or Linux users.
- Limited Laravel-specific integrations compared to Herd and Valet.

---

## Valet
Valet is Laravel-developed tool, designed to keep your development environment as lightweight as possible. It’s perfect for developers who want minimal overhead and an easy way to access local sites.

### Key Features
- **Single Nginx Server**: Unlike Apache-based environments, Valet runs a single Nginx instance, which uses less memory and is very responsive.
- **Automatic TLD Routing**: Projects are automatically available at a .test domain (e.g., projectname.test), saving you from having to configure virtual hosts manually.
- **Compatibility**: Works seamlessly with MySQL, Redis, and even third-party tools like Node.js.

### Pros
- Minimal resource usage; doesn’t require a full virtual machine.
- Automatic, user-friendly URLs for quick access to projects.

### Cons
- macOS-only, limiting its accessibility.
- Primarily for PHP-based projects, and not ideal for other stacks.
- CLI based, there's no graphical interface supported (there's a package that support minimal graphical interface for Valet, called [PHP Monitor](https://github.com/nicoverbruggen/phpmon))

---

## Herd

The newest Laravel-developed tools, just like Valet but with more support to Windows platform. It aims to simplify the process of setting up a full-stack environment without the usual hassle.

### Key Features
- **Easy Setup**: Herd provides a pre-configured environment for PHP, MySQL, and Redis, among others.
- **PHP Switching**: Quickly switch PHP versions, which is handy for testing projects across different PHP environments.
- **User-Friendly GUI**: Unlike command-line setups, Herd offers a graphical interface, making it accessible even for beginners.

### Pros
- Great for Laravel projects; everything is pre-configured and optimized.
- Lightweight and tailored specifically for PHP and Laravel workflows.

### Cons
- Unavailable for Linux users
- Not as versatile for non-PHP projects.

---

## Comparison Table

| Feature                | XAMPP                 | Laragon               | Valet                 | Herd                  |
|------------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| **Platform**           | Cross-Platform        | Windows               | macOS                 | macOS & Windows       |
| **PHP Version Switch** | ❌                    | ✔️                    | ❌                    | ✔️                    |
| **Auto-Routing**       | ❌                    | ✔️                    | ✔️                    | ✔️                    |
| **Lightweight**        | ❌                    | ✔️                    | ✔️                    | ✔️                    |
| **Full Environment**   | ✔️                    | ✔️                    | ❌                    | ❌                    |

## Conclusion

Choosing the best development tool varies from developer to developer, as there are many factors that influence individual needs and workflows. Each tool has its strengths, so try a few to see which aligns best with your development style and project requirements!