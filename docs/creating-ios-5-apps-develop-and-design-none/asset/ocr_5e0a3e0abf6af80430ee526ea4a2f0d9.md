This code uses a simple low-pass filter to pull out the gravity signal. Each update step, we nudge the current gravity value slightly based on our current acceleration information. High-frequency changes (like shaking the phone) tend to cancel themselves out before they can accumulate enough to have much of an effect. Gravity, on the other hand, provides a constant pull that changes relatively slowly compared to user-imparted motion. This lets the pull of gravity accumulate rapidly, producing a relatively accurate gravity vector.

Note that we only need the x- and y-components of our gravity vector. Therefore, we don’t even bother to calculate the z-component. Instead, we simply set it to 0.0f. This saves us a little computation time on each update.

Once we have calculated our gravity vector, the steps are the same as before. We pass it to addAcceleration: and update our UI.

Next, let’s look at the addAcceleration: method.

```
```objective-c
- (CGPoint)addAcceleration:(CMAcceleration)acceleration {

    // Update velocity.

    CGPoint velocity = self.velocity;
    velocity.x += (CGFloat)acceleration.x * self.accelerationRate;
    velocity.y -= (CGFloat)acceleration.y * self.accelerationRate;

    // Update location.

    CGPoint location = self.canvas.currentDrawPoint;
    location.x += velocity.x;
    location.y += velocity.y;
    self.velocity = velocity;
```
```

We start by updating our cursor’s velocity based on the x- and y-components of the gravity vector. We multiply this by our accelerationRate parameter, letting us scale the device’s responsiveness.

It’s worth noting that Core Motion can use a number of different reference frames. Here, our gravity vector is given in the device’s reference frame. If you’re holding the phone in front of you in portrait orientation, x points to the right, y points up, and z points straight ahead through the phone’s screen.

The CMDeviceMotion’s attitude works somewhat differently. It gives the device’s orientation in a fixed reference frame. We can select the desired reference frame