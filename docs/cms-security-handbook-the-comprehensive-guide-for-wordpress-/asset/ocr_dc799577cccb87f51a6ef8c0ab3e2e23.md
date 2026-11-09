+   - LameRemote
+   - ProjectMayhem
+   - Backdoor.IRC.flood
+   - Backdoor.Hacarmy.E
+   - W32.Spybot, W32.Cissi.W
+   - W32.Linkbot.M
+   - W32.Zotob.D

Those open ports identified through an Nmap scan indicate trouble.

# Installing Nmap

Nmap is available for Linux and Windows. Installation on your Linux server can be run from the command line with one of the two following commands:

```
```text
# rpm Manager : rpm -vhU http://www.nmap.org/dist/<version>
Yum install nmap
```
```

> > **NOTE** You should be sure to run an update if you install from any source except directly from nmap.org.

For full installation instructions, review the documentation at http://nmap.org/book/inst-linux.html#inst-rpm

Another method to install and run Nmap is from a Windows desktop. Download the latest version from nmap.org and install as you would any other Windows application.

> > **WARNING** Before reviewing some of Nmap’s more useful commands, be sure you understand that legal restrictions may vary by the location the server is in. In other words, scanning a server in a particular country or state may be a crime. Therefore, never use Nmap to scan a server you do not expressly have permissions to scan. It’s simply not a good idea, and could land you in trouble.

# Using Nmap

The version of Nmap discussed here is running with a graphical user interface (GUI), but the commands are identical for other setups. The GUI for Nmap looks like Figure 4-7 on startup.

Here are some of the main features of this screen:

+   - *Target* — This is the target server. It can be a domain name or IP address.
+   - *Profile* — These are preconfigured settings that change the way Nmap scans the target.