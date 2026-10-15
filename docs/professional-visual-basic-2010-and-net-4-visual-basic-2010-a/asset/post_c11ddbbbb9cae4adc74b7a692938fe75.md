
![](img/d99870e80390742f93963da7be0b2e61_943_0.png)

# FIGURE 28-10

![](img/d99870e80390742f93963da7be0b2e61_943_1.png)

# FIGURE 28-11

When you click the OK button, your MagicButton class is now available to you in the Toolbox (see Figure 28-12). Add the Magic.MagicButton control to your form, as shown in Figure 28-13, by dragging the control onto the form. Note that references to AxMagic and Magic are automatically added to the project in the Solution Explorer window within the References folder, as shown in Figure 28-14.

![](img/d99870e80390742f93963da7be0b2e61_943_2.png)

# FIGURE 28-12

![](img/d99870e80390742f93963da7be0b2e61_944_0.png)

# FIGURE 28-13

![](img/d99870e80390742f93963da7be0b2e61_944_1.png)

# FIGURE 28-14

All you need to do now is initialize the Caption property to ON, and code up a handler for the mouse Click event:

```
Private Sub AxMagicButton1_ClickEvent(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles AxMagicButton1.ClickEvent
    AxMagicButton1.CtlState = CType(1 - AxMagicButton1.CtlState, Short)
    If (AxMagicButton1.CtlState = 0) Then
        AxMagicButton1.Caption = "OFF"
    Else
        AxMagicButton1.Caption = "ON"
    End If
End Sub
```

Note something slightly peculiar happening here. In the course of importing the control into .NET, the variable State mutated into CtlState. This is because there is already a class in the AxHost namespace called State, which is used to encapsulate the persisted state of an ActiveX control.

# Trying It All Out, Again

When you run this application, note that the control is in the ON position, as shown in Figure 28-15. If you click the control, it changes to the OFF position, as shown in Figure 28-16.

![](img/d99870e80390742f93963da7be0b2e61_945_0.png)

![](img/d99870e80390742f93963da7be0b2e61_945_1.png)

# USING .NET COMPONENTS IN THE COM WORLD

So far, this chapter has established, through a couple of examples, that you can use your COM legacy components within any of your .NET-based applications. You do not have to throw everything out quite yet. Now it’s time to consider the opposite question: Can you run .NET components in the COM world?

Why on earth would you want to run .NET components in the COM world? It is not immediately obvious, in fact, because migration to .NET would almost certainly be application-led in most cases, rather than component-led. However, it is possible (just) to imagine a situation in which a particularly large application remains not based on .NET, while component development moves over to .NET. Let’s assume that’s the case for the next section. The technology is quite cool, anyway.

# A .NET Component

Let’s take a look at the .NET component. Here, you will implement an exact copy of the functionality created earlier with the MegaCalculator and MeanCalculator components, except you will use Visual Basic 2010, rather than VB6.

Begin by creating a Class Library project called MegaCalculator2. Here is the entire code of the interface for the Class Library:

```
Public Interface IMegaCalc
Sub AddInput(ByVal InputValue As Double)
Sub DoCalculation()
Function GetResult() As Double
Sub Reset()
End Interface
```

Code snippet from IMegaCalc

Now create another Class Library project called MeanCalculator3. This will contain a class called MeanCalc that is going to implement the interface IMegaCalc, as a mirror of the MeanCalc in your original VB6 MeanCalculator2 project. As before, you need to add a reference to MegaCalculator2 first, although, to make this easier, go to the File menu and choose to add an existing project to this solution and import the MegaCalculator2 project into the current solution. Now add a reference to this project that is part of the solution.

Once that reference exists you can add the following class definition for MeanCalc:

```
Public Class MeanCalc
Implements MegaCalculator2.IMegaCalc
Dim mintValue As Integer
Dim mdblValues() As Double
Dim mdblMean As Double
Public Sub AddInput(ByVal InputValue As Double) _
    Implements MegaCalculator2.IMegaCalc.AddInput
mintValue = mintValue + 1
ReDim Preserve mdblValues(mintValue)
mdblValues(mintValue - 1) = InputValue
End Sub
Public Sub DoCalculation() _
    Implements MegaCalculator2.IMegaCalc.DoCalculation
Dim iValue As Integer
mdblMean = 0
If (mintValue = 0) Then Exit Sub
For iValue = 0 To mintValue - 1 Step 1
mdblMean = mdblMean + mdblValues(iValue)
Next iValue
mdblMean = mdblMean / iValue
End Sub
Public Function GetResult() As Double Implements _
    MegaCalculator2.IMegaCalc.GetResult
GetResult = mdblMean
End Function
Public Sub Reset() Implements MegaCalculator2.IMegaCalc.Reset
mintValue = 0
End Sub
Public Sub New()
Reset()
End Sub
End Class
```

