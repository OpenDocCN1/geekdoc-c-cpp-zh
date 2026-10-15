```
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
namespace BindingtoCLROBject
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private Data name1 = new Data();
        public MainWindow()
        {
            InitializeComponent();
            nameGrid.DataContext = name1;
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            string message = name1.EmployeeID;
            string caption = name1.Name;
            MessageBox.Show(message, caption);
        }
    }
}
```

7. Press the F5 key to run the BindingtoCLROBject application. When you run the application, a window containing four text boxes appear. Add the data in all the text boxes and click the SHOW DATA button. You can see the final output of the BindingtoCLROBject application in Figure 25.20:

![](bbox=[0.345, 0.565, 0.645, 0.785])

Figure 25.20: Displaying the Message Box

# Binding an ADO.NET Object in WPF

To bind a WPF application to an ADO.NET object, you need to create a connection string and bind your controls by specifying their ItemSource and ItemTemplate properties. Let's create a WPF application, named ADO.NETtoWPF (also available on the CD) and add the code provided in Listing 25.15 to the MainWindow.xaml file: