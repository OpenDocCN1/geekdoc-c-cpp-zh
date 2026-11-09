+   - *What prerequisites are there for this patch?* — Find out whether you must uninstall the old code, reboot the machine, or have other code installed with it to make it work.
+   - *Do you have the expertise in-house to apply the patch?* — Some patches may include Apache Web Server upgrades, PHP updates, MySQL updates, and other compiled environments. This could be a situation where some coding must take place.
+   - *Will this patch result in procedural changes?* — Think about scenarios where backup/restores or other documented procedures will change.
+   - *Will this patch result in a reboot?* — Most of the time, this should be “no.” However, if a patch requires the server to be rebooted before it can take effect, then a scheduled downtime is likely in order.
+   - *What downstream clients (internal or external) may be affected?* — What will the impact be to the user community? Will workflows, new login procedures, passwords, or other processes change?
+   - *What departments or organizations should you involve?* — This can include ancillary departments such as compliance, telecom, networking, or even outside vendors.
+   - *What systems may be impacted?* — For example, will your patch change your PCI compliance status?
+   - *Will this patch require a software developer or system administrator to update?* — This can be the case in instances such as PHP or Apache web server updates. Any time you have a compiled application, it involves more than just simply applying patches.

Other questions that may arise will be specific to your environment. After you add any additional questions to this list, set out to write a set of procedures to test and answer these questions before you deploy the patch.

# Obtaining Safe Patches

Your methodology should take into account where the patches are coming from. A few cases have been documented in which a source was contaminated by a hacker, resulting in the distribution of hacked code.

Plenty of cases have also occurred where download sites have been hacked, which may leave you with the impression that the download may not be safe. Fortunately, this occurrence is rare, but be sure to scan everything with a virus-scanning program either during or after the download.

Some websites offer distribution of a patch that is not necessarily the vendor’s or developer’s site. These are referred to as mirror sites. They are usually very safe and should not present any problems.