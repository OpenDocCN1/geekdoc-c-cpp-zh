# FRAMEWORK EFFECTS

Okay, so custom effects and HLSL are so far out of our scope you can’t even see them from here. But the Framework defines two effects that are usable (and useful) even for mathematically challenged programmers like me. Drop shadows are a common technique for setting off areas of the interface, and blurs can be very cool when combined with animation (which we’ll discuss in the next chapter).

![](bbox=[0.12, 0.28, 0.35, 0.48])

![](bbox=[0.41, 0.28, 0.67, 0.43])

![](bbox=[0.71, 0.3, 0.86, 0.41])

![](bbox=[0.41, 0.46, 0.54, 0.54])

RenderingBias determines whether the system generates the effect really fast, or really well. The default is Performance.

KernelType is the algorithm used to blur the image. The default is Gaussian, which works well in most situations, although Box is slightly faster.

> # PUT ON YOUR THINKING HAT
> 
> UIElement (from which, you’ll remember, just about every WPF class descends), defines an Effect property that allows you to specify a single effect. Can you add a drop shadow to the Canvas elements we used in our brush explorer?