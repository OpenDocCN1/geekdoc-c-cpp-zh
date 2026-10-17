```
#import <Foundation/Foundation.h>
void doSomething(NSUInteger count, NSArray *objects, NSString *string){
    NSObject *objectID = nil;

    for (NSUInteger i = 0; i< count; i++){
        NSObject *obj = [objects objectAtIndex:i];

        if([obj isMemberOfClass:[NSString class]]){
            objectID = [[NSString alloc] initWithString:string];
        }

        //Do Something

        if (objectID != nil){
            [objectID release];
        }
    }
}
```

FIGURE 17.4 A memory issue flagged by the static analyzer

# MEMORY OVER-RELEASES

Again in simple terms, an over-release in a Cocoa application is when an object is sent a -release too many times, causing its memory to be deallocated too soon. Any subsequent attempt to communicate with it will cause your application to crash. In Figure 17.4, the analyzer finds a potential over-release scenario on line 27.