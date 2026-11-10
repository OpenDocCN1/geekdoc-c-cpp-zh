![](bbox=[0.148, 0.103, 0.593, 0.294])

**Figure 5-9** Enhancement Category

If your structure has a currency (type CURR) or quantity (type QUAN) fields, you should maintain reference fields in the CURRENCY/QUANTITY FIELDS tab (as shown in Figure 5.10). A currency field should refer to a currency key field (type CUKY) and a quantity field should refer to a UNIT OF MEASURE field (type UNIT). The reference fields can exist in the same table or another table.

Maintaining the reference fields for currency and quantity fields is mandatory, and the system uses this reference to insert the relevant currency or unit when the field is outputted. If the reference field exists in the same table, then the system can use the reference to automatically apply the correct formatting to the output. While providing the reference fields, enter the reference table name and reference field name in the respective columns.

![](bbox=[0.148, 0.606, 0.948, 0.804])

**Figure 5.10** Reference Fields Maintained for Currency and Quantity Fields in Table VBRP

[Figure 5.10](#) shows the reference fields as maintained in billing document item table VBRP. The VOLUM field of table VBRP is of type QUAN and is referenced to the