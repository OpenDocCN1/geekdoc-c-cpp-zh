because it contains a compiled copy of all your code. Not only is this a great way to secure your source code, but it also enables you to distribute databases that are smaller (because they contain no source code) and always keep their modules in a compiled state.

To create an ACCDE file, choose Save As from the File tab, Save Database As, and Make ACCDE, as shown in Figure 31.24.

# FIGURE 31.24

Create an ACCDE file to protect your database.

![](bbox=[0.168, 0.315, 0.872, 0.586])

# Securing the Environment

A serious Access application must be secured from unauthorized users. The built-in user-level security system (enforced by the ACE database engine, not by Access) provides multiple levels of security. You can, for example, secure a single database object (form, table, report) from individuals, groups, or individuals within groups. A user can even have multiple levels of security (provided the user has been assigned multiple login names). All the Access security objects, their properties, and methods are accessible throughout Access Visual Basic code.

User-level security is available only in the MDB database format. The ACCDB format provides other types of data protection, such as password-protected strong encryption, that is not