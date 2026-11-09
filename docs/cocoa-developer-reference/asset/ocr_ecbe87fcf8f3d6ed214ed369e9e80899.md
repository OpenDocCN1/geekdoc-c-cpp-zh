# Figure 7.14

The Bindings tab links items to data structures in the application, bypassing standard accessors and allowing for automated refreshes and updates. Bindings are not available on the iPhone.

![](bbox=[0.186, 0.221, 0.412, 0.589])

The *Connections* tab, shown in Figure 7.15, is used to link an object to outlets and actions defined in code. When you select the tab, the Inspector window displays a list of available outlets and actions. The linking process is detailed in the next chapter. After linking, you can click this tab to review the connections between an object and its supporting code.

The *Identity* tab, shown in Figure 7.16, defines an object’s class, sets an optional tool tip, and defines optional runtime attributes. You can also highlight objects with a colored tag for convenience. This is a cosmetic feature that doesn’t affect the object’s appearance in the application, but makes it easier to view related objects in IB. The Class Identity field at the top of the Identity tab is the most useful element. Use it to set the class of an object using a drop-down list that displays a list of available classes. This list is automatically preset to show compatible classes; for example, you’re not allowed to reclass an application object as a slider object, but you can change a text field into a different type of text field with slightly different features.