Code snippet from MeanCalc

Before compiling this application, make sure the component that you are building is COM-visible. To do this, right-click on the MeanCalculator3 solution within Visual Studio 2010 Solution Explorer and select Properties from the context menu.

From the Properties window, select the Application tab, and then select the Assembly Information button to open the Assembly Information dialog. At the bottom of this dialog you will find a check box called Make assembly COM-Visible (see Figure 28-17). Make sure that this is checked and then compile the application.

This component is quite similar to the VB6 version, apart from the way in which Implements is used. After this is all in place, build the assembly. If you have security issues with this compilation, then you need to ensure that you are running Visual Studio as an administrator. Now we come to the interesting part: How do you register the resulting assembly so that a COM-enabled application can make use of it?

# RegAsm

The tool provided with the .NET Framework SDK to register assemblies for use by COM is called RegAsm. This tool is very simple to use. If all you are interested in is late binding, then you simply run it as presented in Figure 28-18. Make sure you’ve started the Command window as administrator.

![](img/d99870e80390742f93963da7be0b2e61_947_0.png)

FIGURE 28-17

![](img/d99870e80390742f93963da7be0b2e61_947_1.png)

FIGURE 28-18

The only challenge with RegAsm is finding the thing. It is usually found lurking in %SystemRoot%\Microsoft.NET\Framework\<version> where version is the current .NET Framework version number. You might find it useful to add this to your path in the system environment. You can also use the Visual Studio command prompt (found in the Microsoft Visual Studio menu under Visual Studio Tools) to directly access this tool.

However, there is probably even less reason for late binding to an exported .NET component than there is for early binding, so we’ll move on to look at early binding. For this, you need a type library, so add another parameter, /tlb as shown on the following line and in Figure 28-19:

```
C:\Users\[user name]\Documents\Visual Studio 2010\Projects\[Project Hierarchy]
\bin: regasm meancalculator3.dll /tlb:meancalculator3.tlb
```

![](img/d99870e80390742f93963da7be0b2e61_948_0.png)

# FIGURE 28-19

Now, when you look in the target directory, not only do you have the original MeanCalculator3.dll, you’ve also acquired a copy of the MegaCalculator2.dll and two type libraries: MeanCalculator3.tlb and MegaCalculator2.tlb. You may need both of these if you need to register your new libraries on a machine not running .NET (for example a machine with only VB6 installed), so it was good of RegAsm to provide them for you. You need the MegaCalculator2 type library for the same reason that .NET needed the MegaCalculator assembly: because it contains the definition of the IMegaCalc interface that MeanCalculator is using, in this case in a format familiar to Regsvr32. Of course without .NET you still can’t run your components on that machine, but you could have them in place for build purposes.

At that point it is simply a matter of creating a reference to your components in VB6 and running your application. Appendix B talks about the Interop libraries which were provided by the Visual Basic team to simplify this process even further, and if you are working to incorporate .NET capabilities with an existing COM based application it is suggested you refer to this section.

# TlbExp

In fact, Microsoft provides you with not one, but two tools for registering .NET apps as COM objects. The other one is TlbExp, which, as its name suggests, is the counterpart of TlbImp. You can use TlbExp to achieve the same result as RegAsm in the previous section.

# P/INVOKE

While up until now we’ve focused on interfacing with COM, it bears noting that .NET can also interoperate below the COM layer with traditional C/C++ DLLs. Since even with Windows 7 the core interfaces for Windows are provided outside of .NET and often unrelated to COM, you may find yourself wanting to implement a call to get at some operating system level feature. The P/Invoke interface allows .NET developers to make calls to existing or custom methods implemented in a traditional language. However, it is, to say the least, difficult.

I worked on a P/Invoke project for which we manually created each of the necessary interface definitions in order to support calls to external methods. To say that this was a painful process I would prefer to never repeat is an understatement. However, it was an effective way to access capabilities not provided by .NET.

Fortunately, Jarod Parsons, who was working with the Visual Basic team, has helped simplify this process for us. As part of the Visual Basic Team blog on MSDN, Jarod posted an excellent entry that refers to a tool that he helped create which will automatically find and generate P/Invoke proxies for you. You can find his blog post at http://blogs.msdn.com/vbteam/archive/2008/03/14/making-pinvoke-easy.aspx.
