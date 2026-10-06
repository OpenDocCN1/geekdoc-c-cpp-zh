# Oracle SQL Developer Data Modeler for Database Design Mastery

> TIP
nYou might want to close a physical model if you are not using it to free memory for other purposes.

# Defining Users and Roles

To be able to define and grant privileges, you need to define users and roles. And to be able to define users and roles, you need to know what kind of users you will have for the system so you can design the roles and name them accordingly. And of course then create the users and name them accordingly when designing the roles and users is what kind of privileges you will need for the database. The same needs can be grouped together for a role, and a user can be granted all the roles needed. It is also important to create a naming standard for the users and roles. Naming standards for users and roles cannot be documented in Data Modeler, but they must still exist. If the naming standard is clear, creating and maintaining roles, users, and database object privileges is much easier.

> TIP
Agree on naming standards for users and roles.

There are two kinds of users: object owners (schema owner) and individual users who will be granted privileges. You might want to have a different naming standard for these two kinds of users to know which one is which. Every Oracle physical model has the MDSYS and PUBLIC by default. You can create additional users in the Browser pane by right-clicking Users and selecting New. You will see several tabs in the Properties dialog that opens: General, Roles, System Privileges, Clusters, Tables, Indexes, Materialized Views, Views, Dimensions, Sequences, Synonyms, Procedures, Functions, and Comments. In the General properties, you define the name for the user, the authentication method (by password, externally, or globally), and the password (identifier). You can also define the default tablespace, temporary tablespace, profile, and other properties used when generating the DDL for a CREATE USER clause for Oracle 12c. On the Roles tab, you can grant roles to this user, and on the System Privileges this user. On the Comments tab you can type comments on this user. If a user is a schema user and has objects on its schema, those objects are listed on the other tabs in the User Properties dialog.

> NOTE
If you defined schemas in the logical model, they are completely different than these users and are not copied to the physical model.