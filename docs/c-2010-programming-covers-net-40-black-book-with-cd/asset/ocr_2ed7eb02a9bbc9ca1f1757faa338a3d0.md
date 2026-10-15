```
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Printing;
using System.Windows.Xps;
using System.Windows.Xps.Packaging;
using System.IO;

namespace PrintingDocument
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

        private void PrintButton_Click(object sender, RoutedEventArgs e)
        {
            XpsDocument myXPSDocument = new XpsDocument("../../Penguin.xps",
                FileAccess.Read);
            FixedDocumentSequence myXPSDocumentSeq =
                myXPSDocument.GetFixedDocumentSequence();
            DocumentPaginator XPSpaginator = myXPSDocumentSeq.DocumentPaginator;
            PrintDialog myPrintDialog = new PrintDialog();
            Boolean printResult = (Boolean)myPrintDialog.ShowDialog();
            if (printResult == true)
            {
                myPrintDialog.PrintDocument(XPSpaginator, "XPS Document Printing");
                MessageBox.Show("printing in process...");
            }
        }
    }
}
```

In Listing 9.12, there are four new namespaces, namely System.Printing, System.Windows.Xps, System.Windows.Xps.Packaging, and System.IO namespaces included in the code-behind file because an XPS document is to be printed. You also need to add references to the System.Printing namespace and the ReachFramework assembly.

The code within the PrintButton_Click() method executes when you click the PrintButton button. In this method, an XPS document, myXPSDocument, is created using the XpsDocument class. The XPS document, myXPSDocument, is instantiated with the Penguin.xps file and has the read access. Note that the Penguin.xps file is available in the current project folder; therefore, the ../../ escape sequence is used to access it.

A FixedDocumentSequence type variable, myXPSDocumentSeq, holds the myXPSDocument. The document paginator of the myXPSDocumentSeq variable is then assigned to the DocumentPaginator type variable XPSpaginator. The document paginator allows you to print multiple pages of a file or document and paginates the pages according to the changes in the file.

An object named myPrintDialog of the PrintDialog class is defined in the PrintButton_Click() method. This object represents the print dialog box and the result of the dialog box is held in a boolean variable printResult. The printResult variable gets its value from the button that a user clicks when the dialog box is displayed using the ShowDialog() method. The next statement, the if statement, checks whether the printResult variable contains the value, true, that is, whether the user clicks the Print button in the dialog box. In case the value of the printResult variable is true, the printing of the specified XPS document starts.