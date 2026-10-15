
> If you stop and restart your VB6 application, Visual Studio will maintain the attachment, but if you close the VB6 IDE, then you'll need to reattach the debugger in Visual Studio.

## VB6 Development

Overall, the development process in VB6 is simple. Once you have either built your project or deployed it to the machine on which you have the VB IDE, you'll need to add references to both the Microsoft Interop Form Toolkit library and your custom DLL. Keep in mind that both of the DLLs must be registered on your VB6 IDE machine in order for them to be visible. If you are building on the same machine, then they are automatically visible. Once you have added references for these libraries, you can create a new instance of your Interop Form's Form class and call the standard methods and any custom methods you've exposed on that form.

The one key point to remember, which was mentioned earlier but bears repeating, is that if you have created a custom constructor, in order to use it, you will call an Initialize method on your Interop Form's Form class.

## Final Interop Tips

As noted earlier in the book during the discussion of the WPF Interop controls, the Interop control packages aren't perfect. Each has certain limitations that reduces its desirability for the long term. To resolve this, keep track of how much of various branches you have already converted. There will be a point where it is time to convert a larger section so that you can reduce the number of different Interop DLLs that you are using.

Along these lines, note that you can't put an Interop Form and an Interop user control into the same project. Each of these items needs its own DLL; and, in fact, you should consider it a best practice to only expose the DLL for a single form or control. Similarly, don't plan on calling a VB6 form from within your Interop Form. The Interop logic was written to enable you to call .NET from VB6.

In terms of interfaces, the Interop layer was designed to support only a minimum number of interface types. In particular, the String, Integer, and Boolean types should be at the core of what you expect to pass in terms of data. In theory, the Object type is supported, which enables you to pass custom data, so you could pass a Recordset from .NET to VB6 or vice versa; of course, VB6 doesn't know about a Dataset object, so you need to reference VB6 types as the generic object. In general, the best practice is to keep your interfaces as simple as possible.

When you start the VB6 IDE with your project, it attaches to your DLL. Normally this isn't an issue until you first run your VB6 application. At this point, you can't rebuild your Interop project. The Interop project is, in fact, referenced and therefore locked by VB6. If you need to rebuild your Interop project, you need to first shut down the VB6 development environment so that your code will correctly reference your latest build. As noted previously, debugging your Interop project from VB6 isn't the most productive set of steps.

If you change any of the method attributes, you need to regenerate the Interop wrapper classes that you generated in the last step of creating your Interop Forms project. Moreover, although it wasn't covered, you can raise errors from .NET into VB6. To do this, you want to leverage the following method call on the custom My namespace that was defined as part of your Interop Form:

```
My.InteropToolbox.EventMessenger.RaiseApplicationEvent("CRITICAL_ERROR", _ "Error Detail.")
```

The other runtime issue that you may encounter is that certain internal events to your .NET application will not be triggered in the same fashion that they were in VB6. Under VB6, for example, when you referenced a
property on a Form class, this triggered the Load event on that class. Under .NET, the Load event is not fired until the form is being displayed, so you need to recognize the impact on any code that you previously set to run on the Load event.

The remaining issue is related to the VB6 IDE. The IDE and VB6 don’t really recognize that if you have started a .NET DLL, there are other in-memory classes to release. For a deployed application, this isn’t an issue because when the application is closed, all of the memory associated with the application is automatically released. When you are debugging in VB6, however, the core process is associated with the IDE, not your application. As a result, the resources are not released between debugging cycles. To ensure that they are released, you can explicitly instantiate a series of code modifications contained in the Interop help files and release the .NET resources associated with your application. The recommendation is to implement these calls only after your references with the Interop tools are functioning correctly.

## USING THE POWER PACKS 3.0 TOOLS

Unlike the Interop Forms Toolkit, the Power Packs extensions are intended to facilitate some of the same development simplicity that existed in VB6 for tasks such as printing. These classes aren’t meant to support Interop, they are meant to support migration in the sense that the code for creating simple geometric shapes or using the VB style of form printing could be implemented using syntax similar to that of VB6. After these Power Packs were released, the printing syntax was so popular that the Visual Basic team migrated those classes into the core features of Visual Studio 2008. The continued success of the 3.0 features led to the inclusion of the most of the 3.0 Power Packs classes in Service Pack 1 for Visual Studio 2008. These components, along with the repeater control continue to ship with Visual Studio 2010.

Similar to the Interop Forms Toolkit, the Power PacksTools are already installed for Visual Studio 2010. For previous versions of Visual Studio then can be downloaded and installed from the Microsoft downloads. If you review a typical Windows Forms project in Visual Studio 2010, you’ll see the display shown in Figure B-4, which already includes the controls as part of your default Toolbox.

Unlike the Interop Forms Toolkit, there is no need to begin with a special project template. There is no COM Interop involved because the Power Packs don’t target VB6. They target experienced VB developers who want to be able to continue to implement certain tasks in the same way they could in VB6.

When your application ships, you still need to ensure that you create a dependency for the Power Packs library if you aren’t using the DLLs that are included with Visual Studio, but that’s it. Additionally, because the Power Packs are just another set of .NET libraries, there aren’t any issues related to debugging.

For the sample project shown in Figure B-4, you can create a new Windows Forms application and add the PrintForm control to it. Visual Studio 2010 has a Toolbox section for the Visual Basic Power Packs, showing the OvalShape and RectangleShape shape controls along with the LineShape, Data Repeater and PrintForm controls, as shown in Figure B-4.

Add a RectangleShape to the upper section of the display and an OvalShape to the center of the display. Without getting into pages of details here, using the Visual Studio designer, you should customize the look and feel of the display by adding a variety of controls. Take some time to color and fill the shape controls with a solid color. The gradient colors are defined by selecting a fill color (Coral), a FillGradientColor (Navy), a FillGradientStyle (Horizontal), and a FillStyle (Solid). All of this can and should be done within the Visual Studio designer to achieve a display similar to what is shown in Figure B-5.

![](img/d99870e80390742f93963da7be0b2e61_1155_0.png)

## FIGURE B-4

![](img/d99870e80390742f93963da7be0b2e61_1155_1.png)

## FIGURE B-5

The application should build. The next step is to ensure that the check box in the lower-right center, labeled “Landscape” in the figure, is checked. Having done this, label the button in the bottom center of the display “Print Me” and double-click it in the Design view to trigger the automatic event handler generation.
