The watch variable is a System.Diagnostics.Stopwatch object. The StopWatch type is useful for timing operations. The static StartNew method of the StopWatch type creates a new instance of a StopWatch object and starts it running. You can query the running time of a StopWatch object by examining the ElapsedMilliseconds property.

The generateGraphData method populates the data array with the graph to be displayed by the WriteableBitmap object. You'll examine this in the next step.

When the generateGraphData method has completed, the elapsed time (in milliseconds) appears in the TextBox control.

The final block of code creates the graphBitmap WriteableBitmap object. The information held in the data array is copied into this object for rendering. The simplest technique is to create an in-memory stream that can be used to populate the PixelBuffer property of the WriteableBitmap object. You can then use the Write method of this stream to copy the contents of the data array into this buffer. The Invalidate method of the WriteableBitmap class requests that the operating system redraws the bitmap using the information held in the buffer. The Source property of an Image control specifies the data that the Image control should display. The final statement sets Source property to the WriteableBitmap object.

+   6. Examine the code for the generateGraphData method, shown here:

Click here to view code image

```
private void generateGraphData(byte[] data)
{
    double a = pixelWidth / 2;
    double b = a *;
    double c = pixelHeight / 2;
    for (double x = 0; x < a; x++)
    {
        double s = x * x;
        double p = Math.Sqrt(b - s);
        for (double i = -p; i < p; i += 3)
        {
            double r = Math.Sqrt(s + i * i) / a;
            double q = (r - 1) * Math.Sin(24 * r);
            double y = i / 3 + (q * c);
            plotXY(data, (int) (-x + (pixelWidth / 2)), (int) (y + (pixelHeight / 2)));
            plotXY(data, (int) (x + (pixelWidth / 2)), (int) (y + (pixelHeight / 2)));
```