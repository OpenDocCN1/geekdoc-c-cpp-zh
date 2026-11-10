
## 2.3 SOFTWARE TYPES

Software gets down to work the moment you switch on the computer. Until the computer is shut down (if at all), a variety of software keep the computer busy. Some software run continuously without your knowing it while others are explicitly run by users. Computer software can be broadly divided into two types:

- *System software*: This is the software run by the computer to manage the hardware connected to it. Users don't have much control over its functioning, but their own programs (application software) use the services offered by system software whenever required.
- *Application software*: Software of this type relates to a specific application, say, one that makes hotel bookings or creates special effects in movies. The vast majority of programmers are engaged in developing application software.

These two types of software have vastly different characteristics and require different skills; it is rare for a programmer to be proficient in both. In this chapter, we examine the commonly used software of both categories. Some of them may not be available on your computer, so make sure you have them installed before you can use them.

### 2.3.1 System Software

A program typically needs to access the CPU, memory, hard disk, monitor and keyboard. If it acts alone, then it must know the details of these resources. Because the same program may also run on different hardware, how does one design an application that need not know the hardware it is running on? This is possible only if another software sits between the application and the hardware. This go-between is *system software*. Because of its direct access to the hardware, system software is able to provide the services needed by programs and users.

Most system software is run by the computer on startup, first from a ROM and then from the hard disk. The others are invoked when programs need them, say, for printing a report. *In some cases, a user may also directly use a program of this type.* System software include but are not restricted to the following:

- *Basic Input Output System (BIOS)*: This is a small program that checks the hardware devices and peripherals at boot time and then loads the operating system.
- *Operating system*: This is the central system software that manages both the hardware and programs running on the computer. Because all programs need its services, the operating system remains in memory as long as the computer is up.
- *Device driver*: Every hardware needs a special software that knows how to handle it. Programs access a device driver by making a call to the operating system.
- *Compilers and associated programs*: This category of system software is special because it is invoked by users. A programmer invokes a compiler program to convert the source code written by them to machine code.

When a program run by a user (*application software*) needs to access hardware (say, a printer), it makes a call to system software to get the job done. For this reason, the BIOS and operating system are loaded into memory before users can run their programs. On an idle machine, it’s not unusual for 1 GB of RAM to be occupied by the operating system even though CPU activity may be very low.

System software is a specialized domain that requires knowledge of hardware. Lower-level languages have this knowledge, the reason why many routines of system software are written in assembly language (a low-level language). A C programmer must also know assembly language to be able to write system software.

We will briefly examine the first three categories of system software in this chapter. Compilers, being a programmer’s tool, belong to Chapter 4 where it is discussed in depth.

> **Takeaway:** When a computer is booted, the BIOS residing in ROM makes an initial check of the computer’s hardware. It then loads the operating system from disk. Subsequently, application software use the OS to access all hardware, the reason why the OS must always reside in memory.

> **Note:** In general, system software is written by the vendor that makes the hardware.

### 2.3.2 Application Software

Software not directly connected with hardware but related to a specific real-life situation is known as *application software*. The vast majority of the software that we encounter every day belongs to this type. The smartphone industry even has a smart name for it; they call it “apps.” The first application software was probably the payroll but today application software represents virtually every business activity:

- *Office software*: When the desktop PC came into being, office software was one of its first applications. This category now comprises three separate applications—word processing, spreadsheet and presentations. Word processing almost single-handedly drove out the typewriter from the market. We will be discussing these three applications in this chapter.
- *Database software*: This software package, commonly known as *Data Base Management System (DBMS)*, allows data having a uniform structure to be stored in a database. Each line of a database comprises multiple *fields* that may be added, modified and queried using simple instructions. Microsoft Office has a DBMS component (Access), but it is Oracle that dominates this space.
- *Communications software*: Computer networking led to the development of software that allowed users to communicate with one another. Email had been popular for offline communication before Skype and WhatsApp moved in as online applications. Mail handling is discussed in Section 2.14.1.
- *Entertainment software*: Home entertainment on the PC has also seen the rise of software related to gaming and multimedia. The VideoLAN (VLC) software serves as a one-stop shop for playing most audio and video formats. Gaming software remains extremely popular and challenging for software developers.

is pressed. If POST encounters a problem, it responds with a well-documented combination of beeps. The system halts at that moment and does not load the operating system.

After POST, the BIOS tries to locate the drive containing the operating system. It checks CMOS for the list of bootable drives and their search sequence. Following that sequence, the BIOS tries to locate the *boot loader* (a small program) in the first sector of every drive. If found, the BIOS runs the boot loader which eventually loads the operating system. This process is called *bootstrapping*, an allusion to the lifting of one’s boots by its bootstraps.

We said that the BIOS loads *device drivers*, but what are they? A device driver is a system software that is associated with a device. System and application programs access and drive the device by invoking its driver. The BIOS needs to load an initial set of these drivers because the CPU must have access to the key devices to be able to load the operating system. However, modern operating systems eventually replace the drivers loaded by the BIOS with their own set of drivers.

The BIOS has its limitations of course. It doesn’t allow booting from a network or from a drive whose capacity exceeds 2.2 TB. After dominating the personal computer for over 30 years, the BIOS is making way for the *Unified Extensible Firmware Interface (UEFI)* which overcomes these limitations. UEFI is hardly a basic system; it is a pseudo-operating system that can be used to back up files or access the Internet even before the OS has been loaded. Modern PCs support UEFI; your PC may already be having one.

> **Tip:** If the computer doesn’t load the operating system even after successfully clearing POST, check whether you have left a DVD or CD in the drive. Disks not containing an OS won’t have the boot loader in the first sector, so the boot sequence is halted until you remove the disk and reboot the system.

> **Note:** Changes made to the BIOS settings are actually made in the battery-powered CMOS RAM and not to the BIOS itself, which contains only the program. The BIOS is usually resident in EEPROM or flash memory, so the usual update restrictions apply (1.9.2). A BIOS in flash memory or EEPROM is easily replaced but not one that resides in a ROM, where the entire ROM chip has to be replaced.

## 2.5 THE OPERATING SYSTEM (OS)

We have been constantly referring to this term as if our lives depended on it. At least a computer’s life depends on the operating system because no hardware or software can do without it. An *operating system (OS)* is a system software that manages the computer’s hardware to provide a complete and safe environment for running programs. It acts as an interface between programs and the hardware resources that these programs access (like memory, hard disk and printer).

If a computer had to run only one program, then it wouldn’t need an operating system. All the code for accessing hardware could be built into the program itself. If the printer needed replacement, the program would have to be changed as well. It would then be impossible to accommodate a second program to run on the same computer. Fortunately, a computer runs multiple programs that need all resources to be shared and managed. The following represent the key features of an operating system:
