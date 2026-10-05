# Chapter 3 How to code and test a Windows Forms applications

The bar appears under a renamed variable

```
decimal total = Convert.ToDecimal(txtSubtotal.Text);
```

The menu that's available from the bar

```
decimal total = Convert.ToDecimal(txtSubtotal.Text);
```

```
decimal discount
// Rename 'subtotal' to 'total'
if (subtotal)
{
discountrecurrent = .2m;
```

The Preview Changes dialog box

![](bbox=[0.085, 0.312, 0.695, 0.638])

# Description

+   - The process of revising and restructuring existing code is known as refactoring. Visual Studio provides many features that make it easy to refactor your code.

+   - When you change a name that's used in your code, Visual Studio displays a bar beneath the modified name. Then, you can display a smart tag menu by moving the mouse over the bar, and you can click on the drop-down list to display a menu that contains the appropriate refactoring commands.

+   - You can use Visual Studio's refactoring features to modify the structure of your code by extracting methods, encapsulating fields, and so. To do that, you often begin by selecting a block of code. Then, you can right-click on the code and select the appropriate command, or you can select the command from the Refactor menu.

+   - Some refactoring commands display a dialog box that lets you preview the changes before you make them. Then, you can deselect any changes that you don't want to make.

Figure 3-13 How to refactor code