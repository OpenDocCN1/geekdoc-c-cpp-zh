4. In Solution Explorer, expand the MainPage.xaml file and then double-click MainPage.xaml.cs to display the code in the Code and Text Editor window.

The form uses a WriteableBitmap object (defined in the Windows.UI.Xaml.Media.Imaging namespace) called graphBitmap to render the graph. The code in the plotButton_Click method creates this object, the class instance variables pixelWidth and pixelHeight specify the horizontal and vertical resolution, respectively, for the WriteableBitmap object:

Click here to view code image

```
public partial class MainPage : Window
{
    // Reduce pixelWidth and pixelHeight if there is insufficient memory available
    private int pixelWidth = 10000;
    private int pixelHeight = 5000;
}
```

...

> Note
This application was developed and tested on a desktop computer with 8 GB of memory. (It was also tested on a 4 GB machine.) If your computer has less memory than this available, you might need to reduce the values in the pixelWidth and pixelHeight variables; otherwise, the application might generate OutOfMemoryException exceptions, causing the application to terminate without warning.
't increase these values if you have a bigger machine; the UWP model has a limit on the amount of memory that an application can use—currently around 2 GB, even on a desktop computer. If you exceed this value, your application might be terminated without warning. the rationale behind this limitation is that many devices on which UWP applications run are memory constrained, and a single app should not be allowed to consume all the memory resources available to the detriment of other apps.