> **NOTE** You should perform another full backup of the files and database after you complete any upgrades.

The download of Drupal contains a file called `Upgrade.txt` with the instructions for this process, should you get stuck.

# Updating the Core with Drupal 7

With Drupal 7, although the procedures to update the core from a minor release are easy enough to do, going between major versions requires a different procedure. Take the time review the documentation and plan your upgrade (which will involve finding modules compatible with version 7.0). Read the most current documentation available before you start.

# Updating Drupal Modules

Drupal modules are very easy to update; just follow these steps:

+   1. Download and unzip the module.

> **NOTE** Take time to read the instructions that *may* be with the module. The developer may have a different set of update instructions. If so, those will supersede the instructions presented here.

+   2. Run a full backup and copy the backup file off of the server. Switch the site to maintenance mode by visiting the administrative link at `yoursite.com/admin/settings/site-maintenance`.

+   3. Disable any dependent modules. When it comes to Drupal modules, keep in mind that modules can share dependences with other modules. Thus, you may encounter an issue when trying to disable a module. Don’t worry; disabling a dependent module requires only a few additional steps.

Figure 7-18 shows an example of a module that cannot be disabled until you remove the dependency on another module. Notice that the Content module is grayed out.

![](bbox=[0.132, 0.817, 0.759, 0.93])

**Figure 7-18:** Drupal module dependency