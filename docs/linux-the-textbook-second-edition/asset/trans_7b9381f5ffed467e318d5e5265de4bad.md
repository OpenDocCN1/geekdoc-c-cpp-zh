

----> Package git.x86_64 0:1.8.3.1-12.el7_4 will be installed
Output truncated...

3. Test to see that the version shown in Step 2 was loaded and installed with the following command:

```
[root@centos] # git --version
```

## W26.1.2 Webmin Download and Installation

For Webmin Installation on Debian-family-
Example W26.1 Webmin Installation
Step 1. Add the official repository. You can do this by appending these two lines to your /etc/apt/sources.list file, using the following commands:

```
$ sudo vi /etc/apt/sources.list
```

Then, add the two lines shown here:

```
deb http://download.webmin.com/download/repository sarge contrib
deb http://webmin.mirror.somersettechsolutions.co.uk/repository sarge contrib
```

Save and exit the file.

Step 2. Fetch and install the Gnu Privacy Guard (GPG) key for Webmin, using the following commands:

```
$ sudo wget http://www.webmin.com/jcameron-key.asc
$ sudo apt-key add jcameron-key.asc
```

Step 3. Install Webmin with the following commands:

```
$ sudo apt-get update
$ sudo apt-get install webmin -y
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
apt-show-versions libauthen-pam-perl
The following NEW packages will be installed:
apt-show-versions libauthen-pam-perl webmin
0 upgraded, 3 newly installed, 0 to remove and 45 not upgraded.
Need to get 15.3 MB of archives.
Output truncated...
```

For Webmin Installation on CentOS 7 (Note that all the following commands are executed as root!)-

- 1. Update all the currently installed software to the latest version available using the command:
- [root@centos] # yum -y update

- 2. Use a Web browser, go to the Webmin download page, and check for the Webmin RedHat Package Manager (RPM) package. The RPM package works for any RedHat, Fedora, or CentOS system. To download the package, use wget on the command line. For our CentOS system, we used the following command:
- [root@centos] # wget http://prdownloads.sourceforge.net/webadmin/webmin-1.831-1.noarch.rpm

To proceed with the installation, you need to make sure that all dependencies are installed on your CentOS Virtual Private Server ( VPS). If they are not installed, you can install them using the following command:

```
[root@centos] # yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty
```

Once the dependencies are installed, you can install Webmin using the following command:

```
[root@centos] # rpm -U webmin-1.831-1.noarch.rpm
```

3. To start Webmin, use the following command:

```
[root@centos] # service webmin start
```

To enable Webmin on system boot, use the following command:

```
[root@centos] # chkconfig webmin on
```

4. Before you can login to Webmin via a Web browser, you need to first adjust the public zone of firewalld with the following commands:

```
[root@centos] # firewall-cmd --permanent --zone=public --add-port=10000/tcp
[root@centos] #firewall-cmd --reload
```

5. To access Webmin, open your favorite Web browser, enter HTTPS as protocol, enter your server IP address and use 10000 as a port number.
https://YOUR-IP-ADDRESS:10000

You can accept the exception to the SSL certification. Then login to Webmin with the username set to root and root’s password.

## 17.2 Linux System Installation

### Linux Mint 18 Cinnamon Installation from a DVD-created ISO File in Ten Easy Steps

We are assuming that you want to install a 64-bit version of Linux Mint onto computer hardware that has an Internet connection, where it will be the only operating system on the hard drive, and you want to dedicate the entire hard drive to Linux Mint, so the hardware boots into Linux Mint.

- 1. Download the ISO image from www.linuxmint.com/download.php
- Choose the edition you want, in our case 64-bit Cinnamon Desktop version.

- 2. “Burn” the ISO image to a DVD or to a USB thumbdrive. We do not give instructions here for that operation.

- 3. Boot your computer to the DVD or USB thumbdrive, however, that is achieved with your hardware. Generally, that is done by pressing a function key on the keyboard, and selecting the boot device order.

