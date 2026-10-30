Each type of object has its own Property Sheet and properties. These include the form itself, each of the form sections, and each of the form’s controls. Once you’ve displayed the Property Sheet by clicking Property Sheet on the Design tab, you can change what the Property Sheet displays in two ways: by selecting the object on the form or by choosing the object from the Property Sheet’s combo box. The Property Sheet will instantly change to show the properties for the selected object.

# FIGURE 17.27

Setting a control’s Control Source property.

![](bbox=[0.185, 0.307, 0.493, 0.615])

# Naming control labels and their captions

You might notice that each of the data fields has a label control and a text box control. Normally, the label’s Caption property is the same as the text box’s Name property. The text box’s Name property is usually the same as the table’s field name—shown in the Control Source property. Sometimes, the label’s Caption is different because a value was entered into the Caption property for each field in the table.

When creating controls on a form, it’s a good idea to use standard naming conventions when setting the control’s Name property. Name each control with a prefix followed by a meaningful name that you’ll recognize later (for example, txtTotalCost, cboState, lblTitle). Table 17.2 shows the naming conventions for form and report controls. You can find a complete, well-established naming convention online at www.xoc.net/standards.