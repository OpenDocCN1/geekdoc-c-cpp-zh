
these machines have that kind of memory? What is the file system type of the CentOS 7 computer? Given your Linux system and hardware, what options of the **inxi** command would be most useful and revealing for you to use?

## 17.2.2 Installation of Linux

Since we treat four representative Linux systems as models for various things we show throughout this chapter, the quickest way of installing any one of these systems is to follow the online instructions supplied with the software, for the version that you are installing. We supply installation instructions in Appendix A, Section 17.2, for Linux Mint, version 18.2. As stated in Section 17.1, we suggest limiting the installation to a single-disk system, where Linux is the only operating system on the disk. We also suggest using the 64-bit ISO-created DVD medium available at the following websites, for the particular version of Linux you want to install:

- Debian: www.debian.org
- Ubuntu: www.ubuntu.com
- Linux Mint: www.linuxmint.com
- CentOS: www.centos.org

The step-by-step installation process, guided by the instructions that are part of the documentation for the particular Linux system you want to install, and the choices you make during installation, have defaults for the simple installation we advise you to do. For example, for the four systems listed, we recommend that you use the default disk partition scheme when you are installing to a single hard drive system. Going with the defaults is particularly true if you do an installation of the GUI version of any of the earlier representative systems.

## 17.2.3 System Services Administration, Startup, and Shutdown Procedures

This section details the general procedures for starting up, managing the startup process, and gracefully shutting down Linux. It gives a brief overview of the steps that the system goes through in successfully starting up and shutting down. It then gives some further references to the basic but important systemd services administration utilities available to a system administrator. In those further references, we give examples of commands for manipulating and changing system services by enabling and running new services.

### 17.2.3.1 The Boot and Startup Processes

At its very simplest, a computer running a systemd-controlled Linux system goes from a powered-off state to full, normal operation in the sequence Booting, then Startup. This is shown in detail as

Booting

- The firmware on the main system board finds the bootable media.
- From the bootable media, the bootloader program loads the monolithic kernel from the boot media into RAM and starts it.

Startup

- The kernel uses the commands passed by the bootloader to find the main file system, at which point it can find and run systemd.
- systemd runs other programs to find the file systems and start network and all necessary local service processes.

The term “booting” is used here to mean bringing the operating system from a complete power-off condition to a point where systemd can take over. Then in “startup,” systemd brings the computer to a steady-state fully normal operating condition.

Figure 17.1 illustrates the sequence of powering on, booting, startup, and shutdown on a typical modern computer running Linux. In Figure 17.1

- Power on means pushing the power on button on the hardware.
- Power-On Self-Test (POST) is hardware initialization done in conjunction with the bootloader programs.
- On our representative Linux systems, the Basic Input/Output System (BIOS) and the Unified Extensible Firmware Interface (UEFI) are the firmware systems that take over initialization of the booting sequence.
- The GRand Unified Bootloader, version 2 (GRUB2), is the bootloader program.
- The kernel is initiated, runs, and then executes /etc/systemd, which in turn brings the system to a normal operating state defined by the default Target. In a text-based server, this default Target is usually defined as multiuser.target. In a GUI environment, this default Target is usually defined as graphical.target.
- The shutdown procedure is illustrated in Section 17.2.3.2.

Further details of how a Linux system that is using systemd starts up are given in Section W26.2.3.1.1, titled “systemd Bootup,” at the book website.

The BIOS booting component process, and its modern equivalent, the UEFI process, work according to specifications that control and define the firmware interface to the operating system. The operations of systemd when Linux starts up, and shuts down, are shown in detail in Chapter 18. As shown in Figure 17.1, several steps occur before systemd as a startup and initialization program takes over. POST, BIOS (or UEFI), GRUB2, and then the kernel, initialize hardware and prepare for the first process to be run from the root file system. After the root file system is found and mounted, systemd takes over and is

![](img/2a18e06cd9c6395e451f26126ecba1fd_551_0.png)

FIGURE 17.1 Booting, startup, and shutdown on a systemd Linux system.

then responsible for initializing all remaining hardware, mounting all necessary file systems, invoking the default systemd target, and managing the start of system services.

But then what does an ordinary user do when a normal boot and startup cannot be done at all, or normal shutdown cannot be achieved, for whatever reason?

For booting and startup, barring power or hardware-related issues exposed during POST, such as failed hard disk or memory, there are a couple of steps you can take to examine the possible problem. You can actually intercede at any of the steps illustrated in Figure 17.1.

You can attempt to boot the system into “rescue” mode, by trying to boot to the systemd emergency or rescue target states. This is shown in detail in Chapter W27, Sections 2.1 and 5.1.8.8, at the book website. This is similar to the legacy operation of entering “single-user” mode upon booting.

You can also use the bootloader program, GRUB2, to enter a “recovery” mode upon booting. On our representative Linux Mint system, when POST is completed successfully, and just before GRUB2 takes over the boot process, you can hold down the Shift key on the keyboard to enter a GRUB2 menu. On other Linux systems, that interrupt can be different.

Be aware that we do not give the details of GRUB2 configuration and modification here.

The advanced option of the GRUB2 menu includes choices for booting into alternative, or previous, “boot environments,” and into recovery modes for those environments. These environments are usually named according to kernel version. So if you have upgraded the operating system kernel during the course of using your computer system, different environments with different kernels will be available to you. For an ordinary user, this choice for troubleshooting the system, by entering these system states during the boot stage, is a useful possibility that would help you recover data, logs, and other valuable information.

When a system hangs up during the shutdown procedure, a contemporary way of diagnosing the problem is to examine the systemd journal, with the journalctl command, as shown in Chapter W27, Sections 27.2.4 and 6.2. This way, if some process or program is preventing the system from reaching a powered-off condition, the journal logs will allow you to see what that process or program is. On shutdown, systemd attempts to stop all services, and unmount all file systems. The system is finally powered down. We give more details of how a Linux system using systemd shuts down in the next section.

# Exercise 17.3

How can you boot into an alternative environment found on another boot medium on your computer system, and in which phase of the bootup process is this alternative method presented to you? Why would you want to do this? Make note of exactly how that is done on your system. Also, draw an arrow in Figure 17.1 that would specify what path would be followed if the system needs to be rebooted rather than powered off.

## 17.2.3.2 systemd and Traditional System Reboot or Shutdown

systemd is in charge of taking the system from the normal operating condition to a power-off state or to reboot the system. The relevant systemd systemctl commands that achieve shutting the system down or rebooting it, and briefly what they accomplish, are shown in Table 17.1. We describe these commands

# TABLE 17.1

systemd Shutdown Commands

| Command | Description |
|---|---|
| systemctl halt | Halts the system |
| systemctl poweroff | Powers off the system |
| systemctl reboot | Restarts the system |
| systemctl suspend | Suspends the system |
| systemctl hibernate | Hibernates the system |
| systemctl hybrid-sleep | Hibernates and suspends the system |
