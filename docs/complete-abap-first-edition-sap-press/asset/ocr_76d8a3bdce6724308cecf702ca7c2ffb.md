In this section, we’ll explore some of the important ABAP Workbench tools that you'll use to develop ABAP programs. We'll explore other ABAP Workbench tools as we progress through this book.

ABAP Workbench tools are integrated with development objects, and the ABAP Workbench provides forward navigation support to move between objects. For example, if you're editing the program code in the ABAP Editor and come across a statement in which a function module is called, simply double-clicking the function module name will open the function module in the Function Builder tool.

Because you use different ABAP Workbench tools to design and develop various objects in an ABAP application, instead of juggling between ABAP Workbench tools in different screens, SAP provides an application called *Object Navigator* (Transaction SE80).

Object Navigator organizes all the development objects in a tree-like hierarchy, which makes it easy to edit the application’s different objects. We'll look more closely at the structure of the Object Navigator screen in Section 3.2.7.

Let's explore the ABAP Workbench tools and see how they're integrated into the Object Navigator to provide an IDE.

# 3.2.1 ABAP Editor

One of the main components of ABAP Workbench is ABAP Editor, in which you write and edit ABAP code. The main transaction to open ABAP Editor is Transaction SE38, but the editor also is integrated into other ABAP Workbench tools, like Class Builder, Function Builder, and Screen Painter.

In ABAP Editor, you can choose one of three different modes:

+   - **Front-End Editor (New)** (source code mode)
+   
+     The new front-end editor is a universal programming tool optimized for ABAP since the release SAP NetWeaver 7.0 and is available with SAP GUI for Windows 6.40 patch level 10 or higher. It is fully integrated with the SAP environment and provides various features beyond those in the old editor, such as code completion, code templates, changing the color of ABAP keywords and the background color, auto-filling parameter interfaces for procedures, and so on.
+   - **Front-End Editor (Old)** (plain text mode)
+   
+     The old front-end editor works in plain text mode and provides a basic feature