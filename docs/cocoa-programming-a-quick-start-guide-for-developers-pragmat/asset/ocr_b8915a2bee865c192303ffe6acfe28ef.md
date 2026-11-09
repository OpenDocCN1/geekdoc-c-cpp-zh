As you'll see in the next section, self.name = nil will both release name and set it to nil.⁶

# 6.10 Retain and Release in a Setter

Here's an example of the retain-release pattern you'll use when changing the value of an object.⁷ Suppose you already have created an object named greeter of type Greeter. An idiomatic setGreeter method using the retain-release pattern would look something like this:

```
- (void) setGreeter: (Greeter *) newGreeter {
    if (newGreeter != greeter) {
        [newGreeter retain];
        [greeter release];
        greeter = newGreeter;
    }
}
```

You are being sent the object newGreeter. You want to own it to do something with it, so it is your job to retain it. On the other hand, you are about to set the variable greeter to point to the object referenced by newGreeter.

First, check to make sure the pointers aren't pointing at the same memory location. If they are, then there is nothing to do. If not, then go ahead and set greeter to now point to the object referenced by newGreeter.

You are going to need to hold on to the object that newGreeter points to, so you send it a retain message. On the other hand, you don't need the object that greeter points to anymore, so you release it. Now you set greeter to point to what newGreeter points to. Even though you are never going to use the variable newGreeter again, you are going to use what it pointed to. This whole retain-release cycle was retaining and releasing what the variables point to and not the variables themselves.

This retain-release method of memory management does have parallels in everyday life. For example, the conference hotel where I wanted to stay was completely booked. They put me on the waiting list, and I

> 6. There are potential consequences that could come up if you are using Key Value Observing and someone else is still registered to listen to changes in the object being released and set to nil. I tend to just send the variable the release message in dealloc and leave it at that.

> 7. You saw this briefly when we were looking at property memory attributes in the previous chapter. This version is slightly different, and now you better understand the retain-release cycle.