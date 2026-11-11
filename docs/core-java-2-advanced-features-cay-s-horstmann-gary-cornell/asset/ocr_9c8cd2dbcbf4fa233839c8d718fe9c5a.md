In this section, we will show you how you can easily print a drawing on a single sheet of paper, how you can manage a multipage printout, and how you can benefit from the elegance of the Java 2D imaging model and easily generate a print preview dialog box.

# 11.12.1 Graphics Printing

In this section, we will tackle what is probably the most common printing situation: printing a 2D graphic. Of course, the graphic can contain text in various fonts or even consist entirely of text.

To generate a printout, you have to take care of these two tasks:

+   - Supply an object that implements the `Printable` interface
+   - Start a print job

The Printable interface has a single method:

```
int print(Graphics g, PageFormat format, int page)
```

That method is called whenever the print engine needs to have a page formatted for printing. Your code draws the text and the images to be printed onto the graphics context. The page format tells you the paper size and the print margins. The page number tells you which page to render.

To start a print job, use the PrinterJob class. First, call the static getPrinterJob method to get a print job object. Then set the Printable object that you want to print.

```
Printable canvas = ...;
PrinterJob job = PrinterJob.getPrinterJob();
job.setPrintable(canvas);
```

> > **CAUTION:** The class `PrintJob` handles JDK 1.1-style printing. That class is now obsolete. Do not confuse it with the `PrinterJob` class.

Before starting the print job, you should call the printDialog method to display a print dialog box (see Figure 11.32). That dialog box gives the user a chance to select the printer to be used (in case multiple printers are available), the page range that should be printed, and various printer settings.

Collect printer settings in an object of a class that implements the `PrintRequestAttributeSet` interface, such as the HashPrintRequestAttributeSet class.

```
HashPrintRequestAttributeSet attributes = new HashPrintRequestAttributeSet();
```

Add attribute settings and pass the attributes object to the printDialog method.