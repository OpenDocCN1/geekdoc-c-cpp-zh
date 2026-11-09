
### Advanced Security After Installation

As you have seen, many of the open source CMSs have a number of security add-ons available. Take the time to review all the tools available for your particular CMS to ensure you are safe.

On the commercial front, one tool that does a good job of protecting the PHP-based CMSs against most attacks is *SecureLive* from *SecureLive.net*. It works with Joomla!, Drupal, and WordPress. It offers a number of very strong security features to help defend against hackers, and has a site report card to help you isolate other issues that could result in successful attacks.

Other good security measures to consider deploying are *mod_security* and another open source product, *ConfigServer Firewall* (available from *www.configserver.com*).

The key is to look at all your options (both Open Source and commercial) to ensure that you are not dependent on a *single* product, but rather can layer your defenses.

### Cleanup and Verification Before Going Live

As a general rule, you should ensure that any installation files have been removed, temporary accesses have been changed, and so on, before you go live. Following is a checklist of things to do before you go live:

- Remove administrative access to any non-administrative personnel.
- Make a clean backup of the **new and pristine** site.
- Remove installation files (where appropriate).
- Ensure that any temporary files are removed.
- Double-check file and directory permissions.
- Verify that your design specifications have been met before making a final payment to a third-party developer.
- Record passwords (after you have changed them **all**) in a safe place.
- Copy the database to a separate location.
- Make a list of all third-party add-ons (that is, plug-ins, extensions, add-ons (Plone), themes, templates, and modules).
- Double-check to ensure your CMS application is at the latest version before you launch.

## Summary

In this chapter, you learned about some of the business decisions involved with CMS selection that are often overlooked, decisions such as cost, supportability, and complexity. You learned about two different methods to set up a development environment, and how to do some planning on paper before you start.

You learned about installation for all four CMSs covered in this book in the context of security, including a generic setup and some post-installation tips. You learned about some security tools (both free and commercial), and how to clean things up before you go live.

Chapter 4 takes a look at how to review the security on your existing site, a process known as baselining.

## CHAPTER 4

## Baselining Your Existing Website

In any business operation, you certainly want to consider both man-made and natural disasters that could impact your IT functions. You should create a matrix to identify what threats exist in your operation, the level of impact they could have, and what the plan of action is. This is known as the *baseline*.

In a phrase, this is an analysis of the impact statement to your business — that is, what the loss or reduction of availability of an IT system would have on your business. Out of this, you’ll be able to mix the risk management into your planning.

A very simple example of a baseline report could involve the server environment for your office. You would be concerned about power, backups, and cooling. You should also be concerned about the uninterruptible power supply (UPS), whether you keep backups onsite or take them away, and the capability to cool the server in the summer if you lost air conditioning. Table 4-1 shows what the baseline report for these concerns would look like.

**Table 4-1: Sample Baseline Report**

| SERVER | CONCERNS | THREAT LEVEL AND RECOMMENDED ACTIONS |
|---|---|---|
| Primary server | Power | *Medium* — In the event of a power outage, the systems can run about 20 minutes on the battery-powered UPS. Ensure that the shutdown script runs properly when UPS switches to battery. |
| Server Room | Cooling | *Critical* — In the event that air conditioning is not available in the summer, when it's required, the server must be monitored for overheating. Future plans should include installing a spot cooler in the server room. |
| Recovery | Backup tapes | *Low* — The tapes are stored in the server room. The new plan will be to keep a rotating set of tapes offsite for security. |

This very simple example shows where some of the operational threats are for a system.

This chapter shows you how to review the server and the CMS to make a determination of what threats exist in your site, and what mitigating factors you should employ.

For example, you may find that you are running an older version of a CMS and cannot upgrade because your site's CMS has some custom hacks (changes) made to it. The upgrade would cause those changes to go away. Yet, the version you are on is vulnerable, and you must update. In that situation, your mitigation would be a plan to move those changes to the new version of the CMS, test, document, and deploy. This might be an expensive solution, and would be time-consuming. By building your baseline, you'll be able to see everything that must be updated.

### Starting Your Baseline

Baselining your site can yield quite a bit of valuable information. Some of that information will be useful to you on a regular basis. Following are some baseline items that are general to most sites:

- *Inventory* — What is installed on your site and your server?
- *Version control* — What are the versions of the installed extensions?
- *Patches* — What needs to be updated?
- *Security holes* — Do you have any software or settings (such as open ports) that may be a cause for security concern?
- *Improvement of workflow* — In going through your site, do you see anything that is causing poor performance, such as an older (but not insecure) package installed on your CMS? Or do you have users with too much access?

Determining this baseline gives you a good handle on what you are specifically dealing with in your site. You may have other questions and responses you want to add, depending on your site. The following sections take a closer look at a couple of items on that list.

#### Taking Inventory

When you review your website, you may easily find third-party add-ons that you forgot about. Although they may be disabled on the site, they could be a point of attack. Alternatively, the add-on may have been installed with a valid software installation, but it is simply out of date and vulnerable. Either way, it’s during this inventory period that you can begin the baseline process by capturing all the data in a spreadsheet.

At a minimum, you should capture the following information:

- The version of the CMS you are currently running
- Each third-party add-on that is installed on the system
- Special configurations or setup instructions unique to your website
- Distribution and version of the server’s operating system
- Installed operating system modules such as PHP, MySQL, and so on
- The version of Apache Server that is installed and running
- Specifics about the skin of the CMS (themes, templates, portlets, and so on), including the version, the URL from where you obtained it, and so on

Figure 4-1 shows a sample spreadsheet representing one means to input this type of data. By doing this, you can quickly check what should be updated or removed. Of course, you would add columns or rows to fit your particular environment.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_126_0.png)

**Figure 4-1:** Sample inventory sheet

#### Documentation

Documentation is very valuable. Having it will make your job easier.

Use whatever tool works best for you when you create your baseline documentation. Define the format or tool you will use to capture documentation and stick with it. In other words, don’t change from one to another to another without good reasons.

Your system has many areas to document. Based on your particular needs, you’ll know what those are. The following sections take a look at four areas that are fairly common to look at for your baseline.

##### CMS

As mentioned, for your CMS, you should capture and record the installed components, extensions, modules, plug-ins, or add-ons. Capture the core CMS version information. Don’t forget that there are likely many settings that, if lost, would cause you concern. Document those settings in this report.

Your last update should be noted as follows:

- The name of the software or script
- The installed version
- The current version (the installed and current versions should be the same)
- The date you updated it

This information can help you when reaching out for technical assistance, planning upgrades to new versions, and in recovery.

##### Network

Network documentation might include information for something as simple as a Wi-Fi router or cable modem provided by your ISP. It could be as complex as a router and switches.

Although the following list will vary depending on your setup, these are some typical data points to capture:

- Manufacturer of device
- Firmware (BIOS) version
- Software versions used to manage it
- Telnet settings to connect to it
- IP settings (internally facing and externally facing)
- Subnet mask
