# Example 9-5

```
double percent;
inValue = label5.Text;    // inValue previously declared as string
inValue = inValue.Remove(inValue.Length - 1, 1);
percent = double.Parse(inValue) / 100;
```

The last three lines in Example 9-5 could be written in one statement, as shown in Example 9-6. Both produce the same results.

# Example 9-6

```
percent = (double.Parse(label5.Text.Remove
    (label5.Text.Length - 1, 1))) / 100;
```

Now that you have both values stored in the double variable, simple arithmetic can be performed and the result displayed in the txtTotalDue TextBox object. Example 9-7 includes those statements.

# Example 9-7

```
double ans;
ans = (purchaseAmt * percent) + purchaseAmt;
txtTotalDue.Text = String.Format("{0:C}",ans).ToString();
```

Figure 9-15 shows the output produced after the user enters a value and clicks the Compute button.

![](bbox=[0.2, 0.88, 0.44, 0.97])

Figure 9-15 Tax calculator output