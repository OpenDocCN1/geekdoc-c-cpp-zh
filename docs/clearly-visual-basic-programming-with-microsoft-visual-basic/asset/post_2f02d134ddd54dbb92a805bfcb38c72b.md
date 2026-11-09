
## CREATING THE USER INTERFACE

The **Windows Form Designer window** is where you create (or design) your application's user interface. The designer window shown in Figure 4-6 contains a **Windows Form object**, or form. A **form** is the foundation for the user interface in a Windows application. A form automatically includes a title bar that contains a default caption—in this case, Form1—as well as Minimize, Maximize, and Close buttons. At the top of the designer window is a tab labeled Form1.vb [Design]. [Design] identifies the window as the designer window. Form1.vb is the name of the file on your computer's hard disk (or on the device designated by your instructor or technical support person) that contains the Visual Basic instructions associated with the form.

![](img/cf88270932e011575089da06b940a1d9_77_0.png)

Figure 4-6: Windows Form Designer window

You create the user interface by adding objects (such as buttons, check boxes, and list boxes) to the form. The objects added to a form are called **controls**. Because the controls are graphical in nature, the user interface is often referred to as a graphical user interface, or **GUI**. You add the controls to the form using the tools contained in the **Toolbox window**. In the next set of steps, you begin creating the Wizard Application interface shown in Figure 4-7. The interface contains four controls: two picture boxes and two labels. You use a **picture box** to display an image on the form. You use **label controls** to display text that the user is not allowed to edit while the application is running. Some label controls simply identify the contents of other controls. The label controls in Figure 4-7, for example, identify the contents of the picture boxes. Label controls also are used in an interface to display program output, such as the result of calculations. In the following steps, you also will learn how to move, delete, undelete, and size a control.

![](img/cf88270932e011575089da06b940a1d9_78_0.png)

**Figure 4-7:** Wizard Application user interface

### To begin creating the Wizard Application user interface:

- 1. Click the **Label** tool in the toolbox, but do not release the mouse button. Hold down the mouse button as you drag the mouse pointer to the lower-left corner of the form. As you drag the mouse pointer, you will see a solid box, as well as an outline of a rectangle and a plus box, following the mouse pointer. Notice that a blue line appears between the form’s left border and the control’s left border, and between the form’s bottom border and the control’s bottom border. The blue lines are called margin lines, because their size is determined by the contents of the control’s Margin property. The purpose of the margin lines is to assist you in spacing the controls properly on a form. See Figure 4-8.

![](img/cf88270932e011575089da06b940a1d9_79_0.png)

Figure 4-8: Label tool being dragged to the form

- 2. Release the mouse button. A label control appears on the form, and an asterisk (*) appears on the designer window's tab to indicate that the form has been changed since the last time it was saved. See Figure 4-9.

![](img/cf88270932e011575089da06b940a1d9_79_1.png)

Figure 4-9: Label control added to the form

