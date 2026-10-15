
Having done that, go ahead and write the code for the mean calculation. You do that in a class called MeanCalc:

```
Option Explicit
Dim mintValue As Integer
Dim mdblValues() As Double
Dim mdblMean As Double
Private Sub Class_Initialize()
Reset
End Sub
Private Sub IMegaCalc_AddInput(InputValue As Double)
mintValue = mintValue + 1
ReDim Preserve mdblValues(mintValue)
mdblValues(mintValue) = InputValue
End Sub
Private Sub IMegaCalc_DoCalculation()
Dim iValue As Integer
mdblMean = 0#
If (mintValue = 0) Then Exit Sub
For iValue = 1 To mintValue
mdblMean = mdblMean + mdblValues(iValue)
Next iValue
mdblMean = mdblMean / mintValue
End Sub
Private Function IMegaCalc_GetOutput() As Double
IMegaCalc_GetOutput = mdblMean
End Function
Private Sub IMegaCalc_Reset()
mintValue = 0
End Sub
```

Code snippet from MeanCalc

## Step 2: Registering the Legacy Component

If you have made it this far, then you should now have your legacy component. When developing your new .NET application on the same machine, you do not need to do anything more because your component is already registered by the build process. However, if you are working on an entirely new machine, then you must register it there. To do that, open a command window (on Windows Vista and Windows 7, ensure that you start the command window with administrator permissions) and register it with the following command using regsvr32.exe found at C:\Windows\system32:

![](img/d99870e80390742f93963da7be0b2e61_933_0.png)

FIGURE 28-1

```
regsvr32 MeanCalculator2.dll
```

You should then see the result shown in Figure 28-1.

## The .NET Application

For the .NET application used in this chapter, you only need to instantiate an instance of the MeanCalc object and get it to figure out a mean calculation for you. In order to accomplish that, create a .NET Windows Forms Application project in Visual Basic called CalcApp. Laid out, the form looks like what is shown in Figure 28-2.

The two text boxes are called txtInput and txtOutput, respectively; the second one is not enabled for user input. The three command buttons are btnAdd, btnCalculate, and btnReset, respectively.

![](img/d99870e80390742f93963da7be0b2e61_934_0.png)

# FIGURE 28-2

## Referencing the Legacy COM Component from .NET

Before you dive into writing the code behind the buttons on the form, you first need to make your new application aware of the MeanCalculator2 component. Add a reference to the component via the Project Properties. From the References tab select the “Add…” button to open the Add Reference dialog box. This dialog contains five tabs: .NET, COM, Projects, Browse, and Recent. From the COM tab, select Interop .MeanCalculator2 (see Figure 28-3).

![](img/d99870e80390742f93963da7be0b2e61_934_1.png)

# FIGURE 28-3

Note that in the list of references shown in the References tab, you can now see the MeanCalculator component. This view is presented in Figure 28-4.

![](img/d99870e80390742f93963da7be0b2e61_935_0.png)

FIGURE 28-4

## Inside the .NET Application

Now that you have successfully referenced the components in the .NET application, you can finish coding the application, using the functionality provided via the COM components. To start making use of the new capabilities provided by the COM component, add to the code a global variable (mobjMean) that will hold a reference to an instance of the mean calculation component, as shown here:

```
Public Class Form1
    Dim mobjMean As MeanCalculator2.MeanCalc = New MeanCalculator2.MeanCalc()
```

Code snippet from Form1

Next, add the code behind the form’s buttons. First, working with the Add button, add the following code that calls the COM component:

```
Private Sub btnAdd_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles btnAdd.Click
    mobjMean.AddInput(CDbl(txtInput.Text))
    txtInput.Text = ""
End Sub
```

Code snippet from Form1

This adds whatever is in the input text box into the list of numbers for the calculation. Next, here’s the code-behind for the Calculate button:

```
Private Sub btnCalculate_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles btnCalculate.Click
    mobjMean.DoCalculation()
```

.NET assembly (DLL) that acts as a wrapper for the COM object. If you are doing this a lot, then it might be better to do the wrapping once and for all, and then let your application developers import the resulting .NET assembly instead. Let’s see how you might accomplish this task.

The process that creates the default interop assembly on behalf of Visual Studio is called tlbImp.exe. The name stands for Type Library Import, and that’s pretty much what the process does. It is included in the .NET Framework SDK, and you might find it convenient to extend the PATH environment variable on your machine to include the \bin directory of the .NET Framework SDK.

TlbImp takes a COM DLL as its input and generates a .NET assembly DLL as its output. By default, the .NET assembly has the same name as the type library, which will — in the case of VB6 components — always be the same as the COM DLL. This means you have to explicitly specify a different output file. You do this by using the /out: switch. If you want to see what’s going on at each step in the process, then you should also specify the /verbose flag:

```
tlbimp MeanCalculator2.dll /out:MeanCalculatorNet2.dll
```

Having converted your COM DLLs into .NET assemblies, you can now reference them in an application as you would any other .NET DLL.

## Late Binding

You’ve seen that you can successfully do early binding on COM components within a .NET application, but what if you want to do late binding instead? Suppose you don’t have access to a type library at application development time. Can you still make use of the COM component? Does the .NET equivalent of late binding even exist?

The answer is yes, it does, but it is not as transparent as it is with VB6. Let’s take a look at what occurred in VB6. If you wanted to do early binding, you would do this:

```
Dim myObj As MyObj
Set myObj = New MyObj
MyObj.MyMethod (...)
```

For late binding, it would look like this instead:

```
Dim myObj As Object
Set myObj = CreateObject ("MyLibrary.MyObject")
MyObj.MyMethod (...)
```

There is actually an enormous amount of activity going on under the hood here but most of that is beyond the concern of a .NET developer.

## An Example for Late Binding

For the sample being built in this chapter, let’s extend the calculator to a more generic framework that can feed inputs into a number of different calculation modules, rather than just the fixed one it currently implements. For this example, you’ll keep a table in memory of calculation ProgIDs and present the user with a combo box to select the correct one.

## The Sample COM Object

The first item to note with late binding is that you can only late bind to the default interface, which in this case is MeanCalculator2.MeanCalc. Fortunately, this component was developed as a standalone library, with no references to other interfaces.

## The Calculation Framework

For your generic calculation framework, you’ll create a new application in Visual Basic 2010 called CalcFrame. You will basically use the same dialog box as before, but with an extra combo box at the top of the form. This new layout is illustrated in Figure 28-7.

![](img/d99870e80390742f93963da7be0b2e61_938_0.png)

# FIGURE 28-7

The new combo box is called cmbCalculation. For this to work, you also need to disable the controls txtInput, btnAdd, btnCalculate, and btnReset until you know whether the selected calculation is valid. You'll want to access the properties of the new drop down and add two. Begin your application by importing the Reflection namespace, which you need for handling the application's late binding:

```
Imports System.Reflection
```

Once the form is in place, add a few member variables to the code of your application:

```
Public Class Form1
    Inherits System.Windows.Forms.Form
    Private mstrObjects() As String
    Private mnObject As Integer
    Private mtypCalc As Type
    Private mobjcalc As Object
```

Code snippet from Form1

From there, add a few new lines to Form1_Load:

```
Private Sub Form1_Load(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles MyBase.Load
    mnObject = 0
    AddObject("Mean", "MeanCalculator2.MeanCalc")
    AddObject("StdDev", "StddevCalculator.StddevCalc")
    If (mnObject > 0) Then
        cmbCalculation.SelectedIndex = 0
    End If
End Sub
```

Code snippet from Form1
