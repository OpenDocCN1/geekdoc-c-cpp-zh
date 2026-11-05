![](bbox=[0.05, 0.04, 0.95, 0.43])

Repeat the above 3 steps for the Tutorial Name text box.

+   1. So click on the Tutorial Name text box
+   2. Go to the properties window
+   3. Choose the Text property
+   4. Choose the TutorialName option under demotbBindingSource

**Step 6)** Next we need to change the Binding Source property of the BindingNavigator to point to our Demotb data source. The reason we do this is because the Binding Navigator needs to also know which table it needs to refer to.

The Binding Navigator is used to select the next or previous record in the table. So even though the data source is added to the project as a whole and to the text box control, we still need to ensure the Binding Navigator also has a link to our data source. In order to do this, we need to click the Binding navigator object, go to the Binding Source property and choose the one that is available

![](bbox=[0.08, 0.8, 0.92, 0.92])