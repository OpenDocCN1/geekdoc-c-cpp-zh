From the Properties window, select the Application tab, and then select the Assembly Information button to open the Assembly Information dialog. At the bottom of this dialog you will find a check box called Make assembly COM-Visible (see Figure 28-17). Make sure that this is checked and then compile the application.

This component is quite similar to the VB6 version, apart from the way in which Implements is used. After this is all in place, build the assembly. If you have security issues with this compilation, then you need to ensure that you are running Visual Studio as an administrator. Now we come to the interesting part: How do you register the resulting assembly so that a COM-enabled application can make use of it?

# RegAsm

The tool provided with the .NET Framework SDK to register assemblies for use by COM is called RegAsm. This tool is very simple to use. If all you are interested in is late binding, then you simply run it as presented in Figure 28-18. Make sure you’ve started the Command window as administrator.

![](bbox=[0.53, 0.08, 0.88, 0.35])

FIGURE 28-17

![](bbox=[0.09, 0.42, 0.75, 0.63])

FIGURE 28-18

The only challenge with RegAsm is finding the thing. It is usually found lurking in %SystemRoot%\Microsoft.NET\Framework\<version> where version is the current .NET Framework version number. You might find it useful to add this to your path in the system environment. You can also use the Visual Studio command prompt (found in the Microsoft Visual Studio menu under Visual Studio Tools) to directly access this tool.

However, there is probably even less reason for late binding to an exported .NET component than there is for early binding, so we’ll move on to look at early binding. For this, you need a type library, so add another parameter, /tlb as shown on the following line and in Figure 28-19:

```
C:\Users\[user name]\Documents\Visual Studio 2010\Projects\[Project Hierarchy]
\bin: regasm meancalculator3.dll /tlb:meancalculator3.tlb
```