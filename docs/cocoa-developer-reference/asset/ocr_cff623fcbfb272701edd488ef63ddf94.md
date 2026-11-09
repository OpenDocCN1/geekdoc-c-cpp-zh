The `sharedInstance` property is set to `self`, and when other objects call `shared`, they receive the App Delegate’s `self` value. They can then use

```
```objective-c
[[NSOperationAppDelegate shared] sendAMessage];
```
```

You can implement a `shared` property in this way in any custom class, as long as there is exactly one instance.

```
```objective-c
//in yourClass
static yourClass *sharedInstance;
sharedInstance = self;
//In another object
[[yourClass shared] sendAMessage];
```
```

Don’t use this idiom when you create a class that requires multiple instances.

![](bbox=[0.118, 0.388, 0.187, 0.442])

# TIP

Don’t be confused by the fact that the class name is `NSOperationAppDelegate`. This is a custom class used to demonstrate the features of `NSOperation`. It’s not a prebuilt Cocoa class, and you can’t use it in your own application. But you can use the `shared` idiom, as long as you slot in your class name, as shown previously.

Other key features of the code include:

+   - An instance of `NSOperationQueue` manages the task list.
+   - Tasks are created with different initialization values.
+   - Tasks are added to the run queue with `addOperation`.
+   - The `taskDidFinish:` method is an optional custom method used to report the completion of a task. It’s triggered in each task by calling `performSelectorOnMainThread:`, as shown in the previous listing.

To summarize, follow these steps to use NSOperation:

+   1. Subclass `NSOperation` to create a class for your task.
+   2. Add an `initWith:` method to implement parameter passing. Copy passed parameters to local properties or values.
+   3. Add a `main` method as an entry point to the task code. Add extra local methods as needed.
+   4. Optionally, add a `performSelectorOnMainThread` method to report when the task exits or when it needs attention.
+   5. In your main thread, create an instance of `NSOperationQueue`.
+   6. Create and initialize instances of your task class, as needed.
+   7. Run them by adding them to the task queue with `addOperation:`.