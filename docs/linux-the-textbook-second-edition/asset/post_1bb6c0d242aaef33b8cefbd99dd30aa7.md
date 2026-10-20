
### 18.1.1 Some Prerequisites

Although much of the material in this chapter can be done without having done anything else in this book, there are some things which we assume that you have done in preparation for your work here.

The following is a list of those prerequisites, from specific to general knowledge of material covered:

- 1. Knowing the structure of a Linux command and having basic mastery of file maintenance commands.
- 2. Being familiar with the materials presented in the core chapters of this book, Chapters 3–11.
- 3. Basic and advanced Bash shell programming as shown in Chapters 12 and 13.
- 4. Having read through and referring to Chapter 17 on system administration.

An overview of the top-down architecture of the components of systemd is given in Figure 18.1.

You should first understand and follow these instructive points we make about Figure 18.1:

- 0. Things (from the point of view of the user typing Utility Commands available at the top level of Figure 18.1) work in a descending order, from highest to lowest layers.
- 1. Starting at the top layer, the Utility Commands are what you can type at the Linux command line. These commands implement the user-side, front end to systemd. The most prominent and important one, the systemctl command, is detailed in Section 18.3.
- 2. The next layer contains Daemons and Targets. systemd Daemons are what control all other Linux daemons, and services, including systemd itself. Targets are basically operating states you can put Linux in.

![](img/2a18e06cd9c6395e451f26126ecba1fd_633_0.png)

FIGURE 18.1 systemd architecture.

- 3. The next layer contains the Core features, most prominently Units. Units are what describe and define services, affecting everything in Linux service management. Units affect everything in Linux.
- 4. The next layer, Libraries, contains what the upper layers call upon to get their work done.
- 5. The lowest layer, the Kernel, is where cgroups and other kernel modules do all of the essential control. That is why cgroups, and their application to systemd, are one of the most important features of systemd for the system programmer. We cover cgroups from the user’s perspective in Chapter 17, Section 8.1.2.

For example, a user executes a correctly formulated systemd command on the command line. This command is passed through the Daemons and Targets layer and affects appropriate modules in that layer. These modules in turn affect Core layer modules, such as invoking or executing a Target Unit. This invocation or execution uses the library modules in the lower layer to change the state of the Kernel at that lowest layer.

Units, Targets, and the systemctl command are the most important items in the context of the diagram, particularly for a novice user trying to understand systemd.

### 18.1.2 Where to Get Further Help and Documentation

Documentation for systemd exists right on your Linux system!

We encourage you to read through and generally refer to the following man pages on your system (or on the Internet). Starting from the top, and arranged in order of detail, you can use these man pages to gain further and more complete information about the specific topics that we cover in this chapter:

```
systemd.unit, systemd.target, systemctl,
systemd.special, systemd.directives, systemd.service, journalctl
systemd.socket, systemd.device, systemd.mount, systemd.automount, systemd.swap,
systemd.path, systemd.timer, systemd.scope, systemd.slice, systemd.snapshot
```

These man pages can serve as an electronic reference library, directly on your Linux system, for systemd. For example, if you don’t remember the exact meanings of, and how to apply, the arguments to the systemctl command, you can refer to its man page on your system to refresh your memory!

### Exercise 18.2

Carefully read through the man pages on your system for systemd.unit, systemd.target, and systemctl, and then write a brief, paragraph-long summary, in your own words, that will assist you with each topic. Then refer to these summaries when doing the remainder of the work we show in this chapter and in Chapter W27 at the book website.

## 18.2 System Start-Up, Initialization, and Shutdown Using systemd

To begin to understand what systemd is, and part of what it achieves as a “superkernel,” we examine the first and last major tasks that systemd accomplishes for the Linux operating system—start-up and shutdown. The first of these tasks is what systemd was introduced for: to more effectively and efficiently replace the older UNIX and Linux init systems. But, as you explore more of this chapter, you will come to understand that systemd is much more than this.

### 18.2.1 An Overview of the Start-Up and Shutdown Processes

The basic details of how a Linux system that is using systemd boots and starts up are given in Chapter 17, Section 2.5. In this section, we further expand upon the particulars of the start-up phase, with regard to the systemd-specific steps involved.

As seen in Chapter 17, several processes come into play even before systemd as an initialization program takes over during system start-up. Figure 17.1 illustrates booting with POST, BIOS or UEFI, GRUB, and then start-up, where the kernel initializes hardware and prepares for the first process to be run from the root file system. After the root file system is found and mounted, systemd takes over and is then responsible for initializing all remaining hardware, mounting all necessary file systems, managing the start of system services, and allowing fine-grained control over all processes.

On shutdown, systemd stops all services and unmounts all file systems (detaching the storage programs handling them). The system is then either rebooted or finally powered down.

### Exercise 18.3

What process is Process Identification number 1 (PID 1) on your system, and how did you find this out?

### Exercise 18.4

Describe, in your own words, the differences between the boot process and the start-up process in Linux. Refer specifically to the steps the system goes through to achieve the states that it is in during those general processes.

### 18.2.2 systemd Start-Up: Targets, Target States, and Target Units

After the boot phase is over, systemd is the controlling component of the start-up phase, and is responsible for the completion of start-up. It does this by initializing the required file systems, services, and drivers that are necessary for the normal operating condition of the system. With systemd, this process is split up into “run-time” steps (operations that happen as the system is actually executing in real time), whose objectives are to reach required, or requested, “target states,” formerly known as “run levels” in UNIX and Linux jargon. The entire process is done as much as possible in parallel. This parallelism achieves a significantly faster start-up time, a hallmark of systemd-controlled Linux. The start-up procedure also has no fixed path through it, so that the order in which “target units” are reached is determined when the system is actually started up. We give a complete definition, and provide examples, of targets, target states, and target units, in the sections that follow.

“Dependencies” are sequentially ordered relations between target units. When systemd takes over the start-up phase, it first activates target units that are upstream dependencies of a target state known as the default.target, and then proceeds to activate all other downstream dependencies. default.target is an alias of graphical.target or multi-user.target, depending on whether the system by default has been configured for a GUI (on a desktop system, for example) or only for a text console, CUI (on a server system, for example). Generally, desktop users prefer the GUI environment because of its graphical interactive operations and window system. Servers generally have a CUI because of the low memory and resource overhead involved in operating at that target state. It is important to realize that both use cases have very specific performance requirements, and therefore different target unit activation requirements as well.

Figure 18.2 shows the ordering of “milestone” target unit descriptions reached according to whether a GUI graphical.target or CUI multi-user.target state is ultimately reached. The arrows describe which units are called in what order, from top to bottom.

In terms of target unit dependencies, targets higher up in the diagram are the dependencies of targets lower down in the diagram.

Some representative milestone target units, in the order that they are called, are as follows: local-fs-pre.target, sysinit.target, basic.target, and graphical.target. Other target units, such as timers.target, are called by basic.target, and can affect system state when their “dependencies,” i.e., the resources and other target states that depend on them, require it.

### Exercise 18.5

Why do you think that multi-user.target is a necessary prerequisite of achieving the graphical.target state of the system?
