# ## Inheriting from the Object Class

You have been creating your own classes since you wrote your first program in Chapter 1. You learned that every `object` created in C# automatically inherits from a base class named `object` that is in the `System` namespace. `Object` has four methods that every `class` written in C# inherits as long as it provides a reference to the `System` namespace. One of these, the `ToString()` method, you have used in many of your programs. Figure 11-2 uses IntelliSense to show the signature for `Object.ToString()` and the names of the other methods inherited from `object`.

![](bbox=[0.187, 0.311, 0.913, 0.502])

**FIGURE 11-2** Methods inherited from an object

# ## Inheriting from Other .NET FCL Classes

You also experienced inheritance when you developed Windows-based programs in Chapters 9 and 10. The Windows forms classes that you created inherited from the `System.Windows.Forms.Form` class. Extending that class enabled you to build on the functionality that was included as part of that .NET Framework class. Adding instantiated objects from classes such as `Button`, `Label`, `TextBox`, and `ListBox` enabled you to add functionality to your program with minimal programming. To inherit from the `System.Windows.Forms.Form` class, new entries were added to your `class` definition. Figure 11-3 illustrates what Visual Studio adds when you decide to build a Windows application by choosing the **Windows Forms Application** template from the Project Type menu.

```
~~~csharp
public partial class PresentationGUI : Form
{
~~~
```

**FIGURE 11-3** Derived class