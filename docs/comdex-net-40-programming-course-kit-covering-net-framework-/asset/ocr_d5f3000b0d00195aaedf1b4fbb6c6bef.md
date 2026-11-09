Noteworthy methods of the **BaseValidator** class are listed in Table 4.2:

| Method | Description |
|---|---|
| `Validate` | Allows validation on the associated input control and updates the IsValid property |
| `GetValidationProperty` | Specifies the validation property of a control, if it exists |

Now, let’s discuss the use of all the validation controls in detail one by one.

# Using the RequiredFieldValidator Control

The **RequiredFieldValidator** control ensures that the user has entered the required data in the input control, such as the **TextBox** control, to which it is associated. For example, if you are entering data to buy a T-shirt in an input control, then it is necessary to enter the size of the T-shirt that you want to buy. If you do not enter the size, the validation control displays an error message. The **RequiredFieldValidator** control exists within the **System.Web.UI.WebControls** namespace.

The noteworthy property of the RequiredFieldValidator class is listed in Table 4.3:

| Property | Description |
|---|---|
| `InitialValue` | Handles the initial value of the associated input control |

Perform the following steps to learn to use the **RequiredFieldValidator** control:

+   1. *Open Microsoft Visual Studio 2010*, as shown in Fig.ASP-4.1:

![](bbox=[0.244, 0.505, 0.78, 0.776])

Fig.ASP-4.1

+   2. *Select* **File→New→Web Site** to create a new Web site, as shown in Fig.ASP-4.2: