When the form is loaded during runtime, create an instance of the PrintDocument class, and wire up the three main event handlers described earlier:

```
```csharp
private void Form1_Load(object sender, EventArgs e)
{
    printDoc = new PrintDocument()
    {
        DocumentName = "Printing from Photo Viewer"
    };
    printDoc.BeginPrint += new PrintEventHandler(printDoc_BeginPrint);
    printDoc.PrintPage += new PrintPageEventHandler(printDoc_PrintPage);
    printDoc.EndPrint += new PrintEventHandler(printDoc_EndPrint);

    try
    {
        //---load the application settings values
        // into the textbox controls---
        ...
```
```

In the event handler for the BeginPrint event, initialize the page counter as well as the fonts of the text to be used for printing the page:

```
```csharp
void printDoc_BeginPrint(object sender, PrintEventArgs e)
{
    //---initialize the page counter---
    pagecounter = int.Parse(txtFrom.Text);

    //---initialize the fonts---
    f_title = new Font("Arial", 16, FontStyle.Bold);
    f_body = new Font("Times New Roman", 10);
}
```
```

In the EndPrint event handler, dereference the font variables used:

```
```csharp
void printDoc_EndPrint(object sender, PrintEventArgs e)
{
    //---de-reference the fonts---
    f_title = null;
    f_body = null;
}
```
```

Finally, the event handler for PrintPage is the place where you do the bulk of the work of sending the output to the printer. Basically, you use the Graphics object in the PrintPageEventArgs class to specify the output you want to print. For example, to draw a rectangle you would use the e.Graphics.DrawRectangle() method (where e is an instance of the PrintPageEventArgs class). To print a string, you use the e.Graphics.DrawString() method. After printing, you increment the