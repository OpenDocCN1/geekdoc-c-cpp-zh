Here's an example of such code from the Gyrometer sample (js/scenario1.js):

```
```javascript
gyrometer = Windows.Devices.Sensors.Gyrometer.getDefault();

var minimumReportInterval = gyrometer.minimumReportInterval;
var reportInterval = minimumReportInterval > 16 ? minimumReportInterval : 16;
gyrometer.reportInterval = reportInterval;

gyrometer.addEventListener("readingchanged", onDataChanged);    // Remember to remove as needed

function onDataChanged(e) {
    var reading = e.reading;

    document.getElementById("eventOutputX").innerHTML = reading.angularVelocityX.toFixed(2);
    document.getElementById("eventOutputY").innerHTML = reading.angularVelocityY.toFixed(2);
    document.getElementById("eventOutputZ").innerHTML = reading.angularVelocityZ.toFixed(2);
}
```
```

The samples for the compass, inclinometer, and orientation sensor also have scenarios for calibration because each one has a limited degree of accuracy.

**Relative axes** With all the directional sensors, the values they report through their readings are relative to the device orientation (portrait or landscape), rather than being absolute. If you allow different rotations, you'll need to take these into account, which is especially important for portrait-first devices like smaller 7" or 8" tablets. The specific mathematics for these cases is beyond the scope of this book, however, so refer to Aligning sensors with your app's orientation on the Windows App Builder blog for more details.

With the Orientation Sensor, a *quaternion* can be most easily understood as a rotation of a point (x,y,z) about a single arbitrary axis. This is different from a rotation matrix, which represents rotations around three axes. The mathematics behind quaternions is fairly exotic because it involves the geometric properties of complex numbers and mathematical properties of imaginary numbers, but working with them is simple and frameworks like DirectX support them. See the OrientationSensor sample for more.

Speaking of orientation, I mentioned that the SimpleOrientationSensor works a little differently. Its purpose is to supply quadrant orientation rather than exact orientation, which is perhaps all you need. For example, a star chart app would need to know if a slate device is upside-down so that it can adjust its display (along with a compass reading) to match the sky itself.

To summarize this sensor's usage:

+   - Call Windows.Devices.Sensors.SimpleOrientation.getDefault to obtain the object.
+   - Call the getCurrentOrientation to obtain a reading.
+   - The orientationChanged event provides for ongoing readings, where eventArgs contains *orientation* (a reading) and *timestamp* properties.