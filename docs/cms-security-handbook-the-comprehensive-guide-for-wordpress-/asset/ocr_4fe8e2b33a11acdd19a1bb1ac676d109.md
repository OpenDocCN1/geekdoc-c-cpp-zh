# ## Anonymous FTP

One type of situation that has the potential to be abused is the anonymous login. What this means is that an FTP server set up in this fashion will accept any legitimate FTP connection with no or minimal authentication.

An anonymous user can upload, download, or read any files available to it. Although FTP typically won’t allow you to access above a specific level, it will more than likely allow you access to the website itself.

This would give the hacker the capability to upload a shell program, backdoor application, or viruses. Attackers often set up listeners on the server, which will allow them to eavesdrop on your activity. All in all, you should never allow an anonymous user on your FTP server.

Ensure that you do not have anonymous users. Additionally, make sure each person authorized to use FTP has his or her own login credentials. This enables auditing of activity.

# ## Weak Passwords

Many FTP systems do not restrict the retrying of a connection multiple times. In that scenario, a malicious user could simply keep trying username and password combinations until a good one is found.

Your action here is to ensure that your password is very difficult to guess. Although there’s no solid rule, here are a few tips:

+   - Use a combination of uppercase and lowercase letters, as well as allowable punctuation.
+   - If your password (no matter if it is uppercase or lowercase) is in a dictionary, or could be similar in spelling, do not use it.
+   - Change your FTP passwords regularly. On a site with lots of FTP users and activity, you should change it every 30 days.

# ## Misconception of Security

Many people believe that FTP is safe and secure. One issue is the sharing of FTP credentials to upload files. This is less of a technical issue and more of a trust issue. That is, in trusting the person to whom you are giving the credentials, you are giving that person and that person’s machine access to your server. If the machine is compromised, that person could easily expose you to the malware.

There was once a case where a site was severely hacked. The attacker came through the FTP server with legitimate credentials. After reviewing the logs and a lot of detective work, it turned out that a subcontractor had hired another subcontractor to assist him.