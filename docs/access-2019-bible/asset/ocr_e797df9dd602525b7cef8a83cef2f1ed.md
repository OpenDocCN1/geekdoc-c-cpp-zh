require hundreds of different variables. VBA forms often have dozens of different controls on them, including text boxes, command buttons, option groups, and other controls. Keeping track of the variables, procedures, forms, and controls in even a moderately complicated VBA application is a daunting task.

One way to ease the burden of managing the code and objects in an application is through the use of a naming convention. A naming convention applies a standardized method of supplying names to the objects and variables in an application.

The most common naming convention used in Access applications uses a one- to four-character prefix (a tag) attached to the base name of the objects and variables in a VBA application. The tag is generally based on the type of control for controls and the type of data the variable holds or the scope for variables. For example, a text box containing a person's last name might be named txtLastName, while a command button that closes a form would be named cmdClose or cmdCloseForm.

The names for variables follow a similar pattern. The string variable holding a customer name might be named sCustomer, and a Boolean variable indicating whether the customer is currently active would be bActive.

Using a naming convention is not difficult. Most of the code in this book uses one-character prefixes for variables and three-character prefixes for control names. The actual naming convention you use is not important. The important point is that you use the convention consistently. As you write more VBA code, the right convention for you will become obvious. Table 25.3 shows one naming convention.

**TABLE 25.3  A Sample Naming Convention**

| Control/Data Type | Prefix | Example |
|---|---|---|
| Control: Text Box | txt | txtFirstName |
| Control: Label | lbl | lblFirstName |
| Control: Command Button | cmd | cmdClose |
| Control: Frame | frm | frmOptions |
| Control: Combo Box | cbx | cbxCustomers |
| Control: List Box | lbx | lbxProducts |
| Control: Check Box | chk | chkActive |
| Control: Option Button | opt | optFemale |
| Type: Byte | bt | btCounter |
| Type: Boolean | b | bActive |
| Type: Integer | i | iCounter |
| Type: Long | l | lCustomerID |
| Type: Single | sn | snTaxRate |