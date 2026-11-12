
We also need to replace the init method with a new designated initializer:

```objective-c
#pragma mark - initialization
- (id)initWithFileURL:(NSURL *)url
{
    self = [super initWithFileURL:url];
    if (self) {
        _weightHistory = [[NSMutableArray alloc] init];
    }
    return self;
}
```

We're still overriding our superclass's designated initializer. The name has changed and it takes an argument—but since we just pass the argument on to the superclass, it doesn't affect our implementation. Also, we've deleted the code that initialized our _defaultUnits property. Other than that, everything's the same.

Now we just need to implement a few required features. Specifically, we need to override the UIDocument methods to save and load our data. We need to change our weightHistory accessors, letting us alert the superclass whenever a change is made. Finally, we need to deal with version conflicts whenever they arise.

## SAVING AND LOADING THE DOCUMENT

The easiest way to save and load our UIDocument is to simply convert our model into an NSData instance. This isn't absolutely required. UIDocument has a number of methods we could override to more fully customize our saving and loading code—but we should try to use simple NSData or NSFileWrapper objects whenever possible.

Currently, our WeightHistory class has a single instance variable: our weightHistory mutable array. So how do we convert an array into an NSData object? A quick glance at the class references for NSMutableArray and NSData doesn't reveal any obvious methods for converting one into the other; however, NSMutableArray does adopt the NSCoding protocol. This means we can load and save our array using a keyed archiver—and keyed archivers can read and write to NSData objects (or directly to files, for that matter).

There’s just one catch: All the objects in our array must also adopt the NSCoding protocol. Unfortunately, our WeightEntry class does not. Fortunately, this is easy to fix. Let’s start by adding the protocol to WeightEntry’s interface:

```objective-c
@interface WeightEntry : NSObject <NSCoding>
```

Then open the implementation file and define the keys that we will need. Place these before the @implementation block.

```objective-c
static NSString* const WeightInLbsKey = @"WeightHistoryWeightInLbs";
static NSString* const DateKey = @"WeightHistoryDate";
```

Now we need to implement NSCoding’s required methods. First, let’s implement the encodeWithCoder: method.

```objective-c
#pragma mark - NSCoding Methods
- (void)encodeWithCoder:(NSCoder *)encoder {
    [encoder encodeFloat:self.weightInLbs forKey:WeightInLbsKey];
    [encoder encodeObject:self.date forKey:DateKey];
}
```

This is relatively straightforward. When saving an object hierarchy, each object’s encodeWithCoder: method is called in turn. The object is responsible for saving all of its non-transient internal data. In our case, we simply save our data using our WeightInLbsKey and DateKey.

Next, implement the initWithCoder: method.

```objective-c
- (id)initWithCoder:(NSCoder *)decoder {
    self = [super init];
    if (self) {
        _weightInLbs = [decoder decodeFloatForKey:WeightInLbsKey];
        _date = [[decoder decodeObjectForKey:DateKey] retain];
    }
    return self;
}
```

We actually saw initWithCoder: in “Building a Custom View” in Chapter 5. GraphView used it when loading from a nib file. As it turns out, the system uses NSCoding to store and load nibs.

In many ways, initWithCoder: mirrors our designated initializer. If the superclass adopts the NSCoding, we should call the superclass’s initWithCoder: method. Just like our designated initializer, we assign the return value from the superclass’s initWithCoder: method to self. As long as self is a valid object (not equal to nil), we decode the rest of our data using our keys and assign those values to our instance variables. Then we return self.

In WeightEntry, our superclass (NSObject) does not adopt NSCoding. As a result, we cannot call [super initWithCoder: decoder]. Instead, we call the superclass’s designated initializer.

In both cases, this bypasses our class’s designated initializer. Therefore, we need to make sure our initWithCoder: method duplicates any of the setup and configuration steps performed in the designated initializer. initWithWeight:units:forDate: sets both the _weightInLbs and _date instance variables, so we do the same thing here. In fact, initWithCoder: is a bit simpler. We know that the weights are always saved in pounds, so we don’t need the extra logic to convert from kilograms.

If you look at our GraphView class, you will see a similar relationship. Both initWithFrame: and initWithCoder: call [self setDefaults]. Again, initWithCoder: duplicates our designated initializer’s configuration steps.

With that out of the way, we can now override UIDocument’s contentsForType: error: and loadFromContents:ofType:error: methods.

```
#pragma mark - iCloud Methods
- (id)contentsForType:(NSString *)typeName
    error:(NSError **)outError {
    return [NSKeyedArchiver archivedDataWithRootObject:
        self.weightHistory];
}
```

## USING KEYED ARCHIVES

When using NSKeyedArchiver or NSKeyedUnarchiver, all the objects and values are given a key to identify them. These keys must be unique within the scope of the current object being saved or loaded. Therefore, if you are creating a public class that might be subclassed in the future, you should add a prefix to your keys to prevent collisions with any possible future subclasses. Additionally, you should avoid starting your keys with $, NS, or UI, since these are used by the system. Apple’s documentation recommends appending the full class name to the front of the key.

While the keys add a little complexity, they give us considerable flexibility when loading our data. We can load the data in any order and even selectively choose which data to load. This gives us better support for forward and backward compatibility should our data structure change, letting us easily add or remove keyed values from our archives.

Keyed archives are easy to use. You can store an object hierarchy into an NSData object by calling the NSKeyedArchiver's `archivedDataWithRootObject:` class method. You save it to disk by calling `archiveRootObject:toFile:` instead.

The system will take your root object and call its `encodeWithCoder:` method, passing in a properly formatted NSKeyedArchiver object. The keyed archive contains a number of methods that you can use to store raw C values (e.g., `encodeBool:forKey:`, `encodeInt:forKey:`, and `encodeFloat:forKey:`). It also includes a method for encoding other objects, unsurprisingly named `encodeObject:forKey:`. These children objects must also adopt the NSCoding protocol. The system then calls their `encodeWithCoder:` method, passing along the keyed archive, until the entire object hierarchy is saved.

Unarchiving works the same way. Simply call NSKeyedUnarchiver’s `unarchiveObjectWithData:` or `unarchiveObjectWithFile:` method. This will build the object hierarchy, calling `initWithCoder:` on each object, and then return the root object.

The archivers are smart enough to notice when your object graph has multiple references to the same object, and they will correctly save or load just one version of the object with all the references properly linking to that object. This means we can make our object graph as complex as we like. We don’t need to worry about loops or circular references.

However, for the sake of performance, we want to minimize the number of objects we save and load. Unless the operations are computationally intense, you should manually set, calculate, or create any values that you can, and save and load only those values that you absolutely must. If your object graph has multiple references to the same object, there is a good chance that you could save and load the object once, and assign all the other references manually.
