```
NSURLRequest *request = [NSURLRequest requestWithURL:url];
__unused NSURLConnection *fetchConn = [[NSURLConnection alloc] initWithRequest:request
    delegate:logger
    startImmediately:YES];
__unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
    target:logger
    selector:@selector(sayOuch:)
    userInfo:nil
    repeats:YES];
[[NSRunLoop currentRunLoop] run];
}
return 0;
}
```

The instance of **Logger** will need an instance of **NSMutableData** to hold onto the bytes as they arrive. Add an instance variable to Logger.h:

```
#import <Foundation/Foundation.h>
@interface Logger : NSObject {
    NSMutableData *incomingData;
}
- (void) sayOuch:(NSTimer *)t;
@end
```

Now implement some of the delegate methods in Logger.m:

```
#import "Logger.h"
@implementation Logger
- (void) sayOuch:(NSTimer *)t {
    NSLog(@"Ouch!");
}
// Called each time a chunk of data arrives
- (void) connection:(NSURLConnection *)connection
    didReceiveData:(NSData *)data
{
    NSLog(@"received %lu bytes", [data length]);
    // Create a mutable data if it doesn't already exist
    if (!incomingData) {
        incomingData = [[NSMutableData alloc] init];
    }
    [incomingData appendData:data];
}
// Called when the last chunk has been processed
- (void) connectionDidFinishLoading:(NSURLConnection *)connection
{
    NSLog(@"Got it all!");
```