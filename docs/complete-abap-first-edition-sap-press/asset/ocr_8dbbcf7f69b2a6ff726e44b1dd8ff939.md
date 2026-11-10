| Field Name | Field Type |
|---|---|
| Container Number | Type C, length 6 |
| Material Number | Type C, length 18 |
| Material Description | Type C, length 40 |
| Quantity | Type P, decimals 2 |
| Shift Indicator | Type C, length 1 |
| Date | Type D |
| User Name | Type C, length 20 |
| Deletion Indicator | Type C, length 1 |

**Table 12.4** Required Fields of Table

# Functional requirements

The application should provide the following functionality:

+   - All the fields except the field to input the container number should be input-disabled.
+   - Provide a Display/Change toggle button in the application toolbar to toggle between display and change modes.
+   - Provide a table control as shown in Figure 12.49. Note that the Shift field is a list box and the Delete field is a checkbox.
+   - Enable the Save button in the standard toolbar to let the user save the data.

![](bbox=[0.148, 0.609, 0.647, 0.867])

**Figure 12.49** Initial Screen of Transaction