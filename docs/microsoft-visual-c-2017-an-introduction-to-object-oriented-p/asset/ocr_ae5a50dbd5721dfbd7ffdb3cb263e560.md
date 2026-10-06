# CHAPTER 12 Using Controls

(continued)

The AbeLincoln file was obtained at www.clipartkid.com. You can visit the site and download other images to use in your own applications. You also should search the Web for "free clip art" and similar phrases.

![](bbox=[0.183, 0.155, 0.226, 0.206])

+   13. In the Solution Explorer, double-click Form1.cs or click the Form1.cs[Design] at the top of the design screen. On the BedAndBreakfast Form, double-click the Lincoln Room Checkbox, and rename the default to start with an uppercase letter. Then add the following statement to the LincolnCheckBoxCheckedChanged() method:

```
private void LincolnCheckBoxCheckedChanged(object sender, EventArgs e)
{
    if (LincolnCheckBox.Checked)
{
        LincolnForm = new LincolnForm();
        LincolnForm.ShowDialog();
        LincolnCheckBox.Checked = false;
    }
}
```

+   14. Save the project and execute it. When the BedAndBreakfast Form appears, click either CheckBox—the appropriate informational Form appears. Close and then click the other CheckBox. Again, the appropriate Form appears.

+   15. Close all forms.

Adding RadioButtons to a Form

Next you add more Controls to the BedAndBreakfast Form. You generally use RadioButtons when a user must select from mutually exclusive options.

+   1. In the Design view of the Form in the BedAndBreakfast project, add a Button near the bottom of the Form. Change the Button's Name property to mealButton and the Button's Text to Click for meal options. Adjust the size of the Button so that its text is fully visible.

+   2. From the menu bar, select Project, Add New Item, and click Windows Form. Name the Form BreakfastOptionForm, and click Add. On the new Form, make the following changes:

+   - Set the Form's BackColor to Yellow.

+   - Drag a Label onto the Form. Name it appropriately, and set its Text to Select your breakfast option.

(continued)