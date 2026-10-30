![](bbox=[0.25, 0.15, 0.78, 0.75])

# Figure 19.2 Arrangement of pseudo terminals under Solaris

From this point on, we’ll simplify the figures by not showing the “read and write functions” from Figure 19.1 or the “stream head” from Figure 19.2. We’ll also use the abbreviation PTY for pseudo terminal and lump all the STREAMS modules above the slave PTY in Figure 19.2 into a box called “terminal line discipline,” as in Figure 19.1.
We’ll now examine some of the typical uses of pseudo terminals.

# Network Login Servers

Pseudo terminals are built into servers that provide network logins. The typical examples are the telnetd and rlogind servers. Chapter 15 of Stevens [1990] details the steps involved in the rlogin service. Once the login shell is running on the remote host, we have the arrangement shown in Figure 19.3. A similar arrangement is used by the telnetd server.

We show two calls to exec between the rlogind server and the login shell, because the login program is usually between the two to validate the user.