**OK** 10 times if the method call had been included inside the loop body. That is why the values produced inside the loop body were concatenated onto the end of the string variable. Only one call to the `MessageBox.Show()` method is included, and that is on the outside of the loop body.

The overloaded method of `MessageBox.Show()` can be sent one of the button types from Table 6–1 and a fourth argument of an icon, as shown in Example 6–8.

```
EXAMPLE 6.8

MessageBox.Show(result, "1 – 10 and their "
                 + "squares",
                 MessageBoxButtons.YesNoCancel,
                 MessageBoxIcon.Information);
```

Figure 6–6 shows the output produced when the `Show()` method of Example 6–8 replaces that which appears in the full program from Example 6–6.

![](bbox=[0.186, 0.446, 0.913, 0.759])

**FIGURE 6–6** Button and icon arguments to `MessageBox.Show()`

The .NET Framework `class` library includes several predefined icons that can be included as the fourth argument to the `MessageBox.Show()` method. Table 6–2 lists some you may want to include in your applications.