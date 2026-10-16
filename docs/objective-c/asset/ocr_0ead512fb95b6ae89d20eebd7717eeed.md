This may sound cool, just on the surface, but what makes it even cooler is that when declaring a category, you do not need to have access to the original source code of the class that you are extending. Furthermore, a category is not a subclass. Meaning, the methods that you are adding are actually being added to the implementation of the class that you are directly manipulating. Any users of that class in your application will have access to those methods on instances of that class simply by virtue of you declaring a category on it.

Although it is considered poor form to do so, you can use categories to override existing methods. When doing this, even third-party libraries will call your modified method when referencing the class in question instead of the original.

If you’re coming to Objective-C from another dynamic language such as Ruby or Smalltalk, you may be familiar with the concept of mixins. Mixins and categories share a lot in common, and you could even say that categories are the Objective-C version of a mixin.

# Declaring categories

Categories are declared similarly to how you declare class interfaces. Meaning, you declare a category by first typing @interface and then the class name that you wish to modify. After the class name, instead of the superclass, as in the case of declaring a class, you put the name of the category that you are declaring inside parentheses. Listing 8.1 shows an example category declared on the NSMutableString class.

Listing 8.1

An example category on NSMutableString adding the ability to insert a GUID into the string

```
#import <Foundation/Foundation.h>

@interface NSMutableString (GUID)

- (void)appendGuid;

@end
```

In this particular code, I’m adding a category to the NSMutableString class that will generate a globally unique identifier (GUID). For now, this category simply appends the GUID onto the end of whatever string is there.