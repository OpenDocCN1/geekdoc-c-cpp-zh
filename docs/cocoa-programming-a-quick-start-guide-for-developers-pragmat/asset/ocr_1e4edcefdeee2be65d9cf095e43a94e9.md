Reading from the right, when you initialize an object, the first thing you do is make a call to the superclass’s init method. You assign this initialized object to self, and then you test that self is not nil. If it isn’t, then go ahead and customize it as we’ve done in line 11. This lets you start with all the initializations you had before you started writing this method and then fill in the additional initializations on top of them. Finally, you return your object in line 13.

You’ll often see this slightly more verbose way of accomplishing the same thing:

```
    - (id) init
    {
        self = [super init];
        if (self != nil) {
            name = @"World";
        }
        return self;
    }
```

If you use this second version, I prefer you replace `if (self != nil)` with `if(self)`.^10

Now let’s look at line 6 in the greeting method. We are returning a formatted string. This is similar to what you’ve seen in many other languages. You create a string with placeholders like `%d` in it. You follow the string with a comma-separated list of the values that replace the placeholders in the string.

In our case, we are using a new Cocoa type `%@`, which displays a string representation of a Cocoa object (as specified in its `description` method). In our case we have this:^11

```
    [[NSString alloc] initWithFormat:@"Hello, %@!", name]
```

This means we replace the `%@` with the value of `name`, which is currently `World`.^12 Our result is `Hello, World!`.

10. For a full discussion of `self` and `[super init]`, see Matt Gallagher’s article at http://cocoawithlove.com/2009/04/what-does-it-mean-when-you-assign-super.html. It’s also informative and entertaining to read Wil Shipley’s article on using `self= [super init]`, which you can find at http://www.wilshipley.com/blog/2005/07/self-stupid-init.html. Be sure to read to the end where he concludes it’s a good thing to use.

11. If you already know about memory management in Objective-C, you’ll see that I am introducing a memory leak here. It’s deliberate and is taken care of by the garbage collector, and later we’ll talk about what to do when we don’t have a garbage collector.

12. For more details on formatted strings, you can look up the method `stringWithFormat:` in the docs. This points to an article called “Formatting String Objects” with some examples