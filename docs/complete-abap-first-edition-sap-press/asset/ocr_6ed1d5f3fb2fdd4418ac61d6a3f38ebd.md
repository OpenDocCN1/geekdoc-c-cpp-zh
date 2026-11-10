NETWR field from the context. If you use the wrong field, the system will automatically prompt you to convert the field when binding.

+   6. When adding fields of a structure or table, you can directly drag the structure from the data view instead of manually adding individual fields. You also can insert the fields using the Insert menu, as shown in Figure 18.92.

![](bbox=[0.145, 0.201, 0.615, 0.555])

Once all the fields are added to the form, activate it. To pass data to the form, we call it from the driver program. Calling the form is similar to the process for a smart form.

# ### 18.3.3 Driver Program

When the form is activated, a function module is generated. We call this generated function module in the driver program to pass the data to the form. Similar to smart forms, when the form is transported, the corresponding function module is generated in the target system. This function module may have a different name in the target system than in the current system. Therefore, we use the `FP_FUNCTION_MODULE_NAME` function module to identify the corresponding function module name for the form.