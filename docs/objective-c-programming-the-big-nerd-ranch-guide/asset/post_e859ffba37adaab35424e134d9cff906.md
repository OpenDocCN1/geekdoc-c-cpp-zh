
## 16
## Developer Documentation

In the last chapter, I gave you some useful tidbits about the class NSArray. When you begin programming without my guidance (including taking on Challenges in this book), you will need to find such tidbits yourself. This is where Apple's documentation comes in.

To see the documentation in Xcode, bring up the Organizer (click the [icon] button at the top right of the Xcode window) and choose the Documentation tab.

![](img/5f9368899ebf8d92fc145f8def1e89f8_103_0.png)

There are essentially five types of documentation that Apple provides:

- *References:* Every Objective-C class and every C function is tersely documented in these pages.
- *Guides and Getting Started:* Guides are less terse and group ideas conceptually. For example, there is an *Error Handling Programming Guide* that describes the myriad of ways that Mac and iOS developers can be informed that something has gone wrong.
- *Sample Code:* These are small, complete projects that demonstrate how Apple expects its technology to be used. For example, there is a WeatherMap project that shows how to make custom annotations on iOS map views.
- *Release Notes:* Every time a new version of Mac OS or iOS comes out, it is accompanied by a set of release notes. The release notes tell developers what has changed since the last version.
- *Technical notes, Articles, Coding How-to’s, and Technical Q&A’s:* These are bite-sized documents that address specific issues.

You can browse the documentation, but there is a lot of it. More commonly, you will access the documentation via search.

### Reference pages

At the top of the lefthand pane in Organizer, click the 🚀 button to bring up the search panel. Type NSArray into the search field, and the search results will appear below the search field. In the Reference section, click on NSArray to see the *reference page* for *NSArray*.

#### Figure 16.2 NSArray reference page

![](img/5f9368899ebf8d92fc145f8def1e89f8_104_0.png)

It would be difficult to overstate how important these reference pages will be to you and how important they are for programmers of all levels. Apple has worked really hard to create huge libraries of code for your convenience. You will learn about these libraries primarily through reference pages. As you go through this book, take a moment to look up the reference pages for new classes as you use them and see what else they can do. You can also search for methods, functions, constants, and properties by name. (You’ll learn about properties in Chapter 17.) The more comfortable you get using these pages, the faster your development will go.

At the top of the class reference for **NSArray**, you can learn several things about the class. It inherits from **NSObject**. (More about this soon in Chapter 18.) It conforms to several protocols (which we’ll discuss in Chapter 25). It is part of the Foundation framework and has shipped with every version of Mac OS X and every version of iOS.

At the end of the header, there is a list of guides that discuss **NSArray** and sample code that shows off the capabilities of **NSArray**. Click on *Collections Programming Topics* to open that guide.

#### Figure 16.3 Collections Programming Topics

![](img/5f9368899ebf8d92fc145f8def1e89f8_105_0.png)

This particular guide discusses the collection classes (including **NSArray** and **NSMutableArray**). Unlike the class reference, a guide is a pleasant read, in which ideas are introduced in a sensible order.

Now use the back button at the top of the document pane to go back to the **NSArray** reference page. Curious about what other messages you can send to an **NSArray**? Scroll down the reference page and find the list of methods that **NSArray** implements. Say you’re looking for a way to check if an array contains a particular item. In that case, you’d run across the **containsObject:** method and read its description:

#### Figure 16.4 Reference for containsObject:

```objectivec
containsObject:

Returns a Boolean value that indicates whether a given object is present in the array.
   - (BOOL)containsObject:(id)anObject
Parameters
anObject
An object.
Return Value
YES if anObject is present in the array, otherwise NO.
Discussion
This method determines whether anObject is present in the array by sending an isEqual: message to each of the array's objects (and passing anObject as the parameter to each isEqual: message).
Availability
Available in Mac OS X v10.0 and later.
See Also
   - indexOfObject:
   - indexOfObjectIdenticalTo:
Related Sample Code
Sketch+Accessibility
TimelineToTC
Declared In
NSArray.h
```

Now you know everything you need to know to send this message in your code.

