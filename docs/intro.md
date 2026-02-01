# Introduction to Linux

- Welcome page and syllabus: <a href="https://hpc2n.github.io/linux-command-line-101/intro/">https://hpc2n.github.io/linux-command-line-101/intro/</a>
    - Also linked at the mini terminal on the top left of the page. 

## What is Linux

!!! note 

    Most of the commands you learn in this course are agnostic and should work on any Linux/Unix like system. macOS is a Unix based operating system, and the majority of the commands are the same. 

Linux is a family of open-source Unix-like operating systems based on the Linux kernel, an operating system kernel first released on September 17, 1991, by Linus Torvalds.

An operating system kernel is the software that sits underneath all of the other software on a computer, managing the computer’s hardware (CPU, GPU, memory, storage...) and handling the connections between your other software and the hardware.

Linux is:

* Multitasking capable
* Multi user system
* Open source
* Free of charge

Linux is typically packaged as a Linux distribution, which includes the kernel and supporting system software and libraries, many of which are provided by the GNU Project.

In addition, a windowing system of some sort (X11, Wayland) interfaces directly with the underlying operating system and libraries, providing support for graphical hardware, pointing devices, and keyboards. The window manager generally runs on top of this windowing system.

!!! Note "Distributions (distros)"

    There are many Linux distribuitions, including Ubuntu, Debian, Fedora, Gentoo, and many others. Most distributions are free and open source, but there are also commercial distributions, like Red Hat Enterprise and SUSE.

    Desktop Linux distributions include <a href="https://en.wikipedia.org/wiki/Desktop_environment" target="_blank">a desktop environment</a>, like GNOME, MATE, KDE Plasma, Xfce, Unity, or many others. Most of what the user sees is provided by a window manager and applications written using a widget toolkit.

## Shells

A shell is an interface between the keyboard and the operating system (OS), i.e., it takes commands the user gives via the keyboard and sends it to the OS. The OS then performs the actions requested. 

There are several shells designed to work with Linux/Unix systems, each of which has somewhat different properties and syntax: 

- The Bourne Shell (sh)
- **The GNU Bourne-Again shell (bash)**
- The C shell (csh)
- The TENEX C shell (tcsh)
- The Korn Shell (ksh)
- The Z Shell (zsh)

!!! Important 

    Most centers have ``bash`` as default. There are several reasons, but one is that it compatible with SLURM---the batch scheduler used at most centers in Sweden. The ``bash`` shell is also good for scripting.

    For the majority of the material in this course, it does not matter which shell you are using, but there are some commands where it is relevant. We will therefore be using ``bash`` for this course.

## Why Linux/Unix (shell) 

The Linux/Unix shell has existed for a very long time (Thompson shell, 1971; Bourne shell, 1979). 

It continues to be used because it is a very powerful tool that lets users perform complex tasks. These tasks can often be done using a few keystrokes or maybe a few lines of code. 

It can be used to automate repetitive tasks or to combine smaller tasks into **scripts**, which helps the user work faster and more effectively. 

Using the Linux/Unix shell is fundamental for a large number of advanced computing tasks, including in HPC (high-performance computing). 

In addition, most HPC clusters run some flavour of Linux because it:

- Is stable and reliable
- Is customisable
- Is lightweight
- Runs on any hardware
- Has a strong support community
- Has many flavours that are open-source and free
- Has lots of applications

While Linux is only used on about 3% of desktops, the vast majority of web servers (>96%), most mobile devices (Android is based on the Linux kernel), and all supercomputers on the <a href="https://en.wikipedia.org/wiki/TOP500" target="_blank">Top500 list</a> run Linux. In line with this: **NAISS services use Linux**.  

For all of these reasons, and many more, it is a good idea to be proficient in Linux. This course aims to help you with that.

!!! seealso "See also"

    There is much more information about <a href="https://en.wikipedia.org/wiki/Linux" target="_blank">Linux on Wikipedia</a>.
    
    Some pages with guides and/or cheat sheets: 
    
    - <a href="https://linuxhandbook.com/" target="_blank">The Linux Handbook</a>
    - <a href="https://www.geeksforgeeks.org/linux-tutorial/" target="_blanks">https://www.geeksforgeeks.org/linux-tutorial/</a>
    - <a href="https://itsfoss.com/free-linux-training-courses/" target="_blank">14 Free Training Courses to Learn Linux Online</a>
    - <a href="https://tldp.org/LDP/intro-linux/intro-linux.pdf">Introduction to Linux - A Hands on Guide</a>
    - <a href="https://cloudacademy.com/course/linux-fundmentals-1346/the-linux-directory-structure/" target="_blank">Linux Fundamentals</a>
    - <a href="https://www.digitalocean.com/community/tutorials/linux-commands" target="_blank">Top 50+ Linux Commands You MUST Know</a>
 
