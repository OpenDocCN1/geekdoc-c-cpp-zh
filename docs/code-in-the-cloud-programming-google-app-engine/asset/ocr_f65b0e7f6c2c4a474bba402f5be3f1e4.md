and the corresponding page:

![](bbox=[0.117, 0.068, 0.467, 0.282])

This looks good for what it is, but if we tried to add more to the UI, such as the entry block at the bottom—as in our mockup—it would end up flowing around the two floats. If the navbar was shorter than the transcript, other things would flow to the left around it, just as in our original mockup.

What we need is a way of saying, “Don’t flow around this.” That’s what a *clear* is for. If we add `clear: both;` to our CSS for any element, we’ll get what we wanted. You can say `clear: left`, which will clear left-floats; `right`, which will clear right-floats, or `both`; which will clear all floats.

Let’s add a class `clearer` to the `<p>` tag for the additional text and add `p.aclear { clear: both; }` to our style sheet. The result is shown here, exactly as we wanted:

![](bbox=[0.117, 0.628, 0.467, 0.881])