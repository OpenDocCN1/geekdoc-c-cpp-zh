
# 25 Protocols

NSURL *url = [NSURL URLWithString:
 @"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
NSURLRequest *request = [NSURLRequest requestWithURL:url];

__unused NSURLConnection *fetchConn = [[NSURLConnection alloc] initWithRequest:request
 delegate:logger
 startImmediately:YES];

__unused NSTimer *timer
 = [NSTimer scheduledTimerWithTimeInterval:2.0
 target:logger
 selector:@selector(sayOuch:)
 userInfo:nil
 repeats:YES];

[[NSRunLoop currentRunLoop] run];
}
return 0;
}

Now implement the method that will get called in Logger.m:

- (void)zoneChange:(NSNotification *)note
{
 NSLog(@"The system time zone has changed!");
}

Build and run the program. While it is running, open **System Preferences** and change the time zone for your system. You should see that your **zoneChange:** method gets called. (On some systems, it seems to get called twice. This is not cause for concern.)

## Which to use?

In this chapter, you have seen three kinds of callbacks. How does Apple decide which one to use in any particular situation?

- Objects that do just one thing (like **NSTimer**) use target-action.
- Objects that have more complicated lives (like an **NSURLConnection**) use helper objects, and the most common type of helper object is the delegate.
- Objects that might need to trigger callbacks in several other objects (like **NSTimeZone**) use notifications.

## Callbacks and object ownership

With all of these callbacks, there is a danger that objects waiting for the callbacks might not get deallocated correctly. Thus, it was decided that:

- **Notification centers do not own their observers.** If an object is an observer, it will typically remove itself from the notification center in its **dealloc** method:

```objective-c
- (void) dealloc
{
    [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```

- **Objects do not own their delegates or data sources.** If you create an object that is a delegate or data source, your object should “excuse” itself in its **dealloc** method:

```objective-c
- (void) dealloc
{
    [windowThatBossesMeAround setDelegate:nil];
    [tableViewThatBegsForData setDataSource:nil];
}
```

- **Objects do not own their targets.** If you create an object that is a target, your object should zero the target pointer in its **dealloc** method:

```objective-c
- (void) dealloc
{
    [buttonThatKeepsSendingMeMessages setTarget:nil];
}
```

None of these issues exist in this program because your **Logger** object will not be deallocated before the program terminates. (Also, in a bit of a fluke, in this exercise I used two well-documented exceptions to the rules: an **NSURLConnection** owns its delegate and an **NSTimer** owns its target.)

At this point, I need to talk about a slightly abstract concept. Someone once said, “It is important to remember that who you are is different from what you do.” The same is true of objects: the class of an object is different from its *role* in a working system. For example, an object may be an instance of `NSMutableArray`, but its role in an application may be as a queue of print jobs to be run.

Like the array-as-print-queue example, really great classes are more general than the role they may play in any particular application. Thus, instances of that class can be used in several different ways.

We’ve talked about how to specify a class. Is it possible to specify a role? To some degree, we can specify a role using the `@protocol` construct.

For example, in an iOS application, you frequently display data in an instance of the class `UITableView`. However, the `UITableView` object does not contain the data it displays; it has to get data from another source. You have to tell it “Here is the object that will fulfill the role of your data source.”

Figure 25.1 UITableView datasource

![](img/5f9368899ebf8d92fc145f8def1e89f8_177_0.png)

How did the developer who created the `UITableView` class specify the role of `UITableView`’s data source? He created a *protocol*. A protocol is a list of method declarations. Some methods are required, and some are optional. If your object is to fulfill the role, it must implement the required methods and may choose to implement the optional methods.

The data source protocol for `UITableView` is named `UITableViewDataSource`, and here it is (comments are mine):

```objective-c
// Just like classes, protocols can inherit from other protocols.
// This protocol inherits from the NSObject protocol
@protocol UITableViewDataSource <NSObject>

// The following methods must be implemented by any table view data source
@required

// A table view has sections, each section can have several rows
- (NSInteger)tableView:(UITableView *)tv numberOfRowsInSection:(NSInteger)section;

// This index path is two integers (a section and a row)
// The table view cell is what the user sees in that section/row
- (UITableViewCell *)tableView:(UITableView *)tv
    cellForRowAtIndexPath:(NSIndexPath *)ip;

// These methods may (or may not) be implemented by a table view data source
@optional

// If data source doesn't implement this method, table view has only one section
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tv;

// Rows can be deleted and moved
- (BOOL)tableView:(UITableView *)tv canEditRowAtIndexPath:(NSIndexPath *)ip;
- (BOOL)tableView:(UITableView *)tv canMoveRowAtIndexPath:(NSIndexPath *)ip;
- (void)tableView:(UITableView *)tv
    commitEditingStyle:(UITableViewCellEditingStyle)editingStyle
    forRowAtIndexPath:(NSIndexPath *)ip;
- (void)tableView:(UITableView *)tv
    moveRowAtIndexPath:(NSIndexPath *)sourceIndexPath
    toIndexPath:(NSIndexPath *)destinationIndexPath;
// To save ink and paper, I'm leaving out a few optional method declarations.
@end
```

(Like classes, protocols have reference pages in Apple's developer documentation, which you can search for and browse to see the methods a protocol contains.)

When you create a class to fulfill the role of UITableView's data source, you explicitly say, "This class conforms to the UITableViewDataSource protocol" in the header file. It looks like this:

```objective-c
@interface TerrificViewController : UIViewController <UITableViewDataSource>
...
@end
```

That is, "TerrificViewController is a subclass of UIViewController and conforms to the UITableViewDataSource protocol."

If your class conforms to several protocols, list them within the angle brackets:

```objective-c
@interface TerrificViewController : UIViewController <UITableViewDataSource, UITableViewDelegate, UITextFieldDelegate>
```

Then, in the TerrificController.m file, you need to implement the required methods in each protocol. If you forget to implement one of the required methods, you will get a stern warning from the compiler.

You will also browse through the optional methods and pick out the ones that you wish to implement. If you implement them, they will be called automatically at the appropriate time.

Final note: In the **Callbacks** program in Chapter 24, you made an instance of **Logger** the delegate of an **NSURLConnection** object. But you didn’t declare in `Logger.h` that **Logger** conforms to a protocol. As this is being written, there is no formal protocol for **NSURLConnection** delegates. I would not be surprised if this changes. (If when building **Callbacks** you received a warning along the lines of “This object doesn’t conform to the **NSURLConnectionDelegate** protocol,” this change has occurred.)

## Property Lists

Sometimes you need a file format that can be read by both computers and people. For example, let’s say that you want to keep a description of your stock portfolio in a file. As you add new stocks, it would be nice to be able to edit that file easily by hand. But, it might also be handy for one of your programs to be able to read it. When facing this problem, most Objective-C programmers use a *property list*.

A property list is a combination of any of the following things:

- NSArray
- NSMutableDictionary
- NSString
- NSData
- NSDate
- NSNumber (integer, float or Boolean)

For example, an array of dictionaries with string keys and date objects is a property list (or just a "P-list").

Reading and writing a property list to a file is really easy. In Xcode, create a new project: a Foundation Command Line Tool named stockz and add the following code:

```objective-c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[])
{
    @autoreleasepool {

        NSMutableArray *stocks = [[NSMutableArray alloc] init];
        NSMutableDictionary *stock;

        stock = [NSMutableDictionary dictionary];
        [stock setObject:@"AAPL"
                 forKey:@"symbol"];
        [stock setObject:[NSNumber numberWithInt:200]
                 forKey:@"shares"];
        [stocks addObject:stock];
```
