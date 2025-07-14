---
title: 'Living with Linux: My Evolving Experience as a Daily Driver'
date: 2025-07-14 10:21:23
tags:
- Linux
- Fedora
---

In early 2025, I moved full-time to Linux—part out of curiosity, part out of a desire for more control. Since then, I’ve experienced the ups and downs of daily life with this open-source ecosystem: from unexpected crashes to surprising stability, from frustration to fascination.

## 🎮 Gaming Is Surprisingly Smooth

Gaming on Linux has become far more approachable. I’ve been playing _House of Legacy_ using Steam with **Proton**, and it runs great—smooth framerate, no stutters, and no crashes so far.

Even better, I’ve been able to use a **Windows save editor** by accessing the compatibility layer’s save directory such as:

```bash
~/.steam/steam/steamapps/compatdata/<game-id>/pfx/drive_c/...
```

It takes a little digging, but once you know where to look, it works just like it would on Windows.

## 💻 Terminal Customization That Works for Me

Linux has completely changed how I interact with my system—especially through the terminal.

#### Zsh + Oh My Zsh

I use **Zsh** with **Oh My Zsh** as my shell environment. It gives me a cleaner, more productive terminal with:

- Command autosuggestions
- Git-aware prompts
- Theme support
- Aliasing for commonly used commands

On top of that, I’ve added some essential extensions:

- **Syntax highlighting** for better command readability
- **Directory tree tools** for navigating large folder structures
- Colorized `ls` output and a better-looking prompt

This setup feels comfortable and efficient. It’s not overly flashy—but it gets out of my way and helps me get things done.

## 🪟 Minimal Use of Tmux, But It Helps

I don’t live inside **tmux**, but when I need to run multiple terminal processes—especially during coding, deployments, or watching logs—it’s incredibly useful.

Without custom configuration, even the basics are powerful:

- Vertical and horizontal pane splitting
- Session persistence across terminal tabs
- Easy process management from a single window

It’s like having a mini tiling window manager inside my terminal.

## 🪟 Window Tiling? Sort of.

I don’t use a dedicated tiling window manager like `i3` or `bspwm`. Instead, I rely on **GNOME extensions** that mimic tiling behavior. It’s less hardcore, but it’s effective enough for how I work.

With simple keyboard shortcuts and snapping features, I can:

- Split the screen between terminal and browser
- Keep my editor and file manager side by side
- Stay organized without having to drag and resize windows manually

It’s the right balance of convenience and control for me.

## 🧱 Surviving a Kernel Panic

One of the first major issues I encountered was a **kernel panic** after updating to **kernel 6.15**. On reboot, the system wouldn’t load—just a wall of logs and a frozen screen. No GUI. No terminal. Nothing.

Luckily, GRUB still listed **kernel 6.14**, which booted without issue. I quickly rolled back and marked it as a lesson learned: **don’t rush into kernel updates**. Especially when the current version is already stable.

## ⚠️ Compatibility Challenges After Updates

Another thing I ran into: **application compatibility breaking after updates**. A few packages I regularly used stopped working properly. One of them just wouldn’t launch at all.

The fix required manually upgrading some dependencies. Not overly complex, but it taught me to always:

- Check what a system update is touching
- Keep track of critical tools
- Avoid full updates right before deadlines or busy days

With Linux, **you get the latest tech**, but sometimes, you need to be your own support technician.

## 🔧 It Feels Like My Computer Now

This is what Linux gives me—**real ownership**. I control how it looks, how it runs, how it updates, and what it prioritizes.

That said, it’s not always smooth. I’ve run into unexpected roadblocks—like SELinux interfering with custom nginx configurations. Trying to serve files from non-default directories led to permission denials, even when ownership and chmod settings looked correct.

It turns out SELinux had tighter controls behind the scenes, and I had to learn about setting the correct security contexts. Not exactly plug-and-play—but another opportunity to understand my system more deeply.

Every fix like that feels earned. And once it’s fixed, it tends to __stay__ fixed.

## ☕ Final Thoughts

Linux isn’t perfect. Things break. Updates demand attention. And sometimes you’ll spend half an hour fixing something that used to “just work.”

But every fix teaches you something. Every configuration deepens your connection with the machine. Over time, it becomes more than an OS—it becomes a **craft**.

Maybe the distro I use is still considered generic or beginner-friendly. I’m not building my system from scratch like the hardcore `Arch` or `Gentoo` users. But you know what?

**It works for me.**

And that’s what really matters.