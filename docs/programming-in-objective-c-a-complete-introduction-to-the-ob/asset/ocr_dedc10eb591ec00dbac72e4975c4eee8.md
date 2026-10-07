# Dictionary Objects 357

```
// Store three entries in the glossary

[glossary setObject: "@A class defined so other classes can inherit from it"
forkKey: "@abstract class"];
[glossary setObject: "@ implement all the methods defined in a protocol"
forkKey: "@adopt";
[glossary setObject: "@Storing an object for later use"
forkKey: "@Archiving"];

// Retrieve and display them

NSLog("%@abstract class: %@", [glossary objectForKeyKey: "@abstract class"]]);
NSLog("%@adopt: %@", [glossary objectForKeyKey: "@adopt"]]);
NSLog("%@archiving: %@", [glossary objectForKeyKey: "@archiving"]]);

[pool drain];
return 0;
```

# Program 15.14 Output

abstract class: A class defined so other classes can inherit from it
adopt: To implement all the methods defined in the protocol
archiving: Storing an object for later use

The expression

```
[NSMutableDictionary dictionary]
```

creates an empty mutable dictionary. You can add key-value pairs to the dictionary using
tset:forKey method. After the dictionary has been constructed, you can
retrieive the value for a given key using the objectForKey: Program 15.14
shows how the three entries in the glossary were retrieved and displayed. In a more prac-	ional, the user would use the type to define and the program would search
the glossary for its definition.

# Enumerating a Dictionary

Program 15.15 illustrates how a dictionary can be defined with initial key-value pairs
using the dictionaryWithObjectsAndKeys method. An immutable dictionary is cre-
tated, and the program also shows how a fast enumeration can be used to retrieve
each element from a dictionary one key at a time. Unlike array objects, dictionary objects
ar ordered, so the first-key pair placed in a dictionary might not be the first
key extracted when the dictionary is enumerated.

# Program 15.15

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[])
{
NSAutleasePool *pool = [[NSAutleasePool alloc] init];
```