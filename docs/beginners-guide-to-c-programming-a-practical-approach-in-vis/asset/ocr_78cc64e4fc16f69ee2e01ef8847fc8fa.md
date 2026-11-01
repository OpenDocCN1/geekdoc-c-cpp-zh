9. We obtain the ceiling(x) in a similar way:

```
private void ceilingButton_Click(object sender, EventArgs e)
{
    double x = Convert.ToDouble(input1.Text);
    output.Text = Math.Ceiling(x).ToString();
}
```

Code 13.11

10. We will use the double type representations of both x and y inputs to calculate the max(x, y) function as follows:

```
private void maxButton_Click(object sender, EventArgs e)
{
    double x = Convert.ToDouble(input1.Text);
    double y = Convert.ToDouble(input2.Text);
    output.Text = Math.Max(x, y).ToString();
}
```

Code 13.12

11. Similarly, the x^y, i.e. x^y will be calculated via the pow(x, y) method:

```
private void powButton_Click(object sender, EventArgs e)
{
    double x = Convert.ToDouble(input1.Text);
    double y = Convert.ToDouble(input2.Text);
    output.Text = Math.Pow(x, y).ToString();
}
```

Code 13.13

12. Finally, we will display the pi (π) number existing in the Math class when the Pi Button is clicked:

```
private void piButton_Click(object sender, EventArgs e)
{
    double pi = Math.PI;
    output.Text = pi.ToString();
}
```

Code 13.14

13. We can now build and run the project. The program window will appear as in Figure 13.16. Let's enter some numbers for x and y TextBoxes. I entered 2 and 4, respectively. Firstly, click the Sin(x) Button to calculate sin(2) as shown in Figure 13.17.