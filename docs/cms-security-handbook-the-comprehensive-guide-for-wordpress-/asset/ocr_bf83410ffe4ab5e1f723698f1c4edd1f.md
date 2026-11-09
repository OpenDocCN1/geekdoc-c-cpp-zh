In “Entry 1,” enter the following command:

```
php -q /home/site_directory/public_html/drupal/cron.php
```

The path you enter is specific to your setup.
This allows the scheduler in the Backup and Migrate module to run. Set the options you want for your particular system, and then click Save.

Next, log in to your administrator console in Drupal. For the purposes of this walkthrough, let’s say the Admin Menu module has been installed, so you will be starting there:

+   1. Open the Admin Menu and select Content Management > Backup and Migrate. The module opens, as shown in Figure 6-17.

![](bbox=[0.14, 0.327, 0.707, 0.614])

**Figure 6-17:** Backup and Migrate module

+   2. Click Profiles to set up your specific needs. For the List Profiles option, you will see listed the Default Settings, which is standard. For the purposes of this walkthrough, a profile called files has been created. From this screen, click “Create a new profile”; the Create Profile screen appears, as shown in Figure 6-18.
+   
+   3. Fill in the Profile Name and “Backup file name” fields. Select any additional timestamp, compression, and file encryption options that fit your needs.
+   
+   4. Scroll down the page to see the following categories of options:
+      - **Database Options** — These allow you to include or exclude tables from a database, and/or the data in tables.
+      - **File Backup Options** — These allow you to exclude specific files or directories from your backup.