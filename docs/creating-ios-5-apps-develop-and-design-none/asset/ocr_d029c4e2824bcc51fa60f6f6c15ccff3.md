```
```objective-c
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
```

Our drawRect: method is fairly simple. We just grab a reference to the current context, then call drawSketchToContext: We’re breaking out the actual drawing code so that we can reuse it later when we export our images.

In drawSketchToContext: we create an image from our image context (again, protected by a dispatch_sync block). Then we just want to draw our image to our context. The context will already have a clipping path set to the rect argument—so we don’t need to do any additional clipping. CGContextDrawImage() is smart enough to only copy the data inside the clipping path.

However, we have a problem. If we just call CGContextDrawImage(), our image will appear upside down (flipped vertically, not just rotated 180 degrees). The problem comes from the difference in coordinate systems. By default, iOS uses a coordinate system with the origin at the upper-left corner, with positive numbers going down and to the right. Mac OS X has the coordinate system in the lower-left corner, with the coordinates going up and to the right. Core Graphics (and some other technologies, like Core Text) are based on the original OS X coordinate system.

Usually this isn’t a problem, since the graphics contexts are typically inverted and offset before we perform any drawing. For example, in Chapter 5 we freely mixed UIKit and Core Graphics methods with no coordinate problems. However, we will occasionally find some rough patches in odd corners of the framework. CGContextDrawImage() is a prime example. This method places the image in the correct position for our graphics context, but internally it flips the image contents.