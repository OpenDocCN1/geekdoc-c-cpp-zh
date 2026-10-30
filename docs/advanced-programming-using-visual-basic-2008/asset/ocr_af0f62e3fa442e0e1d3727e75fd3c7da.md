# Feedback 1.1

+   1. A set of classes for developing and running Windows applications, Web applications, and WCF services written in multiple languages on multiple platforms.
+   
+   2. What are the meaning and function of each of these terms?
+      a. CLR: Common Language Runtime, an environment that manages the execution of code during run time, including security and memory management.
+      b. CLS: Common Language Specification, standards that specify how a language that interacts with the CLR should behave.
+      c. MSIL: Microsoft Intermediate Language, the result of a compile of a .NET source language.
+      d. PE: Portable executable file, combines the MSIL with metadata.
+   
+   3. Each value type variable has its own memory location; reference type variables refer to an object. If you assign one reference type variable to another, both variables refer to the same object in memory.

# Feedback 1.2

```
CopyrightLabel.Text = My.Application.Info.Copyright
```

# Feedback 1.3

Use one of the time methods of the Now object. A timer is necessary to update the time.

```
Private Sub Timer1_Tick(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Timer1.Tick
    ' Update the time in the status bar.

    CurrentTimeStatusStripLabel.Text = Now.ToShortTimeString
End Sub
```

# Feedback 1.4

```
Dim AnAboutForm As New AboutForm
With AnAboutForm
    .MdiParent = Me
    .Show()          ' Modeless.
    .ShowDialog()    ' Modal.
End With
```