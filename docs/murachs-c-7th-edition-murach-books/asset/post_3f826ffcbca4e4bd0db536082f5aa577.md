
## A group box that contains two radio buttons

![](img/844f608d10a44654833ea5efc8a2e7a7_330_0.png)

## Common members of radio button and check box controls

| Property | Description |
|----------|-------------|
| Checked | Gets or sets a Boolean value that indicates whether the control is checked. |

| Event | Description |
|-------|-------------|
| CheckedChanged | Occurs when the user checks or unchecks the control. |

## Code that sets the value of a radio button and check box

```
rdoCreditCard.Checked = true;
chkDefault.Checked = true;
```

## Code that checks the value of a radio button

```
private void rdoCreditCard_CheckedChanged(object sender, EventArgs e)
{
    if (rdoCreditCard.Checked == true)
        EnableControls();
    else
        DisableControls();
}
```

## Code that gets the value of a check box

```
bool isDefaultBilling = chkDefault.Checked;
```

## Description

- To determine whether a radio button or check box is checked, you test its Checked property.
- You can use a group box to group controls. Group boxes are typically used to group controls like radio buttons that function as a group.
- To add controls to a group box, drag them from the Toolbox into a group box. If you’ve already added the controls you want to include in the group box to the form, just drag them into the group box.
- Any radio buttons that aren’t placed within a group box function as a separate group.
- If you move a group box, all of the controls it contains move with it.

**Figure 10-4** How to work with radio buttons, check boxes, and group boxes

## A form in Tab Order view before and after the tab order is changed

![](img/844f608d10a44654833ea5efc8a2e7a7_332_0.png)

- To display a form in Tab Order view, select it and then select the View→Tab Order command. This displays the tab index for each control as in the first form above.
- If the form isn’t displayed in Tab Order view, display the Options dialog box (Tools→Options), select the General category in the Environment group, and uncheck the Optimize Rendering for Screens with Different Pixel Densities option.
- To change the tab indexes of the controls, click on the controls in the sequence you want to use. As you click, the new tab indexes appear as in the second form above.
- The first time you click on a control in Tab Order view, the tab index is set to the next number in sequence, starting with zero for the first control. If you click on the same control more than once, the tab index is increased by one each time you click.
- The controls in the group box are displayed with sub indexes as illustrated by the radio buttons above. Then, you can click on the group box to change its index and the main indexes of the controls it contains. To change the sub indexes of the controls in the group box, click on them individually.
- The tab order determines the order in which controls receive the focus when the Tab key is pressed. The TabIndex property of the controls determines this order.
- By default, the value of a control’s TabIndex property is determined by the sequence in which it’s added to the form. The TabIndex property is set to 0 for the first control, 1 for the second control, and so on.
- A label can’t receive the focus. As a result, you typically don’t need to include the labels in the tab order. However, if the label defines an access key, the TabIndex property of the label should be set to one less than its related control. That way, the related control will receive the focus when the access key for the label is activated.
- When setting the tab order, you can skip controls whose TabStop, Enabled, or Visible properties have been set to false, unless those properties will change as the form runs.

## How to get the information you need for using a control

If you click on the All Windows Forms group in the Toolbox, you can see that Visual Studio provides more than 60 different controls that you can use as you develop an application. In this book, though, you’re only going to learn how to use the most useful controls along with their most useful members.

What that means is that you’re going to have to learn how to use other controls on your own. On the job, this is a skill that every professional needs to master because doing this type of research is a large part of application development. The good news is that Microsoft’s online documentation includes an abundance of information on the Windows Forms controls.

The easiest way to get this information is to go to the web address shown at the top of Figure 10-6. Then, you can expand the items in the left pane to locate and display the information you want on a control. In this figure, I started by expanding the “Controls to Use on Windows Forms” item. Then, I expanded the “DateTimePicker Control” item and selected the “DateTimePicker Control Overview (Windows Forms)” topic. This is usually a good place to start when you’re learning how to use a control that you haven’t used before.

Once you have a basic idea of how a control works, you can display other topics that describe specific features or functions of the control. You can do that by using the links that are available within a topic or by selecting topics from the left pane.

In addition to the topics that are listed for a control, you may want to review the members of the class that defines the control. You can do that by clicking the name of the control in a topic to display the topic for the control class. You can also display the information for individual members by selecting them from the left pane.

## The web address for getting help information for controls

https://docs.microsoft.com/en-us/dotnet/framework/winforms/controls/

## Some of the Help documentation for the DateTimePicker control

![](img/844f608d10a44654833ea5efc8a2e7a7_334_0.png)

## Description

- To display the information for a control in Microsoft’s online documentation, go to the web address above and expand the Controls to Use on Windows Forms item in the left pane. Then, expand the item for a control and select a topic.
- To start, you can review the information about the basic function and usage of the control. To do that, select the Overview topic for the control from the left pane of the window to display information like that shown above. You can also view other topics to learn about specific features of the control.
- In addition to information about a control, you can display information about the class for the control. To do that, you can click on a link for the control in the documentation.
- The help information for most control classes includes a summary of all members that are available from the control. You can view more detailed information for a member by clicking on the link for that member in the summary. You can also display this information by expanding the item for the member type in the left pane and then selecting the member.

**Figure 10-6** How to get the information you need for using a control

## How to work with multi-form projects

In previous chapters, you learned how to create applications that consist of a single form. However, most Windows applications use two or more forms. In the topics that follow, you’ll learn the basic skills for creating applications that consist of two or more forms. In particular, you’ll learn how to create an application that consists of a main form and one or more forms that are displayed as dialog boxes.

### How to add a form to a project

When you start a new project for a Windows application, it consists of a single blank form. To add another form to the project, you use the Add New Item dialog box shown in Figure 10-7. From this dialog box, you select the Form (Windows Forms) template and then enter the name of the new form. When you click the Add button, the new form is created with the name you specify.

You can also add an existing form to a project using the Add Existing Item dialog box. This can be useful if you want to use the same form in two different projects or if you want to create a form that’s similar to an existing form. Note that when you add an existing form from another project, that form is copied into the new project. That way, any changes that you make to the form won’t be applied to the original form, which is typically what you want.

Also note that a form you add from another project is typically in a different namespace than the forms in the current project. Because of that, you’ll usually change the namespace for the form so it’s the same as the namespace for the other forms. Alternatively, you can add a using directive for the form’s namespace to each form that refers to it.