### Quick Help

But there's an easier way to get from the editor where you're writing code to the wellspring of knowledge in the documentation. Close the Organizer and return to your DateList project.

In main.m, find the line that includes [dateList addObject:now]. Hold down the Option key and click on addObject:. The Quick Help window will appear with the information about that method:

#### Figure 16.5 Quick Help window

![](img/5f9368899ebf8d92fc145f8def1e89f8_107_0.png)

Notice that there are links in the Quick Help window. If you click a link, it will open the appropriate documentation in the Organizer. Handy, right?

If you want to see that Quick Help all the time, you can open it as a pane in Xcode.

In the upper-right corner of the Xcode window, find a segmented control called View that looks like **1 2 3** and indicates Xcode’s lefthand, bottom, and righthand panes. Selecting and de-selecting these buttons will hide and show the respective panes.

The lefthand pane, which you’ve used plenty by now, is called the navigator. The bottom pane, which you’ve also seen, includes the console and is called the debug area. The righthand pane is called Utilities. Click the righthand View button to reveal Utilities. At the top of Utilities, click the **?** button to reveal the Quick Help pane.

This pane will show help for the text selected in the editor. Try it: just select the word “NSMutableArray” in the editor:

#### Figure 16.6 Quick Help pane

![](img/5f9368899ebf8d92fc145f8def1e89f8_108_0.png)

Note that when you select something else, the Quick Help pane will immediately update to show the documentation for the new selection.

### Other options and resources

If you Option-double-click on any text, the Organizer will search for that string.

If you Command-click on any class, function, or method, Xcode will show you the file where it is declared. (Try Command-clicking the word “NSMutableArray”.)

#### Figure 16.7 The declaration of NSMutableArray

![](img/5f9368899ebf8d92fc145f8def1e89f8_108_1.png)

If there are several declarations that match, you’ll get a pop-up when you Command-click. Try Command-clicking **addObject:**.

From time to time, Xcode will call back to the mothership to see if there is any updated documentation. It will download the updates and re-index them for easy searching. You can trigger an immediate check for updates in the preferences panel for Xcode.

Apple hosts a collection of discussion mailing lists at http://lists.apple.com/, and several of them are devoted to developer topics. If you can’t find an answer in the docs, try searching the archives of the lists. (As a courtesy to the thousands of people on each list, please search the archives carefully before posting a question.)

There is one more resource that you should know about: stackoverflow.com. This website is a very popular place where programmers ask and answer questions. If you can think up a few keywords that describe the sort of problem you are having, you can probably find an answer there.

## 17
## Your First Class

So far, you have only used classes created by Apple. Now you get to write your own class. Remember that a class describes objects in two ways:

- methods (both instance methods and class methods) implemented by the class
- instance variables within each instance of the class

You're going to write a **Person** class, similar to the `struct Person` you wrote in Chapter 10. Your class will be defined in two files: `Person.h` and `Person.m`. `Person.h`, known as the *header* or *interface file*, will contain the declarations of instance variables and methods. `Person.m` is known as the *implementation file*. This is where you write out the steps for, or *implement*, each method.

Create a new project: a Foundation Command Line Tool named **BMITime**.

To create a new class, select **File → New → New File....** From the Mac OS X section on the left, select **Cocoa** and choose the **Objective-C class template**. Name your class **Person** and make it a subclass of **NSObject**. Finally, make sure the **BMITime** target is checked and click **Save**.

Notice that the new class files, `Person.h` and `Person.m`, now appear in the project navigator. Open `Person.h`. Declare two instance variables and three instance methods:

```objectivec
#import <Foundation/Foundation.h>
// The class Person inherits all the instance variables
// and methods defined by the class NSObject
@interface Person : NSObject
{
    // It has two instance variables
    float heightInMeters;
    int weightInKilos;
}
// You will be able to set those instance variables using these methods
- (void)setHeightInMeters:(float)h;
- (void)setWeightInKilos:(int)w;
// This method calculates the Body Mass Index
- (float)bodyMassIndex;
@end
```

Notice that you declared the instance variables inside of curly braces and you declared the methods after the variables and outside of the curly braces.
