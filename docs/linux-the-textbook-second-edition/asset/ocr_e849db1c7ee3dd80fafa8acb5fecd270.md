# Debian-family Installation of emacs

Type the following command to install emacs:

```
$ sudo apt-get install emacs24
```

# CentOS Installation of emacs

As with all of the following installations on CentOS, there were some preliminary steps that needed to be taken before we could use Yellow Dog Updater, Modified (YUM). On our CentOS 7.4 system, we had to first stop and disable the packagekit app that is holding the lock on YUM. Then we could install the epel “extras” package, in which emacs is found. Use the following commands to do this, and then to install emacs with YUM:

```
[root@centos]# systemctl stop packagekit
[root@centos]# systemctl disable packagekit
[root@centos]# yum install epel-release
Output truncated...
[root@centos]# yum install emacs
Output truncated...
[root@centos]#
```

# W25.5.7 Version Control with git

Installing git on Debian-family-

```
$ sudo apt install git
[sudo] password for bob: zzz
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  git-man liberror-perl
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk
  gitweb git-arch git-cvs git-mediawiki git-svn
The following NEW packages will be installed:
  git git-man liberror-perl
0 upgraded, 3 newly installed, 0 to remove and 111 not upgraded.
Need to get 3,760 kB of archives.
After this operation, 25.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Output Truncated...
Setting up git (1:2.7.4-0ubuntu1) ...
$
```

On CentOS (Note that all of the following commands are run as root!)-

+   1. You have to stop and disable the packagekit app so that it releases its lock on YUM. Do this with the following commands:
+      [root@centos] # systemctl stop packagekit
+      [root@centos] # systemctl disable packagekit

+   2. Now you can install git with the following command:
+      [root@centos] # yum install git -y
+      Loaded plugins: fastestmirror, langpacks
+      Loading mirror speeds from cached hostfile
+        * base: mirror.web-ster.com
+        * epel: mirrors.develooper.com
+        * extras: mirror.cs.pitt.edu
+        * updates: centos.mirror.constant.com
+      Resolving Dependencies
+      --> Running transaction check