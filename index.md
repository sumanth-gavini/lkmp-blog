---
title: "My Linux Kernel Mentorship Journey"
date: 2025-09-10
author: Sumanth Gavini
tags: [Linux Kernel, Mentorship, Open Source, Backporting, sysfs_emit, syzbot, Community]
---

## Introduction  

My expiernce with the Linux Kernel Bug Fixing [Summer 2025] Mentorship Program

Summer 2025 - https://mentorship.lfx.linuxfoundation.org/project/8822c262-9795-4c84-a7c8-43346e2f5974

Participating in the **Linux Kernel Mentorship Program** has been one of the most transformative experiences in my career. Over the past months, I had the privilege of working on upstream kernel contributions, collaborating with mentors, and learning from both fellow mentees and the broader kernel community.  

In this blog, I’ll share:  
1. My **technical contributions** (sysfs cleanup & driver backports).  
2. The **tools and debugging methods** I relied on.  
3. What I learned from **mentors, fellow mentees, and the Linux kernel community**.  
4. Key takeaways and reflections from this journey.  

You can also explore my contributions on the mailing list archives: [lore.kernel.org search for Sumanth Gavini](https://lore.kernel.org/all/?q=sumanth+gavini).  

---

## Cleaning Up sysfs Show Functions  

One of my first tasks was migrating sysfs `*_show()` functions from `scnprintf()` to the newer `sysfs_emit()` helper.  

### Why This Change Matters  

- **Consistency**: Kernel documentation (`Documentation/filesystems/sysfs.rst`) mandates `sysfs_emit()` in sysfs functions.  
- **Safety**: It handles buffer boundaries correctly, minimizing risks of overflow.  
- **Maintainability**: Brings consistency across kernel subsystems.  

### Example Contributions  

- **USB Audio Gadget (f_uac1):**  
  [commit bb76f0d843a2](https://github.com/torvalds/linux/commit/bb76f0d843a26d11bed5df2793b492ca414de0a4)  

- **USB Audio Gadget (f_uac2):**  
  [commit 7168c06d9ba0](https://github.com/torvalds/linux/commit/7168c06d9ba0932466272ac8bfbdd793a4fab636)  

Though small, these patches aligned the code with kernel best practices and improved quality.  

---

## Backporting Driver Fixes to Stable  

I also worked on **backporting patches** to long-term stable (LTS) branches (`linux-6.1.y`), ensuring reliability for production systems.  

### My Backport Contributions  

- **HID MCP2221 Driver:**  
  [hid-mcp2221.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/drivers/hid/hid-mcp2221.c?h=linux-6.1.y&id=0499d5d579d4e552f5c67d74e56b150de31369d5)  

- **Dummy Network Driver:**  
  [dummy.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/drivers/net/dummy.c?h=linux-6.1.y&id=30c8ec6997edf393e6cba83e4753607d490751d8)  

- **Bluetooth HCI Sync:**  
  [hci_sync.c fix in linux-6.1.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/net/bluetooth/hci_sync.c?h=linux-6.1.y&id=cd55c13bbb3d093ae601aa97e588ed4c1390ebb1)  

### Why Backporting Is Important  

- **Stability:** Ensures critical fixes reach LTS users without forcing upgrades.  
- **Reliability:** Embedded, industrial, and automotive systems depend on stable kernels.  
- **Learning:** Improved my ability to adapt patches across kernel versions and resolve conflicts.  

---

## Tools & Debugging  

Some of the tools I relied on during the mentorship:  

- **cscope/ctags + ripgrep** – efficient code navigation.  
- **smatch** – static analysis for detecting issues.  
- **make htmldocs** – verifying documentation changes.  
- **syzbot** – automated fuzzing via [Syzkaller](https://github.com/google/syzkaller).  
  - Worked with **syzbot reproducers** (especially C repros) to debug crashes and verify fixes.  
- **QEMU/KVM** – running instrumented kernels in virtual machines.  
- **gdb/objdump** – analyzing and debugging kernel crashes.  
- **printk/ftrace** – runtime tracing and performance debugging.  

These tools mirrored professional workflows and deepened my debugging and analysis skills.  

---

## Learning from Mentors  

Working under **Shuah Khan** and **David Hunter** was invaluable.  

- They stressed **kernel documentation compliance**, clean patch design, and subsystem best practices.  
- Reviews taught me to write **better commit messages**, improve readability, and handle revisions.  
- I also learned how to communicate clearly on mailing lists and collaborate in a distributed open-source project.  

Their guidance gave me confidence to contribute meaningfully.  

---

## Learning from Fellow Mentees  

Being part of a cohort was equally rewarding:  

- **Peer discussions** often revealed new approaches to debugging and development.  
- **Collaboration** helped me learn different styles of structuring patches and handling feedback.  
- **Encouragement** from peers kept me motivated during challenging debugging sessions.  

---

## Learning from the Linux Kernel Community  

The broader kernel community was an incredible learning resource:  

- **Mailing lists (lore.kernel.org):** Observing discussions and reviews showed me how collaborative decision-making works.  
- **Patchwork and Subspace:** Helped me understand how patches are tracked and integrated.  
- **Syzbot & KernelCI:** Reinforced the importance of automated fuzzing and CI in maintaining kernel quality.  

---

## Key Takeaways  

- **Attention to Detail:** Even small changes like using `sysfs_emit` matter in large codebases.  
- **Collaboration First:** Open-source thrives on communication, review, and iteration.  
- **Backport Skills:** Learned how to carry modern fixes to LTS kernels.  
- **Proactive Debugging:** Gained hands-on experience with syzbot and kernel fuzz testing.  

---

## References  

- [Linux Kernel Mentorship Program](https://wiki.linuxfoundation.org/lkmp)  
- [Kernel mailing lists](https://lore.kernel.org)  
- [Patchwork](https://patchwork.kernel.org)  
- [Subspace](https://subspace.kernel.org/)  
- [Syzbot Dashboard](https://syzkaller.appspot.com/upstream)  
- [Kernel.org](https://www.kernel.org/) & [Documentation](https://docs.kernel.org)  
- [Kernel CI Dashboard](https://dashboard.kernelci.org/tree)  
- [Submitting Patches Guide](https://www.kernel.org/doc/html/latest/process/submitting-patches.html)  
- [Kernel Newbies](https://kernelnewbies.org)  
- Articles: [How to Send a v2 Patch](https://staticthinking.wordpress.com/2022/07/27/how-to-send-a-v2-patch/), [Using lei & b4](https://josefbacik.github.io/kernel/2021/10/18/lei-and-b4.html), [b4 for Kernel Contributors](https://hackerbikepacker.com/b4-for-kernel-contributors), [Exploring syzbot](https://hackerbikepacker.com/syzbot), [Becoming a Kernel Contributor](https://hackerbikepacker.com/kernel-contributor-1)  

---

## Acknowledgments  

I am deeply grateful to the **Linux Foundation** for this program.  

Special thanks to my mentors:  
- **Shuah Khan** – [Mentor Profile](https://mentorship.lfx.linuxfoundation.org/mentor/5b5c6ac7-5735-4ed6-9666-4ddd0a140c0c)  
- **David Hunter** – [Mentor Profile](https://mentorship.lfx.linuxfoundation.org/mentor/9826853a-13a2-4397-8bdb-9f4f2b6aad62)  

Their mentorship and support made this journey possible.  

---

## Conclusion  

My Linux Kernel Mentorship journey combined **technical contributions** (sysfs cleanup and stable backports) with **community learning** (mentorship, peer collaboration, and mailing list participation).  

It taught me the value of small, consistent contributions, the importance of collaboration, and the professional workflows that keep the Linux kernel reliable.  

I look forward to continuing as a contributor in kernel subsystems such as USB, HID, networking, and real-time Linux.  
