
content. Thus, no value was assigned to the Content property. The other labels have a value for Content. The Name property associated with the controls becomes the control's identifier.

The **Solution Explorer** window in Figure 10-19 shows a MainWindow.xaml.cs file. This is the code behind file. Yes, there is still the code behind file found with WPF applications. This is the main feature that WinForms and WPF applications share in common. With a slight modification of property names, you have the same program statements written for the WPF application as you had with the WinForms application. Example 10-23 shows the program statements found in the code behind file.

### Example 10-23

```csharp
// WPF Example.xaml
// CheckBox and RadioButton objects
// added to the Windows form.
// Illustrates wiring several methods to
// the same event handler.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WPF_Example
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void ComputeCheckChanged(object sender,
                                         RoutedEventArgs e)
        {
            decimal cost = 0M;
            this.txtBxResult.Text = " ";

            if (this.ckBxSwim.IsChecked == true)
            {
                cost += 50;
            }
            if (this.ckBxSnorkel.IsChecked == true)
            {
                cost += 25;
            }
            if (this.ckBxDive.IsChecked == true)
            {
                cost += 100;
            }
            if (this.radBeginner.IsChecked == true)
            {
                cost += 10;
                this.lblMsg.Content = "Beginner - Extra $10" +
                                      " charge";
            }
            else if (this.radAdvanced.IsChecked == true)
            {
                cost -= 15;
                this.lblMsg.Content = "Advanced - Discount + $15";
            }
            else
            {
                this.lblMsg.Content = "   ";
            }
            this.txtBxResult.Text = cost.ToString("C");
        }
    }
}
```

A large number of namespaces are automatically referenced and added as **using** statements. These are shown in Example 10-23.

Adding and controlling images in a WPF application is very easy. Once an image is dragged onto the window, a Source property is available for browsing to the desired image. A dialog box enables you to add any number of images to the application. You have great control over resizing and placing images in the application. The Name property was set to bkImage. Using the Order menu option (right mouse-clicking on the image), the image was Sent to the Back and resized so it could be used as the background image. The image was stretched to fill the full window. The XAML file has the following new tag added to the file.

```xml
<Image Height="335" HorizontalAlignment="Left"
       Margin="-11,-24,0,0"
       Name="bkImage" Stretch="Fill"
       VerticalAlignment="Top" Width="526"
       Source="/WPF_Example;component/Images/DC_Trip%20129.JPG"/>
```

A special Images folder is automatically created when you place an image on the window. When you compile an application that contains XAML files, the markup gets converted into binary XAML (BAML). BAML is a tokenized, binary representation of XAML. This binary representation is then stored inside the application’s resources and loaded as needed by WPF during the execution of your program. The main advantage of this approach is that you get a faster user interface load time by reading a binary stream than through parsing XML. Figure 10-20 shows the final output when the application runs.

![](img/e33ae760e23d89eac66541252ad65de8_633_0.png)

**Figure 10-20** WPF application

## TabControl Objects

There may be times when you build applications that require too many controls for a single screen. You will recall that an important design consideration is to avoid cluttering your graphical user interface (GUI). Readability is very important. An option that you have available is to add tab controls to the page. The TabControl object displays multiple tabs, like dividers in a notebook or labels in a set of folders in a filing cabinet. This control makes it possible to create a multiple-page dialog box similar to what you see with many Windows applications. A Windows form using tab controls is illustrated in Figure 10-21.

![](img/e33ae760e23d89eac66541252ad65de8_634_0.png)

**Figure 10-21** Tabbed controlled application

Each separate tab can be clicked to display other options, as shown in Figure 10-21. You can place pictures, buttons, labels, or any control on each tabbed page. Add a TabControl object to the page by dragging the control from the Container section of the Toolbox onto your blank form. You can move the control to the upper-left corner of the form and use the size handles to stretch the control so that it covers the form, as is illustrated in Figure 10-22.

![](img/e33ae760e23d89eac66541252ad65de8_634_1.png)

**Figure 10-22** TabControl object stretched to fill form

When the `TabControl` object is placed on the form, as shown in Figure 10-22, two tabs are included by default. Additional tabs can be added or removed by right-clicking on a tab and selecting the **Add Tab** option. The most important property that the TabControl has is the `TabPages` property. The `TabPages` property enables you to format individual tabs. Clicking the ellipsis beside the `Collection` value displays the **TabPage Collection Editor** shown in Figure 10-23.

![](img/e33ae760e23d89eac66541252ad65de8_635_0.png)

**Figure 10-23** TabControl's TabPage Collection Editor

You change the appearance of the tabs using the **TabPage Collection Editor**. You can display images on tabs, change the background or foreground colors, or change the text using the `Text` property. You also change the order of the tabs using the Collection Editor by selecting the tab and using the arrows to the right of the member name to move the tab to its preferred position. Tabs can be displayed vertically instead of horizontally using the `Alignment` property. Multiple rows of tabs can be displayed by setting the `MultiLine` property to `true`. You can also register `Click` events for each of the tabs so that when an individual tab is selected, its Click event method is executed.

![](img/e33ae760e23d89eac66541252ad65de8_635_1.png)

Do not confuse the `TabControl` objects with the tab order that is used to move from one control to another using the `Tab` key. Each form has its own tab order. By default, the order is the same as the order in which the controls are placed on the form. You can change that order by setting the `TabIndex` property for each of the controls. Tab-order numbering begins with zero.

## Programming Example: DinerGUI Application

This example demonstrates event-driven applications that include the design and implementation of a graphical user interface. Two classes are constructed to separate the business logic from the presentation details. The first `class` defines a template for a food order `object`. It includes behaviors for processing an order that includes selections for entrée, drink, and special requests. The `class` assigns prices to each item selected and determines the overall price of the order. The other `class` instantiates an `object` of the Order `class` and instantiates a Windows Form `object` to represent the graphical user interface. Using the .NET predefined Controls classes, Label, ComboBox, ListBox, RadioButton, CheckBox, and Menu objects are added to the Form `object`. The problem specification for the DinerGUI application is shown in Figure 10-24.

![](img/e33ae760e23d89eac66541252ad65de8_636_0.png)

**Figure 10-24** Problem specification for DinerGUI example
