# CHAPTER 3
Adding Behavior to a Cocoa Realm

**Figure 3-4** Where to put declarations in the interface file

```
#import <Foundation/Foundation.h>
Additional imports
Function and data type declarations
@Interface Controller : NSObject (
    Instance variables
)
@end
```

See "Instance Variables" (page 119) and "Functions, Constants, and Other C Types" (page 132) for information about these types of declarations.

You begin the class interface by importing the appropriate Cocoa frameworks as well as the headers for any types that appear in the interface. The #import preprocessor command is similar to #include in that it incorporates the specified header file. However, #import improves on efficiency by including the file only if it was not previously included, directly or indirectly. The angle brackets following the command identify the header file it is from, after a slash, the header file itself.
The syntax for it is #import line the form:

```
#import <Framework/File.h>
```

The framework must be in one of the standard system locations for frameworks. In the example in Listing 3-2 (page 117), the class interface files the file Foundation.h from the Foundation framework. As in this case, the Cocoa convention is that the header having the same name as the framework contains a list of #import commands that define all public interfaces (and other headers) of the framework. Incidentally, if you're defining part of an application, all you need to do is import the Cocoa.h file of the umbrella framework.

If you must import a header file that is for your project, use question marks rather than angle brackets as delimiters; for example:

```
#import "MyDataTypes.h"
```

The class implementation file has a simpler structure, as shown in Listing 3-3. It is important that the class implementation file begin importing the class interface file.

**Listing 3-3** The basic structure of an implementation file

```
#import "Controller.h"

@implementation Controller

@end
```

You must write all method and property implementations between the @implementation and @end directives. The implementations of functions related to the class can go anywhere in the file, although they are also put between the two directives. Declarations of private types (functions, structures, and so on) typically go between the #import commands and the @implementation directive.

# Basic Subclass Design
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.