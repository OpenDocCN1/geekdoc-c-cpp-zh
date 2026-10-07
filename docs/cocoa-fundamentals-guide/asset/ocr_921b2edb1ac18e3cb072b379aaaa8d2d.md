# CHAPTER 3

Adding Behavior to a Cocoa Program

# Resource Management and Other Efficiencies

There are all sorts of things you can do to enhance the performance of your objects and, of course, the application incorporates and manages these objects. These procedures and disciplines range from multithreading to drawing optimizations and techniques for reducing your code footprint. You can learn about these things by reading Cocoa Performance Guidelines and other performance documents.

Yet you can, before adopting a more advanced performance technique, improve the performance of your objects significantly by following three simple, common-sense guidelines:

+   Don't load a resource or allocate memory until you need it.

If you load a resource of the program, as a nil file or an image, and don't use it until much later, or don't use it at all, that is a inefficiency. Your program's memory footprint is bloated for no reason. You should load or allocate memory only when there is an immediate need.

For example, if your application's preferences are in a separate nil file, don't load that file until the user chooses Preferences from the allocation menu. The same caution goes for allocating memory for some task; hold off on allocation until the need for memory appears. This technique of lazy-loading or lazy-allocation is easily implemented. For example, if your application has an image that loads, upon the first user request, for displaying in the user interface. Listing 3-9 shows one approach: loading the image in the getter for the image.

# Listing 3-9 Lazy-loading of a resource

```
(NSImage*)image |
if (!image) // fooImage is an instance variable
NSString *imagePath = [[NSBundle mainBundle] pathResource:@"Foo" ofType:@"jpg"];
if (!imagePath) return nil;\image = [[NSImage alloc] initWithContentsOfFile:imagePath];
return image;
```

+   Use the Cocoa API; don't dig down into lower-level programming interfaces.

Much effort goes into making the implementations of the Cocoa frameworks as robust, secure, and efficient as possible. These implementations introduce many interdependencies that you might not be aware of. If, instead of using the Cocoa API for a certain task, you decide to "roll your solution" using lower-level interfaces, you'll probably end up writing code, which introduces a greater risk of error or inefficiency. Also, by leveraging Cocoa, you are better prepared to take advantage of future enhancements at the same time you are insulated from changes in the underlying implementations. So use the Cocoa for a programming if one exists and its capabilities answer your needs.

+   Practice good memory-management techniques.

If you do not enable garbage collection (which is disabled in default in iOS), perhaps the most important thing you can do to improve the efficiency and robustness of your custom objects is to practice good memory-management techniques. Make sure every object allocation, copy message is matched with a corresponding release message or retain message. Become familiar with the policies and techniques for proper memory management and practice, practice, practice. See Memory Management Programming* guide for complete details.

# Basic Subclass Design

2010-12-13 | © 2010 Apple, Inc. All Rights Reserved.