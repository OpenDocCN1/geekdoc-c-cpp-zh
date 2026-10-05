# MainPage.xaml MainPage.xaml

```
PrimitiveDataTypes PrimitiveDataTypes.MainPage typeSelectionChanged(object sen +
10 using Windows.UI.Xaml.Controls.Primi typeSelectionChanged
11 using Windows.UI.Xaml.Data;
12 using Windows.UI.Xaml.Input;
13 using Windows.UI.Xaml.Media;
14 using Windows.UI.Xaml.Navigation;
```

// The Blank Page template is documented at https://go.microsoft.com

```
namespace PrimitiveDataTypes
{
// <summary>
// An empty page that can be used on its own or navigated to within
// </summary>
```

```
public sealed partial class MainPage : Page
{
references
public MainPage()
{
this.InitializeComponent();
}
```

```
1 reference
private void selectedItemSelected(object sender, SelectionChanged
ListBoxSelectedItem = (type.SelectedItem.Content.ToString())
witch (selectedType.Content)\{
case "int":
showIntValue();
break;
case "long":
showLongValue();
break;
```

No issues found Ln: 30 Ch: 42 SPC CRLF

By default, the search is not case sensitive. If you want to perform a case-sensitive search, select the **Aa (Match Case)** button below the text you're searching for.

Instead of the Edit menu, you can press **Ctrl+F** to display the Find dialog. And you can press **Ctrl+H** to display the Quick Replace dialog.

As an alternative to using Quick Find, you can locate the methods in a class by using the **Class Members** dropdown list above the Code and Text Editor window, on the right. This dropdown list displays all the methods in the class, along with the variables and other items that the class contains. (You'll learn more about these items in later chapters.) In the dropdown list, choose