The PrintDialog object's PrintDocument method takes a DocumentPaginator object as a parameter.

That object generates the pages of a printout, and the PrintDocument places them in a single print job.

![](bbox=[0.095, 0.146, 0.656, 0.343])

FIGURE 17-5

DocumentPaginator is an abstract class that defines methods for you to implement in a subclass. Those methods give the PrintDocument method information such as the printout's total number of pages and the objects to print.

The PrintShapes example program uses a ShapesPaginator class that inherits from DocumentPaginator to print four pages of shapes. Figure 17-5 shows the output saved by the Microsoft XPS Writer printer and displayed in XPS Viewer.

The following code shows how the program responds when you click on its "Print Shapes" button. Like the previous code that used PrintVisual, it displays a PrintDialog and sees whether the user selects a printer and clicks OK. It then calls the PrintDocument method, passing a paginator object and a job title.

```
// Print the shapes.
private void btnPrintShapes_Click(object sender, RoutedEventArgs args) {
    PrintDialog pd = new PrintDialog();
    if (pd.ShowDialog() == true) {
        pd.PrintDocument(
            new ShapesPaginator(
                new Size(pd.PrintableAreaWidth, pd.PrintableAreaHeight),
                *Shapes*")n            ));
    }
}
```

PrintShapes

# PRINTING PRONTO, PART 2

If you call PrintDocument without displaying the dialog, then the printout is immediately sent to the default printer.