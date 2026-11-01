```
{
    numbersComboBox.Items.Add(i);
    i++;
} while (i <= stopValueInt);
}
```

Code 9.24 (cont'd)

6. Build and run the project. The following program window will appear:

![](bbox=[0.35, 0.34, 0.62, 0.58])

Figure 9.11. The program window

When we enter a number greater than 2 and click the Populate button, the ComboBox will be populated from 2 to this number:

![](bbox=[0.35, 0.72, 0.65, 0.88])

Figure 9.12. ComboBox populated by the values

The operation of the program is the same as the while loop example for the greater or equal to 2 entered in the TextBox. However, if we enter a number lower than 2, e.g. 2, then the difference of the do-while loop comes into play: