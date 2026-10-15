```
<MenuItem Header="Exit" Command="Close" />
</MenuItem>
</Menu>
<DocumentViewer Name="docViewer" />
</DockPanel>
</Window>
```

+   2. Right-click the name of the application in Solution Explorer and select Add Reference from the context menu. The Add Reference dialog box opens.

+   3. Select the ReachFramework and System.Windows.Forms namespaces under the .NET tab of the Add Reference dialog box.

After adding references to the application, add the code given in Listing 11.11 to the code-behind file (MainWindow.xaml.cs) of the MainWindow.xaml file:

# Listing 11.11: Showing the Code for the MainWindow.xaml.cs File

```
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
using System.IO;
using System.Windows.Forms;
using System.Windows.Xps.Packaging;
namespace Fixeddocuments
{
public partial class MainWindow : Window
{
    public MainWindow() : base()
    {
        InitializeComponent();
        AddCommandBindings(ApplicationCommands.Open, OpenCommandHandler);
        AddCommandBindings(ApplicationCommands.Close, CloseCommandHandler);
    }
    private void OpenCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        OpenFileDialog dlg = new OpenFileDialog();
        dlg.Filter = "Xps Documents (*.xps)|*.xps";
        dlg.FilterIndex = 1;
        if (dlg.ShowDialog() == System.Windows.Forms.DialogResult.OK)
        {
            if (_xpsDocument != null)
                _xpsDocument.Close();
            try {
                _xpsDocument = new XpsDocument(dlg.FileName, System.IO.FileAccess.Read);
            }
            catch (UnauthorizedAccessException)
            {
                System.Windows.MessageBox.Show(
                String.Format("Unable to access {0}", dlg.FileName));
                return;
```