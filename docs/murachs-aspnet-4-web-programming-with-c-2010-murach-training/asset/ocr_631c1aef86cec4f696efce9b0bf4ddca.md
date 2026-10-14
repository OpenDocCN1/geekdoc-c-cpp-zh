# How to use access keys with web server controls

Access keys let the user select controls by using keyboard shortcuts. If, for example, you designate F as the access key for an input field that accepts a customer’s first name, the user can move the focus directly to this field by pressing Alt+F. Figure 6-4 shows how to use access keys with ASP.NET.

To create an access key, you simply add the AccessKey attribute to the control you want to create the keyboard shortcut for. Since this attribute is defined by the System.Web.UI.WebControls.WebControl class, you can use it with any web control. Note, however, that the access keys you define for a form can conflict with the access keys that are defined for a browser. Because of that, you’ll want to be sure to test them with all the modern browsers.

When you use access keys with text boxes and other controls that are identified by literal text, it’s common to underline the access key in the literal text. To do that, you can use a Span element with a class attribute. This is illustrated by the text that identifies the two text boxes in this figure. Here, the class attribute has a value of “accesskey”. Then, you can code a style rule for this class that sets the text-decoration property to underline.

If you use a label to identify a control instead of literal text, you can assign the access key to the label and then underline the appropriate letter of the label. In this case, you should also code the AssociatedControlID attribute to specify the control that should receive the focus when the user uses the access key.

You can also specify an access key for a button control as illustrated by the aspx code in this figure. However, you can’t underline the access key in a button control. That’s because buttons are rendered using the <input type="submit"> HTML element, and this element doesn’t provide a way to format the text that’s displayed by the button.

# How to set the focus on a web server control

ASP.NET provides two features that let you set the focus to a specific control on a form. First, you can use the DefaultFocus attribute of the form to determine which control receives the focus when the page is first displayed. In figure 6-4, for example, this attribute is set to the txtName control.

Second, you can move the focus to a control at runtime. To do that, you use the Focus method of the control. The statement shown in this figure, for example, moves the focus to the txtEmail control.

# How to set the default button control

ASP.NET also lets you set the button that’s activated by default when you press the Enter key. To do that, you set the DefaultButton attribute of the form. In the example in this figure, this attribute is set to the btnNext button. Because of that, the form is posted back to the server when the Enter key is pressed, and the method for the Click event of the Next button is executed.