The PageApp example program shown in Figure 22-3 uses a NavigationService to move between its pages.

![](bbox=[0.15, 0.148, 0.656, 0.447])

FIGURE 22-3

When you click on one of the buttons shown in Figure 22-3, the program uses the NavigationService’s Navigate method to open the new page. The following code shows how the program moves to the “Add Customer” page shown in Figure 22-4:

```
private void btnAddCustomer_click(object sender, RoutedEventArgs e)
{
    NavigationService.Navigate(new pagAddCustomer());
```

This code calls the NavigationService’s Navigate method, passing it new pagAddCustomer Page object.
In addition to displaying a Page object, the Navigate method can display a web page. The following code executes if you click the Help icon in the lower-right corner of Figure 22-3. This code navigates to the web page www.vb-helper.com/wpf.htm.

```
// Go to the help web site.
private void btnHelp_Click(object sender, RoutedEventArgs e)
{
    NavigationService.Navigate(new Uri("http://www.vb-helper.com/wpf.htm"));\}
```