There is a special item named Pointer (indicated with a small mouse pointer icon) in each tab or the Toolbox. You cannot drag it to the design surface. Click it if you previously selected a component but you changed your mind and don't want to place it on the design surface.

# Components in the Toolbox

The Toolbox always displays a set of components that can be used in the current context. If you are designing a WPF form, only those components appear on the Toolbox that can be added to WPF forms. When you are designing a web page, the appropriate ASP.NET and HTML controls are offered in the Toolbox, but not others (for example, WPF controls).

The current set of documents is determined by the following factors:

+   - Active document — Each document (source code, form designers, UML diagrams, and so on) has an associated designer entity that provides the design surface with its built-in interactions. This designer can co-operate with the Toolbox and tell which components to offer to the user (or any views belonging to the document) gets
- Active solution — The solution loaded into Visual Studio has a hierarchy that may contain components that can be put on the Toolbox. The designer behind the active document can negotiate with the Toolbox that certain components in the active solution must also be displayed.

5-34 shows an example of the Toolbox displayed for the WPF Designer, where the current solution contains several WPF controls.

![](bbox=[0.147, 0.555, 0.903, 0.936])