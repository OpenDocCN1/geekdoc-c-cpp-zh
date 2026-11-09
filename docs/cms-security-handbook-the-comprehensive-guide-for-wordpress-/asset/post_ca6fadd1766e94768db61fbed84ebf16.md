
![](img/8bd670d4939cf71dbd0c6123d1b834ff_114_0.png)

**Figure 3-15:** Drupal Security Review module

![](img/8bd670d4939cf71dbd0c6123d1b834ff_114_1.png)

**Figure 3-16:** Detailed Actions needed

# Permissions

Permissions in this context are associated with the user roles. In Drupal 6, two roles are created, anonymous and authenticated. Drupal 7 has a third default role, administrator.

However, you must observe some rules to maintain security. The Drupal roles are not difficult to understand. Observe a few basic rules:

- Any right granted to the anonymous role is not inherited by the authenticated role.
- Any right granted to the authenticated role is automatically shared by every user who belongs to that group.

For example, if you assign a user authenticated backup duties (that is, you give that user permission to use the “Backup and Migrate” module), then everyone would automatically get the right to use that module. It’s likely that you would not want everyone to have that right. A better way to assign specific roles is to create a role specifically for backup (or other functions). Let’s walk through how to do this.

Figure 3-17 shows an example of the default view of roles.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_115_0.png)

**Figure 3-17:** Default Drupal 6 roles

Suppose you want to add a role to handle the backup functions. To do this, go to the `www.YourSite/admin/user/roles` menu. Here, you click the “Add role” button, as shown in Figure 3-18.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_115_1.png)

**Figure 3-18:** Adding a role in Drupal 6

After you add the role, assign permissions to it by clicking the “edit permissions” option and assigning the permissions, as shown in Figure 3-19.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_116_0.png)

**Figure 3-19:** Assigning backup permissions

You may have noted that, in this example, the backup user role has been restricted from having “delete backup files” privileges. You can choose any level of granularity you need for any role.

The role of `backup_user` is now the only one with the capability to run the backup and restore functions. Had you given the authenticated user role the rights to use the “Backup and Migrate” module, then everyone with login capability could do backups, restores, and delete old backup files. In other words, this would introduce chaos.

## Drupal 7

Permissions are treated very similarly in Drupal 7, with the added benefit of an administrator role already being predefined, as shown in Figure 3-20. As you can see, with Drupal 7, you now have the capability to assign administrative tasks to an administrator role automatically.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_116_1.png)

**Figure 3-20:** Default roles in Drupal 7

This brings up the Zope Management Interface shown in Figure 3-21.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_118_0.png)

**Figure 3-21:** Create a new Plone site

> **NOTE** If the Zope Management Interface does not come up, ensure that your Zope instance is running by typing `./bin/plonectl` at a shell (`$`) prompt.

Click “Create a new Plone site” and follow the prompts to quickly and easily set up your Plone website. To manage it, enter the following:

```
http://localhost:8080/manage
```

To add content, visit the domain where it's installed and log in. From there, you can add content and other code to make the site uniquely yours.

## Other Resources

Chapter 6 of this book shows you how to back up and restore your Plone site. Plone is a very detailed topic and the best documentation is available online.

- For more details on Plone security, see http://plone.org/documentation/kb/securing-plone.
- Because Plone is supported on many different platforms, the instructions for each platform are beyond the scope of this book. For more information, see http://plone.org/documentation/plone-topics/installation.

Plone is a heavy-duty and secure CMS. It requires strong technical skills, and, thus, may be the wrong choice for a small business starting out that does not have access to technical resources.

## Installing WordPress

Of the four CMSs discussed in this book, WordPress is by far the easiest to install. There is very little to go wrong during your WordPress installation.

To begin, uncompress the WordPress installation files and upload them to the root of your website. After you complete this, browse to your site to commence the installation.

The first installation step (using WordPress version 3.0.3) is to create the configuration file, which WordPress can handle for you. As shown in Figure 3-22, simply click the “Create a Configuration File” button.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_119_0.png)

**Figure 3-22:** Automatic creation of `wp-config.php`

The configuration file contains all the pertinent information for your site to function.

The site itself stores its content in a database. The next screen you see provides you with the information you will need to get started. After you understand the information shown in Figure 3-23, click the “Let’s go!” button.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_119_1.png)

**Figure 3-23:** Pre-install checklist

On the ensuing database connectivity screen shown in Figure 3-24, you enter the details regarding the setup of your server. Enter the appropriate data for your setup. One particular point to note is that you can change the Table Prefix `wp_` setting to something else such as `mysite_`. This has the benefit of obscuring attack bots that look for the `wp_` and attempt to attack based on that. However, you can easily just install with the defaults.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_120_0.png)

**Figure 3-24:** WP database setup

After you fill in the database details, WordPress will run a check to ensure that it can talk to the database. If all is well, it shows the message shown in Figure 3-25. When you see this screen, it means that the WordPress installation script was able to successfully connect to the database and is ready to install.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_120_1.png)

**Figure 3-25:** Running actual installation

Click “Run the install” button to continue.

You’ve now reached the part of the installation where you name your site and provide all the personal information, as shown in Figure 3-26. You should rename your username to something other than admin. This helps protect against bots that try a brute-force attack based on the admin username.

> **WARNING** Note that brute-force attacks are not limited to the word *admin*, but will try typical usernames. Choose a name that is semi-difficult to find, or choose a random selection of numbers and letters.

Click “Install WordPress” to complete your installation.

# Optional Security Plug-in for WordPress

In the WordPress plug-in directory (www.wordpress.org) is a *security scan* tool that does a quick check of some basic items. Though very basic, it runs through a checklist of a few items that may be easy to miss. Visit http://wordpress.org/extend/plugins/wp-security-scan to obtain the plug-in. To install the plug-in, use the normal installation routine.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_121_0.png)

**Figure 3-26:** Personalizing the WordPress site

In a test server example, the tool provided a few tips such as no `.htaccess` file being found. Additionally, it said the defaults were still enabled, such as the user `admin` still being present.

You should install this tool and review the report to see what your security is like.

# Shared Hosting

If you are running on a shared hosting server, consider running the following command on your configuration file. This locks out prying eyes from reading your database settings. You need to run this at the command prompt of your server (if available). If you are unable to do that, ask your host to set your permissions.

```
chmod 750 wp-config.php
```

> **NOTE** With your WordPress site, you can force SSL logins and SSL administration, meaning that all your usernames and passwords are sent encrypted to the server. For more information, see http://codex.wordpress.org/Administration_Over_SSL
