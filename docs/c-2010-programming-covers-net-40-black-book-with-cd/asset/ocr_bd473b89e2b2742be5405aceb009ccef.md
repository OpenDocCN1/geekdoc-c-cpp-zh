# In Depth

In a distributed computing network that contains a number of objects, such as servers, printers, and databases; it becomes difficult for users to locate and use these objects at a specific time. For this purpose, the concept of directory service was introduced. A directory service is used to store all the information required to manage the use of these objects in a centralized location; thereby, simplifying the process of locating and managing these objects. A directory service is different from a directory in the sense that a directory service is both the source of the information and the technique that makes the information available to the users; whereas, a directory simply stores the required information. In addition, a directory service also plays an important role in maintaining the network infrastructure of an organization, administering a system, and controlling the access to company’s information systems. From Windows Server 2000 onwards, a directory service has been introduced with new name, Active Directory (AD).

AD stores information and data about networks and domains on Windows based computers and servers. It contains three basic categories: resources, services, and objects in a hierarchical structure. Resources include hardware resources, such as printers and scanner; services include services of Web email servers, and objects include users in the form of computer nodes of a domain and network.

In this chapter, you learn about AD, its structure, significance, and how to administer it. You also learn about user accounts and groups in AD. Next, you learn about the System.DirectoryServices namespace, which provides classes to access AD from an application created in .NET Framework 4.0. In the Immediate Solutions section, you learn how to create users and groups in AD and create a Windows Forms application to access these users or groups.

Let’s start by learning about the structure of AD.

# Structure of Active Directory

AD includes forests and domains in a hierarchical structure, where a forest is a collection of domains, which in turn are collections of Organization Units(OUs). An OU is a collection of users, groups, and computers; where a user is an individual person, a group is a group of user accounts, and a computer is a specific workstation. Figure 37.1 shows the structure of an AD:

![](bbox=[0.08, 0.71, 0.96, 0.87])

Figure 37.1: Displaying the Structure of AD