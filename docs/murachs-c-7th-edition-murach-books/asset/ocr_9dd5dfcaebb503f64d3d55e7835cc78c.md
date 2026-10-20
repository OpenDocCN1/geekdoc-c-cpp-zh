# A form in Tab Order view before and after the tab order is changed

![](bbox=[0.05, 0.15, 0.95, 0.35])



+   • To display a form in Tab Order view, select it and then select the View→Tab Order command. This displays the tab index for each control as in the first form above.
+   
+   • If the form isn’t displayed in Tab Order view, display the Options dialog box (Tools→Options), select the General category in the Environment group, and uncheck the Optimize Rendering for Screens with Different Pixel Densities option.
+   
+   • To change the tab indexes of the controls, click on the controls in the sequence you want to use. As you click, the new tab indexes appear as in the second form above.
+   
+   • The first time you click on a control in Tab Order view, the tab index is set to the next number in sequence, starting with zero for the first control. If you click on the same control more than once, the tab index is increased by one each time you click.
+   
+   • The controls in the group box are displayed with sub indexes as illustrated by the radio buttons above. Then, you can click on the group box to change its index and the main indexes of the controls it contains. To change the sub indexes of the controls in the group box, click on them individually.



+   • The tab order determines the order in which controls receive the focus when the Tab key is pressed. The TabIndex property of the controls determines this order.
+   
+   • By default, the value of a control’s TabIndex property is determined by the sequence in which it’s added to the form. The TabIndex property is set to 0 for the first control, 1 for the second control, and so on.
+   
+   • A label can’t receive the focus. As a result, you typically don’t need to include the labels in the tab order. However, if the label defines an access key, the TabIndex property of the label should be set to one less than its related control. That way, the related control will receive the focus when the access key for the label is activated.
+   
+   • When setting the tab order, you can skip controls whose TabStop, Enabled, or Visible properties have been set to false, unless those properties will change as the form runs.