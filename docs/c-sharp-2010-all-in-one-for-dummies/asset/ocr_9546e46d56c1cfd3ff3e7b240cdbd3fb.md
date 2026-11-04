Most of the functions that you use every day, though, are encapsulated within seven mostly new namespaces under the System.Net namespace:

+   - **Cache**: This function has a lot of enumerators that manage the browser and network caching functions built into the namespace.
+   - **Configuration**: This function grants access to the properties that you need to set to make many of the other System.Net classes work.
+   - **Mail**: This function takes over for System.Web.Mail to facilitate the sending of Internet e-mail.
+   - **Mime**: This function bundles file attachments with the Mail namespace.
+   - **NetworkInformation**: This function gets details about the network around your application.
+   - **Security**: This function implements the network security managed by many classes of System.Net.
+   - **Sockets**: This function utilizes the most basic network connections available to Windows.

# Using the System.Net Namespace

The System.Net namespace is code-oriented, which means that few implementations are specifically for user interfaces. Most everything that you do with these classes is behind the scenes. You have few drag-and-drop user controls — the System.Net namespace is used in the Code View.

To demonstrate this, in the rest of this chapter, I go over building a Windows Forms application that has the following requirements:

+   - Check the network status.
+   - Get a specific file from the Internet.
+   - E-mail it to a specific e-mail address.
+   - Log the whole transaction.

This is not an insignificant set of requirements. In fact, even in the 1.0 and 1.1 versions of C#, this would be difficult. One of the main goals of the System.Net namespace in this version is to make common tasks much easier. You can start by loading the sample code or by starting a new project and following the steps in the following sections.