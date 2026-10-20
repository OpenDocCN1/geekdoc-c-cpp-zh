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

# 17.2 Linux System Installation

# Linux Mint 18 Cinnamon Installation from a DVD-created ISO File in Ten Easy Steps

We are assuming that you want to install a 64-bit version of Linux Mint onto computer hardware that has an Internet connection, where it will be the only operating system on the hard drive, and you want to dedicate the entire hard drive to Linux Mint, so the hardware boots into Linux Mint.

+   1. Download the ISO image from www.linuxmint.com/download.php
+   Choose the edition you want, in our case 64-bit Cinnamon Desktop version.

+   2. “Burn” the ISO image to a DVD or to a USB thumbdrive. We do not give instructions here for that operation.

+   3. Boot your computer to the DVD or USB thumbdrive, however, that is achieved with your hardware. Generally, that is done by pressing a function key on the keyboard, and selecting the boot device order.