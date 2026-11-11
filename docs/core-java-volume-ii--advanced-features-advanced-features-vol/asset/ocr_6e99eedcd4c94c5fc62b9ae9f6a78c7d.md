![](bbox=[0.294, 0.141, 0.793, 0.465])

**Figure 11.60** A cross-platform print dialog box

> **NOTE:** Prior to JDK 1.4, the printing system used the native print and page setup dialog boxes of the host platform. To show a native print dialog box, call the `printDialog` method with no parameters. (There is no way to collect user settings in an attribute set.)

During printing, the print method of the `PrinterJob` class makes repeated calls to the `print` method of the `Printable` object associated with the job.

Since the job does not know how many pages you want to print, it simply keeps calling the print method. As long as the print method returns the value `Printable.PAGE_EXISTS`, the print job keeps producing pages. When the print method returns `Printable.NO_SUCH_PAGE`, the print job stops.

> **CAUTION:** The page numbers that the print job passes to the print method start with page 0.

Therefore, the print job doesn’t have an accurate page count until after the printout is complete. For that reason, the print dialog box can’t display the correct page range—instead, it displays “Pages 1 to 1.” You will see in