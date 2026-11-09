that this is happening is when your disk is filling up with spam mail quite quickly in the SENT or TEMP folders.

These are signs that your mail server has likely been compromised, and you should take care of the problem immediately. In most Linux-based e-mail systems, the folders are accessible by the administrator. You can review your folders to see what is in them.

Containing an e-mail breach involves following a number of steps, and lots of cleanup.

# Step One: Check for Open Relay Servers

The first step is to ensure that you are not running an open relay e-mail server. Quite a few sites can help you test for open relays on your server. If you have an open relay, contact your host or e-mail administrator for assistance. You may consider looking at commercial tools available on such sites as DNSSTUFF.COM to assist with your e-mail tests.

# Step Two: Scan Your Ports

Next, scan your ports using NMAP (from insecure.org). You should ensure that all the ports are closed that should be closed. Each server is different, so telling you what ports you should open or close beyond the normal 80, 443, 21, and 25 is impossible. Contact your host or network administrator to assist with that. If you find a high number of ports open, then you may have been severely hacked with lots of embedded malware on the server.

# Step Three: See Who Is Logging In

To see who is logging in, you must first get to the shell using SSH. After you log on as the root user, type W at the # prompt to see who is logged in. If more than one root user is logged in, as shown in Figure 9-11, your server might have been compromised.

![](bbox=[0.141, 0.761, 0.762, 0.849])

Figure 9-11: Unauthorized logon

In the example shown in Figure 9-11, the server was compromised and was sending out thousands of pharmacy spam e-mails a day. As shown in the figure, a quick check revealed that two root users were on.