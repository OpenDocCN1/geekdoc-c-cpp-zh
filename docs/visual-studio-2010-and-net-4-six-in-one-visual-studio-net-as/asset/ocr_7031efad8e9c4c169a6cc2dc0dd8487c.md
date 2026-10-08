To actually capture the Click event, select the Button, and use the Property Browser. Activate the Tabs within the Property Browser, and locate the Click event handler. Now that you can search for a property or event — this is very handy because there are tons of properties or events for most controls. Double-click on the empty drop-down to select "Click" text, and a Button_Click event handler will be created for you within the code-behind file (MainPage.xaml.cs). The XAML file will have the wiring for the new event handler:

```
<Button HorizontalAlignment="Center" VerticalAlignment="Center" Click="Button_Click">
```

Just as in ASP.NET, Silverlight controls have their own code-behind files. Let’s have a look at the code-behind you opened (Listing 8-3).

# LISTING 8-3: MainPage.xaml.cs

```
using System;
using System.Collections.Generic;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;

namespace HelloWorld
{
    public partial class MainPage : UserControl
{
        public MainPage()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
        }
    }
```

![](bbox=[0.03, 0.355, 0.09, 0.395])



The MainPage class is a partial class — the other part of the class is created from the MainPage .xaml file. (You can inspect it by right-clicking the InitializeComponent call in the constructor, and selecting "Go To Definition" from the context menu.) The class is inherited from