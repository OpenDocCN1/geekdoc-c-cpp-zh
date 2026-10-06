| Method | Description |
|---|---|
| +(id) dictionaryWithCapacity:size | Creates a mutable dictionary with an initial specified size |
| -(id) initWithCapacity:size | Initializes a newly allocated dictionary to be of an initial specified size |
| -(void) removeAllObjects | Removes all entries from the dictionary |
| -(void) removeObjectForKey:key | Removes the entry for the specified key from the dictionary |
| -(void) setObject:obj forKey:key | Adds obj to the dictionary for the key key and replaces the value if key already exists |

# ## Set Objects

A set is a collection of unique objects, and it can be mutable or immutable. Operations include searching, adding, and removing members (mutable sets); comparing two sets; and finding the intersection and union of two sets.

In this section we'll take a quick look at three set classes: NSSet, NSMutableSet, and NSIndexSet. We'll also mention the class NSCCountedSet in passing so you'll know when you might need or want to use that set.

Program 15.16 shows some basic operations on sets. Say you wanted to display the contents of your sets several times during execution of the program. You therefore have decided to create a new method called print. You add the print method to the NSSet class by creating a new category called Printing. NSMutableSet is a subclass of NSSet, so mutable sets can use the new print method as well.

# ## Program 15.16

```
#import <Foundation/Foundation.h>

// Create an integer object
```