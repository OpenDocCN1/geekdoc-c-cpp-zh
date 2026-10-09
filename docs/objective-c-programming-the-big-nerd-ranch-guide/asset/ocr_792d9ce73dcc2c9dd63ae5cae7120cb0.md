```
NSURL *url = [NSURL URLWithString:
 @"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
NSURLRequest *request = [NSURLRequest requestWithURL:url];

__unused NSURLConnection *fetchConn = [[NSURLConnection alloc] initWithRequest:request
 delegate:logger
 startImmediately:YES];

__unused NSTimer *timer
 = [NSTimer scheduledTimerWithTimeInterval:2.0
 target:logger
 selector:@selector(sayOuch:)
 userInfo:nil
 repeats:YES];

[[NSRunLoop currentRunLoop] run];
}
return 0;
}
```

Now implement the method that will get called in Logger.m:

```
- (void)zoneChange:(NSNotification *)note
{
 NSLog(@"The system time zone has changed!");
}
```

Build and run the program. While it is running, open **System Preferences** and change the time zone for your system. You should see that your **zoneChange:** method gets called. (On some systems, it seems to get called twice. This is not cause for concern.)

# Which to use?

In this chapter, you have seen three kinds of callbacks. How does Apple decide which one to use in any particular situation?

+   *   Objects that do just one thing (like **NSTimer**) use target-action.
*   Objects that have more complicated lives (like an **NSURLConnection**) use helper objects, and the most common type of helper object is the delegate.
*   Objects that might need to trigger callbacks in several other objects (like **NSTimeZone**) use notifications.

# Callbacks and object ownership

With all of these callbacks, there is a danger that objects waiting for the callbacks might not get deallocated correctly. Thus, it was decided that: