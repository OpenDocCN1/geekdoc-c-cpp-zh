> **CAUTION**
> 
> Toolbars and tab bars do not work well with split views and popovers, especially when they are placed at the bottom of the screen. Apple's guidelines suggest that apps should not use them. However, you can add two separate navigation bars to the views in a split view layout. This improves the appearance of an app, even if the navigation bar is cosmetic and does nothing.

# # Developing for iOS in Xcode

The iPhone Simulator and its target devices support a subset of the standard Xcode debugging tools. Interface Builder is also simplified. The Library lacks many of the standardized objects available in OS X, including menu trees and the various data controller types. UIKit objects replace the view design objects available in OS X. To support the different frameworks in iOS, the SDK includes alternative documentation, new code samples, and a different set of iOS project templates to match various possible app types. Template details are listed a little later in this chapter.

# ## Using the Xcode Simulator

The Xcode Simulator is adequate for basic testing, and it can emulate display rotation and shake events. However, the Simulator is not a perfect model of the target devices. Code runs much more quickly in the Simulator, so it cannot be used for performance testing. There may also be minor differences between the simulated SDK and the iOS running on a real device. Code that works in the Simulator may occasionally crash on hardware and vice versa.

> **CROSS-REF**
> 
> For information about downloading and installing Xcode and the iPhone Simulator, see Chapter 4.

The Simulator can emulate an iPhone and an iPad. To test iPhone apps on the iPad, choose the iPad Simulator as the Active Executable in the Build selector drop-down menu in Xcode. This runs the app inside the iPad’s emulation window.

To convert an iPhone project to an iPad project, make a safety copy outside Xcode. Load the copy into Xcode, right-click a compiled target, and choose Upgrade Current Target for the iPad. This modifies the nib file and makes it possible to run the app as a full-screen native iPad app. There is no way to downgrade an iPad project back to the iPhone.

> **TIP**
> 
> In spite of its limitations, you should use the Simulator for most of your development cycle. Compiling and loading an app into a hardware device take an extra minute or two, which slows down development. It can also clutter devices with unwanted, half-finished apps.