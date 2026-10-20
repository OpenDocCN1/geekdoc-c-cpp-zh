```
[root@centos]# systemctl stop packagekit
[root@centos]# systemctl disable packagekit
[root@centos]# yum install epel-release
Output truncated...
[root@centos]#
[root@centos] # yum install gparted
Loaded plugins: fastestmirror, langpacks
ep el/x86_64/metalink
| 12 kB 00:00:00 epel
| 4.3 kB 00:00:00 (1/3): epel/x86_64/group_gz
| 261 kB 00:00:10 (2/3): epel/x86_64/updateinfo
| 839 kB 00:00:18 (3/3): epel/x86_64/primary_db
| 6.1 MB 00:00:19 Loading mirror speeds from cached hostfile
* base: mirror.cogentco.com
* epel: mirror.sfo12.us.leaseweb.net
* extras: centos.sonn.com
* updates: mirrors.seas.harvard.edu
Resolving Dependencies
--> Running transaction check
--> Package gparted.x86_64 0:0.19.1-6.el7 will be installed
Output truncated...
Installed:
 gparted.x86_64 0:0.19.1-6.el7
Dependency Installed:
 polkit-gnome.x86_64 0:0.106-0.1.20170423gita0763a2.el7
Complete!
[root@centos]#
```

# W26.4.7 Installing ZFS

For Ubuntu 16.04 and Linux Mint 18.2-
From Example W26.8a Adding a New Hard Drive Using ZFS
Update your package manager, and download and install the zfsutils-linux on your system, using the following commands:

```
$ sudo apt update
Output truncated...
$ sudo apt upgrade
Output truncated...
$ sudo apt install zfsutils-linux
Output truncated...
```

+   1. Once the zfsutils-linux is installed, list the zpools on your system with the following command, to test that the installation has been successful:

```
$ sudo zpool list
[sudo] password for bob: zzz
no pools available
$
```

For Debian 9.1 and later

Because of our installation type, we needed to keep the Debian 9.1 installation DVD mounted on our computer to execute the following steps. Of course, some of these steps may not be necessary if there are bug fixes in later versions of Debian!

Step 1. You must enable the contrib, nonfree repositories available, by using the sed editor to find and replace the word “main” in the file /etc/apt/sources.list:

```
[root@debian]# sed -i 's/main/main contrib non-free/g' /etc/apt/sources.list
```

Then you can update your Debian systems’ packages.