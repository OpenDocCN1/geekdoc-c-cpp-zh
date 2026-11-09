Methods are listed as signatures — one-line summaries that list the type, output type, name, and parameters used in the method. Signatures end with a semicolon. They do not include implementation code.

In both the interface and implementation files, Objective-C uses the – character as a prefix for instance method definitions and + as a prefix for class method definitions.

```
```
- (void) thisIsAnInstanceMethod;
+ (void) thisIsAClassMethod;
```
```

# ## Defining accessors: setters and getters

In Objective-C, properties are private and invisible unless setter and getter methods are defined for them. Setters write values; getters read them. Properties can allow either or both modes of access. You can define setters and getters explicitly with code, or implicitly using the @synthesize directive.

Use @synthesize to generate the setters and getters required for simple read and write operations. The directive works rather like a macro, and it creates setter and getter code automatically. It also implements dot-format property access.

```
```
anInt = anObject.numberOfElephants;
anObject.numberOfWheels = 5;
```
```

This syntax is common in other languages. In Objective-C, it is only valid if the properties are synthesized.

Use explicit setter and getter code when reading or writing a property triggers a more complex outcome, such as a change in the state of an object or an operation that accesses other properties and features. For example, a setter can automatically redraw visible graphics when a window's size is changed, or a getter can count the number of times a property has been accessed and write the count to another property.

By convention, getter method names are identical to the name of the property they access, while setters prefix the name with set. Define setters and getters in the interface as follows:

```
```
- (int) numberOfElephants; //A getter for the numberOfElephants property
- (void) setNumberOfWheels: (int) aNumber; //A setter for the numberOfWheels property
```
```

To use them, the syntax is

```
```
anInt = [anObject numberOfElephants];
[anObject setNumberOfWheels: 5];
```
```

The compiler doesn't enforce this naming convention, but it's used in Cocoa and it helps make the code easy to read. There are no restrictions on the complexity of setter and getter code. If necessary, a single setter method can dramatically change the state of the entire application.