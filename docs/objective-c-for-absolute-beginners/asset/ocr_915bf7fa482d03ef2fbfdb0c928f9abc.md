# Introducing Properties

When we created instance variables for the Book object, we manually created the methods that could be used to access these variables. Now that you know how to do this manually, let's look at how to take advantage of something called properties. A property is a short way of having the compiler functions to get and/or the value of an instance variable. As you learned earlier, instance variables are generally accessible from outside of the object itself, so having methods to get and set these variables becomes essential.

The following is the interface (header) file to the Book object that we created earlier. Let's see what it takes to have the Objective-C compiler create its getters and setters for us.

+   Listing 8-13. Adding properties to the Book object.
// Book.h
// Mybookstore
// Created by M.R. Fisher on 8/28/11. All rights reserved.
// Copyright (c) 2011 www.committed-code.com.
//
#import <Foundation/Foundation.h>
@interface Book : NSObject {
}
// @property(nonatomic,strong) NSString *title;
// @property(nonatomic,strong) NSString *author;
// @property(nonatomic,strong) NSString *description;
//
@end

Lines 14–16 show the property declarations for the instance variables. Properties are not required for all instance variables, the ones we want to expose to the world. In the example, however, we are creating properties for all of our instance variables. Notice that the actual instance variable declarations used to be between the { } brackets are now gone. When using properties with Xcode 4 it is no longer necessary to declare the instance variables and the properties. The compiler is now smart enough to do this for you.

A property starts with a @property directive. This tells the Objective-C compiler to build us the automatic getter and/or setter. Whether it is a getter and/or setter is included in the declaration. Let's discuss this code:

```
@property¹ (nonatomic,strong) NSString* title;
```