
Traditionally, we would do this using a mutex to block access to critical sections.
In Objective-C, we could do this by adding the `@synchronized` directive. However,
starting with iOS 4.0, we have a better way.

iOS 4.0 brought Grand Central Dispatch (GCD) to iOS. GCD is a block-based
technology that lets us manage concurrency without explicitly using threads. It is
highly optimized, and it can automatically balance access to system resources based
on your system’s capabilities. For example, it will automatically split a concurrent
task among more threads when running on a 12-core Mac Pro than it does when
running on an iPhone 4.

For more information, check out the Grand Central Dispatch Reference and
the Concurrency Programming Guide in Apple’s documentation. In this chapter,
we simply use GCD to place tasks on a background queue or to move tasks back to
the main thread. We will also use it here, to protect critical sections.

We start by creating a dispatch queue in Canvas’s `initWithFrame:` method.

```objective-c
_serialQueue = dispatch_queue_create(
    "com.freelancemadscience.GravityScribbler.canvas",
    DISPATCH_QUEUE_SERIAL);
```

The `dispatch_queue_create()` function takes two arguments. The label can
be used to identify our queue in the debugger and in crash reports. We use reverse
DNS-style naming to guarantee that we have a unique label for our queue. Next,
the `DISPATCH_QUEUE_SERIAL` attribute defines our queue as a serial queue.

> **NOTE:** While GCD greatly simplifies concurrent programming,
> it doesn’t protect us from all the ugly, underlying details. For example,
> we can still create deadlocks by nesting `dispatch_sync()` calls (e.g.,
> `dispatch_sync(queue, ^{dispatch_sync(queue, ^{[self myMethod]});});`).
> The primary advantage of using `dispatch_sync()` over block-based
> threading is simply performance. GCD code will run significantly faster
> than its block-based equivalent.

![](img/fe9fea534a8e7868f811f7cd33da015f_456_0.png)

All GCD queues operate in strict FIFO order—the first block in is the first block out. Serial queues also guarantee that only one block will run at a time. Concurrent queues may process multiple blocks at once, splitting them across two or more threads, depending on system resources.

Now back to our previous code, `dispatch_sync()` simply dispatches a block to the specified queue and then waits until the block is finished. Since our serial queue will only process one block at a time, we can wrap our critical sections in `dispatch_sync()` blocks, serializing access to our image context.

Now let’s look at the actual drawing. When our cursor moves, the view controller will call Canvas’s `addLineToPoint:` method.

