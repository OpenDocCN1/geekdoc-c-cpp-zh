
## How to add help information

Because Forms applications use the standard Windows interface, users who are already familiar with other Windows applications should quickly adapt to these applications. In addition, you should try to design and develop each application so it is as easy to use as is practical. Nevertheless, almost all applications can benefit from the addition of at least a minimum of help information.

One way to add help information to a form is to add a Help menu. Then, you can add items to the menu for various topics. When the user selects one of these items, you can display a dialog box with the appropriate information. You can also add help information to a form by using tool tips and context-sensitive help.

## How to add tool tips

Earlier in this chapter, you learned how to add tool tips to toolbar buttons. In addition, you can add tool tips to each control over the form and to the form itself. Figure 24-10 shows how.

To tool tips, you add a ToolTip control to the form. Then, a ToolTip property becomes available for the form and each of its controls. This property is listed in the Properties window along the other properties of the form or control. You can set this property to the text you want displayed when the user places the mouse pointer over the form or control. In this figure, for example, the tool tip for the Initial Cost text box on the Deprecation form describes the value that should be entered.

## How to add context-sensitive help

If you want to display help information that is more extensive than what you normally display in a tool tip, you use the HelpProvider control. This control lets you provide context-sensitive help for a form or control. Then, the user can display the help for the control that has the focus by pressing the F1 key. If help text isn't provided for that control, the help text for the form is displayed if it's provided.

To specify the help text for a form or control, you use the HelpString property that becomes available when you add a HelpProvider control to the form. In this figure, for example, the Deprecation form shows some context-sensitive help that describes the function of the form.

## Chapter 24

## How to enhance the user interface

## 75

### A tool tip

![](img/3148667e42d4db35b3d08576aaa1fa01_770_0.png)

### Context-sensitive help

![](img/3148667e42d4db35b3d08576aaa1fa01_770_1.png)

## How to work with a tool tip

- A tool tip is a brief description of a control that is displayed automatically when you place the mouse pointer over that.
- To create tool tips for form, add a ToolTip control to the form. A control named toolTip1 will appear in the Component Designer at the bottom of the window.
- The ToolTip control makes a property named "Tooltip on tooltip1" available for each control on the form and for the tips itself. You can enter the text for the tool tip in this property.

## How to work with context-sensitive help

- To provide context-sensitive help for a form or control, add a HelpProvider control to the form. A control named helpProvider1 will appear in the Component Designer at the bottom of the window. This control makes several properties available for the form and each control it contains.
- To display a text string when the user presses the F1 key for the control that has the focus, enter the text for the "HelpString" property of the control.
- You can also enter text for the HelpString property of the form. Then, that is displayed at the location of the mouse pointer if a help string isn't specified for the control that has the focus.
- When you enter text for the "HelpString on helpProvider1" property, the "ShowHelp on helpProvider1" property automatically changes from false to true.

Figure 24-10 How work with tool tips and context-sensitive help

## Perspective

Now that you've completed this chapter, you have the basic skills for developing applications that use single-document or multiple-document interfaces. In addition, you learned how to add menus, toolbars, and help information to an application. With those skills, you should be able to create applications with professional user interfaces. You should also be able to figure out how to add other enhancements to your interfaces.

## Terms

- single-document interface (SDI) page
- startup form menu
- multiple-document interface (MDI) menu item
- parent form toolbar
- child form tool tip
- tab context-sensitive help

## Exercise 24-1 Create the SDI application

In this exercise, you'll create the SDI version of the Financial Calculations application that's presented in this chapter.

### Open the project and adjust the startup form

1. Open the FinancialCalculations project in the C:\C# 2010\Chapter 24\FinancialCalculationsSDI folder. This project contains the beginning of a startup form from frmMain.
2. Open the Designer window for the startup form, select the PictureBox control, and note how the Image in the Properties window is set. Then, delete this setting and note that the image in the PictureBox is gone. To restore this image, select the Choose image from the PictureBox smart menu to open the Select Resource dialog box. Then, find the name Murach logo in the FinancialCalculationsSDI folder, and complete the dialog boxes.
3. Select the box that contains "Financial Calculations" in a larger normal font size. Then, click on the plus before the Font property in the Properties window, and change the name to Times Roman, change the size to 15, and turn italics on.

### Add existing forms from other projects

4. Use the Adding Item box to add frmFutureValue file in the C:\C# 2010\Chapter 24\FutureValue folder to your project.
5. Use the Adding Item box to add frmDepreciation.cs file in the C:\C# 2010\Chapter 24\Depreciation folder to your project.

### Add the code for the startup form and fix other issues

6. Add code to startup form that creates instances of the Future Value and Depreciation forms and responds to the Click events.
7. Change the Exit button on the Future Value form to a Close button, and change the handler for the Click event so it closes the form instead of exiting the application.
8. If you were to run the application at this point, you would have build errors because the three forms are in different namespaces. One way to fix this is by using statements at the beginning of the startup form that import the Future Value and Depreciation namespaces. Do that now.
9. Run and test the application. When the startup form is displayed, use it to display multiple versions of the Future Value and Depreciation forms. Make sure the Close button on each form works, and make sure the Exit button on the startup form closes all open forms.
10. Another way to fix the names problem is to change the namespaces for the FutureValue and Depreciation forms to FinancialCalculations so all forms are in the same namespace. To test that, delete the statements used in step 9, change the namespaces, and run the application again.
11. Close this version of the Financial project.

## Exercise 24-2 Create the MDI application

In this exercise, you'll create the MDI version of the Financial Calculations application.

### Convert the SDI application to an MDI application

1. Create a copy of the FinancialCalculationsSDI folder. Rename this folder FinancialCalculationsMDI and store it in the C:\C# 2010\Chapter 24.
2. Display the form frmMain in Design view and delete all controls from this form. Then, set the IsMdiContainer property of the Financial Calculations form to true to identify it as the parent form, and resize the form so it's large enough to hold several child forms.

### Add the File menu to the parent form

3. Add a MenuStrip to the form, and note that it's displayed in the Component Designer at the bottom of the Form Designer. Also notice that a box with the words "Type Here" appears at the top of the form.
4. Use the Menu Designer to add the File menu with four menu items that display a new Future Value form, display a new Depreciation form, close the active form, and exit from the application. Include access keys if you like. Then, use the Menu Designer to name these menu items mnuFutureValue, mnuNewDepreciation, mnuClose, and mnuExit, and include a separator between the Close and Exit items.
