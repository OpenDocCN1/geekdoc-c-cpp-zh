
Choose the menu item Build > Build & Debug. You should see a boilerplate message in your Console window followed by something like this:[^5]

```text
Greeter name: Maggie
  created: 2009-09-18 14:24:43 -0400
objc[11179]: [Free(id): message respondsToSelector:
                 sent to freed object=0x3b06760
Program received signal: EXC_BAD_INSTRUCTION.
```

This is so unhelpful. We only know which object has been freed because we freed it ourselves to demonstrate this, but in a large program where objects are coming and going, it would be harder to track down the offending object.

We’re going to use zombies to help us out here. To enable them, select Executables > Flashlight in Groups & Files. Right-click the file, and choose Get Info; or, with Flashlight selected, press ⌘I. Choose the Arguments tab, and at the bottom you should see the “Variables to be set in the environment:” text.

Add an environment variable by clicking the + button at the bottom-left corner. Enter `NSZombieEnabled` for the name of the variable and `YES` for the value.

![](img/9355405953264484a02198b0e3d25b7e_113_0.png)

Close the window. Click Build & Debug again. This time you should see this in the Console:

```text
Greeter name: Maggie
  created: 2009-09-18 16:13:57 -0400
*** -[Greeter respondsToSelector:]:
     message sent to deallocated instance 0x380d950
```

This time the zombie helps us see that the type of the object is a `Greeter`. This technique helps a lot when debugging and trying to figure out which freed object you are messaging. Before going on, remove the variable that enables NSZombies. You don’t want to be holding onto these objects when you deploy your application.

[^5]: If you don’t see this message, try to do a Build > Clean All Targets, and click Build & Run again.

### 6.9 Cleaning Up in dealloc

When the reference count for an object reaches zero, its `dealloc` is called. This is where you clean up the resources used by your object. For example, in `Greeter` there are two pointers to objects that we own: `name` and `today`. We need to send each a `release` when our `Greeter` object is about to be destroyed. We do this by overriding the `dealloc` method:

Download Memory/Flashlight16/Classes/Greeter.m

```objective-c
- (void) dealloc {
    [name release];
    [today release];
    [super dealloc];
}
```

Note that in the `init` method we let the superclass do its initialization before we did our custom initialization. Here we clean our custom objects up first and end with a call to `[super dealloc]`.

You can add this line to your `dealloc` to output a quick message to the Console window when your `Greeter` object is being freed.

```objective-c
NSLog(@"In Greeter dealloc.");
```

If you are a belt and suspenders type of person and want to make sure that there's no chance that you end up sending a message to a freed object, then you may want to set the variables to `nil` after you release them like this:

Download Memory/Flashlight16/Classes/Greeter.m

```objective-c
- (void) dealloc {
    [name release];
    name = nil;
    [today release];
    today = nil;
    [super dealloc];
}
```

Here you are releasing the instance variable and setting it to `nil`. You can combine these steps using the corresponding property like this:

Download Memory/Flashlight16/Classes/Greeter.m

```objective-c
- (void) dealloc {
    self.name = nil;
    self.today = nil;
    [super dealloc];
}
```

As you'll see in the next section, `self.name = nil` will both release `name` and set it to `nil`.[^6]

### 6.10 Retain and Release in a Setter

Here's an example of the retain-release pattern you'll use when changing the value of an object.[^7] Suppose you already have created an object named `greeter` of type `Greeter`. An idiomatic `setGreeter` method using the retain-release pattern would look something like this:

```objective-c
- (void) setGreeter: (Greeter *) newGreeter {
    if (newGreeter != greeter) {
        [newGreeter retain];
        [greeter release];
        greeter = newGreeter;
    }
}
```

You are being sent the object `newGreeter`. You want to own it to do something with it, so it is your job to retain it. On the other hand, you are about to set the variable `greeter` to point to the object referenced by `newGreeter`.

