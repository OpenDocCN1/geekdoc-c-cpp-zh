# CHAPTER 2
Cocoa Objects

```
CFLocaleRef myLocale = CFLocaleCopyCurrent();
NSLocale * myNSLocale = (NSLocale *)myLocale;
[myNSLocale autorelease];
NSString *identifier = [myNSLocale localeIdentifier];
CFShow((CFString*)@identifier: stringByAppendingString:identifier);
// logs identifier for current locale
```

Note from the example that the memory management functions and methods are also interchangeable—you can use CFRelease with a Cocoa object and release with a Foundation object.

> Note: When using garbage collection, there are important differences to how memory works for Cocoa objects and Foundation objects. See "Using Foundation with Garbage Collection" for details.

Toll-free bridging has been available since Mac OS X v10.0. Table 2-5 provides a list of the data types that are interchangeable between Core Foundation and Foundation. For each pair, the table lists the version of Mac OS X in which toll-free bridging between them became available.

Table 2-5 Data types that can be used interchangeably between Core Foundation and Foundation

| Core Foundation type | Foundation class | Availability |
|---|---|--|
| CFArrayRef | NSArray | Mac OS X v10.0 |
| CFAttributedStringRef | NSAttributedString | Mac OS X v10.4 |
| CFCalendarRef | NSCal | Mac OS X v10.4 |
| CFCharacterSet | NSCharacterSet | Mac OS X v10.0 |
| CFDataRef | NSData | Mac OS X v10.0 |
| CFDateRef | NSDate | Mac OS X v10.0 |
| CFDictionaryRef | NSDictionary | Mac OS X v10.0 |
| CFErrorRef | NSError | Mac OS X v10.5 |
| CFLocaleRef | NSLocale | Mac OS X v10.4 |
| CFMutableArrayRef | NSMutableArray | Mac OS X v10.0 |
| CFMutableAttributedStringRef | NSMutableAttributedString | Mac OS X v10.4 |
| CFMutableCharacterSet | NSMutableCharacterSet | Mac OS X v10.0 |
| CFMutableDataRef | NSMutableData | Mac OS X v10.0 |
| CFMutableDictionaryRef | NSMutableDictionary | Mac OS X v10.0 |
| CFMutableSetRef | NSMutableSet | Mac OS X v10.0 |
| CFMutableStringRef | NSMutableString | Mac OS X v10.0 |

Toll-free Bridging
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.