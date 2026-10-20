+   1. Use the Software Manager to install absolutely essential applications that you need to use that are not already preinstalled by default (Firefox, LibreOffice). For us, that included, in priority order, opensshd, Filezilla, Gparted, VirtualBox, and Webmin. We also put desktop icons on our Cinnamon desktop for all of our important applications. We supply some of the installation instructions for this software in Appendix A.
+   2. Our highly recommended storage model dictates the use of ZFS, so we installed the zfsutils-linux package. The Linux Mint operating system was built on an SSD, and we added an additional spinning hard disk mirrored pair of vdevs for user data file storage immediately after installing zfsutils-linux.
+   3. Since printing documents was an essential operation that our system needed to perform, we attached and setup via Common UNIX Printing System (CUPS; as shown in detail on the website, in Chapter W26, Section W26.5, titled "CUPS Printing"), a laserprinter directed to the hardware of the computer with a USB connection.
+   4. We exposed our Linux Mint system on the Internet as a basic ssh server, so we immediately modified the sshd configuration file, and constructed ufw firewall rules, according to what we show in this chapter, to secure the system. In addition, we also installed the fail2ban package with its defaults to protect against brute-force attacks, mainly on port 22. If you are using a CentOS system, selinux is enabled and enforced by default, whereas it is not in the Debian family.
+   5. We minimally exposed our Linux Mint system as a Web server (using nginx and our custom programs as shown on the website), but went with the default security measures for those applications.
+   6. We needed only a sparse set of additional users and groups on the system, so we immediately set those up using the method shown in Section 17.3.4, and added to them as necessary. This method of adding new users and groups conforms to item 2. The primary advantage this confers is that users, and their data files, are on their own redundant pair of hard drives, discreet and maintained separately from the operating system installation. We feel that this model is useful for a single-user computer desktop system, a shared multiuser computer, or low-to-midlevel enterprise-level servers as well.

There are various Linux commands that survey system hardware, to provide you with a basis for doing performance tuning and postinstallation modification of the system. Some of these are lscpu, lshw, hwinfo, lspci, lspci, lsusb, inxi, lsblk, df, fdisk, mount, free, hdparm, and examining the relevant contents of the /proc directories. We detailed the use of some of these in previous chapters and illustrate the use of some of them in this chapter as well.

But, to get a very useful summary of the actual postinstallation configuration of their system, we have found that the Linux inxi command is the most useful and expedient way for beginners.

We show three uses of that command, on three different server-class machines: an HP ProLiant MicroServer running Linux Mint, an IBM System x3650 [-7979E9U] running Debian 9, and a Dell PowerEdge T110 running CentOS 7.4.

Note that, on the Dell PowerEdge T110 running CentOS 7.4, we had to install inxi as superuser first, using the command yum install inxi.

We utilize various options that yield our specific required outputs for those machines, as follows:

```
$ sudo inxi -GSCMm -t c -P -x
[sudo] password for bob: qqqqq
System:  Host: bob-ProLiant-MicroServer Kernel: 4.4.0-89-generic x86_64 (64 bit gcc: 5.4.0) Console: tty 0
Distro: Linux Mint 18.2 Sonya
Machine:  System: HP product: ProLiant MicroServer serial: 5C7142P200
Mobo: N/A model: N/A Bios: HP v: 041 date: 07/29/2011
CPU:  Dual core AMD Turion II Neo N40L (~MCP-) cache: 2048 KB
flags: (lm nx sse sse2 sse3 sse4a svm) bmips: 5990
clock speeds: max: 1500 MHz 1: 1000 MHz 2: 1300 MHz
```