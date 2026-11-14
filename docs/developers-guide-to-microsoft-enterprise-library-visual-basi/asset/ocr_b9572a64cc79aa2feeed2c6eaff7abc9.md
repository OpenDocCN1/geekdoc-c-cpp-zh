# # Importing Namespaces

After importing the appropriate assemblies in your projects, you will probably want to add **Imports** statements to your project files to simplify your code and avoid specifying objects using the full namespace names. Start by importing the two core namespaces that you will require in every project that uses Enterprise Library:

+   - Microsoft.Practices.EnterpriseLibrary.Common
+   - Microsoft.Practices.EnterpriseLibrary.Common.Configuration

Depending on how you decide to work with Enterprise Library in terms of instantiating the objects it contains, you may need to import two more namespaces. We’ll come to this when we look at object instantiation in Enterprise Library a little later in this chapter.

You will also need to import the namespaces for the specific application blocks you are using. Most of the Enterprise Library assemblies contain several namespaces to organize the contents. For example, as you can see in Figure 3, the main assembly for the Logging block (one of the more complex blocks) contains a dozen subsidiary namespaces. If you use classes from these namespaces, such as specific filters, listeners, or formatters, you may need to import several of these namespaces.

![](bbox=[0.106, 0.425, 0.835, 0.815])

FIGURE 3 Namespaces in the Logging block