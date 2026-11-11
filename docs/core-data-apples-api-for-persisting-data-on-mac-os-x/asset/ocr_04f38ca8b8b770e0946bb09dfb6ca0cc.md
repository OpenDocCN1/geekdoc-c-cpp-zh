Finder both in place of a standard file icon and in Cover Flow. The preview is used when Quick Look is invoked in Finder, Mail, and so on. Therefore, the Quick Look template creates two .c (now .m) files, one for each. We will tackle the thumbnail file first.

# ### Generating the Quick Look Thumbnail

The file GenerateThumbnailForURL.m has one function inside it that is called by the Quick Look manager (part of the operating system). This function expects that we will be populating the QLThumbnailRequestRef and returning the OSStatus of noErr. Based on the documentation for Quick Look, even if we suffer a complete failure inside of our plug-in, we should always return noErr.

As you can probably guess, our thumbnail generation code is going to be very simple. Since we already have an image included with each recipe, we are simply going to pass that image back whenever it is requested.

```
```objective-c
Download Spotlight/QuickLookPlugin/GenerateThumbnailForURL.m
OSStatus GenerateThumbnailForURL(void *thisInterface,
                                 QLThumbnailRequestRef thumbnail,
                                 CFURLRef url,
                                 CFStringRef contentTypeUTI,
                                 CFDictionaryRef options,
                                 CGSize maxSize)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    @try {
        NSDictionary *metadata;
        metadata = [NSDictionary dictionaryWithContentsOfURL:(NSURL*)url];
        NSString *pathToImage = [metadata valueForKey:@"kPPImagePath"];
        if (!pathToImage) {
            //No image available
            return noErr;
        }
        NSData *imageData = [NSData dataWithContentsOfFile:pathToImage];
        if (!imageData) {
            //Unable to load the data for some reason.
            return noErr;
        }

        QLThumbnailRequestSetImageWithData(thumbnail, (CFDataRef)imageData, NULL);
    } @finally {
        [pool release], pool = nil;
    }
    return noErr;
}
```
```