
Here's an example of such code from the Gyrometer sample (js/scenario1.js):

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

The samples for the compass, inclinometer, and orientation sensor also have scenarios for calibration because each one has a limited degree of accuracy.

### Relative axes
With all the directional sensors, the values they report through their readings are relative to the device orientation (portrait or landscape), rather than being absolute. If you allow different rotations, you'll need to take these into account, which is especially important for portrait-first devices like smaller 7" or 8" tablets. The specific mathematics for these cases is beyond the scope of this book, however, so refer to Aligning sensors with your app's orientation on the Windows App Builder blog for more details.

With the Orientation Sensor, a *quaternion* can be most easily understood as a rotation of a point (x,y,z) about a single arbitrary axis. This is different from a rotation matrix, which represents rotations around three axes. The mathematics behind quaternions is fairly exotic because it involves the geometric properties of complex numbers and mathematical properties of imaginary numbers, but working with them is simple and frameworks like DirectX support them. See the OrientationSensor sample for more.

Speaking of orientation, I mentioned that the SimpleOrientationSensor works a little differently. Its purpose is to supply quadrant orientation rather than exact orientation, which is perhaps all you need. For example, a star chart app would need to know if a slate device is upside-down so that it can adjust its display (along with a compass reading) to match the sky itself.

To summarize this sensor's usage:

- Call Windows.Devices.Sensors.SimpleOrientation.getDefault to obtain the object.
- Call the getCurrentOrientation to obtain a reading.
- The orientationChanged event provides for ongoing readings, where eventArgs contains *orientation* (a reading) and *timestamp* properties.
- The reading is a `SimpleOrientation` value whose meaning is relative to the native device orientation:
  - `notRotated`, `rotated90degreesCounterclockwise`, `rotated180degreesCounterclockwise`, `rotated270degreesCounterclockwise`. Note that these are entirely different from view orientations like landscape and portrait that you’d pick up in media queries and so forth. A portrait-first device in its native state, for example, will report a portrait view orientation but `notRotated` as its `SimpleOrientation`.
  - `faceup`, `facedown` (tablet devices only).

For a demonstration, see the `SimpleOrientationSensor` sample.

## What We’ve Just Learned

- "Design for touch, get mouse and stylus for free" is a message that holds true, because working with pointer and gesture input from a variety of input devices doesn’t require you to differentiate between the forms of input.
- Using built-in controls is the easiest way to handle input, but you can also handle `pointer*` events and `MSGesture*` events directly, when needed. You can also feed `pointer*` events into a custom gesture recognizer (that issues its own events).
- The Windows touch language includes tap, press and hold, slide/pan, cross-slide (to select), pinch-stretch, rotate, and edge gestures (from top/bottom and from the sides). A tap is typically handled with a `click` event, whereas the others require the creation of an `MSGesture` object, association of that object with a pointer, and handling of `MSGesture*` event sequences which provide for manipulations and inertial motions together.
- The touch language also has mouse, stylus, and keyboard equivalents. For mouse and stylus, there is very little work an app needs to do (such as sending mouse `wheel` events to the gesture object). Keyboard support must be implemented separately, but simply uses the standard HTML/JavaScript events.
- Keyboard support also includes accommodating the soft (on-screen) keyboard, which appears automatically for text input fields and other content-editable elements. It automatically adjusts its appearance according to input type, and will slide the app contents up if necessary to avoid having the keyboard overlap the input control. An app can also handle visibility events directly to provide a better experience than the default.
- The Inking API provides apps with the means to record, save, and render an entire series of pointer activities, where the strokes can also be fed into a handwriting recognizer.
- The Geolocation API in WinRT provides apps with access to GPS data as well as events when the device has moved past a specified threshold, including support for geofencing.
- The WinRT API represents a number of sensors that can also be used as input to an app. In addition to geolocation, the sensors are compass, orientation, simple orientation (quadrant-based), inclinometer, gyrometer, accelerometer, and ambient light.
- Most sensors follow the same usage pattern: acquire the sensor object, get a current reading, and possibly listen to the `readingchanged` event. They are very easy to work with, leaving much of your energy to apply them creatively!

