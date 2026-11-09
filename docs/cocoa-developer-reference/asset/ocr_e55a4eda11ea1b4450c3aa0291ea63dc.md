**Figure 8.1**

Creating a working layout ready for editing. On a dual monitor system, you can keep the code visible in one window and IB’s windows visible in another. A single monitor system is less convenient.

![](bbox=[0.169, 0.205, 0.813, 0.597])

# Introducing the Interface Builder workflow

As outlined in the previous chapter, Interface Builder and Xcode do not create automatic links between objects in a nib file and objects in code. You must add links manually, and until you do, the nib objects and the code remain disconnected. If you load a nib without creating links, it appears in memory, but your code can’t access its features. When the user interacts with it, it doesn’t send messages to your application.

Linking is a complex multistage process. It’s error prone, and many basic build errors are created by missing links and other nib-related problems. These errors are usually trivial and easy to repair, but the most efficient way to avoid them is by following an explicit workflow, shown in Figure 8.2. The items in bold are critical steps. You must work through these steps for every object in the nib that is accessed from your code.