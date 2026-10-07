
# CHAPTER 11: Storing Information

![](img/322e107ddf8f5cd963a6efafdcd86f38_265_0.png)

Figure 11–16. Binding the columns.

You should be done. Click on Run and you should be able to see your new application window. Click on Add and it should add a row to the Table View. Click in the Column cell and you can edit the Title and the Price. You will notice that when you quit and relaunch your application, it will remember the values you stored in there before.

This is a very cursory introduction to Core Data for Mac OS X and IOS. Core Data is a very powerful API and can take a lot of time to master.

# Summary

We've finally reached the end of the chapter. Here is a summary of the things that we have covered.

- Preferences
  - You learned to use NSUserDefaults to save and read preferences from a file, both on the iPhone and a Mac OS X computer.
- Database
  - You learned what a database is and why using one can be preferable to saving information in a preferences file.
  - You learned about the database engine that Apple has integrated into the Mac and iPhone, and the advantages and limitations of this database engine.
- Core Data
  - Apple provided a framework for interfacing with the SQLite database. This framework makes the interface much easier to use.
- Book Store Application
  - You created a simple Core Data application.
  - You used Xcode to create a data model for your Book Store application. You learned how to create a relationship between two different Entities.
  - You used Xcode to create a simple interface for your Core Data model.

# Exercises

- Add more fields to the Book entity. Try adding the publisher, pages, and an ISBN number.
- Change the layout of the Book tab. Reorder the columns.
- Add a default value to the author's first and last names.

# Protocols and Delegates

Congratulations! You are acquiring the skills to become an iOS developer! However, there are two additional topics that iOS developers need to understand to be successful: protocols and delegates. It is not uncommon for new developers to get overwhelmed by these topics, so we thought it best to introduce the foundation topics of the Objective-C language first.

## Multiple Inheritance

We discussed object inheritance in Chapter 1. In a nutshell, object inheritance means a child can inherit all the characteristics of its parent. See Figure 12–1.

![](img/322e107ddf8f5cd963a6efafdcd86f38_267_0.png)

Figure 12–1. Typical Objective-C inheritance

C++, Perl, and Python each have a feature called multiple inheritance. **Multiple inheritance enables a class to inherit behaviors and features from more than one parent.** See Figure 12–2.

However, problems can arise with multiple inheritance because it allows for ambiguities to occur. Due to this, Objective-C does not implement multiple inheritances. Instead, it implements something called a **protocol**.

![](img/322e107ddf8f5cd963a6efafdcd86f38_268_0.png)

Figure 12–2. Multiple inheritance

# Understanding Protocols

Apple defines a protocol simply as a list of methods declarations, unattached to a class definition, with the exception that it is not defining a particular class. A protocol is very similar to a class interface but you must implement the methods listed for Protocols. For example, the methods that report user actions for the mouse could be placed into a protocol. See the following example:

```
- (void)mouseDown:(NSEvent *)event;
- (void)mouseDragged:(NSEvent *)event;
- (void)mouseUp:(NSEvent *)event;
```

Any class that wants to respond to mouse events could adopt the protocol and implement its methods. Protocols are very easy to use since they are not related to class hierarchy and any class can implement them.

Throughout the book, we have used the example of a bookstore. Previously, we discussed the fact that our bookstore may sell different types of media and have discussed how inheritance would help out in that situation. For the purpose of explaining protocols, let’s say that our bookstore also sells gum and candy. We would want to create a class for those items. Call it EdibleItem. It would not make sense to have gum inherit the same methods as a book or magazine, but all of the items would need to be sold and the inventory would need to be tracked. In this case, it would make sense to add the methods to a protocol that could be shared by each of the items.

> NOTE: A protocol is much different than inheritance. When a class inherits from another class, it not only receives the method declarations, but it also receives the methods themselves. When using a protocol, the declarations are brought over, but the methods themselves need to be written.

# Protocol Syntax

The interface example for a protocol is

```
@protocol InventoryItem;
- (void)removeFromInventory;
- (void)addToInventory;
@end
```

The implementation file for this protocol example would be

```
@interface MyClass : SomeSuperClass < InventoryItem>
@end
```

Any object that wants to implement the InventoryItem protocol would include < InventoryItem> after the object definition.

For example, we could create the interface for the edible objects we sell.

```
@interface Edible : NSObject <InventoryItem>
{
}
```

It is not uncommon for iOS developers to have multiple protocols for their objects. Additional protocols are placed after the first followed by a comma,

```
@interface EditTextItem : UITableView <InventoryItem,SaleItem>
{
}
```

This example illustrates the power of delegates. EditableItem now has all of the method declarations from InventoryItem and SaleItem.

Methods that are defined for the object's delegate are called delegates methods.

# Understanding Delegates

Delegates are helper objects. They enable us to control the behavior of our objects. The methods listed in the protocol become **helpers** to MyClass.

> NOTE: The key to understanding delegates is to know that a delegate is a separate object consulted in order to augment the behavior of a host object. Then, can create an application delegate that can affect the behavior of the iOS UIApplication object without subclassing or changing the UIApplication class. The object you create is the delegate object, and the messages that UIApplication will send your object are called delegate methods. These are typically defined in a protocol (<UIApplicationDelegate>) which your class must adopt. To work, a delegate object must be set as the delegate property of the host.

We now use these methods in our object. For example, including the <CLLocationDelegate> protocol in our class must adopt. The following example shows the method we will use and include inside our object:

**Listing 12-1.** *Delegate example*

```objective-c
@implementation MyLocationController
@synthesize locationManager;

- (id)init {
    self = [super init];
    if (self != nil) {
        self.locationManager = [[CLLocationManager alloc] init];
        self.locationManager.delegate = self;
    }
    return self;
}

-(void)locationManager:(CLLocationManager *)manager
    didUpdateLocation:(CLLocation *)newLocation
    fromLocation:(CLLocation *)oldLocation
{
    NSLog("Location: %@", [newLocation description]);
}

(void)locationManager:(CLLocationManager *)manager didFailWithError:(NSError *)error
{
    NSLog("Error: %@", [error description]);
}

(void)dealloc {
    self.locationManager release;
    [super dealloc]
}
@end
```
