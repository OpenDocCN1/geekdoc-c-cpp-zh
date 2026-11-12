
The stop value is only used as output from the block. Setting it to YES halts enumerateObjectsUsingBlock:. Here is a simple example using this method:

```objectivec
NSArray* array = [NSArray arrayWithObjects:@"Bill", @"Anne",
                                @"Jim", nil];
[array enumerateObjectsUsingBlock:
  ^(id obj, NSUInteger idx, BOOL *stop) {
    NSLog(@"Person %d: %@", idx, obj);
  }];
```

This returns the following output to the console:

```text
Person 0: Bill
Person 1: Anne
Person 2: Jim
```

Notice that we could duplicate the functionality of enumerateObjectsUsingBlock: by passing in a selector and having our enumeration method call the selector for each item in the array. We start by creating a category on NSArray.

```objectivec
@implementation NSArray (EnumerateWithSelector)
- (void)enumerateObjectsUsingTarget:(id)target
                            selector:(SEL)selector {
    for (int i = 0; i < [self count]; i++) {
        [target performSelector:selector
                     withObject:[self objectAtIndex:i]
                     withObject:[NSNumber numberWithInt:i]];
    }
}
```

Notice that we did not need to alter the implementation of enumerateObjectsUsingBlock: at all. We also didn't need any instance variables. Most importantly, everything is kept nicely in one place.

Best of all, the solution is scalable. If we want different behaviors somewhere else—no problem. We write a new block, capture all the local variables we need, and then call our generic enumeration method. A single generic method handles all our needs.

NOTE: Before ARC, we had to be a little careful with blocks. By default, blocks were built on the stack, and they were destroyed once they went out of scope. To store a block in an instance variable for later execution, we had to copy the block to the heap. Then we had to release it once we were done. Fortunately, ARC has simplified things yet again. We can create blocks, store them, use them, and even return them. We don't need to worry about whether they're on the heap or on the stack. ARC handles all the copying and memory management details for us.

![](img/fe9fea534a8e7868f811f7cd33da015f_127_0.png)

### WRAPPING UP

Whew. This chapter has covered a lot of ground. Don’t worry if you didn’t catch it all on the first pass. We will get a lot of practice using Objective-C in future chapters. And, unfortunately, this chapter really only scratches the surface. Many of these topics are quite deep. If you have any questions, be sure to check out Apple’s documentation. In particular, I recommend the following: The Objective-C Programming Language, Programming with ARC Release Notes, Key-Value Observing Programming Guide, and Block Programming Topics.

Next up, let’s start applying what we’ve learned and build a productivity application from scratch.

## 3 PRODUCTIVITY APPLICATION ARCHITECTURE

Throughout the rest of this book, we will focus on developing a single application. Chapter by chapter, we will cover every step required to build and test this application, from creating the initial project to prepping it for sale.

In this chapter, we will focus on our application's overall architecture. We will define the user's flow through the application, connecting our basic views and the transitions between them. We will also build our application's model and link it to our view controllers. Finally, we will touch on a number of smaller topics: enabling compiler warnings to produce cleaner code, implementing the methods that control vital aspects of our app, running our application on iOS devices, and even exploring the inner workings of nib files.

![](img/fe9fea534a8e7868f811f7cd33da015f_130_0.png)

### UNDERSTANDING PRODUCTIVITY APPS

The original iPhone Human Interface Guidelines (HIG) organized applications into three general categories: utility, productivity, and immersive applications. Utility applications provide a single view of the data with little or no interaction. Productivity applications manage and organize complex data. Immersive applications use custom views and controls, taking over the entire screen to provide a rich, interactive user experience.

Apple has since dropped these categories from the iOS HIG, and that makes a certain amount of sense. As the platform continues to mature, developers naturally push against these boundaries. Few modern applications fit cleanly into one of these categories. Even back when the iPhone first came out, many applications used a hybrid approach. Look at the iPod app. Its Cover Flow interface injects an immersive element into an otherwise straightforward productivity app.

However, there seems to be some benefit to at least thinking about these categories, especially when you are designing a new application. They can help you identify your application's core features and then focus your design to maximize those features.

We looked at a simple utility application in Chapter 1. Honestly, there's not a lot to say about them. Utility apps provide a quick way to access relatively simple information. One screen, a few settings—if you're thinking of anything more complicated than that, you should probably consider a different approach.

Over the next few chapters, we will look at productivity applications. These apps manage and organize complex data. While you may provide some custom user interfaces, you should focus heavily on usability. Work to create a clean, streamlined solution that helps the user to move through the data in an unobtrusive and intuitive manner.

Productivity applications typically use three tools to organize and interact with your data: UITabBarController, UINavigationController, and UITableView. You may not need all three, but these are the primary built-in tools for sifting through data.

The UITabBarController lets the user easily switch between different tasks or different groups of data. For example, the Clock application lets the user choose between the different time-related tasks: World Clock, Alarm, Stopwatch, and Timer. The iPod app, on the other hand, allows the user to select different views of their data: Albums, Artists, Genres, Songs, Playlists, Videos, and so on. The App Store mixes both approaches, displaying three data groups (Features, Categories, and Top 25) and two tasks (Search and Updates).

### WHAT DOES “PRODUCTIVITY” MEAN ANYWAY?

The name “productivity app” is somewhat misleading. While many of these applications do focus on traditional productivity-oriented tasks, like to-do lists and calendars, any application that emphasizes data and organization may benefit from the productivity style.

Mail is a perfect example of a traditional productivity app. It allows you to manage incoming and outgoing messages from a variety of email accounts. Many social networking applications also fall into this category—though you’d have trouble convincing me that Facebook improves productivity. Even the iPod app falls into this category, since its main task is organizing and accessing data.

The tab bar can support any number of tab items. However, it can only show five tabs at a time. UITabBarController automatically manages any extra tab items by providing a More button and letting the user customize the items that appear on the tab bar. Note that if you have more than five tabs, the tab bar will display only four of them, since the More button takes up one of the spaces.

Next, the UINavigationController lets users move from general to more specific views. This controller maintains a stack of views. When a new view is added to the top of the stack, that view slides in from the right while the old view slides off to the left. When the top view is popped from the top of the stack, the animation is reversed. This provides a very intuitive interface for moving through a hierarchy of views.

While both UITabBarController and UINavigationController manage navigation between views, UITableView handles the actual display of data. Tables are often used to present lists. For example, the list of email accounts, the list of mailboxes within a single account, or even the list of messages within a single mailbox. UITableView displays a single column of cells. Individually, each cell can be quite complex, combining images, icons, and formatted text. In general, a single cell type is used throughout the table. Each cell represents a different entry from a list of similar items.

However, UITableView has a secondary use as well. We can create a static table to organize a fixed set of heterogeneous pieces of data. In this case, the entire table is used to represent a single entry. Each row has its own unique formatting, displaying some aspect of this entry. As we change entries, the number and type of rows remain the same, only the data changes. We often use static tables to display detailed information about a selected leaf object in our data hierarchy.
