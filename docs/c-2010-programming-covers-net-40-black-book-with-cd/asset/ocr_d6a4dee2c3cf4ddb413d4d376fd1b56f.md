4. Add a new Windows Forms project, named Displayer (also available on the CD-ROM), in the PrivateAssembly solution, to use this DLL file.

5. Right-click the Displayer project in the Solution Explorer and select the Set as StartUp Project option option from the context menu to make this new project the startup project

6. Add the PrivateAssembly.dll reference file in the Displayer project by right-clicking it in the Solution Explorer and selecting Project→Add Reference.

Now, you can use the classes in the PrivateAssembly.dll class library; for example, to use Class1, you refer to it as PrivateAssembly.Class1.

7. Add a Button control on the Form of the to the Displayer application and set its Text property to Call Display.

8. Double click the Button control to generate its Click event handler and add the code, as shown in Listing 33.10:

# Listing 33.10: Showing the Code for the Form1.cs File

```
PrivateAssembly.Class1 c1 = new PrivateAssembly.Class1();
private void button1_Click(object sender, EventArgs e)
{
    c1.Display("Hello from Visual C#!");
}
```

Next, build the Displayer application by using the Build→Build Displayer menu item, and run it. The Form1 appears in which click the button1 button. When you click the button, the Display method displays a message box, as shown in Figure 33.14:

![](bbox=[0.22, 0.42, 0.65, 0.585])

# Figure 33.14: Showing a Message Box After Clicking the Button

Now select the PrivateAssembly reference under the Reference folder of the Displayer application in the Solution Explorer. If you look at the properties of the PrivateAssembly reference, you would find that its Copy Local property is set to True. As a result, if you navigate to the bin\Debug directory (or bin\Release, if you have set your build settings for Release) of the Displayer application, you would find a copy of PrivateAssembly.dll. This is the private assembly which is only used by the Displayer application to execute properly. If this assembly is replaced by a new one or even deleted, only the Displayer application will be affected.

# Creating a Multifile Assembly

We have already seen single-file assemblies in the form of PrivateAssembly.dll, Displayer.exe, ASimpleClient.exe, and SharedObject.dll. Now we learn how assemblies distributed across different files work by creating an application, MultiFileAssembly (available in the CD-ROM). Performing the following steps to create the MultiFileAssembly application:

+   1. Open Notepad and write the code, as shown in Listing 33.11:

# Listing 33.11: Showing the Code for Class1.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```