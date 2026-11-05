When the `TabControl` object is placed on the form, as shown in Figure 10–22, two tabs are included by default. Additional tabs can be added or removed by right-clicking on a tab and selecting the **Add Tab** option. The most important property that the TabControl has is the `TabPages` property. The `TabPages` property enables you to format individual tabs. Clicking the ellipsis beside the `Collection` value displays the **TabPage Collection Editor** shown in Figure 10–23.

![](bbox=[0.173, 0.252, 0.744, 0.575])

**Figure 10–23**　TabControl's TabPage Collection Editor

You change the appearance of the tabs using the **TabPage Collection Editor**. You can display images on tabs, change the background or foreground colors, or change the text using the `Text` property. You also change the order of the tabs using the Collection Editor by selecting the tab and using the arrows to the right of the member name to move the tab to its preferred position. Tabs can be displayed vertically instead of horizontally using the `Alignment` property. Multiple rows of tabs can be displayed by setting the `MultiLine` property to `true`. You can also register `Click` events for each of the tabs so that when an individual tab is selected, its Click event method is executed.

![](bbox=[0.173, 0.805, 0.237, 0.856])

Do not confuse the `TabControl` objects with the tab order that is used to move from one control to another using the `Tab` key. Each form has its own tab order. By default, the order is the same as the order in which the controls are placed on the form. You can change that order by setting the `TabIndex` property for each of the controls. Tab-order numbering begins with zero.