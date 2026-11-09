
## Log Review

Every day, millions of website owners read the newspaper, or get their news online. They watch the morning “talking heads” inform them about what happened in some part of the world. They consume the information that helps them feel informed. Sadly, 99.999 percent of the news they consume makes zero difference to them.

Many website owners rarely (if ever) look at their systems or website logs. If they would do so, they would get a lot more beneficial information that could impact their day. If they would review the log files, they could see things such as disk space usage, bandwidth consumption, attempts to break in, errors on their sites, and much more.

Log files are records of events for such software as operating systems, applications, content management systems, and blog software. Hardware systems such as servers also record logs. Logs are historical, and are critical to your site’s safety. Information you should be interested in includes details about visitors to your site, your system’s applications, and events that may be causing errors within the system.

There are plenty of state and federal regulations for log retention, and there are potentially industry-related laws. Another reason for log retention is, in the event of a lawsuit, you may have a requirement to produce months of data. In all cases, check with your lawyer, because this is not legal advice.

This chapter examines everything you need to know about these logs. That’s not to say that you’ll learn about everything you can know about them, but just the information you need.

The reason that you should care about logs is that they can warn you of impending problems, fraudulent activity, unauthorized activity, or hardware problems such as failing disk drives. If you manage a server, you’ll want to monitor the machine logs. Logs provide a view of activity on your site, allowing you to tweak your site to reach your goals.

In short, logs are the history book for your servers and website.

## Understanding the Need to Retain Logs

From a legal perspective, retaining logs is more and more important to many businesses. In fact, the Payment Card Industry (PCI) Data Security Standard (DSS) dictates the need for a business to “track and monitor all access to network resources and cardholder data.” This means you must ensure that you track your visitors, as well as access to your servers and resources. You are required to ensure that the logs are safe from alteration. Consult with a PCI auditor for specific retention questions for log data.

One benefit of maintaining good logging is the capability to track down what happened after a server or website is hacked.

Here’s a real-world example from an FTP server’s log following an upload of an exploit via FTP on the server. (The source of the attack and some other data have been removed to protect the website’s identity.)

```text
Admin [17/Sep/2010:04:23:44] "*STOR exp_imgownowar.c"
Admin [17/Sep/2010:04:23:44] "*STOR pwnkernel.c"
Admin [17/Sep/2010:04:23:45] "*STOR exp_chedbaary.c"
Admin [17/Sep/2010:04:23:46] "*STOR exp_wunderbar.c"
Admin [17/Sep/2010:04:23:47] "*STOR exp_therebel.c"
Admin [17/Sep/2010:04:23:48] "*STOR exp_moosecock.c"
Admin [17/Sep/2010:04:23:48] "*STOR exp_vmware.c"
Admin [17/Sep/2010:04:23:49] "*STOR exp_framework.h" 226
Admin [17/Sep/2010:04:23:49] "*STOR exp_run_null_exploits.sh"
Admin [17/Sep/2010:04:23:50] "*STOR run_nonnull_exploits.sh"
Admin [17/Sep/2010:04:23:51] "*STOR exp_paokara.c"
Admin [17/Sep/2010:04:23:56] "*STOR exploit.c"
Admin [17/Sep/2010:04:23:56] "*STOR funny.jpg"
Admin [17/Sep/2010:04:23:57] "*STOR exp_powerglove.c"
Admin [17/Sep/2010:04:23:57] "CWD /YourWebSite.com"
Admin [17/Sep/2010:04:23:57] "*STOR exp_run_null_exploits.sh"
```

This log shows that on September 17, the Admin logged into the server at 4:23 AM (local to the server). The files loaded were exploit files meant to bypass several parts of Linux security. The problem is that the real administrator did not log in and upload these files.

The attacker actually had compromised a different machine — one owned by a contract developer who was working on this site. By gaining access to his machine, the attacker was able to grab the username and passwords, attack this website, and more.

Had the logs not been kept, the administrator of the machine would not have been able to track down the source.

A common mistake is not validating the security of a third-party developer’s machines or environment. In this case, the machine was a Mac, and the owner of the machine (the contractor) wrongly assumed that the machine and environment were safe because the developer was not using a PC. The developer was not running anti-virus software on the Mac.

The best course of action in all cases is to set a minimum security standard that third parties must follow. Additionally, assignment of rights to the web server should be specific. That is, if you must provide a password and username, ensure that the information is unique to that individual. This practice will make tracking and auditing easier. Lastly, employ the principle of “least privileges” needed into your standard planning. If third parties don’t need access to everything, then do not allow it.

Logs are important for many reasons, including the following:

- Ensuring legal compliance, such as e-discovery (that is, the process of providing electronic records in a legal discovery)
- Complying with Article 10 of the PCI DSS
- Monitoring the access and activity of third parties
- Ensuring that breaches have not occurred
- Keeping tabs on suspected hacks
- Watching your traffic for trends
- Learning about malfunctions with your site, operating system, or hardware

Throughout the remainder of this chapter, you will learn how to plan, manage, and act on information in your logs.

## Planning for Your Logs

Planning for logs might sound about as fun as going to the dentist. And, yes, sadly, sometimes log management can be painful. However, doing some planning can ease that pain. One great thing is that planning can occur at any time, even if you’ve been running your site for some time.

Your plan should take into account such things as the retention time for logs, when to review (and who reviews) the logs, where you will store the logs, and, of course, how you respond to events.

Most of the time, you can put your logs on auto-pilot with a good plan.

### Developing a Retention Policy

There probably isn’t a good rule that says you must keep logs for “x” months. The amount of time you should keep logs around is very dependent on your business, industry, amount of traffic you receive, and other factors.

The best way to determine how long to retain logs is to consider the following guidelines:

- **Business and legal needs** — Your business may be one that has a legal requirement or a specified need for log retention. This could be that you’re an e-commerce-type business, or perhaps a medically oriented business. It could be that you want to track long-term traffic trends for marketing and search engine optimization (SEO). You will want to define the process used to destroy and retain log data, as well as which logs are to be kept. In this category, your specific needs will outweigh other factors.
- **Size of logs** — Even an average site can quickly create very large access logs. According to Apache.org, 10,000 hits to a website can quickly write out a 1MB log file. This is okay, except when you are trying to review a large log file. If your logs are growing quickly every day, you may want to do a nightly archive, or set up a custom log rotation schedule directly on your server.
- **Time** — In terms of days, weeks, or months, “time” is based on several factors that will be unique to your situation. One thought on this is that logs are nothing more than text files, which compress very well, so storing is not an issue. It’s more of a matter of do you need logs for more than three to six months? After a while, unless it’s a legal requirement or interesting reading, then logs become a filing burden.

### Who Does What and When?

Many of you probably have a small operation. If you only have a single-person company, then who does what is simple. It’s you. If you happen to have a staff of sorts, then it’s a matter of delegation.

The following guidelines are primarily built around business requirements, and not so much around technical requirements:

- **Who do you trust to copy your log files offline?** Who do you trust to log in to your server? Determining who handles the logs is a matter of trust, because giving access to a server is 100 percent trust-based. This holds especially true if you are storing credit card data. The role of the log caretaker should be somewhat of an administrator’s function. If you have a site administrator, then you’ll likely assign this task to the administrator.
- **What the caretaker does with the logs** is, again, very dependent on your business. You may want to perform a review of your logs and just delete
