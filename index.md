---
title: "My Linux Kernel Mentorship Experience"
layout: default
---

# My Linux Kernel Bug Fixing Mentorship Journey

* TOC
{:toc}

## Introduction

I joined the Linux Kernel Bug Fixing Mentorship to gain real experience contributing to the kernel, understand how development happens on LKML, and get comfortable with debugging workflows. Over the weeks I submitted small cleanup patches, attempted syzbot reports, and learned to navigate both the codebase and the community.

This post focuses on the non-technical side of my journey—what I learned from the process and the community. I’ll write/refer to technical details and workflows in separate posts.

---

## Getting Started

My first contributions were cleanup patches: replacing `scnprintf()` with `sysfs_emit()`, fixing documentation warnings, and cleaning up kselftest files. These patches may look small, but they taught me how to write proper commit messages, follow coding style, and interact with maintainers. That foundation was critical before tackling harder bugs.

---

## Working with syzbot

A big part of the mentorship was learning syzbot. The workflow I followed was:

1. Fetch report from the dashboard.
2. Reproduce locally with repro.c under QEMU.
3. Read logs and backtraces to locate the issue.
4. Decide whether it’s something actionable or out of scope.

Not all attempts succeeded. Some reproducers didn’t crash, others hit optimized-out values in `gdb`, and some bugs (like locking or deep filesystem issues) were beyond what I could solve during the mentorship. Still, working through them gave me insight into debugging real kernel problems.

---

## Challenges

I avoided categories like stack corruption, deadlocks, and subsystem-specific bugs (e.g. XFS, bcachefs). They require deep knowledge I haven’t built yet. Instead, I focused on bugs I could at least analyze. Even when I didn’t submit a patch, documenting what I learned was valuable.

---

## Tools

Some of the tools I relied on:

- **cscope/ctags + ripgrep** – code navigation
- **smatch** – static analysis
- **make htmldocs** – verifying doc fixes
- **syzbot repros** – mainly C repros for easier debugging
- **QEMU/KVM** – running instrumented kernels
- **gdb/objdump** – debugging crashes
- **printk/ftrace** – runtime tracing

---

## Reflection

My contributions were modest, but I learned how to use kernel workflows, tools, and debugging practices. The main gaps I saw were time and lack of subsystem specialization. I came into this mentorship with many questions, found answers to some, and left with even more to explore.

What made the biggest difference was the support of Shuah Khan, the mentees, and ex-mentees. Their feedback and willingness to answer questions helped me get unstuck and move faster than I would have on my own. It showed me how much the community aspect matters in kernel development.

---

## Closing Thoughts

This program was an important step in my journey. Thanks to Shuah Khan, the mentees, and the wider community for making it such a valuable experience. I now feel more confident about continuing to learn and contribute to the Linux kernel.