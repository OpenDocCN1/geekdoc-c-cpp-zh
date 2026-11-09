
## Why Activate Your Disaster Recovery Plan?

The *why* behind activating your disaster recovery plan means that some emergency situation previously being defined by the plan you created has arisen. This reason could be any number of issues such as power failure, data loss, or, in this example, a cyber attack.

## Who Should Activate the Plan?

If you are a one-person operation, then *who* will determine that an emergency exists and declare the emergency will be you. In a larger operation (such as a small or medium-sized company), a documented chain of command is usually in place. When a disaster has been declared, the process should be followed to restore operations.

Another tenet of this activation plan is a defined process to notify the affected personnel in the organization about the disaster. This is the point at which you roll out your communications plan.

## How Do You Restore Operations?

The *how* behind implementing the disaster recovery plan depends greatly on what the issue is. In the case of a cyber attack, your procedures should consider doing a full restore from known good backups.

Now that you understand the basics of a disaster recovery plan, take a look at the specifics surrounding the recovery from a hack.

> **WARNING** Depending on when you made your backup, the restored files may still be infected. Trust your backups, but certainly verify that they, too, have not been infected.

## Tools for Successful Recovery

As part of your recovery toolkit, you should keep a few things close by. Although you will use most of the tools examined in this section, some (such as a digital camera) may be highly optional.

### Virus Scanner

Without a doubt, you should be protecting your desktop machine with a good *virus scanner*. In some cases, the virus scanner may also check for viruses in your files. One preferred virus scanner is Kaspersky available from www.kaspersky.com.

provides you with a secure method for connecting to your website. It has a great graphical interface, and eases the upload and download of files.

- Putty — This tool is used to connect to your server via a shell, and provides a command-line utility to your server. It is available from www.chiark.greenend.org.uk/~sgtatham/putty/download.html.

### Clean Machine from Which to Work

Having a clean machine from which to work is handy for downloading potentially infected files. If you do corrupt the machine, or infect it, you can easily re-image the hard disk and restore the machine to a clean state.

### Hand Tools

Having a screwdriver, pliers, nut-driver, and other essential tools for working directly on a server will make your life easier. This only applies if you have physical access to the machine.

### Digital Camera

This tool requirement is applicable only if you have access to the server. The purposes for the camera include snapping pictures of damage, recording the cable configuration, and many more uses.

## Collecting the Information

You should be aware that what follows is not a detailed method for collecting evidence for submission to a court of law. If you are planning on prosecuting an offender, you should immediately engage a professional forensics company to do proper collection of evidence. Do not attempt to change anything; contact a professional. The law requires very specific steps to gather, store, and transport digital evidence.

Additionally, you may easily miss something that a professional would not. If you have any legal questions regarding this process, consult your attorney, because this book is not offering any legal advice.

For the purposes of this discussion, collecting the information is solely for ensuring that the damage is repaired, and changing processes to prevent attacks in the future.

Logs tell you a lot about what the hacker did or didn't do. Likewise, the absence of logs could indicate the hacker erased them. To do so would require a higher level of privilege than a typical web application break-in.

**NOTE** Not all problems in an operation are related to security. Some can be related to availability meaning that the asset (server) was not available, thus impacting the site.

The server (hardware) logs would be of interest to you if you own your own equipment. Today’s server equipment can tell you a lot about how the machine is doing. Knowing that a potential memory failure exists on the horizon, or that a disk drive has degraded (starting to fail), will allow you to be proactive and replace the suspect component. For breach purposes, many manufacturers will record in BIOS or firmware whether a case has been opened.

Make a copy of all the log files. Set those aside for now on a flash drive or CD-ROM. The purpose of the logs is to re-create a picture of what happened. You’ll learn more about that process shortly.

Copying these logs is very important. Because logs could easily be located in non-standard places, you’ll learn more shortly about the generic means to copy them.

Keep in mind a few rules about logs as you go through them:

- If they are not being saved, then clearly you won’t be able to get them.
- A compromised server could easily have its logs removed. If you choose not to use log rotation, you could run out of disk space, which could cause other problems.
- Copying logs weekly or monthly, and deleting the old ones, should be fine. However, your company’s information security policy will supersede that practice.