way of saying, “For each item in this collection, perform these actions” (hence the creation of *forEach*). You use such a construct anytime you need to accomplish this particular purpose, and you know it well because you’ve practiced it so often!

A promise is really nothing different. It’s a particular code structure for a specific purpose: namely, the delivery of some value that might not yet be available in the future. Why this is a promise as we see it in code is essentially the same as we find in human relationships: an agreement, in a sense, between the originator of the promise and the consumer or recipient.

In this relationship between originator and consumer there are actually two distinct stages. I call these *creation* and *fulfillment*, which are illustrated in Figure A-1.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_662_0.png)

**FIGURE A-1** The core relationship encapsulated in a promise.

Having two stages of the relationship is what brings up the asynchronous business. Let’s see how by following the flow of the numbers in Figure A-1:

- 1. The relationship begins when the consumer asks an originator for something, “Can you give me...?” This is what happens when an app calls some API that provides a promise rather than an immediate value.
- 2. The originator creates a promise for the goods in question and delivers that promise to the consumer.
- 3. The consumer acknowledges receipt of the promise, telling it how the promise should let the consumer know when the goods are ready. It’s like saying, “OK, just call this number when you’ve got them,” after which the consumer simply goes on with its life (asynchronously) instead of waiting (synchronously).
- 4. Meanwhile, the originator works to acquire the promised goods. Perhaps it has to manufacture the goods or acquire them from somewhere else; thus, the relationship here assumes that those goods aren't necessarily sitting around (even though they could be). This is the other place where asynchronous behavior arises, because acquisition can take an indeterminate amount of time.
- 5. Once the originator has the goods, it brings them to the consumer.
- 6. The consumer now has what it originally asked for and can consume the goods as desired.

Now if you're clever enough, you might have noticed that by eliminating a part of the diagram—the stuff around (3) and the arrow that says "Yes, I promise..."—you are left with a simple synchronous delivery model. This brings us to this point: receiving a promise gives the consumer a chance to do something with its time (like being responsive to other requests), while it waits for the originator to get its act together and deliver the promised goods.

And that, of course, is also the whole point of asynchronous APIs in the first place, which is why we use promises for those APIs. It's like the difference (to repeat my example from Chapter 3) between waiting in line at a restaurant's drive-through for a potentially very long time (the synchronous model) and calling out for pizza delivery (the asynchronous model): the latter gives you the freedom to do other things while you're waiting for the delivery of your munchies.

Of course, there's a bit more to the relationship that we have to consider. You've certainly made promises in your life, and you've had promises made to you. Although many of those promises have been fulfilled, the reality is that many promises are broken—it is possible for the pizza delivery person to have an accident on the way to your home! Broken promises are just a fact of life, one that we have to accept, both in our personal lives and in asynchronous programming.

Within the promise relationship, then, this means that originator of a promise first needs a way to say, "Well, I'm sorry, but I can't make good on this promise." Likewise, the recipient needs a way to know that this is the case. Secondly, as consumers, we can sometimes be rather impatient about promises made to us. When a shipping company makes a promise to deliver a package by a certain date, we want to be able to look up the tracking number and see where that package is! So, if the originator can track its progress in fulfilling its promise, the consumer also needs a way to receive that information. And third, the consumer can also tell the originator that it no longer needs whatever it asked for earlier. That is, the consumer needs the ability to cancel the order or request.

This complete relationship is illustrated in Figure A-2. Here we've added the following:

- 7. While the originator is attempting to acquire the goods, it can let the consumer know what's happening with periodic updates. The consumer can also let the originator know that it no longer needs the promise fulfilled (cancellation).
- 8. If the originator fails to acquire the goods, it has to apologize with the understanding that there's really nothing more it could have done. ("The Internet is down, you know?")
