# Developing features across layers

Divisions between layers aren’t clean or simple — there’s no discrete “graphics framework” or “animation framework.” Instead, animation features are spread across the Cocoa layer, the Media Layer, and Core Graphics. Similarly, you might expect Core Graphics to be in the Media Layer, but for historical reasons it’s included in the Application Services framework in the Core Services Layer.

So adding a feature to an application usually means mixing code and features from different frameworks. It’s not unusual to use Cocoa to create a user interface, Core Graphics to draw dynamic elements in the interface, and Core Animation to animate the graphics.

There is also some duplication between layers; for example, you can play sound using the Core Audio or AudioToolbox layers. This may seem redundant, but these layers offer different features. Audio Toolbox implements simple file player objects with limited features, while Core Audio includes more complex objects that are more difficult to work with, but can be used for more challenging applications such as real-time sound synthesis.

![](bbox=[0.119, 0.419, 0.188, 0.476])

> **TIP**
> 
> The organization of the frameworks would be very confusing if you had to use all of them all the time. In fact you only need to master a handful of frameworks. Once you know how to create and control a window, add controls, manage mouse clicks and keyboard events, and draw graphics and perhaps add sound, you’ve covered the basics — and they’re not difficult. The rest is useful and interesting, but optional.

# “Toll-free bridged” layers

Some of the objects offer more fundamental duplication. For example, NSString in Cocoa is closely related to CFString in the Core Foundation framework. Some objects are explicitly described as toll-free bridged — Apple’s way of indicating that objects and their interfaces are largely interchangeable, even though they exist in different layers.

In fact, many Cocoa objects are simply wrappers for lower-level functions that are listed in other frameworks. You can ignore this if you develop exclusively in Cocoa, and you can also ignore the lower-level functions unless you need to work with them. But it’s useful to be aware of the relationship because even when class features are duplicated, they’re rarely duplicated exactly. Related frameworks always offer a different balance of features and accessibility, and it’s sometimes possible to use a lower-level framework to solve a problem that can’t easily be solved in Cocoa.

# Using frameworks and layers successfully

If you’re new to Cocoa development, you’ll have realized now that the layer model is only a very rough guide to OS X. In practice, you’ll often find yourself digging through the framework reference documentation to combine features in different layers. But with the overwhelming number of objects and libraries in OS X and the slightly chaotic organization, it can be difficult to get a feel for how to approach problems when starting out with Cocoa.