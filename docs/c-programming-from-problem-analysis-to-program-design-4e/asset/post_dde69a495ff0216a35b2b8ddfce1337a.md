
One additional Label object, label5, is added to the TaxApp form container for the actual tax percentage amount. Because the tax rate is a constant value, the number can be placed on the form at design time. The number can also be used in calculations. This way, users are not required to enter the value.

A good design principle to follow is to keep data entry to a minimum. Limit the amount of typing required by users, and do not have them enter values that can be calculated or obtained from other sources. This reduces the chances that typing errors will corrupt your solutions. It also reduces the amount of coding that might have to be done to deal with data entered in inconsistent formats. If you were to ask users to enter the tax rate for seven and one half percent, one user might enter 0.075; others might enter 7.5%, 7.50%, 7.5 %, 7.5, or 07.50. Entries stored as constants eliminate the need to program for these potential formatting inconsistencies.

After label5 is added to the form, its properties are changed, as shown in Table 9-5.

**TABLE 9-5** TaxApp label5 object properties

| Property | Changes with explanation |
|---|---|
| BackColor | Selected medium blue from Custom tab; changed the value to 50, 50, 192 |
| Font | Selected style of bold italic |
| ForeColor | Selected light blue from Custom tab; could have typed 128, 128, 255 (RGB code for that selection) |
| Text | Typed "7.5%" |

Because labels are not programmed for functionality with this application, the Name property of the Label objects is not changed. The default identifier names (label1, label2, ...) are left as is.

![](img/36e48639a06772bcb0fa1ea2525b33a3_566_0.png)

> Labels are sometimes used to display messages to users during run time. They are especially useful for displaying error messages or text that does not appear with each run of an application. But, labels are most often used primarily to describe other controls on the form.

## TEXTBOX

The TextBox control object, shown in Figure 9–11, can be used to enter data or display text during run time. This is probably the most commonly used control because it can be used for both input and output. Like most other objects of the Control class, the Text property is used to get or set the string value in the control. Normally, a single

**TABLE 9-6 TextBox properties (continued)**

| Property | Description |
|---|---|
| Modified | Gets or sets a value indicating that the TextBox control has been modified since creation or when its contents were last set. |
| MultiLine | Gets or sets a value indicating whether this is a multiline TextBox control. |
| PasswordChar | Gets or sets the character used to mask characters in a single-line TextBox control. |
| ReadOnly | Gets or sets a value indicating whether text in the TextBox is read-only. |
| ScrollBars | Gets or sets which scroll bars should appear in a multiline TextBox control. |
| TextAlign | Gets or sets how text is aligned in a TextBox control. |
| WordWrap | Indicates whether a multiline TextBox control automatically wraps words to the beginning of the next line. |

> **NOTE** The Modified property is not listed in the Properties window because it is used to get or set the value indicating whether the contents of the text box control have been modified by the user since the control was created or its contents were last set.

Remember that in addition to the TextBox properties listed in Table 9-6, all the Control properties and methods shown in Tables 9-2 and 9-3 are available for use with TextBox objects. Several other methods including AppendText(), which adds text to the end of the current text of the TextBox, and Clear() can be used with TextBox objects. There are many interesting events that can be responded to with TextBox objects, and you will read about many of them in Chapter 10.

### ADDING TEXTBOX OBJECTS TO YOUR TAXAPP FORM

Two TextBox objects are added to the TaxApp form. The first is used as an input control allowing the user to enter the total purchase amount. The second is used to display the results of the calculation. Because the values entered or displayed in the TextBox objects must be referenced programmatically, one of the first properties to set is the Name property. textBox1 is renamed txtPurchase, and textBox2 is renamed txtTotalDue. If you want blanks in TextBox objects, you do not have to clear values. By default, the Text property for the TextBox object is set to an empty string.

> **NOTE**
>
> Remember that to set properties, the **Properties** window must be active. If you do not see it on your screen, it can be displayed from the **VIEW** menu. Then click on the control that you want to change and move down the list of properties in the **Properties** window until you locate the property. Type or select the new setting.

Table 9-7 lists the other properties set for the two TextBox objects.

**TABLE 9-7** TaxApp TextBox objects property changes

