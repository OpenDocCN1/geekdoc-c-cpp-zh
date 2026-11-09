# Using memory management heuristics

Finally, there are some heuristic rules that can help with memory management. These are unofficial and not a substitute for formally analyzing the structure of your code. But they can help solve a temporary memory problem while you get other parts of your code working. These are quick-fix, non-final suggestions and shouldn’t be used in production code.

+   - Random crashes tell you that objects aren’t being retained correctly.
+   - References don’t persist across methods. If you create an object inside a method, you should retain it if you want it to be available in another method.
+   - Set pointers to `nil` after releasing them. Releasing a `nil` pointer doesn’t cause a crash.
+   - Beware of delegate objects. Setting a delegate object can do unhelpful things to the retain count of some of its properties.
+   - Beware of Core Animation, which may not manage memory as you’d expect it to.

![](bbox=[0.12, 0.414, 0.188, 0.468])

# TIP

The Object Allocations instrument built into Xcode is invaluable for tracking memory errors. A robust application doesn’t crash because of missing objects, and it doesn’t leak memory because object references are being overwritten. See Chapter 18 for more on this instrument and other diagnostic tips.

# Summary

In this chapter, you learned about data collection objects, memory management, and archiving methods. You explored the key features of `NSArray`, `NSDictionary`, and `NSSet`, and you discovered how to enumerate the items in a collection object, how to search items, and how to process each item with custom code.

Next, you discovered `NSCoder` and investigated how it worked with `NSKeyedArchiver` and `NSKeyedUnarchiver` to create composite object collections that could be saved to a binary file and reloaded and unpacked to restore original object properties.

Finally, you were introduced to practical garbage collection and to some of the less obvious challenges and possible solutions required to work with manual memory management.