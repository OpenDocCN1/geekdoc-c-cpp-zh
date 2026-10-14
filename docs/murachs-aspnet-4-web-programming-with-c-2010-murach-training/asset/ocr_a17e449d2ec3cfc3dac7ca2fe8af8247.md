# Additional property of the required field validator

| Property | Description |
|---|---|
| InitialValue | The initial value of the control that’s validated. If this value isn’t changed, the validation fails. The default is an empty string. |

# A required field validator that checks for a required entry

```
<asp:TextBox ID="txtName" runat="server"></asp:TextBox>&nbsp
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server"
    ControlToValidate="txtName"
    ErrorMessage="You must enter a name.">
</asp:RequiredFieldValidator>
```

# A required field validator that checks that an initial value is changed

```
<asp:TextBox ID="txtBirthDate" runat="server" Width="159px">mm/dd/yyyy</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server"
    ControlToValidate="txtBirthDate"
    InitialValue="mm/dd/yyyy"
    ErrorMessage="You must enter a birth date.">
</asp:RequiredFieldValidator>
```

# A required field validator that forces an option to be chosen from a list box

```
<asp:ListBox ID="lstCardType" runat="server" Width="292px">
    <asp:ListItem Selected="True" Value="None">--Select a credit card--</asp:ListItem>
    <asp:ListItem Value="Visa">Visa</asp:ListItem>
    <asp:ListItem Value="MC">MasterCard</asp:ListItem>
    <asp:ListItem Value="AmEx">American Express</asp:ListItem>
</asp:ListBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator3" runat="server"
    ControlToValidate="lstCardType"
    InitialValue="None"
    ErrorMessage="You must select a credit card type.">
</asp:RequiredFieldValidator>
```

# How the input controls are initially displayed in a browser

![](bbox=[0.15, 0.615, 0.46, 0.74])

# Description

+   - The *required field validator* checks that the user entered data into an input control. It’s typically used with text box controls, but can also be used with list controls.