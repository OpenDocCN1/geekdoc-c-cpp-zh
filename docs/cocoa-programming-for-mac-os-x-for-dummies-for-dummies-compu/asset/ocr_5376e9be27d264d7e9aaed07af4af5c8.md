Besides using **YES** or **NO** for the Objective-C **BOOL** type value, it’s important for another reason: It works with other objects in Cocoa. Again, arrays and other types of collection objects expect their elements to be objects themselves. If you wanted to create an **NSArray** of Boolean values in Cocoa, you'd pass the **BOOL** type to the **numberWithBool** class method of **NSNumber**:

```

//create an NSNumber with a BOOL
n = [NSNumber numberWithBool:YES];

//add the NSNumber to an array
[theArray addObject:n];

```

# Working with Dates

The **NSCalendarDate** class gives you many options when it comes to working with dates and times. One of the most common tasks you perform is finding the current date or time. You can do this in one line of code with an **NSCalendarDate** class method:

```

NSDate *theDate = [NSCalendarDate date];

```

After you retrieve this date, you can easily convert it into an **NSString**, suitable for display. Simply use the **description** method to display the date in standard international format. In this example, **NSLog** displays the date in the console:

```

NSLog(@"theDate = %@", [theDate description]);

```

This yields results like this:

```

theDate = 2008-08-05 05:08:13 -0500

```

The **description** method is okay for quick-and-dirty date displays, but sometimes you want to display the date in a more human-friendly format. The **descriptionWithCalendarFormat** method can help you build an **NSString** that holds the date or time. The **descriptionWithCalendarFormat** method has three parameters. The first parameter is the only one that you have to worry about for simple date work. That parameter is an **NSString** that represents the date in the format you desire.