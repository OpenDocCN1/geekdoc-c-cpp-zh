# Figure 33.12: Setting the Binding Policy for an Assembly

> NOTE
> In case the SharedObject Properties dialog box does not appear, right click the SharedObject assembly that you have just added to the Configured Assemblies folder of the ASimpleClient application and select the Properties option.

+   8. Add the version number, i.e. 1.1.0.0, of the new SharedObject assembly in the New Version field under the Binding Policy tab of the SharedObject Properties dialog box.
+   9. Type 1.0.0.0 in the Requested Version column and click the OK button.

Now, run the ASimpleClient application again and click the Call Greetings button, as shown in Figure 33.13:

# Figure 33.13: The Client Application Using the New Version of an Assembly

Figure 33.13 shows that the ASimpleClient application uses the new version of the SharedObject assembly.

# Side-by-Side Execution of Shared Assemblies

Side-by-side execution is a feature that allows developers and users to install different versions of an assembly in GAC and use them without any conflict among different versions. To avoid any conflict, strong names are used, which are already discussed in this chapter in combination with version numbers.

To elaborate the concept of side-by-side execution, let’s assume that you have two applications—App1 and App2—that are using different versions of the SharedObject assembly. App1 and App2 send requests to the CLR when they need to load the corresponding versions of the assembly. App1’s request contains reference for accessing version 1.0.0.0 and App2’s request contains reference for accessing the version 1.1.0.0. CLR uses the assembly’s manifest and the application configuration file to identify the requested version. After identifying