- 3. Now you will practice repositioning a control on the form. Place your mouse pointer on the center of the label control, then press the left mouse button and drag the control to another area of the form. (Don't worry about the exact location.) Release the mouse button.
- 4. Next, you will practice deleting and then restoring a control. Press the **Delete** key on your keyboard to delete the label control. Click **Edit** on the menu bar, and then click **Undo** to reinstate the label control.
- 5. Drag the label control back to its original location in the lower-left corner of the form.
- 6. Add another label control to the form. Place the label control in the center of the form.
- 7. Drag the Label2 control until its left border is aligned with the left border of the Label1 control, but don't release the mouse button. When the left borders of both controls are aligned, the designer displays a blue snap line, as shown in Figure 4-10. Because both controls are the same size, their right borders also are aligned.

![](img/cf88270932e011575089da06b940a1d9_80_0.png)

Figure 4-10: A blue snap line appears when the borders are aligned

- 8. Release the mouse button.
- 9. Now drag the Label2 control so that the Label2 text is aligned with the Label1 text. When the text in both controls is aligned, the designer displays a pink snap line, as shown in Figure 4-11.

![](img/cf88270932e011575089da06b940a1d9_81_0.png)

- 10. Release the mouse button.
- 11. Use the PictureBox tool to add two picture boxes to the form. See Figure 4-12. (You do not need to worry about the exact location of the controls in the interface.)

![](img/cf88270932e011575089da06b940a1d9_81_1.png)

- 12. The sizing handles on the PictureBox2 control indicate that it is selected. You can use the sizing handles to make a control bigger or smaller. Use the sizing handles to make the PictureBox2 control either bigger or smaller, then click **Edit** on the menu bar, and then click **Undo** to return the control to its original size.
- 13. You are finished with the Toolbox window, so you can auto-hide it. Auto-hide the Toolbox window.

![](img/cf88270932e011575089da06b940a1d9_82_0.png)

To learn more about adding controls to a form, as well as sizing, moving, deleting, and undeleting the controls, view the Ch04-Controls video.

## SAVE, SAVE, SAVE

It is a good practice to save the current solution every 10 or 15 minutes so that you will not lose a lot of your work if the computer loses power. You can save a solution by clicking File on the menu bar, and then clicking Save All. You also can click the Save All button on the Standard toolbar. When you save a solution, the computer saves any changes made to the files included in the solution. Saving a solution also removes the asterisk that appears on the designer window’s tab.

### To save the current solution:

- 1. Click **File** on the menu bar, then click **Save All**.

## MINI-QUIZ 1

- 1. A ____________ control displays text that the user is not allowed to edit while an application is running.
- 2. The ____________ contains the tools you use to add objects to a form.
- 3. GUI stands for ____________.

## WHOSE PROPERTY IS IT?

Every object in a Visual Basic application has a set of attributes, called **properties**, that determine its appearance and behavior. When an object is created, a default value is assigned to each of its properties. The name and current value of each property appear in the **Properties window** when the object is selected.

### To view the form's properties:

- 1. Click the **form** (but not a control on the form) to select it. Sizing handles appear on the form to indicate that the form is selected, and the form's properties appear in the Properties window.
- 2. Scroll up to the top of the Properties window. If necessary, click the **Alphabetical** button in the Properties window to display the property names in alphabetical order. Most times, it's easier to work with the Properties window when the property names are listed alphabetically.
- 3. Click **(Name)**, which is the third item in the Properties list, to select the form's Name property. Figure 4-13 shows a partial listing of the form's properties. (Notice that items within parentheses appear at the top of the Properties list.)

![](img/cf88270932e011575089da06b940a1d9_83_0.png)

Figure 4-13: Properties window showing some of the form's properties

As indicated in Figure 4-13, the Properties window contains an Object box and a Properties list. The Object box shows the name of the selected object—in this case, Form1. The Properties list has two columns. The left column lists the names of the properties associated with the selected object. The right column contains the Settings box for each property. The Settings box displays the current value, or setting, of the property. For example, the current value of the form’s Name property is Form1. Depending on the property, you can change the default value assigned to a property by selecting the property in the Properties list, and then either typing the new value in the Settings box or selecting a predefined value from a list or dialog box. Although not shown in Figure 4-13, a brief description of the selected property appears in the Description pane located at the bottom of the Properties window.

In the next set of steps, you will change the values assigned to the form’s Text, StartPosition, and Font properties. The Text property controls the caption displayed both in the form’s title bar and on the application’s button on the taskbar while the application is running. The StartPosition property specifies the position of the form when it first appears on the screen after the application is started. The Font property determines the type, style, and size of the font used to display the text on the form. A font is the general shape of the characters in the text. Segoe UI, Tahoma, and Microsoft Sans Serif are examples of font types. Font styles include regular, bold, and italic. The numbers 9, 12, and 18 are examples of font sizes, which typically are measured in points, with one point equal to 1/72 of an inch.

### To change the values assigned to some of the form’s properties:

- 1. Scroll down the Properties list, then click **Text** in the list. Type **Wizard Application** and press **Enter**. The Wizard Application text appears in the Settings box and in the form’s title bar.
- 2. Click **StartPosition** in the Properties list. Click the **down arrow** in the Settings box, then click **CenterScreen** to display the form in the center of the screen when the application is started.
- 3. Click **Font** in the Properties list, then click the **...** (ellipsis) button in the Settings box. Doing this opens the Font dialog box.

For applications created for the Windows Vista environment, Microsoft recommends that you use the Segoe UI font, because it offers improved readability. Segoe is pronounced SEE-go, and UI stands for *user interface*. For most of the controls in the interface, you will use the 9-point size of the font. (Applications created for the Windows XP environment typically use the 10- or 12-point Tahoma font.) You can change the Font property for each control individually; however, an easier way is to change the form’s Font property. Any control whose Font property has not been set individually will be assigned the same font as the form.
