+   3. The next layer contains the Core features, most prominently Units. Units are what describe and define services, affecting everything in Linux service management. Units affect everything in Linux.
+   4. The next layer, Libraries, contains what the upper layers call upon to get their work done.
+   5. The lowest layer, the Kernel, is where cgroups and other kernel modules do all of the essential control. That is why cgroups, and their application to systemd, are one of the most important features of systemd for the system programmer. We cover cgroups from the user’s perspective in Chapter 17, Section 8.1.2.

For example, a user executes a correctly formulated systemd command on the command line. This command is passed through the Daemons and Targets layer and affects appropriate modules in that layer. These modules in turn affect Core layer modules, such as invoking or executing a Target Unit. This invocation or execution uses the library modules in the lowest layer to change the state of the Kernel at that lowest layer.

Units, Targets, and the systemctl command are the most important items in the context of the diagram, particularly for a novice user trying to understand systemd.

# 18.1.2 Where to Get Further Help and Documentation

Documentation for systemd exists right on your Linux system!

We encourage you to read through and generally refer to the following man pages on your system (or on the Internet). Starting from the top, and arranged in order of detail, you can use these man pages to gain further and more complete information about the specific topics that we cover in this chapter:

```
systemd.unit, systemd.target, systemctl,
systemd.special, systemd.directives, systemd.service, journalctl
systemd.socket, systemd.device, systemd.mount, systemd.automount, systemd.swap,
systemd.path, systemd.timer, systemd.scope, systemd.slice, systemd.snapshot
```

These man pages can serve as an electronic reference library, directly on your Linux system, for systemd. For example, if you don’t remember the exact meanings of, and how to apply, the arguments to the systemctl command, you can refer to its man page on your system to refresh your memory!

# Exercise 18.2

Carefully read through the man pages on your system for systemd.unit, systemd.target, and systemctl, and then write a brief, paragraph-long summary, in your own words, that will assist you with each topic. Then refer to these summaries when doing the remainder of the work we show in this chapter and in Chapter W27 at the book website.

# 18.2 System Start-Up, Initialization, and Shutdown Using systemd

To begin to understand what systemd is, and part of what it achieves as a “superkernel,” we examine the first and last major tasks that systemd accomplishes for the Linux operating system—start-up and shutdown. The first of these tasks is what systemd was introduced for: to more effectively and efficiently replace the older UNIX and Linux init systems. But, as you explore more of this chapter, you will come to understand that systemd is much more than this.

# 18.2.1 An Overview of the Start-Up and Shutdown Processes

The basic details of how a Linux system that is using systemd boots and starts up are given in Chapter 17, Section 2.5. In this section, we further expand upon the particulars of the start-up phase, with regard to the systemd-specific steps involved.