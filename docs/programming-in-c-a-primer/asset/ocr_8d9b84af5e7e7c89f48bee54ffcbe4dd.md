```
else if (radioButton2.Checked == true)
{
    PrimeNo f2 = new PrimeNo();
    f2.Show();
}
```

![](bbox=[0.06, 0.18, 0.97, 0.65])

Fig. 20.20 The code editor window for FirstForm Form

+   3. Click the Close button represented by a cross, which appears at the top in the Code Editor to close the Editor. The FirstForm.cs [Design] view for the FirstForm form appears.
+   4. Double click the Button control with the text Exit to open the Code Editor with FirstForm.cs file and button2_Click event handler.
+   5. Add the following code in the button2_Click event handler to specify the functionality for closing the FirstForm form:
+       this.Close();
+   This completes the process of adding code to FirstForm form.

# Creating the Factorial Form

We need to create a factorial form to enable us to enter a number and calculate its factorial. To create the Factorial form: