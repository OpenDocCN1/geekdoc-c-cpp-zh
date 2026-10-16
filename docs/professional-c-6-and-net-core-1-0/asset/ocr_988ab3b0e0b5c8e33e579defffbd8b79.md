defining the assertion, you need to generate the code again.

![](bbox=[0.05, 0.15, 0.95, 0.45])

# Figure 19.11

The generated Assert method verifies whether the correct value is in the selected control; if the incorrect value is in the control, it writes an error message:

```
```csharp
public void AssertNewBook()
{
    WpfList uiItemList =
    this.UIBooksDesktopAppWindow1.UIBooksViewCustom.UIAddButton.UIIt;

    Assert.AreEqual(
    this.AssertNewBookExpectedValues.UIItemListSelectedItemsAsString
    uiItemList.SelectedItemsAsString,"problem adding book in list");
}
```
```

For changes to the code, you shouldn’t change the designer-generated code files. Instead, you open the .uitest files to open the dialog shown in Figure 19.12. Here you can split actions into new methods, add delays before actions, and delete actions. Also, you can move the source code from the designer-generated files to custom files where you can change the code later.