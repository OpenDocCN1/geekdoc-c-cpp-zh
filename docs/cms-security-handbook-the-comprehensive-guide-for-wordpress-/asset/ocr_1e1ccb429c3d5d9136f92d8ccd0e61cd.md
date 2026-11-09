# Table 5-2 (continued)

| INSTALLED GROUPS | AVAILABLE GROUPS |
|---|---|
| Legacy Network Server | Cluster Storage |
| Legacy Software Support | Clustering |
| Mail Server | Development Tools |
| Network Servers | Dialup Networking Support |
| OpenOffice Enterprise Distribution | Editors |
| System Tools | Emacs |
| Text-based Internet | Engineering and Scientific |
| Yum Utilities | FTP Server |

yum is a quick way to find and install a package. Using the returned list shown in Table 5-2, you could install a new FTP server quite easily by using the following command:

```
```bash
# yum groupinstall "FTP SERVER"
```
```

You can cluster on one line a set of commands to install, as shown here:

```
```bash
# yum install php-mysql php-devel php-gd php-mcrypt php-pgsql-memcache
php-pspell php-snmp php-xmlrpc php-xml
```
```

This command can install several items, such as MySQL Server and the PHP development tools. It is handy for setup purposes.

# Updating the Server Using yum

After you have updated your server, you are ready to begin the hardening process. You’ll need to log on as the super user. Remember, you’ll see the # prompt after you are logged in. Seeing $ means you are logged in as a regular user. The following examples involve using CentOS to demonstrate the use of yum.

Suppose you wanted to check the system for potential updates. The quickest way to do this is to use the yum update command. This checks that your installed applications are up to date and issues a report. Figure 5-4 shows an example of a server needing an update.

However, if you ran that command and no updates were needed, you would see something similar to Figure 5-5.