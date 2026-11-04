6. Right-click the designer and select View Code.

7. Add a property to the code-behind that allows a page using the control to get to the phone number.

The goal is to get all the content from the controls, patch it together, format it, and deliver it as a public property. Here is the code:

```
private string _phoneNumber;
public string PhoneNumberValue
{
    get
    {
        _phoneNumber = string.Format("({0})({1})-(2)*");
        return _phoneNumber;
    }
}
```

So now we have a control — just like the controls in the Toolbox — that accepts a phone number in pieces and formats it nicely. Let's play with it.

# Using your new control

You'll love using this control. It really does work just like a Toolbox control. Follow these steps to see how it works:

+   1. Right-click on the project, and add a new Web file.
+      I named mine UseThePhoneNumber.aspx.
+   2. Change to the design view.
+   3. Drag the ascx control right from the Solution Explorer onto the design surface.

Ta da! The control shows up just like a plain text box would, but it is just like we formatted it. Check out Figure 3-10.

Figure 3-10:
The Phone Number control.

![](bbox=[0.35, 0.7, 0.85, 0.9])

4. Add a label and a button to the form. Try to fill out the control, click the button, and see the formatted phone number.