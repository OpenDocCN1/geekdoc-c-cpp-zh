
## Anonymous FTP

One type of situation that has the potential to be abused is the anonymous login. What this means is that an FTP server set up in this fashion will accept any legitimate FTP connection with no or minimal authentication.

An anonymous user can upload, download, or read any files available to it. Although FTP typically won’t allow you to access above a specific level, it will more than likely allow you access to the website itself.

This would give the hacker the capability to upload a shell program, backdoor application, or viruses. Attackers often set up listeners on the server, which will allow them to eavesdrop on your activity. All in all, you should never allow an anonymous user on your FTP server.

Ensure that you do not have anonymous users. Additionally, make sure each person authorized to use FTP has his or her own login credentials. This enables auditing of activity.

## Weak Passwords

Many FTP systems do not restrict the retrying of a connection multiple times. In that scenario, a malicious user could simply keep trying username and password combinations until a good one is found.

Your action here is to ensure that your password is very difficult to guess. Although there’s no solid rule, here are a few tips:

- Use a combination of uppercase and lowercase letters, as well as allowable punctuation.
- If your password (no matter if it is uppercase or lowercase) is in a dictionary, or could be similar in spelling, do not use it.
- Change your FTP passwords regularly. On a site with lots of FTP users and activity, you should change it every 30 days.

## Misconception of Security

Many people believe that FTP is safe and secure. One issue is the sharing of FTP credentials to upload files. This is less of a technical issue and more of a trust issue. That is, in trusting the person to whom you are giving the credentials, you are giving that person and that person’s machine access to your server. If the machine is compromised, that person could easily expose you to the malware.

There was once a case where a site was severely hacked. The attacker came through the FTP server with legitimate credentials. After reviewing the logs and a lot of detective work, it turned out that a subcontractor had hired another subcontractor to assist him. The sub-contractor was running a Mac and believed (erroneously) that Macs would not get infected. It turned out that his Mac was indeed infected, and the hacker was listening via a backdoor application and simply obtained the credentials.

After that, the hacker simply logged into the site. The security systems in place had no idea he was a bad guy because he had proper credentials. This is covered in greater detail in Chapter 8.

The problems here were trust and lack of education: The trust was that the subcontractor shared the login, but should have obtained a specific login for himself and the sub-contractor. The sub-contractor was not up to speed on his knowledge of malware and backdoors as they related to the operating system he was using.

This entire situation could have been averted.

Another misconception is that the upload folder is secure. The misconception is that even if someone were to load something, the intruder could not get it to do anything.

This is highly foolish in that even if the intruders couldn’t execute the uploaded material directly, they could entice someone else to. Even more disturbing, improperly set-up folders (directories) could allow the intruder’s access.

FTP is a very old and very insecure protocol. It should never be turned on for any public-facing machine. In essence, if a server is on the Internet, it should not have FTP on it.

> **NOTE** For a very detailed tutorial on FTP, see the guide to VSFTP (very secure FTP, included with Fedora) at www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_-_Ch15_-_Linux_FTP_Server_Setup.

## Exploring Alternative Versions of FTP

Red Hat and Fedora are a couple of the more popular Linux platforms in use today. Red Hat and Fedora currently ship with a fairly secure FTP platform called VSFTP. Overall, if you are going to use an FTP application, then VSFTP is one of the better ones to use. Another reasonably secure (and popular) FTP server is Pure-FTPd.

Both VSFTP and Pure-FTPd allow the use of SSL for passwords and user-names, thus helping to protect your sessions. SSL is used by many reputable firms, and is considered very strong.

> **NOTE** If you are on a shared server, then you have no choice but to use FTP. If security is a concern, do not use a shared hosting situation.

### Using VSFTP

Fortunately, VSFTP has been written by a security researcher. Therefore, much of the normal concerns are gone, because it has been coded with the idea of eliminating many security issues.

To install VSFTP (in Red Hat and Fedora distributions of Linux), log in as root and enter this command:

```
# yum install vsftpd
```

To shut off VSFTP, log in as the root user, and, after ensuring that you have a recent backup, run the following commands to disable or remove VSFTP from your server:

```
# chkconfig vsftpd off
# yum erase vsftpd
```

While still in the VSFTP configuration file, update the banner located at /etc/banners/vsftpd. Be sure to add the appropriate warnings to the FTP user about your information security policy.

Figure 5-14 shows an example from the guide for the Community Enterprise Operating System (CentOS), which is a Red Hat-derived distribution of Linux.

```
220-Hello, %c
220-All activity on ftp.example.com is logged.
220-Inappropriate use will result in your access privileges being removed.
```

**Figure 5-14: Example banner in VSFTP**

Note the %c in the banner. When a user logs in, he or she will see the user information, including username, host, IP address, and potentially other information about the connection in place of that %c. The purpose of changing the banner is to help remind users that their actions are being recorded, and thus ward off potential harm.

VSFTP defaults to allow anonymous access. Thus, if you do install it, you must edit the configuration file to remove anonymous access.

> **NOTE** A complete guide for CentOS on securing and configuring VSFTP is available at www.centos.org/docs/5/html/Deployment_Guide-en-US/ch-server.html.

### Using Pure-FTPd

Pure-FTPd is another good choice if you need to offer FTP servers.

Installing Pure-FTPd includes many steps and a good number of options. Visit http://download.pureftpd.org/pub/pure-ftpd/doc/README to get the full instruction set.

To uninstall Pure-FTPd, log in as root, and execute the following commands. (Be sure you have a recent backup.)

```shell
# ./configure
# make uninstall
```

> **WARNING** Note that you should only take these actions if you are on your own server. These instructions will not work on a shared server. If your server is managed by a host, then you can ask the host to remove Pure-FTPd.

Another option for security is enabling SSL (TLS) with Pure-FTPd. For more information on this topic, see http://forums.theplanet.com/lofiversion/index.php/t-45824.html.

The better protocol to use in place of FTP is SFTP, as discussed in the following section.

## Securing SFTP Communications Ports

As you have seen, FTP generally is a very insecure and easily compromised application. Simply too many cases exist where weak passwords allowed a hacker to gain access and cause damage.

The alternative is SFTP, which has no direct relationship with the FTP protocol. Rather, this protocol depends on the Secure Shell (SSH) protocol for encryption and authentication of the connection.

SSH is the best method currently available to connect to a server. You may hear about several tools that allow you to connect to SSH. Following are some examples of open source tools that support the current version of SSH (SSH-2):

- PuTTY
- Terminal (Mac)
- WinSCP
- FileZilla

> **NOTE** SSH-1 is a vulnerable application and should never be used. Although this note is somewhat dated, it’s important to keep in mind.

The most common software stack for SSH is OpenSSH. The GNU/GPL licensed code is widely available on many web servers. According to the Internet Engineering Task Force (IETF), the organization that ratifies Internet standards, “The SSH File Transfer Protocol provides secure file transfer functionality over any reliable, bidirectional octet stream. It is the standard file transfer protocol for use with the SSH2 protocol.” In other words, SSH sets up a secure communications channel between your machine (the client) and the server.
