The course of events following the telephone call from the client was to immediately download the logs and then remedy the damage.

The response to the event was enhanced by looking through the log files and determining the path the bad guys took.

The access logs did indeed show the bad guys were there, but nothing too odd showed up in the logs. However, activity in the FTP logs indicated that they had uploaded a lot of server-side attack code in addition to the defacement. The defacement was most likely meant as a distraction while the bad guys worked to launch the server-side code. However, the logs pointed to where they uploaded the code, so it was simple to remove the files and repair the damage.

The next action was to determine how the bad guys obtained the username and password. Three people had access to the credentials. Two of the three people were able to quickly prove they were not the source. As it turned out, the third person had his sites hacked by the same people, and he had the credentials on his machine for the hacked website.

You don’t need to be Sherlock Holmes to figure out that this third person was the source. He installed a virus scanner on his Mac and found he had several infected files and three Trojan horse viruses. Cleaning up the damage was routine from that point on.

Thus, the response to this attack was simple:

+   1. Change all passwords system-wide.
+   2. Copy the log files.
+   3. Clean up damage.
+   4. Review the activity of the attackers in the logs.
+   5. Double-check to ensure it is all gone.
+   6. Find the original attack vector (in this case, the third-party contractor’s desktop) and remove it.
+   7. Block the attackers’ IP address (optional).

Had those logs been unavailable, the cleanup could have been accomplished, but how the bad guys got in would not have been revealed. This, of course, assumed that they didn’t break in by using some vulnerability on the server. To all the security systems involved, there was a genuine user.

Logs are very valuable when responding to incidents. Note that in this real-world case, the review did not entail just a single log, but rather multiple log files.

# Using Logs to Respond to Events

When you hear “responding to an event,” it sounds like you’re sending an RSVP to a party indicating that you’ll be attending. In the context of this discussion, however, “responding to an event” could mean responding to a security event or an outage. In either case, you have a problem.