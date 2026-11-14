The assemblies you should add to any application that uses Enterprise Library are the common (core) assembly, the Unity dependency injection mechanism (if you are using the default Unity container), and the container service location assembly:

+   - Microsoft.Practices.EnterpriseLibrary.Common.dll
+   - Microsoft.Practices.Unity.dll
+   - Microsoft.Practices.Unity.Interception.dll
+   - Microsoft.Practices.ServiceLocation.dll

You will also need the assembly **Microsoft.Practices.Unity.Configuration.dll** if you wish to reference specific Unity configuration classes in your code. However, in the majority of cases, you will not require this assembly.

In addition to the required assemblies, you must reference the assemblies that implement the Enterprise Library features you will use in your application. There are several assemblies for each application block. Generally, these comprise a main assembly that has the same name as the block (such as **Microsoft.Practices.EnterpriseLibrary.Logging.dll**), plus additional assemblies that implement specific handlers or capabilities for the block. You only need these additional assemblies if you want to use the features they add. For example, in the case of the Logging block, there is a separate assembly for logging to a database (**Microsoft.Practices.EnterpriseLibrary.Logging.Database.dll**). If you do not log to a database, you do not need to reference this additional assembly.

# # GAC or Bin, Signed or Unsigned?

All of the assemblies are provided as precompiled signed versions that you can install into the global assembly cache (GAC) if you wish. However, if you need to run different versions of Enterprise Library assemblies side by side, this may be problematic and you may prefer to locate them in folders close to your application.

You can then reference the compiled assemblies in your projects, which automatically copies them to the bin folder. In a Web application, you can simply copy them directly to your application's bin folder. This approach gives you simple portability and easy installation.

Alternatively, you can install the source code for Enterprise Library and use the scripts provided to compile unsigned versions of the assemblies. This is useful if you decide to modify the source code to suit your own specific requirements. You can strong name and sign the assemblies using your own credentials afterwards if required.

For more information about side-by-side operation and other deployment issues, see the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.