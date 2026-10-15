```
```csharp
MessageBox.Show("Enter only numbers.");
textBox2.Text = "";
private void button1_Click(object sender, EventArgs e)
{
    MessageBox.Show("The total is " + (Convert.ToInt32(textBox1.Text) + 
    Convert.ToInt32(textBox2.Text)));
}
```
```

6. Press the F5 key to execute the MouseandKeyboardEvents application. Figure 8.57 shows the output of the MouseandKeyboardEvents application:

![](bbox=[0.02, 0.33, 0.96, 0.52])

# Figure 8.57: Displaying the Output of MouseandKeyboardEvents Application

When a user hovers the mouse over the Enter First Number text box, the background color of the text box changes to red, as shown in Figure 8.58:

![](bbox=[0.02, 0.7, 0.96, 0.88])

# Figure 8.58: Demonstrating the MouseEnter Event

When you move away the mouse from the text box, the color of text box changes to white. Now, try entering alphabets in the text boxes. A message, Enter only numbers, is displayed in a message box, as shown in Figure 8.59:

![](bbox=[0.02, 0.99, 0.96, 1.0])

# Figure 8.59: Displaying a Message Box