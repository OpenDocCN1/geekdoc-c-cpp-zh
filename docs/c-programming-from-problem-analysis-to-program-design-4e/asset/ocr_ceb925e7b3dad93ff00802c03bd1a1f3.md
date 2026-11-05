> **NOTE**
> 
> The Control class has over 75 properties and over 100 methods. Not all are useful for every class that derives from it. Thus, you will not see all of the Control members listed in the **Properties** window for classes that derive from it. For example, the **Label** object has its own **Image**, **ImageIndex**, and **ImageList** properties. It does not use Control's **BackgroundImage** method to get or set its background image.

Table 9-3 includes a short list of methods in the System.Windows.Forms.Control class that derived classes inherit. You should explore the online documentation available in Visual Studio to learn about other members. All of the information from Tables 9-2 and 9-3 is developed from the Visual Studio MSDN documentation.

# **TABLE 9-3** System.Windows.Forms.Control methods

| Method | Description |
|---|---|
| Focus( ) | Sets the input focus to the control |
| Hide( ) | Conceals the control from the user |
| Select( ) | Activates a control |
| Show( ) | Displays the control to the user |

> **NOTE**
> 
> One of the most powerful features of the Visual Studio IDE is the extensive help available. You can access Visual Studio's online MSDN documentation web page for help or use installed offline help. Manage help settings from the **HELP** menu option. You **Choose Launch in Browser** or **Launch in Help Viewer** from the **Set Help Preference** menu option. Open the help window using **Ctrl+F1,V**. You can also position your cursor over controls and click on the control or properties and press **F1** to cause the documentation to pop up.

The Show( ) method functions the same way as setting the Visible property to true; Hide( ) does the same thing as setting the Visible property to false. Showing a control is equivalent to setting the Visible property to true. After the Show( ) method is called, the Visible property returns true until the Hide( ) method is called. When you invoke the Focus( ) method with an object such as a textbox, the cursor is positioned on that object. This is very useful when you have a control the user will be typing data into. You will be reading about textboxes later in this chapter.

The System.Windows.Forms.Control class also has a number of predefined events, many of which you will examine in Chapter 10. The System.Windows.Forms.Control click events will be used in this chapter with Button objects.