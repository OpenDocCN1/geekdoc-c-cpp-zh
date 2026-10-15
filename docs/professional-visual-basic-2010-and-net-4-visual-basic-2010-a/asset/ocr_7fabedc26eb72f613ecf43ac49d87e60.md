```
Dim asmDynamic As [Assembly]
asmDynamic = [Assembly].LoadFrom("http://www.dotnetmasters.com/loancalc2.dll")
```

As previously discussed, the brackets around Assembly are needed because it is a reserved keyword in Visual Basic. The brackets indicate that the word applies to the Assembly class, and the keyword is not being used.

After these lines are executed, the code contains a reference to the assembly at the given location. That enables the reflection operations discussed earlier for finding types in the assembly. Recall that one such operation is getting a reference to a particular type (which could be a class, structure, or enumeration) in the assembly.

For dynamic loading, normally the GetType method of the Assembly class is used to get the reference, using a string that represents the identification of the type. The identification consists of the full namespace path that uniquely identifies the type within the current application. Once a reference to a type is obtained, an instance of the type can be created, even though the assembly was loaded dynamically.

For example, suppose that you wanted to get an instance of a certain form in the assembly, with a namespace path of MyProject.Form1. The following line of code would get a reference to the type for that form:

```
Dim typMyForm As Type = formAsm.GetType("MyProject.Form1")
```

The type reference can then be used to generate an instance of the type. To do this, you need another class in the System namespace called the Activator class. This class has a shared method called CreateInstance, which takes a type reference and returns an instance of that type. You could, therefore, get an instance of the form with these lines:

```
Dim objForm As Object
objForm = Activator.CreateInstance(typeMyForm)
```

CreateInstance always returns a generic object. That means it may be necessary to coerce the returned reference to a particular type to gain access to the type's interface. For example, assuming that you knew the object was actually a Windows form, you could cast the preceding instance into the type of System.Windows.Forms.Form and then do normal operations that are available on a form:

```
Dim FormToShow As Form = CType(objForm, System.Windows.Forms.Form)
FormToShow.MdiParent = Me
FormToShow.Show()
```

At this point, the form will operate normally. It will behave no differently from a form that was in a referenced assembly (except for potential code access security limitations, as discussed in Chapter 32).

If the newly loaded form needs to load other classes in the dynamic assembly, nothing special needs to be done. For example, suppose that the form just shown needs to load an instance of another form, named Form2, that resides in the same dynamically loaded assembly. The standard code to instantiate a form will work fine. The CLR will automatically load the Form2 type because it already has a reference to the assembly containing Form2.

Furthermore, suppose that the dynamically loaded form needs to instantiate a class from another DLL that is not referenced by the application. For example, suppose that the form needs to create an instance of a Customer object, and the Customer class is in a different DLL. As long as that DLL is in the same folder as the dynamically loaded DLL, the CLR will automatically locate and load the second DLL.

# Dynamic Loading Example

To see dynamic loading in action, try the following step-by-step example:

+   1. Create a new Windows Forms Application project in Visual Studio and name it DynamicLoading. On the blank Form1 that appears, drag a Button control from the Toolbox, and set its Text property to Load.
+   2. Double-click the Load button to get to its Click event in the Code Editor. Then go to the top of the code module and insert the following Imports statement:

```
Imports System.Reflection
```