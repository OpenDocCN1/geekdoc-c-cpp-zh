446 Chapter 20 Introduction to Cocoa and Cocoa Touch

![](bbox=[0.285, 0.105, 0.715, 0.415])

Figure 20.1 The application hierarchy

The Application Services layer includes support for printing and graphics rendering, including Quartz, OpenGL, and Quicktime.
Directly below your application sits the Cocoa layer. As noted, Cocoa includes the Foundation, Core Data, and AppKit frameworks. Foundation offers classes for working with collections, strings, memory management, the file system, archiving, and so on. AppKit provides classes for managing views, windows, documents, and the user interface for which Mac OS X is well known.
From this description, there seems to be duplication of functionality between some of the layers. Collections exist in both the Cocoa and Core Services layers. However, the former builds on support of the latter. Also, in some cases, a layer can be bypassed or "bridged." For example, some Foundation classes, such as those that deal with the file system, rely directly on Core Services and so bypass the Application Services layer. In many cases, the Foundation framework defines an object-oriented mapping of data structures defined in the lower-level Core Services layer (which is written primarily in the procedural C language).

# Cocoa Touch

iOS devices like the iPhone, the iPod Touch, and the iPad contain a computer that runs a scaled-down version of Mac OS X. Some features in the iPhone’s hardware, such as its accelerometer, are unique to the phone and not found in other Mac OS X computers, such as MacBook Pro’s or iMacs.