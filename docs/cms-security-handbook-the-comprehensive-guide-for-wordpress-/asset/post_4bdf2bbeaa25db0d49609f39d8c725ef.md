
which means that it has four CPUs working. This particular system would be a great workhorse.

Although it’s not listed in most traditional hosting plans, redundancy is a consideration for performance and uptime. Many servers have a “dual-drive” mirrored system, which means that it utilizes two disk drives. If one fails, then the other has a copy of the data. Although that setup is perfect for safety, keep in mind that you are only reading and writing data (there’s lots of reading and writing that happens) to a single drive. Thus, if your site is a medium or heavy transaction site (such as a heavily trafficked forum site, or an e-commerce site that has many people writing data), you’ll incur a performance penalty while waiting on the drive to complete the writes to the disk. Stated quite simply, more hard drives working tend to cause the entire system to perform better.

*Bandwidth* is a measure of the amount of data transfer to and from your server. For example, every time someone visits your home page, you consume a certain amount of bandwidth. That measure is calculated in a peak period using a measurement called the *95th Percentile*. This means that you can consume bandwidth as needed as long as you remain below an average “peak” level over the month.

Now that the basics have been covered, take a look at some example scenarios and how to estimate them.

> **NOTE 3** Cloud computing is not covered in these models.

## Case 1: Light Website Traffic (Shared Hosting)

Case 1 entails a small website acting as a placeholder for a business, consisting of approximately ten total pages. Traffic is light, around 200 to 250 visitors a month. In this example, the obvious choice would be the smallest shared hosting plan your web host offers. There is no need for more. This server can easily be offline for maintenance and not impact the business.

This website would require an external backup. For the cost of this type of site, the host will not be handling the backup. However, the host will maintain the operating system and associated parts.

As an administrator of a shared hosting website, you need a very basic understanding of hosting applications such as cPanel or WHM and other control panel systems. You must have a light level of knowledge for setting up your database. Three of the four CMSs this book focuses on requires a database.

Communications with the server are typically done through a protocol known as *file transfer protocol (FTP)*. Using an FTP client such as FileZilla will be a normal and possibly daily task.

Backing up your site will rest squarely on your shoulders, with few exceptions. Learning to use the available backup tools from your host will save you on the day you need it.

Finally, you must learn the skill of patching your site and keeping it safe from hackers targeting any of the site’s weaknesses.

## Case 2: Medium Website Traffic (VPS)

For this example, this medium-trafficked site hosts a popular forum discussing hot political topics of the day. It hosts a fair amount of graphics and text. The site administrator will need to monitor the bandwidth to avoid overage charges. Traffic is 50,000 to 70,000 visitors a month. Security is a concern here because of the fact that the site was hacked on a shared hosting account when the business first started. The business also needs more control over the server environment. This site’s primary source of revenue is advertising displayed on the site. For this client, a VPS would be in order.

With virtual systems, the bigger concern is the amount of RAM that is on the system, because most modern servers have more CPU power than they normally use. In a VPS or any virtual system, the more RAM you install on the physical server, the better it can perform. As a result, costs will be much higher than traditional shared hosting. This system will be equipped with 12GB to 16GB of RAM.

The administrative skills needed on a VPS could be higher, depending on the hosting company of choice. For example, Rochen.com offers a great deal of support for its virtual server offering. Other hosting providers may offer the same, more, or less. Take this into consideration as you shop. Choosing a fully managed provider will take care of a lot of issues surrounding server management.

If you are tasked with caring for your VPS, then the skill set should include the same as needed for shared hosting, as well as a few additional skills. These skills could include light management of your firewall, scripting for your mod_security or ConfigServer and firewall applications. You’ll need some command-line Linux skills (or the equivalent Windows skills), as well as knowledge of using the Secure Shell (SSH) protocol. This is a safer means to connect to your server than FTP. Tools such as PuTTY or WinSCP are two popular choices for SSH.

Lastly, you’ll want to gain some knowledge of using phpMyAdmin to manage your databases. The time may come where you have to edit or change items in the database. This is the best method to do so, unless you are a database administrator and can use advanced command-line skills.

The good news is that, with most VPS offerings, the technical support group is there to assist you.

## Case 3: Heavy Website Traffic

The example website for a heavy website traffic scenario is a revenue-generating site that distributes training videos on demand. This popular site serves around 250,000 unique visitors a month. They consume more than 1TB to 1.5TB of bandwidth a month. Given that the site runs 24 hours a day, 7 days a week, the business has little room for downtime, and it needs maximum performance.

The optimal solution for this client would be a pair of machines, with one acting as the primary server. The other machine would be available for development, and would contain a copy of the first system. In the event of an outage, the second system would be put into action. One budgetary consideration here is that the host is doing minimal maintenance of this system.

This solution requires a dedicated server and a trained administrator. Most hosting companies will assist with the software, but for a fee. This is based on the fact that, as a dedicated client, you are expected to know how to administer a server. The tasks at a high level are configuration and updating of the server, which sounds simple in a point-and-click world, but in a Linux world means that being able to perform several difficult tasks is required, including the installation and configuration of PHP, Ruby, Python, Perl, and various other compiler and software tools.

Installation and configuration of your Apache web server, log file rotations, and various other features are not trivial tasks, nor is the setup of your MySQL database server. In most cases, these are handled at a command-line prompt using SSH.

Security is an area the administrator of this machine would spend a great deal of time on. Setting up the various layers of protection requires a strong knowledge of the tools and, in some cases, scripting. Because your dedicated server may likely be running a Secure Sockets Layer (SSL) certificate, the administrator will need to configure and install the certificate.

Having a dedicated machine usually implies a dedicated person with the proper skill set and trustworthiness to be operating at the innermost levels of your business operations.

## Using Backups

These generic work models have provided you with a view of each of the needed skills. One common task across all the models is the need to back up the data to an offsite location. That can be as simple as using a tape or CD-ROM. Or it could be a commercial solution such as www.AkeebaBackup.com that does the backup to an offsite cloud.

In all cases, depending on the host, performance of the website during backups may be impacted. Find out how the host conducts backups and ask about the effect on the performance of your site. Remember, in all cases, it’s your data, and it’s your responsibility to ensure that it is backed up — no matter what.
