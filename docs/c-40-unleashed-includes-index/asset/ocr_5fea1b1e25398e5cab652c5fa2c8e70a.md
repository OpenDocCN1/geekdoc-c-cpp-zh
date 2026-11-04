```
```csharp
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace MyFirstWpfApplication
{
    /// <summary>
    /// Interaction logic for Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
        }

        private void button_Click(object sender, RoutedEventArgs e)
        {

        }
    }
}
```
```

**FIGURE 3.47**  Code skeleton for an event handler in WPF.

```
```csharp
internal System.Windows.Controls.TextBox textBox1;

#line default
#line hidden

private bool _contentLoaded;

/// <summary>
/// InitializeComponent
/// </summary>
[System.Diagnostics.DebuggerNonUserCodeAttribute()]
public void InitializeComponent() {
    if (_contentLoaded) {
        return;
    }
    _contentLoaded = true;
    System.Uri resourceLocator = new System.Uri("/MyFirstWpfApplication;component/Window1.xaml", System.UriKind.Relative);
#line 1 "..\..\..\Window1.xaml"
    System.Windows.Application.LoadComponent(this, resourceLocator);
#line default
#line hidden
}
```
```

**FIGURE 3.48**  Generated code for a WPF window definition.

Notice how the XAML file (which gets compiled into the application’s assembly in a binary format called BAML) is loaded through the generated code. From that point on, the XAML is used to instantiate the user interface definition, ready for it to be displayed by WPF’s rendering engine.

As an aside, you can actually create WPF applications without using XAML at all by creating instances of the window and control types yourself. In other words, there’s nothing secretive about XAML; it’s just a huge convenience not to have to go through the burden of defining objects by hand.