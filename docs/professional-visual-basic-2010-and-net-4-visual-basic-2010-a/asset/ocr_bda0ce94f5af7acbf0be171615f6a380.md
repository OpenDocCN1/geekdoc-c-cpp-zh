The error message provides the steps required to enable external access. At this point, you have two options:

+   Provide the External Access Assembly permission to the user account associated with the database owner — You should not do this unless the second option is not possible. This creates a dangerous security hole in your database. It would mean that any Visual Basic code running on the server has external access permissions, and complete access to the database.

+   Sign the assembly, create an account that uses this signature, and then provide the External Access Assembly permission to that account — This is the preferred method for enabling safe external access by a Visual Basic assembly. By signing your assembly and giving the assembly (and the user id associated with the signature) permission, you are limiting the amount of code that can access other servers.

The following steps outline how to provide external access permissions to a Visual Basic assembly using Visual Studio. First, set the permission level to External, as shown in Figure 12-24, and provide a name for the owner of the assembly. This is done using the Database page of the project’s property pages.

![](bbox=[0.09, 0.31, 0.56, 0.54])

FIGURE 12-24

Once you have enabled external access for your Visual Basic code, you also need to sign your assembly. Sign the assembly on the Signing tab of the properties dialog (see Figure 12-25). Use an existing key file or create a new one.

![](bbox=[0.09, 0.63, 0.64, 0.92])

FIGURE 12-25