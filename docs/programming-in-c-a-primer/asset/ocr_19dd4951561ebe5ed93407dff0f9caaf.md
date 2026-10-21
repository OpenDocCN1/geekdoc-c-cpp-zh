# # Adding Code to a Factorial Form

We need to add code to the factorial form to specify the functionality for calculating the factorial of a number and closing the factorial form. To add the code to factorial form:

+   1. Double click the Button control with the text Calculate to display the Code Editor with factorial.cs file and button1_Click event handler for the Button control.
+   
+   2. Add the following code in the button1_Click event handler to specify the functionality for calculating factorial:

```
Program 20.9 | CALCULATING FACTORIAL

int num;
long fact;
if (textBox1.Text.Length > 2)
{
MessageBox.Show("Numbers upto 25 are allowed.");
}
num = Int32.Parse(textBox1.Text);
fact = 1;
while (num >= 1 && num <= 25)
{
fact *= num;
num--;
}
textBox2.Text = fact + "";

```

+   3. Click the Close button represented by a cross, which appears at the top in the Code Editor to close the Editor. The factorial.cs [Design] view for the factorial form appears.
+   
+   4. Double click the Button control with the text Back to FirstForm to open the Code Editor with factorial.cs file and button2_Click event handler.
+   
+   5. Add the following code in the button2_Click event handler to specify the functionality for closing the factorial form:
+   
+   this.Close();

This completes the process of adding code to the factorial form.

# # Creating PrimeNoForm

We need to create the PrimeNo form to enable us to enter a number and check whether that number is a prime number or not. To create the PrimeNo form:

+   1. Add a new form with the name PrimeNo to the SampleWinApp application using the Solution Explorer.
+   
+   2. Change the value of the Text property for the PrimeNo form to Prime Number Form using the Properties window.
+   
+   3. Change the BackColor property of the PrimeNo form using the Properties window.
+   
+   4. Add a Label control and a TextBox control to the PrimeNo form using Toolbox.
+   
+   5. Change the BackColor property of the Label control using the Properties window.
+   
+   6. Change the value of the Text property for the Label control to Enter a number: using the Properties window.