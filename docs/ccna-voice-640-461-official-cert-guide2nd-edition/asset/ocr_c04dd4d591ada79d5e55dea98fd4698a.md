other branches in the tree that must be accessed by going higher than the starting point then back down.

The agreement can specify the root of the domain, but although this is a simple agreement to create, it creates the entire LDAP structure to be searched, which may return unwanted accounts or simply too many accounts.

# LDAP Sync Mechanism

The LDAP Sync agreement specifies when to begin synchronizing and when to repeat the synchronization (a schedule). It is possible to have a synchronization run only once, although this is somewhat unusual.

The first time the synchronization happens, the following events take place:

+   1. All existing end-user accounts in the CUCM database are deactivated (not deleted).
2. Accounts whose CUCM User ID exactly matches a user in LDAP are reactivated, and any settings from LDAP are updated or applied in the CUCM database.
3. Accounts that exist only in LDAP are created in the CUCM database.
4. Any accounts that remain deactivated (meaning they do not exist in LDAP) are deleted from the CUCM database after 24 hours.

# LDAP Custom Filters

The default behavior of LDAP Sync is to import all user accounts from the start point in the tree down. This may cause accounts to be imported that are not wanted. Using a Custom Filter allows an administrator to limit which accounts are imported; for example, a filter could specify that only user accounts in a particular Organizational Unit (OU) are imported. If the filter is changed, a full LDAP sync must be performed for the change to take effect.

# Configure LDAP Sync

Setting up LDAP Sync is surprisingly simple. The main difficulty is typically gaining a full understanding of the target LDAP structure, knowing what containers hold the users to be imported, and knowing where to start the LDAP search.

The basics steps to set up LDAP Sync are as follows:

+   1. Activate the Cisco DirSync service.
2. Configure the LDAP system.
3. Configure the LDAP directory.
4. Configure LDAP Custom Filters.

For CUCM to be able to access and search LDAP, an account must be created in LDAP for CUCM. Configurations may vary between LDAP systems, but the account must essentially read permissions on everything in the search base.