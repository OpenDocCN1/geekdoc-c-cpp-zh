# The @implementation Section 37

![](bbox=[0.283, 0.095, 0.715, 0.193])

Figure 3.1 Declaring a method

When a method takes an argument, you also append a colon to the method name when referring to the method. Therefore, setNumerator: and setDenominator: is the correct way to identify these two methods, each of which takes a single argument. Also, identifying the print method without a trailing colon indicates that this method does not take any arguments. In Chapter 7, "More on Classes," you will see how methods that take more than one argument are identified.

# The @implementation Section

As noted, the @implementation section contains the actual code for the methods declared in the @interface section. Just as a point of terminology, you say that you declare the methods in the @interface section and you define them (that is, give the actual code) in the @implementation section.

The general format for the @implementation section is as follows:

```
@implementation NewClassName
methodDefinitions;
end
```

NewClassName is the same name that was used for the class in the @interface section. You can use the colon followed by the parent class name, as we did in the @interface section:

```
@implementation Fraction: NSObject
```

However, this is optional and typically not done. The methodDefinitions part of the @implementation section contains the code for each method specified in the @interface section. Similar to the @interface section, each method's definition starts by identifying the type of method (class or instance), its return type, and its arguments and types. Instead of the line ending with a semicolon, the code for the method follows, enclosed inside a set of curly braces. Consider the @implementation section from Program 3.2:

```
//---- @implementation section -----
@implementation Fraction
-(void)print
{
    NSLog("%@i/%*i", numerator, denominator);
}

```