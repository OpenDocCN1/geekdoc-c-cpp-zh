OK—so this explains how the compiler improves the last two problems related to code-standability that I mentioned earlier. I haven't yet addressed the first problem: how does a programmer who does not know IndexOf even exists that can operate on a StringBuilder? The answer to this question is in Microsoft Visual Studio's IntelliSense feature. In the editor, when you type a period, Visual Studio's IntelliSense window opens to show you the list of methods that are available. Well, IntelliSense also shows you any extension methods that exist for the type of expression you have to the left of the period. Figure 8-1 shows Visual Studio's IntelliSense icon for an extension method has a down arrow next to it, and the tooltip next to the method indicates that the method is an extension method. This is truly awesome because it is easy to define your own methods on various types of objects and how other programmers discover their methods naturally using these objects of types.

![](bbox=[0.125, 0.297, 0.875, 0.683])

Figure 8-1 Visual Studio's IntelliSense window, extension methods.

# # Rules and Guidelines

There are some additional rules and guidelines that you should know about extension methods:

+   - C# supports extension methods; it does not offer extension properties, extension events, extension operators, and so on.

+   - Extension methods (methods with this before their first argument) must be declared in non-generic, static classes. However, there is no restriction on the name of the class; you can call whatever you want. Of course, an extension method must have at least one parameter, and only the first parameter can be marked with this keyword.

PART II Designing Types