### System Logs

Each CMS has a different approach to logging needs. Apache/Linux servers will write to the normal error log and access log locations.

Each CMS provides different logging capabilities:

- *Drupal* — Drupal has several functions (depending on the Drupal version and the logs you want to watch) to help you monitor logs. The three of interest are watchdog, dblog, and syslog. Using these (again, these are version-dependent), you can monitor the events recorded in your logs. You can always pull the logs manually from most web hosts. For example, you can view watchdog logs at Administer > Logs > Recent Log Entries (`admin/logs/watchdog`).
- *Joomla Logging* — Most tools for Joomla! are designed for analyzing traffic to your site, and not necessarily for monitoring errors, and so on. To get detailed information for logging, reviewing the error.log file or the Apache logs directly is best.
- **Plone** — Plone is based on Python, and the logs for Plone are stored at `/var/log/instance.log`.
- **WordPress** — The logging plug-in of choice for WordPress is WPSYSLOG2, available from `ossec.net` (`www.ossec.net/main/wpsyslog2`). This plug-in logs all the system events, including posts, failed logins, logins, and logouts. It records new users, profiles, and records to the system log. This very useful tool can help you greatly in monitoring your logs.

### Apache Access Logs

One proven means of logging is through Apache. The simplest method to access these logs is to log in to your cPanel control system for your web host. As mentioned in Chapter 8, you should have activated the archiving nightly feature.

Find the Raw Access Logs icon. Click it, and one or more log file choices appear, as shown in Figure 9-1. This starts the download process to your local drive, as shown in Figure 9-2.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_320_0.png)

**Figure 9-1:** Raw Apache access logs from a site

![](img/8bd670d4939cf71dbd0c6123d1b834ff_320_1.png)

**Figure 9-2:** Saving or opening log files

In most cases, the download will consist of a compressed file with the extension .gz. Depending on your operating system and tools, you may need to obtain a tool (such as WinZip) to open the file.

You want to review the logs in detail for any correlation to the hack. Such correlations may be repeated requests for files or applications not there. You may see a high number of POSTS in the log file, which indicates an attempt to upload something. The review of logs can be quite daunting at first. However, over time, you'll become accustomed to it.

Take a look at a few examples to help familiarize you with what to look for. Following is an example of a log entry from a Linux server:

```
192.168.1.1 - - [06/Jul/2010:13:49:39 -0400]
"GET /site/index.php?format=feed&type=rss HTTP/
1.0" 200 5965 "-" "Mozilla/4.0 (compatible;"
```

This is a classic example of an Apache log file. As you learned in Chapter 8, this is the common log format. In this case, the visitor is from 192.168.1.1 and is asking for an RSS feed from the site. The 200 indicates all is well. The following are shown an attempted attack:

```
xxx.xxx.xxx.xxx - - [23/Jul/2010:01:15:49 -0400]
"GET /post/com-xxxxx&Itemid=2& task=
../../../../../../../../../../proc/self/environ00
HTTP/1.1" 410 296 www.domain.com - "-" "libwww-perl/5.834" "-"
```

This example from a log file has been edited to protect the source server. However, you can see from the ../../../../../../../../../../ portion of the file that an attack is attempting to exploit a known vulnerability. Following is another sanitized example of a server that has been a victim of a brute-force dictionary attack:

```
11:22:15 ServerName: Failed password for invalid user dola from
xxx.xxx.xxx.xxx port 57725 ssh2

11:22:15 ServerName: sshd[16667]: Failed password for invalid user
consuelo from xxx.xxx.xxx.xxx port 38984 ssh2

11:22:16 ServerName: sshd[16670]: reverse mapping checking getaddrinfo
for xxx.xxx.xxx.xxx.rev.dns.SourceServer.com [xxx.xxx.xxx.xxx]
failed - POSSIBLE BREAK-IN ATTEMPT!

11:22:16 ServerName: sshd[16670]: Invalid user dolores
from xxx.xxx.xxx.xxx

11:22:16 ServerName: sshd[16670]: pam_unix(sshd:auth): check pass;user
unknown

11:22:16 ServerName: sshd[16670]: pam_unix(sshd:auth): authentication
failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=xxx.xxx.xxx.xxx
```
