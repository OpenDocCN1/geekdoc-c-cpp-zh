![](bbox=[0.247, 0.136, 0.501, 0.315])

![](bbox=[0.522, 0.136, 0.775, 0.315])

Fig.ASP-2.33

Fig.ASP-2.34

16. Select the **By Cheque** radio button. The **By Cash** radio button gets unchecked and the text **You have selected the payment Mode By Cheque:** appears in the Textbox1 control, as shown in Fig. ASP-2.35:

![](bbox=[0.385, 0.372, 0.639, 0.539])

Fig.ASP-2.35

Let’s learn about the **CheckBox** control.

# Using the CheckBox Control

The CheckBox control is similar to the **RadioButton** control to accept the input from user. The only difference between a **RadioButton** and a CheckBox control is that you can select multiple items from a group of CheckBox controls; whereas, the RadioButton control allows you to select only one item at a time. The CheckBox control displays checkmarks that allow the user to toggle between the True and False conditions. This control exists within the `System.Web.UI.WebControls` namespace.

Noteworthy properties of the CheckBox control are listed in Table 2.13:

| Property | Description |
|---|---|
| Checked | Obtains a value showing if the CheckBox control is checked or not |
| Text | Obtains the text label associated with the CheckBox control |

Noteworthy event of the **CheckBox** control is listed in Table 2.14:

| Event | Description |
|---|---|
| CheckedChanged | Occurs when the value of the Checked property changes between various posts to the server |