```objective-c
// Returns the bounds of the line.
- (CGRect)addLineToPoint:(CGPoint)endPoint {
    CGFloat xdist = endPoint.x - self.currentDrawPoint.x;
    CGFloat ydist = endPoint.y - self.currentDrawPoint.y;
    // Just ignore any tiny movements.
    if (((xdist * xdist) + (ydist * ydist)) < self.minDistance)
        return CGRectZero;
    __block CGRect bounds;
    dispatch_sync(self.serialQueue, ^{
        CGContextBeginPath(self.imageContext);
        CGContextMoveToPoint(self.imageContext,
                             self.currentDrawPoint.x,
                             self.currentDrawPoint.y);
        CGContextAddLineToPoint(self.imageContext,
                                endPoint.x,
                                endPoint.y);
        bounds = CGContextGetPathBoundingBox(self.imageContext);
        CGContextStrokePath(self.imageContext);
    });

    bounds = CGRectInset(bounds, -1.0f, -1.0f);
    NSAssert2(CGRectContainsPoint(bounds, self.currentDrawPoint),
        @"%@ does not contain starting point %@",
        NSStringFromCGRect(bounds),
        NSStringFromCGPoint(self.currentDrawPoint));
    NSAssert2(CGRectContainsPoint(bounds, endPoint),
        @"%@ does not contain ending point %@",
        NSStringFromCGRect(bounds),
        NSStringFromCGPoint(endPoint));

    // Update the invalid rectangle.
    if (CGRectEqualToRect(self.invalidRect, CGRectZero)) {
        self.invalidRect = bounds;
    } else {
        self.invalidRect = CGRectUnion(self.invalidRect, bounds);
    }
    // Update the current drawing point.
    self.currentDrawPoint = endPoint;
    return self.invalidRect;
}

We start by calculating the distance between our current cursor position, self.currentDrawPoint, and our new end point. If this distance is below our preset minimum, we just skip the update.

Next, we use dispatch_sync() to wrap our drawing code—again, protecting access to our image context. The drawing code simply creates a path from our old draw point to our new end point. We store a copy of the path's bounds (the __block storage type modifier lets us access the value of bounds outside the dispatch_sync() block). Then we draw the actual path.

We then expand the size of the bounding box by 1 pixel on all sides, just to make sure the entire line segment gets updated, including any joins and line caps. Then we update our invalidRect property. If we don't have an invalid rectangle, we just assign our current bounds. Otherwise, we combine the bounds by storing the union of the two rectangles.

This is important because our line-segment drawing and our view-updating code run on two different threads. If our updates from the accelerometer get ahead of the screen updates, we could add two or more new line segments between each screen update. We want to make sure all of them are drawn correctly.

Once we've added the line segment, our view controller will call updateCanvasUI on the main thread.

```objective-c
// Should be called on the main thread.
-(void)updateCanvasUI {
    self.cursor.center = self.currentDrawPoint;
    // As long as we have a non-zero bounds, redraw the screen.
    if (!CGRectEqualToRect(self.invalidRect,CGRectZero)) {
        [self setNeedsDisplayInRect:self.invalidRect];
        self.invalidRect = CGRectZero;
    }
}
```

This simply updates our cursor's position, then calls setNeedsDisplayInRect: and clears our invalid rectangle. Next time through the run loop, the system will call drawRect:.

```objective-c
- (void)drawRect:(CGRect)rect
{
    CGContextRef context = UIGraphicsGetCurrentContext();
    [self drawSketchToContext:context];
}
```

```objective-c
- (void)drawSketchToContext:(CGContextRef)context {
    // Draw the changed region of the image context.
    __block CGImageRef fullImage;
    dispatch_sync(self.serialQueue, ^{
        fullImage = CGBitmapContextCreateImage(self.imageContext);
    });

    // Need to adjust the coordinates to draw the image.
    CGContextSaveGState(context);
    CGContextTranslateCTM(context, 0.0f, self.bounds.size.height);
    CGContextScaleCTM(context, 1.0f, -1.0f);
    CGContextDrawImage(context, self.bounds, fullImage);
    CGContextRestoreGState(context);
    CGImageRelease(fullImage);
}
```

Our drawRect: method is fairly simple. We just grab a reference to the current context, then call drawSketchToContext: We’re breaking out the actual drawing code so that we can reuse it later when we export our images.

In drawSketchToContext: we create an image from our image context (again, protected by a dispatch_sync block). Then we just want to draw our image to our context. The context will already have a clipping path set to the rect argument—so we don’t need to do any additional clipping. CGContextDrawImage() is smart enough to only copy the data inside the clipping path.

However, we have a problem. If we just call CGContextDrawImage(), our image will appear upside down (flipped vertically, not just rotated 180 degrees). The problem comes from the difference in coordinate systems. By default, iOS uses a coordinate system with the origin at the upper-left corner, with positive numbers going down and to the right. Mac OS X has the coordinate system in the lower-left corner, with the coordinates going up and to the right. Core Graphics (and some other technologies, like Core Text) are based on the original OS X coordinate system.

Usually this isn’t a problem, since the graphics contexts are typically inverted and offset before we perform any drawing. For example, in Chapter 5 we freely mixed UIKit and Core Graphics methods with no coordinate problems. However, we will occasionally find some rough patches in odd corners of the framework. CGContextDrawImage() is a prime example. This method places the image in the correct position for our graphics context, but internally it flips the image contents.
