# Lesson Requirements

In this lesson, you:

+   - Create the forms shown in Figure 9-5.
+   - Declare the form variables outside of any event handler.
+   - In the main form’s Load event handler, add code to create the form instances but don’t display the forms.
+   - Add code to the main form’s Button event handlers to display the corresponding secondary forms non-modally.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

# Hints

+   - Normally every form appears in the taskbar. To avoid cluttering the taskbar with all of the secondary forms, set their ShowInTaskbar properties to False.

# Step-by-Step

+   - Create the forms shown in Figure 9-5.
+     1. Create the main form.
+        a. Start a new project. In the Properties window, expand the main form’s Font property and set its Size subproperty to 12.
+        b. Add the Buttons. Center them as a group and set their Anchor properties to None.
+     2. Create the GettingThereForm.
+        a. Open the Project menu and select Add Windows Form. Enter the form type name GettingThereForm and click Add.
+        b. Set the form’s ShowInTaskbar property to False.
+        c. Add the Label, ListBox, and Buttons. Set the ListBox’s Anchor property to Top, Bottom, Left. Set the Buttons’ Anchor properties to Bottom, Right.
+     3. Create the GettingAroundForm.
+        a. Repeat step 2 for the GettingAroundForm.
+     4. Create the LodgingForm.
+        a. Repeat step 2 for the LodgingForm.