| Object | Property | Changes with explanation |
| --- | --- | --- |
| textBox1 | Name | Typed txtPurchase |
| textBox2 | Name | Typed txtTotalDue |
| txtPurchase | TextAlign | Selected right |
| txtTotalDue | Enabled | Selected false |
| txtTotalDue | TextAlign | Selected right |

> **NOTE**
>
> As controls, such as text boxes and labels, are placed on the form, they are aligned and sized using **FORMAT, Align**; **FORMAT, Make Same Size**; **FORMAT, Center in Form**; and the other options available from the **FORMAT** menu. You are encouraged to experiment and learn to use these options.

As you build your Windows applications, in addition to seeing what the output looks like in the **Form Designer**, you can run the application at any stage as soon as you start the project by selecting the Windows application template.

The output produced from **TaxApp** (after adding the **Label** and **TextBox** objects and setting their properties) is shown in Figure 9-13.

![](img/36e48639a06772bcb0fa1ea2525b33a3_570_0.png)

**FIGURE 9-13** TaxApp with Label and Button objects

> **NOTE**
>
> If you accidentally double-click on the form when you are using the Form **Designer**, it brings up the **Code** Editor. Entering the **Code** Editor this way has the undesirable side effect of creating a `Form1_Load()` method heading for you. The creation of the event does not create an error when you run your application, but it clutters your program listing with an empty method and a statement that registers the event. If you remove the method heading, you should also remove the statement that registered the form load event (`this.Load += new System.EventHandler(this.Form1_Load);`) in the *Designer.cs* file. This same side effect occurs if you double-click other controls such as labels or text boxes. The `label_Click()` or `textBox_TextChanged()` methods are added.

At design time, you change the Text property by pointing and clicking in the Text property box. But, how do you use the Total Amount value entered by the user? How do you place text in the TextBox object beside the Total Due Label object? This cannot be done at design time. It needs to change based on the value the user enters for Total Amount. You are about to experience the programming power of using C# and Visual Studio. Any and all of the properties you changed during design can be accessed as part of a program statement and changed dynamically when your program runs. To experience this powerful characteristic of C#, you will now add a button that performs some calculations and displays the result in the Total Due TextBox object.

## BUTTON

Button objects are added to your form to increase functionality. They enable a user to click a button to perform a specific task. When it is clicked by a user, the event-handler method is automatically called up—if the button has an event-handler method—and is registered as an event to which your program is planning to respond. You place code in the event-handler method to perform any action you choose. A click event is normally associated with a mouse click; however, the click event can be fired when the Enter key or Spacebar is pressed if the button has the focus.

> **NOTE** Having **focus** means being selected for the next activity. When an object has focus, it often appears different from the other controls. It can appear highlighted or selected with a box surrounding it.

Like other control objects, **Button** objects have a number of properties, methods, and events. They also inherit the properties, methods, and events listed previously in Tables 9–2 and 9–3 from the **Control** class. The **Enabled** property, inherited from the **Control** class, can be used to get or set a value indicating whether the control can respond to user interaction. The **Focused** property is used to determine whether the control has focus or is the one currently selected. The **Focus()** method from the **Control** class is useful with **Button** objects to set the input focus to that control. **TabIndex**, also inherited from **Control**, is useful for setting or getting the tab order of the controls on a form container. Selecting **Tab Order** from the **VIEW** menu shows the sequential order of how focus moves from control to control if the Tab key is used. By default, the tab order is the same order as the order of how the controls are added to the form. You can change this order when you are in **VIEW**, **Tab Order** by clicking the controls sequentially to establish the new order. As you do this, a number representing the **TabIndex** property is displayed beside the control.

> **NOTE** You can also set the tab order from the **Properties** window or by writing program statements. A **Tab** object participates in the tab order in that you can set its **TabIndex**. However, labels never receive focus—meaning the control is not stopped at when you press the Tab key. Instead, it is skipped and the next control, that can take focus, is selected.

For a complete list and description of the **Button** members, you should explore the C# documentation provided with Visual Studio.

### ADDING BUTTON OBJECTS TO YOUR TAXAPP FORM

A Button object is dragged to the bottom of the form and its center is aligned with the center of label1, the heading for the form. The Button object’s Name property is set to btnCompute. As noted previously, when you plan to name a control object, this should be one of the first things that is done after it is placed on the form container. Under most circumstances, it will not create problems for you if the Name is not set first. However, with buttons, if you add a click event before naming the control, you may have to go into the code generated by Form Designer and manually modify the name of
