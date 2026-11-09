Should you find yourself in this position, you must first terminate the unauthorized user’s session.

To terminate the unauthorized session, you’ll need the *Process ID (PID)* of the user. To obtain the PID, enter the following command:

```
ps -ef | grep <theusername> or ps -ef | grep sshd
```

This gives you the PIDs of the real root user and the unknown user. Write down both PIDs so you don’t accidentally terminate the real root user.

You then terminate a session as follows:

```
kill -9 xxxxxx
```

In this example, xxxxxx equals the user’s pid.

Finally, change your password and block the unauthorized user’s IP address.

# Step Four: Verify That Spam Is Gone

Next, you must verify the spam e-mails have been removed. Because each e-mail system differs in the way it stores and processes a queue, you should consult the manual for your e-mail system. In general you’ll see something like what is shown in Figure 9-12.

![](bbox=[0.086, 0.517, 0.245, 0.731])

**Figure 9-12:** Typical e-mail subdirectory tree

After you click into the mail queue shown in Figure 9-12, you may discover hundreds of e-mails, as shown in Figure 9-13.

Figure 9-14 shows an example of spam that was retrieved from that example hacked e-mail server’s directory. The sce: field in this particular e-mail contained about 250 e-mail addresses. (Of course, much of the personal information has been wiped out of this screenshot for security and privacy reasons.)

For starters, if you received an e-mail such as this, surely you would realize the United Nations is *not* inviting you to come to a summit. And, unless you are a spammer, and these are in your server’s sent mail box, then finding the