10. On the “Who are you?” screen, type in your name and a username, and most importantly, choose a password you can remember! This will give you root privileges on the newly installed Linux Mint system and put you automatically into the sudoers group. Click on the “Continue” button to install Linux Mint.

### 17.2.3.4 vsftpd Installation, From Example 17.1

The package management system command (either APT, YUM, or one used on your Linux system) used to install the vsftpd package is dependent upon what Linux system you are using. See Section 17.7 for details of package management.

For Debian, Ubuntu, and Linux Mint-

- 1. Download and install the vsftpd server with the following command:

```
$ sudo apt-get install vsftpd
[sudo] password for bob: QQQ
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
  liblxc1 lxc-common lxcfs uidmap
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  vsftpd
0 upgraded, 1 newly installed, 0 to remove and 321 not upgraded.
Output truncated...
Processing triggers for ureadahead (0.100.0-19) ...
Processing triggers for systemd (229-4ubuntu4) ...
$
```

- 2. Use the systemctl command to check the status of the vsftpd service, using the following command:

```
$ systemctl status vsftpd.service
● vsftpd.service - vsftpd FTP server
   Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2016-07-02 12:10:11 PDT; 2min 15s ago
  Main PID: 8780 (vsftpd)
   CGroup: /system.slice/vsftpd.service
           └─8780 /usr/sbin/vsftpd /etc/vsftpd.conf

Jul 02 12:10:10 bob-VirtualBox systemd[1]: Starting vsftpd FTP server...
Jul 02 12:10:11 bob-VirtualBox systemd[1]: Started vsftpd FTP server.
$
```

Notice from the preceding output that the command from Step 1 is not only downloaded but also installed and started, the vsftpd service.

- 3. To check to see that vsftpd is actually accessible on your system from another host, from another host machine on your network, use the ftp command to connect to the vsftpd server on your machine. Substitute the IP address of the machine you want to ftp into for the IP 192.168.0.30 shown in this command:

```
# ftp 192.168.0.30
Connected to 192.168.0.30.
220 (vsFTPd 3.0.3)
Name (192.168.0.30:bob): bob
331 Please specify the password.
```

4. To allow the ftp service in through the firewall on port 21, use the following commands:

```
[root@centos] # firewall-cmd --permanent --add-port=21/tcp
success
[root@centos] # firewall-cmd --permanent --add-service=ftp
success
[root@centos] # firewall-cmd --reload
success
```

5. To connect to FTP server using an already-created user named mansoor, use the following commands, not run as root:

```
[root@centos] # exit

$ ftp 192.168.0.43
Connected to 192.168.0.43 (192.168.0.43).
220 (vsFTPd 3.0.2)
Name (192.168.0.43:bob): mansoor
331 Please specify the password.
Password: QQQ
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> exit
221 Goodbye.
$
```

## 17.4.3 Installing Gparted from the Command Line

For Debian-family (Ubuntu shown)-

```
$ sudo apt-get install gparted
[sudo] password for bob:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
libllvm3.8 libmircommon5 libpango1.0-0 libpangox-1.0-0 libsnapd-glib1 snapd-login-service ubuntu-core-launcher
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
libgtkmm-2.4-1v5 libparted-fs-resize0
Suggested packages:
xfsprogs reiserfsprogs reiser4progs jfsutils kpartx dmraid dmsetup gpart libparted-dev
The following NEW packages will be installed:
gparted libgtkmm-2.4-1v5 libparted-fs-resize0
0 upgraded, 3 newly installed, 0 to remove and 78 not upgraded.
Need to get 1,129 kB of archives.
After this operation, 6,973 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Output truncated...
Setting up gparted (0.25.0-1) ...
Processing triggers for libc-bin (2.23-0ubuntu9) ...
$
```

For CentOS 7

At the time of writing of this book, on our CentOS 7.4 system, we had to first stop and disable the packagekit app that is holding the lock on YUM. Then, we could install the epel “extras” package in which gparted is found. Use the following commands to do this, and then install gparted:

