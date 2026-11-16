![](bbox=[0.1, 0.09, 0.5, 0.4])

Figure 4.11 Cannon Example. © 2014 Timothy Wright.

A standard physics equation for finding the position of an object could be done as follows:

$$d = d_0 + vt - \frac{at^2}{2}$$

where ($d_0$) is the initial position, ($v$) is the velocity, ($a$) is the acceleration, ($t$) is the time, and ($d$) is the resulting position. The problem with using this equation is that it needs the entire time, not just the time between frames. For the instantaneous time, the following equations are more useful:

$$v = \frac{d}{t}, \quad a = \frac{v}{t}, \quad d = vt, \quad v = at$$

These equations use only the current time, not the entire time. Make sure to pay attention to which time value is needed. If the entire time is required, don't just use the elapsed time.

The `initialize()` method sets the default values, creates the cannon model, and scales it by 0.75. When the A or D keys are pressed, the cannon is rotated, and the time delta is used to control the rotation. In previous examples, the rotation delta was set to a