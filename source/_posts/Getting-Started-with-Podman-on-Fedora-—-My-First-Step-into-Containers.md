---
title: Getting Started with Podman on Fedora — My First Step into Containers
date: 2025-06-11 09:03:23
tags:
- Containers
- Linux
- Fedora
---

# What Even _Is_ Podman?

If you're like me and haven't touched Docker much (beyond reading a few how-tos), hearing about **Podman** might make you wonder: _"Do I need to know Docker first?"_

Short answer? **No**.

Podman is a container engine that lets you run lightweight, isolated environments on your system—perfect for spinning up things like databases, dev environments, or small apps.

The cool part? Podman works **without needing a big background service (daemon)** running all the time. Every time you launch a container, Podman runs it directly—no extra layers.

It’s developed by Red Hat, so it’s deeply integrated into **Fedora**, which is where I discovered it.

# Why I Started Using Podman

I didn’t come from Docker. I just needed a way to:

- Run multiple instances of things like **PostgreSQL**, **MariaDB**, and some testing environments
- Keep them separate, easy to start and stop
- Avoid installing them system-wide

Since **Podman is included by default in Fedora**, it made sense to give it a try.

With a single command like:

```bash
podman run -d --name my-postgres -p 5432:5432 postgres
```

…I had a working PostgreSQL container, isolated from the rest of my system. No `dnf install postgres`, no system-wide setup—just one portable container.

# What’s the Deal with Docker?

So, do you need to know Docker to use Podman? Not really. But it helps to understand the comparison because:

- **Most online container tutorials use Docker** commands
- **Podman is mostly compatible** with those commands

In fact, you can alias it:

```bash
alias docker=podman
```

Podman is designed to be a drop-in replacement, but it's also different in key ways.

Here’s how I understand it:

| Docker                                 | Podman                                         |
| -------------------------------------- | ---------------------------------------------- |
| Needs a background daemon              | No daemon needed (runs per-command)            |
| Typically runs as root                 | Can run rootless (as normal user)              |
| No pod concept                         | Native pod support (Kubernetes-style)          |
| Windows/mac support via Docker Desktop | Podman uses lightweight VMs or WSL2            |
| Community default                      | Integrated into Fedora (and Red Hat ecosystem) |

Since I started from scratch, Podman just felt simpler and more “Linux-native.” I didn’t have to install or configure anything extra—it was already there.

# My Early Experience

I’ve used Podman to:

- Run multiple containers with different databases for dev/testing
- Stop and clean them up easily
- Avoid polluting my host system with conflicting packages

And I’m just scratching the surface. There’s pod support, systemd integration, and even rootless containers—which I haven’t explored much yet, but they seem powerful.

# Final Thoughts

If you're on Fedora (or any Linux distro, really) and need to run isolated apps or services, Podman is a great starting point—**especially if you’ve never touched Docker**.

It’s approachable, powerful, and doesn’t require buying into an ecosystem or installing bulky extras.

And if you're curious about containers but don’t want to commit to a complex setup: Podman might be the right first step.
