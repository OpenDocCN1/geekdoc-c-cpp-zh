
The archived (compressed) version. Your needs may include reviewing and archiving the log file, and then pulling it offline. If you have a policy of keeping only, say, the last three months of logs, your task would be to delete the fourth month. As you'll see later in this chapter, you can automate some of this by using log rotation.

- *How often* you perform log maintenance is also based on the needs of your business. Your Drupal site may warrant a daily log archive because of the amount of web traffic. Or, having the logs archived weekly (using log rotation) because of low traffic may be fine. The key is the size of the logs. If they are too big, they are difficult to manage; if they're too small, then you're dealing with busy work.

## Determining Where to Store Logs

Storage of your logs means two things: where and how.

Where are you going to *geographically* store them? Will this area be in a file cabinet at your office or at your home? You probably will not need quick and immediate access to your previous log files, so storing at the office or in a box in the closet shouldn't be a problem. Just consider when you would need the log files, and plan accordingly for retrieval. Be sure you take into account the media they are stored on and the environmental conditions.

The *how* in this equation introduces an electronic question. What type of media will you use? Your options include leaving the files on the server, or making an offline copy onto some type of media.

Although not likely to change, the media could be an issue. Media storage choices include CD-ROM, DVD, or USB key. You should not rely on paper copies.

If you really do have a valid reason to keep your log files for a very long term, consider burning them to CD-ROM or DVD. The prices for read-writable DVD burners have dropped to near CD-ROM levels, so cost should not be a factor. Both of these types of media should be around for the duration of your lifetime.

If you're looking at short-term storage (three to four months), then an inexpensive USB key will suffice just fine. Long-term storage on a USB key is a big “no-no.” Among the many reasons for not using a USB key for long-term storage is the prime concern that data may be lost because of the loss or failure of the key. The wash, spin, and dry cycle when laundering your pants (as well as dangers of other everyday events) is a real-world concern for loss of the data.

## Responding to an Incident

The lines of the earlier FTP log example showed an unauthorized upload of files, which resulted in a defaced Joomla! site. Fortunately, the only real damage was that these hackers replaced the `index.php` file, which was easy to fix.

The course of events following the telephone call from the client was to immediately download the logs and then remedy the damage.

The response to the event was enhanced by looking through the log files and determining the path the bad guys took.

The access logs did indeed show the bad guys were there, but nothing too odd showed up in the logs. However, activity in the FTP logs indicated that they had uploaded a lot of server-side attack code in addition to the defacement. The defacement was most likely meant as a distraction while the bad guys worked to launch the server-side code. However, the logs pointed to where they uploaded the code, so it was simple to remove the files and repair the damage.

The next action was to determine how the bad guys obtained the username and password. Three people had access to the credentials. Two of the three people were able to quickly prove they were not the source. As it turned out, the third person had his sites hacked by the same people, and he had the credentials on his machine for the hacked website.

You don’t need to be Sherlock Holmes to figure out that this third person was the source. He installed a virus scanner on his Mac and found he had several infected files and three Trojan horse viruses. Cleaning up the damage was routine from that point on.

Thus, the response to this attack was simple:

- 1. Change all passwords system-wide.
- 2. Copy the log files.
- 3. Clean up damage.
- 4. Review the activity of the attackers in the logs.
- 5. Double-check to ensure it is all gone.
- 6. Find the original attack vector (in this case, the third-party contractor’s desktop) and remove it.
- 7. Block the attackers’ IP address (optional).

Had those logs been unavailable, the cleanup could have been accomplished, but how the bad guys got in would not have been revealed. This, of course, assumed that they didn’t break in by using some vulnerability on the server. To all the security systems involved, there was a genuine user.

Logs are very valuable when responding to incidents. Note that in this real-world case, the review did not entail just a single log, but rather multiple log files.

## Using Logs to Respond to Events

When you hear “responding to an event,” it sounds like you’re sending an RSVP to a party indicating that you’ll be attending. In the context of this discussion, however, “responding to an event” could mean responding to a security event or an outage. In either case, you have a problem.

The steps outlined here represent a philosophy and not so much a hard-and-fast rule. However, they are built on the experience of dealing with hacked websites.

This section may seem out of place given this chapter’s topic of hardening the server, but the inclusion is based on the fact that if there’s a break-in, it’s important to consider where you missed it.

## Obtain the Evidence

The first order of business is to obtain the log files. These will be all the log files on hand, including archived logs.

Copy these to a USB key or to a separate system, such as a laptop. Be sure you have virus protection enabled to prevent anything from getting on to your machine.

Specifically, copy the directory `/var/log`. This will contain several log files, including the following:

- Boot logs
- Cron logs
- Mail logs
- dmesg (for system start-up events)
- Security logs
- Xfer logs (which may be located elsewhere)

It’s important to preserve these logs because they are a record of events. Navigate to your access logs, typically (but not always) located at `/usr/local/apache/logs`. This will house the following very important information:

- Access logs for the server (not the website)
- Error logs
- SuExec logs
- Your archive directory

Once you have these, you should review them to see what is currently on the site.

## Who Is Logged On

Before moving on to cleanup, determine if there is anyone logged in to the server who should not be.

Using the `netstat` command provides you with a great deal of information about the network subsystem. You’re interested in who is connected and who is logged in. The connected users are likely okay, but it’s good to make note of who they are.

At the root prompt, type `netstat -a`. This will provide you with a great deal of connection information.

Another (and simpler) method is to type the letter `w` at the command prompt as follows:

```
# w
```

This will display all *logged in* users. The difference between the two commands presented here is that `netstat` will show you vital information about other processes and services, whereas `w` shows you who is logged in and from where.

If you are responding to an event and *do not* recognize the users who are *logged in*, terminate the user's session using the `kill` command. You should then look at your user list and remove unauthorized users from it.

If these users are logged in as *root*, you must immediately change your password to prevent them from logging back in.

### What Services Are Running

Another task is to determine *what* is running. For example, if you see a backdoor or virus programs running, you can terminate it.

To see all the running services, enter the following command:

```
# ps -all
```

This will provide you with a huge list of services that are running. Unless you spend a lot of time on the Linux console, you may not recognize all of them.

The purpose of running this command is to capture the resulting information for review. Use the following command to send the information to a text file:

```
ps -all >> filename.txt
```

This will write that information to the file you indicate in *filename.txt*. In this command, note that `all` is case-sensitive.

This command provides you with a snapshot. To monitor the services for an ongoing period, use the following command:

```
# top
```

### Historical View

If you believe your server has been hacked, getting a list of historical logins is vital.

To do so, at the root (#) prompt, enter `last`. This will provide you with a list of who logged in, from where, and when. You'll be able to determine if anyone else is logged in as well.

A convenient way to do this is to use the following command:

```
last >> filename.txt
```
