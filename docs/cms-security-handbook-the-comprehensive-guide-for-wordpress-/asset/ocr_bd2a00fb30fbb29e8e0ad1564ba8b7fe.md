The sub-contractor was running a Mac and believed (erroneously) that Macs would not get infected. It turned out that his Mac was indeed infected, and the hacker was listening via a backdoor application and simply obtained the credentials.

After that, the hacker simply logged into the site. The security systems in place had no idea he was a bad guy because he had proper credentials. This is covered in greater detail in Chapter 8.

The problems here were trust and lack of education: The trust was that the subcontractor shared the login, but should have obtained a specific login for himself and the sub-contractor. The sub-contractor was not up to speed on his knowledge of malware and backdoors as they related to the operating system he was using.

This entire situation could have been averted.

Another misconception is that the upload folder is secure. The misconception is that even if someone were to load something, the intruder could not get it to do anything.

This is highly foolish in that even if the intruders couldn’t execute the uploaded material directly, they could entice someone else to. Even more disturbing, improperly set-up folders (directories) could allow the intruder’s access.

FTP is a very old and very insecure protocol. It should never be turned on for any public-facing machine. In essence, if a server is on the Internet, it should not have FTP on it.

> **NOTE** For a very detailed tutorial on FTP, see the guide to VSFTP (very secure FTP, included with Fedora) at www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_-_Ch15_-_Linux_FTP_Server_Setup.

# Exploring Alternative Versions of FTP

Red Hat and Fedora are a couple of the more popular Linux platforms in use today. Red Hat and Fedora currently ship with a fairly secure FTP platform called VSFTP. Overall, if you are going to use an FTP application, then VSFTP is one of the better ones to use. Another reasonably secure (and popular) FTP server is Pure-FTPd.

Both VSFTP and Pure-FTPd allow the use of SSL for passwords and user-names, thus helping to protect your sessions. SSL is used by many reputable firms, and is considered very strong.

> **NOTE** If you are on a shared server, then you have no choice but to use FTP. If security is a concern, do not use a shared hosting situation.

# Using VSFTP

Fortunately, VSFTP has been written by a security researcher. Therefore, much of the normal concerns are gone, because it has been coded with the idea of eliminating many security issues.