```
#import <Foundation/Foundation.h>
#import "Logger.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Logger *logger = [[Logger alloc] init];

        NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                        target:logger
                                                      selector:@selector(sayOuch:)
                                                      userInfo:nil
                                                      repeats:YES];

        [[NSRunLoop currentRunLoop] run];
    }
    return 0;
}
```

Build and run the program. (You will get an unused variable warning. Ignore it for now.) You should see Ouch! appear in the console every 2 seconds.

Note that the colon is part of the selector. @selector(sayOuch) is not equal to @selector(sayOuch:).

Take a second look at the warning from the compiler. It is saying, “Hey, you created the variable timer, but didn’t use it.” In some settings, like this one, you need to flag a variable as purposefully unused to silence the warnings. This is done with the \_\_unused modifier. Add that now.

```
  \_\_unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                           target:logger
                                                         selector:@selector(sayOuch:)
                                                         userInfo:nil
                                                         repeats:YES];
```

Build it again, and the warning should be gone.

# Helper objects

Timers are simple. They only do one thing: fire. Thus, target-action is a good fit. A lot of simple user interface controls, like buttons and sliders, also use the target-action mechanism. What about something more complex?

In Chapter 23, you used an NSURLConnection method to fetch data from a web server. It worked fine, but there are two problems with the method:

+   *   It blocks the main thread while waiting for all the data to arrive. If you used this method in a real application, the user interface would become unresponsive while the data was fetched.
*   It has no way to callback if, for example, the webserver demands a username and password.

For these reasons, we typically use an NSURLConnection asynchronously. That is, we start it fetching and then await callbacks as the data arrives or the web server demands credentials or the fetch fails. How do you get these callbacks? You supply the NSURLConnection with a helper object. When things happen, the connection sends messages to the helper object. What messages? The guy who wrote