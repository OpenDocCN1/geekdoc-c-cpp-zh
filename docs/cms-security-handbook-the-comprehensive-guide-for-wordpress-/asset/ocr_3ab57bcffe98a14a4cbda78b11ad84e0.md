# ## Advanced Security After Installation

As you have seen, many of the open source CMSs have a number of security add-ons available. Take the time to review all the tools available for your particular CMS to ensure you are safe.

On the commercial front, one tool that does a good job of protecting the PHP-based CMSs against most attacks is *SecureLive* from *SecureLive.net*. It works with Joomla!, Drupal, and WordPress. It offers a number of very strong security features to help defend against hackers, and has a site report card to help you isolate other issues that could result in successful attacks.

Other good security measures to consider deploying are *mod_security* and another open source product, *ConfigServer Firewall* (available from *www.configserver.com*).

The key is to look at all your options (both Open Source and commercial) to ensure that you are not dependent on a *single* product, but rather can layer your defenses.

# ## Cleanup and Verification Before Going Live

As a general rule, you should ensure that any installation files have been removed, temporary accesses have been changed, and so on, before you go live. Following is a checklist of things to do before you go live:

+   - Remove administrative access to any non-administrative personnel.
+   - Make a clean backup of the **new and pristine** site.
+   - Remove installation files (where appropriate).
+   - Ensure that any temporary files are removed.
+   - Double-check file and directory permissions.
+   - Verify that your design specifications have been met before making a final payment to a third-party developer.
+   - Record passwords (after you have changed them **all**) in a safe place.
+   - Copy the database to a separate location.
+   - Make a list of all third-party add-ons (that is, plug-ins, extensions, add-ons (Plone), themes, templates, and modules).
+   - Double-check to ensure your CMS application is at the latest version before you launch.