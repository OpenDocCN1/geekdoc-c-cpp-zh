is almost never an issue. My accessor method might be taking care of other stuff for me. I use my accessor anytime I set that variable." In reality, either approach will work in the vast majority of cases.

# init methods that take arguments

Sometimes an object can't be initialized properly without some information from the method that is calling it. For example, imagine that an appliance can't function without a name. (nil doesn't count.) In this case, you need to be able to pass the initializer a name to use.

You can't do this with **init** because, for now and always, **init** has no arguments. So you have to create a new initializer instead. Then, when another method creates an instance of **Appliance**, it would look like this:

```
`Appliance *a = [[Appliance alloc] initWithProductName:@"Toaster"];`
```

The new initializer for **Appliance** is **initWithProductName**, and it accepts an **NSString** as an argument. Declare this new method in Appliance.h:

```
`#import <Foundation/Foundation.h>

@interface Appliance : NSObject {
    NSString *productName;
    int voltage;
}
@property (copy) NSString *productName;
@property int voltage;
- (id)initWithProductName: (NSString \*)pn;

@end`
```

In Appliance.m, find the implementation of **init**. Change the name of the method to **initWithProductName**: and set productName using the passed-in value.

```
`- (id)initWithProductName: (NSString \*)pn
{
    // Call NSObject's init method
    self = [super init];

    // Did it return something non-nil?
    if (self) {

        // Set the product name
        [self setProductName:pn];

        // Give voltage a starting value
        [self setVoltage:120];
    }
    return self;
}`
```

Before you continue, build the project to make sure the syntax is right.

Now you can create an instance of **Appliance** with a given name. However, if you give Appliance.h and Appliance.m to another programmer, she may not realize she needs to call **initWithProductName**: What if she creates an instance of **Appliance** in the most common way?