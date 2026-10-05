
same effects. Additionally, you will run the app in debug mode. This mode is not optimized for maximum performance, but it provides access to performance information that's not available in release mode. As long as you run all the tests performed using this app in the same mode, the results will provide a valid performance comparison. You shouldn't start any additional programs or services between exercises because these might affect the results that you see.

## To examine and run the GraphDemo single-threaded application

- 1. Start Microsoft Visual Studio 2022, if it is not already running.
- 2. Open the GraphDemo solution, which is located in the \Microsoft Press\VCS\Chapter 23\GraphDemo folder in your Documents folder. This is a UWP app.
- 3. In Solution Explorer, in the GraphDemo project, double-click the file MainPage.xaml to display the form in the Design View window.

Apart from the Grid control defining the layout, the form contains the following important controls:

- An Image control called graphImage This control displays the graph rendered by the application.
- A Button control called plotButton The user selects this button to generate the data for the graph and display it in the graphImage control.

> Note
In the interest of keeping the operation of the application in this exercise simple, it displays the button on the page. In a production UWP app, buttons such as this should be located on a command bar.

- A TextBlock control called duration The application displays the time to generate and render the data for the graph in this label.

- 4. In Solution Explorer, expand the MainPage.xaml file and then double-click MainPage.xaml.cs to display the code in the Code and Text Editor window.

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
This application was developed and tested on a desktop computer with 8 GB of memory. (It was also tested on a 4 GB machine.) If your computer has less memory than this available, you might need to reduce the values in the pixelWidth and pixelHeight variables; otherwise, the application might generate OutOfMemoryException exceptions, causing the application to terminate without warning. Don't increase these values if you have a bigger machine; the UWP model has a limit on the amount of memory that an application can use—currently around 2 GB, even on a desktop computer. If you exceed this value, your application might be terminated without warning. the rationale behind this limitation is that many devices on which UWP applications run are memory constrained, and a single app should not be allowed to consume all the memory resources available to the detriment of other apps.

- 5. Examine the code for the plotButton_Click method:

Click here to view code image

```
private void plotButton_Click(object sender, RoutedEventArgs e)
{
    Random rand = new Random();
    redValue = (byte)rand.Next(0xFF);
    greenValue = (byte)rand.Next(0xFF);
    blueValue = (byte)rand.Next(0xFF);

    int dataSize = bytesPerPixel * pixelWidth * pixelHeight;
    byte data[] = new byte[dataSize];

    Stopwatch watch = Stopwatch.StartNew();
    generateGraphData(data);
    duration.Text = $"Duration (ms): {watch.ElapsedMilliseconds}";
    WriteableBitmap bitmap = new WriteableBitmap(pixelWidth, pixelHeight);
    using (Stream pixelStream = graphBitmap.Buffer.AsStream())
    {
        pixelStream.Seek(0, SeekOrigin.Begin);
        pixelStream.Write(data, 0, data.Length);
        graphBitmap.Invalidate();
        graphImage.Source = graphBitmap;
    }
}
```

This method runs when the user selects the plotButton button. You will select this button several times later in the exercise, which will let you see that a new version of the graph has been drawn each time this method generates a random set of values for the intensity of the red, green, and blue points that are plotted. The graph will be a different color each time you select this button.

The next two lines instantiate a byte array that will hold the data for the graph. The size of this array depends on the resolution of the WriteableBitmap object, determined by the pixelWidth and pixelHeight fields. This size must be scaled by the amount of memory required to render each pixel. The WriteableBitmap class uses 4 bytes for each pixel, which specify each pixel’s relative red, green, and blue intensity and alpha blending value. (The alpha blending value determines the transparency and brightness of the pixel.)

The watch variable is a System.Diagnostics.Stopwatch object. The StopWatch type is useful for timing operations. The static StartNew method of the StopWatch type creates a new instance of a StopWatch object and starts it running. You can query the running time of a StopWatch object by examining the ElapsedMilliseconds property.

The generateGraphData method populates the data array with the graph to be displayed by the WriteableBitmap object. You'll examine this in the next step.

When the generateGraphData method has completed, the elapsed time (in milliseconds) appears in the TextBox control.

The final block of code creates the graphBitmap WriteableBitmap object. The information held in the data array is copied into this object for rendering. The simplest technique is to create an in-memory stream that can be used to populate the PixelBuffer property of the WriteableBitmap object. You can then use the Write method of this stream to copy the contents of the data array into this buffer. The Invalidate method of the WriteableBitmap class requests that the operating system redraws the bitmap using the information held in the buffer. The Source property of an Image control specifies the data that the Image control should display. The final statement sets Source property to the WriteableBitmap object.

- 6. Examine the code for the generateGraphData method, shown here:

Click here to view code image

```
private void generateGraphData(byte[] data)
{
    double a = pixelWidth / 2;
    double b = a * a;
    double c = pixelHeight / 2;
    for (double x = 0; x < a; x++)
    {
        double s = x * x;
        double p = Math.Sqrt(b - s);
        for (double i = -p; i < p; i += 3)
        {
            double r = Math.Sin(i) / a;
            double q = (r - 1) * c;
            double y = i + q;
            plotXY(data, (int)(x + pixelWidth / 2), (int)(y + pixelHeight / 2));
        }
    }
}
```

This method performs a series of calculations to plot the points for a rather complex graph. (The actual calculation is unimportant; it just generates a graph that looks attractive.) As it calculates each point, it calls the plotXY method to set the appropriate bytes in the data array that correspond to these points. The points for the graph are reflected around the x-axis, so the plotXY method is called twice for each calculation: once for the positive value of the x-coordinate, and once for the negative value.

- Examine the plotXY method:

Click here to view code(byte[] data, int x, int y)

```
private void plotXY(byte[] data, int x, int y)
{
    int pixelIndex = (x + y * pixelWidth) * bytesPerPixel;
    data[pixelIndex] = blueValue;
    data[pixelIndex + 1] = greenValue;
    data[pixelIndex + 2] = redValue;
    data[pixelIndex + 3] = 0xBF;
}
```

This method sets the appropriate bytes in the data array that corresponds to x- and y-coordinates passed as parameters. Each point plotted corresponds to a pixel, and each pixel consists of 4 bytes, as described earlier. Any pixels left unset are displayed as black. The value 0xBF for the alpha blend indicates that the corresponding pixel should be displayed with a moderate intensity. If you decrease this value, the pixel will become fainter. Setting the value to 0FF (the maximum value for a byte) will display the pixel at its brightest intensity.

- In the Visual Studio toolbar, make sure the platform is set to x64. Then, on Debug menu, select Start Debugging to build and run the application.

> **Important**
If the platform is set to x86, the app may crash when it runs due to lack of memory resources. An x64 app has access to much more memory than an x86 app, and this app uses lots of memory!
