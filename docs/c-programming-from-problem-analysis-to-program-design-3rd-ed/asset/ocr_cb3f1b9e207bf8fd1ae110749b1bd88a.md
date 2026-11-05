![](bbox=[0.173, 0.096, 0.236, 0.146])

The only requirement for applications with multiple languages is that within the project the source code must use only one language. Thus, if you had a solution file that had three projects, each project could be written in a different language.

# Adding a Reference to the Base Class

Because you are deriving from the Person base class, one of the first things you should do is add a reference to Person.dll. By doing this first, you gain access to the members of the Person class inside this newly created Student class. This can be done several ways in Visual Studio. One option is to use the Solution Explorer window. After selecting the project name, right-click it and select **Add Reference**, as shown in Figure 11–8.

![](bbox=[0.177, 0.343, 0.493, 0.632])

**Figure 11–8**  Adding a reference to a DLL

A window is displayed similar to that shown in Figure 11–9 that enables you to select one of the .NET predefined components or you can use the **Browse** tab to locate Person.dll.