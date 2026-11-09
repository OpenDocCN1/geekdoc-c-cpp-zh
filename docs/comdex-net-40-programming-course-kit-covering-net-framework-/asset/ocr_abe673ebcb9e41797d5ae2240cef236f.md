![](bbox=[0.337, 0.136, 0.686, 0.343])

Fig.C#-1.1

![](bbox=[0.213, 0.357, 0.271, 0.397])

**You learn about the interfaces, virtual members, and abstract members in Chapter2, Object-Oriented Programming**

In Fig.C#-1.1, we have right-clicked the **Display()** method and selected the **View Call Hierarchy** option from the context menu to view all calls made from the **Display()** method or made to call the **Display()** method. As a result, the **Call Hierarchy** window opens, displaying all the methods that the **Display()** method calls and all the methods from where the **Display()** method is called, as shown in Fig.C#-1.2:

![](bbox=[0.341, 0.464, 0.684, 0.666])

Fig.C#-1.2

# ### Live Semantic Errors

Semantic errors are grammatically correct statements, but syntactically incorrect. You can check the semantic errors by using the Live Semantics Errors feature. This feature has been enhanced in C# 2010 to display way lines representing errors and warnings for constructs. These constructs include constructs that are outside the method body, such as return types, parameter types, and default values in method declarations.

# ### Named and Optional Arguments

C# 2010 introduces the concept of named and optional arguments. Named arguments allow you to specify an argument for a parameter by associating the argument with the name of the parameter instead of associating it with the position of the parameter in the parameter list. On the other hand, optional arguments allow you to omit arguments for some of the parameters in a parameter list. Named and