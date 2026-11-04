# Export or Import Breakpoints

Visual Studio 2010 allows you to export or import breakpoints. A breakpoint is a debugging tool that can be used to halt the execution of a .NET application. Breakpoints can be inserted on either a single line of code in a .NET application or on multiple lines of code. The export breakpoints feature allows you to export breakpoints to some other location, such as a different system, to debug a portion of a .NET application. After debugging, the breakpoints can be imported back to the application.

You can export or import breakpoints by using the Breakpoints window, which you can open by selecting Debug→Windows→Breakpoints from the menu bar, as shown in Fig.C+1.21:

![](bbox=[0.28, 0.27, 0.68, 0.48])

Fig.C+1.21

This opens the Breakpoints window.

# Tip

> You can also open the Breakpoints window by using the CTRL+ALT+B keys in combination.

You can insert a breakpoint into a particular piece of code by right-clicking the code and selecting Breakpoint→Insert Breakpoint from the context menu. In Visual Studio 2010, once you have inserted a breakpoint in your application, you can send it to your colleagues along with a bug report. You can pass on breakpoint(s) to your colleagues by using the Export breakpoints button of the Breakpoints window. Breakpoints are exported as an XML file to a location of your choice, from where they can be later imported to a .NET application using the Import breakpoints button of the Breakpoints window, as shown in Fig.C+1.22:

Export Breakpoints Import Breakpoints

![](bbox=[0.24, 0.72, 0.76, 0.81])

Fig.C+1.22

This feature is useful when you need to send the breakpoints through electronic mail (e-mail) to another user or want to change all of the breakpoints at once with a text editor.