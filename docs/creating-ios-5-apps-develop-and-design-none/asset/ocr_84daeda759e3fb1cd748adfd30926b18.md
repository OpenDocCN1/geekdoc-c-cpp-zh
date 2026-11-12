```
```objc
CGImageDestinationAddImage(
    destination,
    self.imageToExport.CGImage,
    (__bridge CFDictionaryRef)metadata);
CGImageDestinationFinalize(destination);
CFRelease(destination);
```
```

Here, we’re going to use a CGImageDestination to write out our image data as a JPEG file in memory. Image destinations abstract the task of writing images in various formats. A single image destination can save one or more images, including thumbnails.

There are simpler ways to generate image file data. UIImageJPEGRepresentation() and UIImagePNGRepresentation() both return an NSData containing the raw data for their respective image file formats. However, these methods don’t let us add our image metadata.

Using an image destination takes three steps. First, we create our CGImageDestinationRef, passing in the NSMutableData to hold our file contents, a uniform type identifier for the image type, and the number of images. The final argument, options, doesn’t yet do anything, but it is reserved for future use. Next, we add the images—including our metadata—to the destination. Finally, we finalize the destination. This will write the image files to our NSData.

```
```objc
// Open email compose window & set initial values.
MFMailComposeViewController* composer =

[[MFMailComposeViewController alloc] init];
[composer setSubject:@"My GravityScribbler drawing"];
[composer setMessageBody:@"Here's a drawing I created"
@" using GravityScribbler." isHTML:NO];
[composer addAttachmentData:imageData
                    mimeType:@"image/jpeg"
                    fileName:@"GravityScribbler.jpg"];
composer.mailComposeDelegate = self;
```
```