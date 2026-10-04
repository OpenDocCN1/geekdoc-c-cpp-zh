# Constructing User Controls 701

+   3. Switch to Design View.

+   4. Drag three text boxes to the designer, next to one another.

If you want to get fancy, put hyphens between them.

+   5. In the Properties panel, set the maxLength for the first two text boxes to 3 and the last one to 4.

This prevents the user from putting too many characters in a field.

+   6. Right-click the designer and select View Code.

+   7. Add a property to the code-behind that allows a page using the control to get to the phone number.

The goal is to get all the content from the controls, patch it together, format it, and deliver it as a public property. Here is the code:

```
private string _phoneNumber;
public string PhoneNumberValue
{
    _phoneNumber = string.Format("{0}-{1}-{2}", phoneNumber);
    return _phoneNumber;
}
```

Now you have a control — just like the controls in the Toolbox — that accepts a phone number in pieces and formats it nicely. You can play with it in the next section.

# Using your new control

You'll love using this control. It really does work just like a Toolbox control. Follow these steps to see how it works:

+   1. Right-click on the project, and add a new Web Form file.

I named mine UsePhoneNumber.aspx.

+   2. Change to the design view.

+   3. Drag the PhoneNumber.ascx control from the Solution Explorer onto the design surface.

Ta da! The control shows up just like a plain text box would, but it is just like you formatted it. Check out Figure 3-10.