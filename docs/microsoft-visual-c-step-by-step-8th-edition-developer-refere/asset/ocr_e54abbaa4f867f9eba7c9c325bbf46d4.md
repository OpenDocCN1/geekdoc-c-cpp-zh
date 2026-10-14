![](bbox=[0.09, 0.06, 0.91, 0.49])

The class members drop-down list box displays all the methods in the class, together with the variables and other items that the class contains. (You will learn more about these items in later chapters.) In the drop-down list, click the typeSelectionChanged method, and the cursor will move directly to the typeSelectionChanged method in the class.

If you have programmed using another language, you can probably guess how the typeSelectionChanged method works; if not, Chapter 4, “Using decision statements,” makes this code clear. At present, all you need to understand is that when the user clicks an item in the ListBox control, the details of the item are passed to this method, which then uses this information to determine what happens next. For example, if the user clicks the float value, this method calls another method named showFloatValue.

5. Scroll down through the code and find the showFloatValue method, which looks like this:

Click here to view code image

```
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}
```