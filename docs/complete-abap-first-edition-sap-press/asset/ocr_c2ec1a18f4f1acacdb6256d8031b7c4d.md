XML Schema-Based Interface: This interface is used when the application processes XML data instead of ABAP Dictionary data—for example, with Web Dynpro ABAP, which defines its own data context. The XML schema-based interface definition looks similar to Figure 18.66. In the XML Schema Source field, you see two options, File and Generated. You can't use the Generated option; it's used when the interface is generated using an API from a Web Dynpro ABAP application. When manually creating an interface, select the File option only.

In the File field, provide the path of the XML file and click the Load button to load the file.

The XML schema, import/export parameters, and exceptions are displayed in the Interface tab. However, you can't make any changes.

![](bbox=[0.142, 0.382, 0.647, 0.52])

**Figure 18.66** XML Schema-Based Interface

Smart Forms-Compatible Interface: This interface type allows you to define an interface that is compatible with applications that have used smart forms previously. The interface defines the parameters that are similar to smart forms; for example, in Figure 18.67, you can see that the Tables option is added to the Form Interface node and to the default importing parameters of the smart form.

This allows you to replace the smart form called with an Adobe form in the application program without having to change the interface parameters.

+   4. For this example, select ABAP Dictionary-Based Interface. The interface, as shown in Figure 18.65, consists of a tree structure on the left, which is used for navigation between different definitions. The right-hand side provides the work area to define the parameters, global definitions, and so on. As you can