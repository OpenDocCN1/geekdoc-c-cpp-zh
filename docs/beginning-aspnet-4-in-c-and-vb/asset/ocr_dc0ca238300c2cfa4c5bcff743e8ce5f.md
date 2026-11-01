```
using System;
using System.Windows.Controls;
using System.Windows.Navigation;

namespace Wrox.ProCSharp.Silverlight.Views
{
    public partial class Welcome : Page
    {
        public Welcome()
        {
            InitializeComponent();
        }
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            startStoryboard.Completed += (sender1, e1) =>
            {
                endStoryboard.Completed += (sender2, e2) =>
                    NavigationService.Navigate(
                        new Uri("/Home", UriKind.Relative));
                endStoryboard.Begin();
            };
            startStoryboard.Begin();
        }
    }
}
```

code snippet WCFRegistration/Views/Welcome.xaml.cs

When you run the application, you can see an animation and the hyperlink buttons, as shown in Figure 38-3.

![](bbox=[0.15, 0.7, 0.83, 0.92])

FIGURE 38-3