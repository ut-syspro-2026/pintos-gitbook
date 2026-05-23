# 🌈 Welcome to Pintos

## Introduction

**Pintos is a simple operating system framework for the 80x86 architecture.** It supports **kernel threads**, **loading and running user programs**, and **a file system**, but it implements all of these in a very simple way. In the Pintos projects, you will strengthen its support in all three of these areas. You will also add a virtual memory implementation.

**Pintos could, theoretically, run on a regular IBM-compatible PC**. Unfortunately, it is impractical to supply every student a dedicated PC for use with Pintos. Therefore, we will run Pintos projects in a system simulator, that is, a program that simulates an 80x86 CPU and its peripheral devices accurately enough that unmodified operating systems and software can run under it. In class we will use the [Bochs](http://bochs.sourceforge.net) and [QEMU](http://fabrice.bellard.free.fr/qemu/) simulators. Pintos has also been tested with [VMware Player](http://www.vmware.com).

**These projects are hard.** They have a reputation of taking a lot of time, and deservedly so. We will do what we can to reduce the workload, such as providing a lot of support material, but there is plenty of hard work that needs to be done. We welcome your feedback. If you have suggestions on how we can reduce the unnecessary overhead of assignments, prevent students from being distracted by redundant work and help class participants concentrate on the more important underlying parts, please let us know.

## History

Pintos was originally developed at Stanford by Ben Pfaff [blp@cs.stanford.edu](mailto:blp@cs.stanford.edu) to substitute for the old OS course project Nachos. After more than a decade of iterations, Pintos has been adopted by over fifty institutes as the OS course project, including Stanford, UC Berkeley, Carnegie Mellon, Johns Hopkins, and so on. You can read the original [Pintos paper](https://benpfaff.org/papers/pintos.pdf) (Yes, they even write a paper for it !) to learn the details of Pintos' design philosophy and its comparison with other instructional operating system kernels, e.g., JOS, Nachos, GeekOS, and so on.

{% hint style="info" %}
**Why the name "Pintos"?:**

First, like nachos, pinto beans are common Mexican food. Second, Pintos is small and a "pint" is a small amount. Third, like drivers of the eponymous car, students are likely to have trouble with blow-ups. —— Ben Pfaff
{% endhint %}

## Project Overview

**There are five labs in total.** Lab0 is designed to prepare you for the later projects and practice your GDB ability, so it is intentionally much simpler than the remaining projects. In Lab1 - 4, you will extend Pintos in different dimensions and make it more robust and powerful.

| Project                       | | Content                                |
| ----------------------------- | | -------------------------------------- |
| **Lab0: Getting Real**        | | Bootstrap Pintos                       |
| **Lab1: Threads**             | | Kernel threads scheduling              |
| **Lab2: User Programs**       | | Load & Run user programs, System calls |
| **Lab3a: Virtual Memory**     | | Demand Paging                          |
| **Lab3b: Mmap Files**         | | Mmap Files                             |
| (optional) Lab4: File Systems | | Implement File systems                 |

**In each lab, we will release all the test cases to support your local development.** After the deadline, we will run the same test suite to grade your submissions, so don't worry that your evil teaching assistants (TAs) will intentionally design many corner cases only to deduct your scores.

However, your evil TAs firmly believe that there is a great difference between "elegant code" and "working code". **So a large part of your score will be determined by the quality of your design document and your code.** Don't worry, your kind TAs firmly resist "involution" and advocates "Ockham's Razor", so we will provide document templates for you to limit your document to hundreds of words long. Also, we will make the scoring criteria of coding style publicly available.
