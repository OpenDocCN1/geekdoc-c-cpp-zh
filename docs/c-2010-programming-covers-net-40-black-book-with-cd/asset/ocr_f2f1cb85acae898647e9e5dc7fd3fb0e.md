In the structure of an AD, a forest represents its security boundary. All the AD objects, including users, groups, and resources are stored in a flat database file. Each object stores its own name as well as the container’s name in which it is contained. Each container itself stores its own name as well as the name of its superior container, and so on, up to the root container. Therefore, the structure of AD can be viewed as a tree of containers also.

Now, let’s learn about the following components of AD:

+   - **Forest** — Represents a single directory containing one or more domains.
+   - **Domain** — Refers to a collection of OUs in a hierarchical order.
+   - **OU** — Refers to a collection of users, groups, and computers.
+   - **Domain controller** — Refers to a server running a version of Windows Server 2008, Windows Server 2003, or Windows 2000 Server operating systems and has AD installed.
+   - **Schema** — Provides object definitions that are used to store information in a directory. It is a single component that itself resides in the directory.
+   - **Data store** — Manages the storage and retrieval of data of a domain controller. It contains three layers; where first layer provides interfaces to access a directory, second layer provides the services to perform the operations of reading and writing data, and the third layer consists of the database itself.
+   - **Database** — Stores the data in a file format and it exists on the hard disk of a domain controller.

Let’s learn the significance of AD.

# Significance of Active Directory

AD provides a secure and centralized network that might span a building, city, or multiple locations across a country. It is a distributed directory service within the Windows Server 2008, Windows Server 2003 and Microsoft Windows 2000 Server operating systems. AD enables you access various objects, including all network users, devices, and resources. It also enables you to make groups of these objects for ease of management.

Some advantages of AD are given as follows:

+   - **Scalability** — Enables you to scale a directory to meet any network requirement by including one or more domains with one or more domain controllers.
+   - **Flexible searching** — Allows you to search users and resources, such as a printer or file, on a network.
+   - **Data storage** — Allows you to store the data of your applications at a centralized location that is shared among applications across a Windows network.
+   - **Systematic directory updates** — Updates the directory data in a secure manner over a network by replicating the data between domain controllers in a synchronized way.
+   - **Remote access** — Allows you to remotely access or administer any domain controller connected to the Windows-based computer over a network.
+   - **Domain Name System (DNS) support** — Allows you to use the DNS system that provides a name resolution service to reflect organizational structure on a domain controller.
+   - **Single and extensible schema** — Refers to a schema of objects and rules that provide the structure requirements for AD objects. You can extend this schema by adding new types of objects or object properties.
+   - **Lightweight Directory Access Protocol (LDAP) support** — Allows you to use the LDAP protocol, which is an industry standard directory access protocol, to access AD objects from management and query applications. AD supports the LDAPv3 and LDAPv2 protocols.

Let’s now learn about the AD objects, users and groups.

# Exploring User Accounts and Groups

A user account in AD consists of all the information, such as the user name, password, logon hours, and the profile location, which is needed to define a user in AD. The user account helps the user to log on to a network to access resources after authenticating the user. Authenticating a user means to identify and allow the user to log in and access resources.