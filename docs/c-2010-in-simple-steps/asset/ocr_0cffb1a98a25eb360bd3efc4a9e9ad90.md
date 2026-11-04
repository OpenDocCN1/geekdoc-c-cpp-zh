Let's create an application named MyNamespace to learn to create namespace by performing the following steps:

+   1. Repeat the steps 1 and 2 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
+   2. In the New Project dialog box, select the Visual C# option from the Installed Templates pane and the Class Library option from the middle pane.
+   3. Enter MyNamespace in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
+   4. Click the OK button. The MyNamespace application is created.
+   5. In the Class1.cs file, add the highlighted code given in Listing 4.27:

Listing 4.27: Creating Namespace

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyNamespace
{
    public class MyClass
    {
        public static void MyMethod()
        {
            Console.WriteLine("I am using my Namespace");
        }
    }
}
```

Listing 4.27 shows that you are creating a namespace named MyNamespace, which consists of a class named as MyClass.

6 Select the Build→Build Solution option from the menu bar to build the MyNamespace application.

In the next section, you learn how to reference a user-defined namespace.

# Referencing Namespaces

You can also use a user-defined namespace in your application. To use a user-defined namespace in your application, you must add reference of that namespace to your application.

Let's create an application named MyApplication to learn to add reference of MyNamespace namespace by performing the following steps:

+   1. Repeat the steps 1 to 3 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
+   2. Enter MyApplication in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The MyApplication application is created.
+   4. Right-click the application name, MyApplication, in the Solution Explorer pane (Fig.C#4.27).
+   5. Select the Add Reference option from the context menu, as shown in Fig.C#4.27: