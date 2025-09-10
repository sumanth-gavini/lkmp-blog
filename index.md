---
title: "My Linux Kernel Mentorship Journey"
date: 2025-09-10
author: Sumanth Gavini
tags: [Linux Kernel, Mentorship, Open Source, Backporting, sysfs_emit, syzbot]
---

## Introduction

My expiernce with the Linux Kernel Bug Fixing [Summer 2025] Mentorship Program

Summer 2025 - https://mentorship.lfx.linuxfoundation.org/project/8822c262-9795-4c84-a7c8-43346e2f5974

Participating in the **Linux Kernel Mentorship Program** has been one of the most formative experiences in my career. It allowed me to work directly on upstream kernel development, collaborate with seasoned maintainers, and deliver improvements that benefit both current and stable releases.

In this blog, I’ll walk you through my contributions in two key areas:
1. **Migrating sysfs show functions** from `scnprintf()` to `sysfs_emit()`.
2. **Backporting driver fixes** to stable kernel branches.

You can also explore my contributions and patches on the kernel mailing list archives: [lore.kernel.org search for Sumanth Gavini](https://lore.kernel.org/all/?q=sumanth+gavini).

---

## Cleaning Up sysfs Show Functions

During the program, I focused on modernizing sysfs output helpers by replacing legacy `scnprintf()` calls with the recommended `sysfs_emit()` in `*_show()` functions.

### Why This Change Matters

- **Consistency**: Kernel documentation (`Documentation/filesystems/sysfs.rst`) specifies using `sysfs_emit()` for formatted sysfs output.
- **Safety**: `sysfs_emit()` manages buffer bounds correctly, minimizing risks like overflow or formatting bugs.
- **Code Quality**: Streamlines the codebase and reinforces a unified coding style across subsystems.

### Example Contributions

- **USB Audio Gadget (f_uac1)**  
  [commit bb76f0d843a2](https://github.com/torvalds/linux/commit/bb76f0d843a26d11bed5df2793b492ca414de0a4)

- **USB Audio Gadget (f_uac2)**  
  [commit 7168c06d9ba0](https://github.com/torvalds/linux/commit/7168c06d9ba0932466272ac8bfbdd793a4fab636)

While subtle, these updates enhance consistency with kernel style guidelines and improve long-term maintainability.

---

## Backporting Driver Fixes to Stable

A significant part of my mentorship effort involved backporting patches to the stable kernel series (`linux-6.1.y`), a critical step to ensure reliability for production-grade systems.

### My Backport Contributions

- **HID MCP2221 Driver**  
  [hid-mcp2221.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/drivers/hid/hid-mcp2221.c?h=linux-6.1.y&id=0499d5d579d4e552f5c67d74e56b150de31369d5)

- **Dummy Network Driver**  
  [dummy.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/drivers/net/dummy.c?h=linux-6.1.y&id=30c8ec6997edf393e6cba83e4753607d490751d8)

- **Bluetooth HCI Sync**  
  [hci_sync.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/net/bluetooth/hci_sync.c?h=linux-6.1.y&id=cd55c13bbb3d093ae601aa97e588ed4c1390ebb1)

### Why Backporting Is Important

- **Stability**: Allows users of long-term kernel releases to benefit from upstream fixes without migrating to a new major version.
- **Reliability**: Especially valuable for embedded, industrial, and automotive systems that prioritize stability.
- **Learning**: These backports honed my skills in navigating older codebases and resolving conflicts during adaptation.

---

## Tools & Debugging

I relied on a suite of powerful tools and techniques throughout the process:

- **cscope/ctags + ripgrep** — Efficient code navigation and search.
- **smatch** — Static analysis to detect coding issues early.
- **make htmldocs** — Validating documentation changes.
- **syzbot** — An automated kernel-fuzzing system powered by Syzkaller.
  - I used **syzbot reproducible crash reports**, especially C reproducers, to pin down and fix bugs reliably.
- **QEMU/KVM** — Virtualized environments for testing instrumented kernel builds.
- **gdb/objdump** — Core tools for debugging kernel crashes.
- **printk/ftrace** — Low-level tracing and runtime diagnostics.

These tools not only accelerated development but also mirrored the workflows of seasoned kernel collaborators.

---

## Key Learnings

- **Documentation Is Vital**: Even minute details in kernel guides (like `sysfs_emit`) can shape patch acceptance.
- **Embrace the Review Process**: Submitting patches taught me to write clear commit messages, comply with coding norms, and incorporate feedback.
- **Mastering Backports**: I developed the ability to adapt modern fixes to legacy kernels and verify their applicability.
- **Understanding syzbot and Fuzz Testing**: Debugging syzbot reports gave me insights into proactive quality engineering for kernel robustness.

---

## References

- [Linux Kernel Mentorship Program](https://wiki.linuxfoundation.org/lkmp)  
- [Kernel Mailing Lists (lore.kernel.org)](https://lore.kernel.org)  
- [Patchwork (patch tracking)](https://patchwork.kernel.org)  
- [Subspace (kernel forums)](https://subspace.kernel.org/)  
- [Syzbot Dashboard](https://syzkaller.appspot.com/upstream)  
- [Kernel.org main site & docs](https://www.kernel.org/) / [Documentation](https://docs.kernel.org)  
- [Kernel CI Dashboard](https://dashboard.kernelci.org/tree)  
- [Submitting Patches Guide](https://www.kernel.org/doc/html/latest/process/submitting-patches.html)  
- [Cregit (Code Review Tool)](https://github.com/cregit/cregit)  
- [Kernel Newbies (Community Resources)](https://kernelnewbies.org)  
- Articles & Tutorials:
  - [How to Send a v2 Patch](https://staticthinking.wordpress.com/2022/07/27/how-to-send-a-v2-patch/)  
  - [Using lei & b4 for Patch Troubleshooting](https://josefbacik.github.io/kernel/2021/10/18/lei-and-b4.html)  
  - [b4 for Kernel Contributors](https://hackerbikepacker.com/b4-for-kernel-contributors)  
  - [Exploring syzbot](https://hackerbikepacker.com/syzbot)  
  - [Journey to Becoming a Kernel Contributor](https://hackerbikepacker.com/kernel-contributor-1)

---

## Acknowledgments

I extend heartfelt thanks to the **Linux Foundation** for facilitating this mentorship opportunity.

Special appreciation to my mentors:  
- **Shuah Khan** — [Mentor Profile](https://mentorship.lfx.linuxfoundation.org/mentor/5b5c6ac7-5735-4ed6-9666-4ddd0a140c0c)  
- **David Hunter** — [Mentor Profile](https://mentorship.lfx.linuxfoundation.org/mentor/9826853a-13a2-4397-8bdb-9f4f2b6aad62)

Their mentorship, feedback, and encouragement have been invaluable to my growth as a kernel developer.

---

## Conclusion

My journey through the Linux Kernel Mentorship Program involved enhancing **code consistency** (`sysfs_emit`), improving **stable branch reliability** (driver backports), and gaining hands-on experience with professional tools like **syzbot**. More importantly, it deepened my appreciation for the rigor and collaboration that drive Linux kernel development forward.

I'm excited to continue contributing to core areas like USB, HID, networking, and real-time Linux.

---

