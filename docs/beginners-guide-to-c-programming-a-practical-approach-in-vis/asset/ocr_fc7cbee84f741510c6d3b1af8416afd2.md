```
```csharp
private void loopButton_Click(object sender, EventArgs e)
{
    int finalValueInteger = Convert.ToInt16(finalValue.Text);
    for (int i = 0; i <= finalValueInteger; i++)
    {
        valuesListBox.Items.Add(i);
    }
}
```
```

Code 9.7

8. Build and run the project. The program will appear as follows:

![](bbox=[0.35, 0.38, 0.62, 0.62])

Figure 9.2. The program window

When we enter an integer to the TextBox and click the Loop! Button, the for loop will insert the numbers from 0 to the number we entered to the ListBox:

![](bbox=[0.35, 0.87, 0.62, 0.95])

Figure 9.3. The for loop listed numbers from 0 to 7