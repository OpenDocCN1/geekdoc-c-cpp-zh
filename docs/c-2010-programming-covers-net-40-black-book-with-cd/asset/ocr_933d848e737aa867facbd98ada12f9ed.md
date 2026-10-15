+   - The Active Directory Schema snap-in— Examines and changes the definition of AD attributes and object classes.

Let’s now explore the System.DirectoryServices namespace.

# The System.DirectoryServices Namespace

Visual Studio 2010 provides the System.DirectoryServices namespace to access Active Directory Domain Services (ADDS) from your .NET applications. The System.DirectoryServices namespace provides two main classes, DirectoryEntry and DirectorySearcher, which use the Active Directory Services Interfaces (ADSI) technology. ADSI is a set of interfaces that enables you to locate and manage resources on a network. It allows you to work with a variety of network providers, such as Internet Information Services (IIS), LDAP, Novell NetWare Directory Service (NDS), and WinNT. When you create an application by using the ADSI technology, you can perform a variety of tasks, such as backing up databases, accessing files and printers, and administering user accounts and groups.

The structure of ADDS is in the form of a tree containing various nodes. Each node represents an AD object that contains a set of properties. Using the System.DirectoryServices namespace, you can read, write, or modify the properties of these objects, or search or traverse the tree.

The description of DirectoryEntry and DirectorySearcher classes is given as follows:

+   - DirectoryEntry — Allows you to read, write, or modify the properties of AD objects.

+   - DirectorySearcher — Allows you to search a node or an object in the ADDS hierarchy. It is important to note that LDAP is the default ADSI provider that supports searching. LDAP provides a mechanism to connect an application with a network or the Internet to search or modify the data of existing directories. However, LDAP is not used to create directories or specify how a directory service operates.

The major classes of the System.DirectoryServices namespace are defined in Table 37.1:

Table 37.1: Major Classes of the System.DirectoryServices Namespace

| Class | Description |
|---|---|
| DirectoryEntry | Encapsulates a node or an object in the ADDS hierarchy |
| DirectoryEntries | Contains a collection of DirectoryEntry objects |
| DirectorySearcher | Performs search operations against ADDS |
| PropertyCollection | Contains the properties of DirectoryEntry |
| PropertyValueCollection | Contains the values of the DirectoryEntry property |
| ResultPropertyCollection | Contains the properties of a SearchResult instance |
| ResultPropertyValueCollection | Contains the values of the SearchResult property |
| SchemaNameCollection | Contains a list of the schema names that the SchemaFilter property of a DirectoryEntries object can use |
| SearchResult | Encapsulates a node in the AD hierarchy that is returned during a search through DirectorySearcher |
| SearchResultCollection | Contains the SearchResult instances that the AD hierarchy has returned during a DirectorySearcher query |
| SortOption | Specifies how to sort the results of a search |

Noteworthy public properties of the DirectoryEntry class are shown in Table 37.2:

Table 37.2: Noteworthy Public Properties of DirectoryEntry Class

| Property | Description |
|---|---|
| AuthenticationType | Obtains or sets the type of authentication to use |