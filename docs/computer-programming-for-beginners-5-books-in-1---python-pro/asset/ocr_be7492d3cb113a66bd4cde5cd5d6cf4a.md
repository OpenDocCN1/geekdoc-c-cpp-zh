# CHAPTER 8:

Logins, Users and Roles

> > “See first that the design is wise and just; that ascertained, pursue it resolutely.” – William Shakespeare

# ### Server Logins

Server logins are user accounts that are created in SQL servers and use SQL Server authentication, which entails entering a password and username to log into the SQL Server instance. SQL Server authentication is different from Windows Authentication, as Windows doesn’t prompt you to enter your password.

These logins can be granted access to be able to log in to the SQL Server, but don't necessarily have database access depending on permissions that are assigned. They can also be assigned certain server level roles that provide certain server permissions within SQL Server.

# ### Server Level Roles

Permissions are wrapped into logins by Server Level Roles. The Server Level Roles determine the types of permissions a user has.

There are nine types of predefined server level roles:

+   - Sysadmin - can perform any action on the server, essentially the highest level of access.
+   - Serveradmin - can change server configurations and shutdown the SQL server.
+   - Securityadmin - can GRANT, DENY and REVOKE server level and database level permissions, if the user has access to the database. The securityadmin can also reset SQL Server passwords.
+   - Processadmin - provides the ability to end processes that are running in a SQL Server instance.
+   - Setupadmin - can add or remove linked servers by using SQL commands.
+   - Diskadmin - this role is used to manage disk files in the SQL Server.
+   - Dbcreator - provides the ability to use DDL statements, like CREATE, ALTER, DROP and even RESTORE databases.
+   - Public - all logins are part of the ‘public’ role and inherit the permissions of the ‘public’ role if it does not have specific server or database object permissions.