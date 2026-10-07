# 384 | CHAPTER 22 NAVIGATION-BASED APPLICATIONS

![](bbox=[0.095, 0.095, 0.603, 0.396])

FIGURE 22-4

The NavigationService object provides other useful properties and methods in addition to Navigate. The following code shows how the program PageApp returns from the "Add Customer" page shown in Figure 22-4 when you click on the checkmark in the lower right:

```
// Prepend we did something and return to the main page.
private void void btnnOk_Click(object sender, MouseButtonEventArgs e)
{
    MessageBox.Show("Customer created.", "Customer created",
    MessageBoxButtons.OK, MessageBox.Information);
    if (NavigationService.CanGoBack())
    {
        NavigationService.GoBack();
    }
    else
    {
        NavigationService.Navigate(new pageMain());
    }
}
```

Available for download on Wrox.com

PageApp

This code first displays a message box. It then checks the NavigationService’s CanGoBack property to see if the user can go back to a previous page — in this case, the program’s ideal state. If CanGoBack is True, the code calls the NavigationService’s GoBack method. If CanGoBack is False, then the code calls the NavigationService’s Navigate method, passing a new pageMain Page object.

The following list summarizes the NavigationService’s most useful properties and methods:

+   * AddBackEntry — Adds a navigation entry that contains a custom state object.