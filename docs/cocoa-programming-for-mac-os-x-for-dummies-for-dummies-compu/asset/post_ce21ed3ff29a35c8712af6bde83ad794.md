
## Figure 3-15: Click the Build button in project window toolbar to run your project.

![](img/ea40cad434a338535474e82c1a6ace20_80_0.png)

## Chapter 4 Interface Builder

**In This Chapter**

- Finding your way around Interface Builder
- Adding controls to an interface
- Editing attributes of a control
- Editing and creating new menus
- Implementing code to use an interface

The second most important component of Cocoa development (Xcode is the first; see Chapter 3) is the eponymous Interface Builder application, which uses you to build interfaces for your Cocoa projects. Interface Builder gives you the ability to construct beautiful interfaces for your software with drag-and-drop ease — without a lick of code. More importantly, the interfaces you create in Interface Builder follow Apple's stringent Human Interface Guidelines, so you have a good chance of producing applications that Mac users (they can be a finicky bunch) like look at and ultimately use.

In this chapter, you take a tour of Interface Builder, examining its functionality as you go. To help you acclimate to Interface Builder, you improve the calculator application that you created in Chapter 3. By the end of this chapter, your calculator will have a new menu, additional interface elements, and added functionality.

![](img/ea40cad434a338535474e82c1a6ace20_82_0.png)

You can find the project files for the chapter on *For Dummies* Web site at www.dummies.com/go/cocoafd.

### A Tour of Interface Builder

To begin working with Interface Builder, make a copy of the finished Chapter 3 project folder. Always make sure that your Cocoa projects and associated files reside on write-enabled media, which is most likely your hard drive.

After you have copied your code to your hard drive, the following to begin working on the project in Interface Builder:

1. Open the My First Project.xcodeproj file.
   Xcode launches, and the project opens.
2. Expand the project's Resources folder in Xcode to reveal the MainMenu.xib file.
3. In Xcode, double-click the MainMenu.xib file to open it in Interface Builder.

MainMenu.xib is the interface file for your calculator project. Figure 4-1 shows the location of the MainMenu.xib file in Xcode.

Although Xcode and Interface Builder are two different applications, they work together to provide you with an integrated Cocoa experience.

**Figure 4-1: MainMenu.xib contains the interface face for your project.**

![](img/ea40cad434a338535474e82c1a6ace20_83_0.png)

Incidentally, the XIB file extension in MainMenu.xib indicates that it is a newer Interface Builder project file format, introduced in Xcode 3. Previously, the file had a NIB extension, which is short for Next Interface Builder. Why NeXT? NeXT is the name of the company Steve Jobs headed before his return to Apple. Apple produced the Next operating system, which became the core of Mac OS X. The XIB file is a carryover from those days. Cocoa geeks still use these NIB files—old habits die hard. Have you ever tried to pronounce "NeXT”? Furthermore, the AS that appears at the beginning of class names in Cocoa stands for NextStep, another historical tidbit in Cocoa left over from NeXT.

When you first launch Interface Builder, you may see as many as five windows. Figure 4-2 shows the various windows as they appear in Interface Builder. Although it is not one of the five main windows, the Strings window might make an appearance, too. The Strings window is less likely to be present than the others but if you use it, feel free to choose it. You don't use it in this chapter.

![](img/ea40cad434a338535474e82c1a6ace20_84_0.png)

**Figure 4-2: Interface Builder has five main windows.**

Design window

Table 4-1 describes why you need each window and how to display one if it isn't currently visible.

| Table 4-1 Main Windows of Interface Builder |
| :--- | :--- | :--- |
| **Window** | **How to Display It** | **What You Do With It** |
| Project window | Double-click the XIB file in Xcode | Store the components of your interface file. |
| Design window | Double-click the Window icon in the XIB project window | Use the window as part of your application's interface. |
| Inspector window | Choose Tools > Inspector | View and edit attributes of your interface and other classes in the project. |
| Library | Choose Tools > Library | Drag controls from the Library window to a design window to create interface. |
| Menu editor | Double-click the MainMenu icon in the XIB project window | Create, delete, or edit menus for your application. |

Using these five windows forms the main tools of Interface Builder. Using these tools in concert, you can build a complete interface for use in a Cocoa application. That's not all Interface Builder can do, though. You can:

- Create classes in your project.
- Connect classes to the elements of your interface by clicking and dragging. These connections serve as a bridge between an interface and your Xcode project.
- Allow Interface Builder to do the dirty work of writing some of the code for your interface. With one click, it produces the necessary interface and implementation files in Xcode, where you add code later.

### The Interface Builder Project Window

The NIB project window is the heart of your project's interface. This is where you store the components of your project's interface. The NIB project window has three different views much like the Finder:

- **Icon:** List the objects in your XIB file as a grid of large icons. Figure 4-3 shows the Icon view format of the Interface Builder project window.

**Figure 4-3: Use the Icon view to get a quick glimpse of the items in an XIB document.**

![](img/ea40cad434a338535474e82c1a6ace20_86_0.png)

- **List:** The objects in your XIB file as a vertical hierarchy. The List view is useful for locating controls in a window. It comes in handy when you want to select a control that's embedded within other controls (see Figure 4-4). It's also useful when you want to move or copy an embedded control to another object or control when you want to view embedded controls in context.

**Figure 4-4: Use the List view to see the class hierarchy of your XIB project.**

![](img/ea40cad434a338535474e82c1a6ace20_86_1.png)

- **Column:** The objects in your XIB file as a horizontal hierarchy (see Figure 4-5). The Column view is similar to List view, except that it displays the hierarchical arrangement of project items horizontally.

**Figure 4-5: The Column displays hierarchical information horizontally.**

![](img/ea40cad434a338535474e82c1a6ace20_87_0.png)

Each new NIB file that Xcode creates for you as part of a new project has six items by default:

- File's Owner
- First Responder
- Font Manager
- Application
- MainMenu
- Window

MainMenu and Window are what you need to concern yourself with for now. As you can probably guess, the MainMenu is where you edit the menus for your interface. The Window is a window object that you can use in your interface.

### Design Window

The Design represents a window in your interface and is where you add controls. Your user then uses these controls to operate your application. To view a Design window:

1. In the NIB project window, double-click Window.
   The contents of the Window object are displayed, as shown in Figure 4-6.
2. With the window opened, select a control.
   For example, select the Calculate button.

**Figure 4-6: The Design window is where you lay out the controls for your interface.**

![](img/ea40cad434a338535474e82c1a6ace20_88_0.png)

3. Press and hold the Option key and move your cursor around the window.
   As you pass over a control, Interface Builder displays guidelines and numbers informing you of the distance between the selected control and the one with the cursor over it. Figure 4-7 illustrates the distance between the button and the answer field.

**Figure 4-7: Select a control and hold the Option key to display guidelines.**

![](img/ea40cad434a338535474e82c1a6ace20_88_1.png)

4. With the button still selected, press and hold the Option key and move your cursor into a section of the window where no control resides.
   You see guidelines that define the location of the selected button. Figure 4-8 shows the position of the button in the Calculator interface.

![](img/ea40cad434a338535474e82c1a6ace20_88_2.png)

You can move the controls in a Design window by dragging them with the mouse. You can also select a control and move it with the arrow keys. As you move a control around a window, Interface Builder displays guides to help you accurately position the control.
