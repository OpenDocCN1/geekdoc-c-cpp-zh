Value transformers are a customizable extension to the transformation code built into bindings. You can use them to convert a value from any object into any other object, or to process values in more complex ways, such as performing math, changing data formats, or even sending values over the Internet to a remote server.

A value transformer is a subclass of the `NSValueTransformer` class. To create and use a transformer, follow these steps:

+   1. **Create a new object in Xcode.** Replace the header and the start of the implementation with the value transformer boilerplate code provided below.
+   2. **Add more boilerplate code to the App Delegate’s initialize method to register the transformer.**
+   3. **Type the transformer’s name into the Value Transformer box under the Model Key Path.**

When you save the nib file and build and run the application, the transformer processes the value pulled from the data source and replaces it with a transformed value.

In this example, you’ll create a transformer called `IndexToNameTransformer` that takes a radio button index and returns a corresponding string. The boilerplate to register the transformer is shown below. Add equivalent code to the App Delegate, replacing the name field with the name of your own transformer object. You can allocate multiple transformers. Each must have a unique name string.

```
```objc
+ (void) initialize {
    NSValueTransformer *transformer =
    [[IndexToNameTransformer alloc] init];
    [NSValueTransformer setValueTransformer:transformer
        forName:@"IndexToNameTransformer"];
}
```
```

The transformer object header declares your custom subclass of `NSValueTransformer`, which defines the transformer’s name.

```
```objc
#import <Cocoa/Cocoa.h>
#import <Foundation/Foundation.h>
@interface IndexToNameTransformer : NSValueTransformer
{}
@end
```
```