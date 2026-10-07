# CHAPTER 13: Memory, Addresses, and Pointers

Listing 13-9. Keeping an Autorelease Variable Available.

```
- (NSDate *)getDate
{
    return [NSDate date];
}
- (void)captureDate
{
    // Capture the current date and store it in the class's iVar
    currentDate = [self getDate retain];
}
- (void)dealloc
{
    // Release the memory for the current_date.
    [currentDate release];
}
```

Notice on line 9 that the getDate method is called and then we immediately send a retain message to the object. This is because getDate is set as autorelease. If the program didn't do this, the memory to current_date would have been autoreleased.

> NOTE: In any iOS application developed before Xcode 4.2, there is a line in the .m file that looks as follows:

AutoreleasePool * pool = [[AutoreleasePool alloc] init];

This is the mechanism the program uses to autorelease memory that has been sent an autorelease message when it was allocated, like our example. The [NSDate date] returns its memory which is automatically added to this autorelease pool and then automatically deallocated at the next run-loop.

# Sending the dealloc Message

Under normal circumstances, your program should never send a dealloc message to another object. There are some exceptions. One of these is when handling the dealloc message itself. You will be dealing with the dealloc message only for objects you create. Listing 13–10 is a snippet of code that shows how a typical dealloc message is coded. Every object that you create should implement a dealloc message except when using ARC, garbage collection, or if there's nothing to release.

Listing 13-10. A typical dealloc implementation.

```
- (void)dealloc
{
    self.iVar = nil;           // If we have ivars, make sure they are deallocated.
// This instance variable is a property (Chapter 10)
    [iVar release];            // Another example. We release an instance variable
// that we we were using - it wasn't a property.
// We finally tell the proper to deallocate itself.
    [super dealloc];          // This is one of the few times dealloc will be called
```