First, check to make sure the pointers aren't pointing at the same memory location. If they are, then there is nothing to do. If not, then go ahead and set `greeter` to now point to the object referenced by `newGreeter`.

You are going to need to hold on to the object that `newGreeter` points to, so you send it a `retain` message. On the other hand, you don't need the object that `greeter` points to anymore, so you release it. Now you set `greeter` to point to what `newGreeter` points to. Even though you are never going to use the variable `newGreeter` again, you are going to use what it pointed to. This whole retain-release cycle was retaining and releasing what the variables point to and not the variables themselves.

This retain-release method of memory management does have parallels in everyday life. For example, the conference hotel where I wanted to stay was completely booked. They put me on the waiting list, and I

[^6]: There are potential consequences that could come up if you are using Key Value Observing and someone else is still registered to listen to changes in the object being released and set to nil. I tend to just send the variable the release message in dealloc and leave it at that.

[^7]: You saw this briefly when we were looking at property memory attributes in the previous chapter. This version is slightly different, and now you better understand the retain-release cycle.

Click Build & Run, and the application behaves correctly. It creates the new object, displays it properly, and then releases it and calls `dealloc`.

```text
Greeter name: Maggie
created: 2009-09-17 14:12:09 -0400
In Greeter dealloc.
```

If instead you click Build & Analyze, you’ll see that two problems are flagged in FlashlightAppDelegate.m. You’ll usually see this problem when the method that returns an object (in our case `greeterFor:`) is defined in a different class than the object that calls it. For this example, both halves of the transaction are included in the same object, and that’s why we successfully created and released the object when we ran the example. The Clang Static Analyzer, however, is identifying a potential problem by looking at the two methods, `greeterFor:` and `applicationDidFinishLaunching:`, separately.

![](img/9355405953264484a02198b0e3d25b7e_117_0.png)

The second error is telling us that we released an object we didn’t own. In fact, if you look at the `applicationDidFinishLaunching:` method, you’ll see that when we released `host` we had no way of knowing that we owned it.

We’ll ignore this problem for now and focus on the other issue. If you look at this code, you’ll see that we own `host` because we created it with an `alloc`:

Download Memory/Flashlight9/Classes/FlashlightAppDelegate.m

```objective-c
- (Greeter *) greeterFor:(NSString *) personName {
    return [[Greeter alloc] initWithName:personName];
}
```

To highlight the problem, let’s create the object and release it in two different steps like this:

Download Memory/Flashlight9/Classes/FlashlightAppDelegate.m

```objective-c
- (Greeter *) greeterFor:(NSString *) personName {
    Greeter *tempGreeter = [[Greeter alloc] initWithName:personName];
    return tempGreeter;
}
```

Where can we release `tempGreeter`?

You can’t just release `tempGreeter` before you return it, or the retain count will be zero and `tempGreeter` will be dereferenced before you try to return it.[^9] You can’t ignore the reference you hold for `tempGreeter`. That’s the memory leak we’re trying to fix. If you don’t release it, you may be holding on to `tempGreeter` after no object is really using it because you haven’t decremented its retain count.

The solution is to use an autorelease pool.[^10] You send `tempGreeter` the `autorelease` message, and it is marked to be released once the method that calls the `greeterFor:` method completes. You can also do this when you create the `Greeter` instance. In that case, you can eliminate the temporary variable and accomplish your needs like this:

Download Memory/Flashlight10/Classes/FlashlightAppDelegate.m

```objective-c
- (Greeter *) greeterFor:(NSString *) personName {
    return [[[Greeter alloc] initWithName:personName] autorelease];
}
```

Now we can solve our second problem by removing the call to `[host release]` in `applicationDidFinishLaunching:`. The object the `host` variable points to is not retained because it is now autoreleased. Since we no longer own this object, we are no longer allowed to release it.

[^9]: I’ll assume that it's obvious that you couldn’t put the call to release the object in the line after the return.

[^10]: For more information on autorelease pools and memory management, see Apple’s publication *Memory Management Programming Guide for Cocoa*.
