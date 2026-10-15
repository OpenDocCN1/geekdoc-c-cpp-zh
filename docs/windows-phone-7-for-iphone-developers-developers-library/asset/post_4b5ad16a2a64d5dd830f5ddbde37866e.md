
We can accomplish this custom extension to the Combatant class using the code in Listing 3.19.

## Listing 3.19 CombatantSquareDancingExtension.cs

```
using System;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Ink;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;

namespace Chapter3
{
    public static class CombatantSquareDancingExtension
    {
        public static void SquareDance(this Combatant dancer)
        {
            Point origin = dancer.Location;
            Point step1 = new Point(origin.X, origin.Y - 1); // move forward
            Point step2 = new Point(step1.X - 1, step1.Y); // move left
            Point step3 = new Point(step2.X, step2.Y + 1); // move back
            Point step4 = new Point(step3.X + 1, step3.Y); // move right
        }
    }
}
```

Although there are no hard and fast rules about naming conventions used for building extension classes, I like to follow a simple naming scheme: [OriginalClass][ExtensionDescription]Extension. The presence of the suffix Extension immediately tells me and any other developer looking at this class that it is not a complete class on its own; rather, it provides additional functionality to some other class. The class being extended is the first section of the name of the extension class. So in our example, a class that extends the Combatant class by providing square dancing capabilities would be called CombatantSquareDancingExtension.

If the code in Listing 3.19 is in scope, it should be perfectly legal (and possibly amusing) to invoke the SquareDance method of any object that is (directly or through inheritance) of type Combatant.

## Summary

In this chapter, you were given a brief overview of some of the core concepts of object-oriented programming (OOP) and how they apply to the tasks of building iOS and Windows Phone 7 applications using Objective-C and C#, respectively.

Those of you who have been programming for a long time might have found some of these concepts remedial, but the key here was to introduce you to the syntax required for day-to-day programming in an object-oriented programming language such as C#. As you progress through the rest of the book, we will be using things like encapsulation, inheritance, properties, methods, interfaces, and extensions extensively, and if you don't have a firm grasp on those concepts now, the rest of the book will be very difficult to read.

If you have read through this chapter and feel as though you now have a decent understanding of how to write OOP code in C#, you are well prepared to dive deeper into the world of building Windows Phone 7 applications and continue with the rest of the book.

This page intentionally left blank

## Event-Driven Programming

> Transmitted at the speed of light, all events on this planet are simultaneous. In the electric environment of information all events are simultaneous, there is no time or space separating events.
> 
> Marshall McLuhan

This chapter provides an overview of an often underrated aspect of modern programming frameworks: events. In many cases when comparing Objective-C to C#, there are subtle linguistic differences while the core concepts remain the same.

This chapter gives you an overview of what true event-driven programming is, how such programming is accomplished in Objective-C, and finally, how this same type of programming can be accomplished in C# within the context of a Windows Phone 7 application.

## What Is Event-Driven Programming?

The subject of event-driven programming is an area in which Objective-C and C# differ greatly and at a core, fundamental level. An event isn’t just a single thing. When an event of some importance occurs, you have three pieces of information that are typically required to take appropriate action in response to that event:

- The object sending the event—This object knows someone is interested in the event that has occurred and is responsible for dispatching that event to all subscribers.
- The event itself—The sender needs to tell the receivers exactly what happened and provide sufficient context.
- The event subscriber or receiver—As far as C# is concerned, if a tree falls in the woods and there are no event subscribers to be told about it, nothing happened. When an event occurs, those objects interested in that event are told and are given the previous two pieces of information: the event sender and the context information about the event itself.

As you read through this chapter, you will see how Objective-C’s “delegate pattern” is used and how that relates to the publish-and-subscribe event-driven model espoused by the .NET Framework.

Another common misconception among both newbies and veterans in the C# world is that events are applicable only to the user interface. For example, most programmers can tell you that events are generated when you tap a button with your finger or when you submit text to an input control. However, far too many programmers don’t know that events can be both useful and powerful when used throughout all levels of your application, not just the UI. You will see extremely powerful examples of how essential event-driven programming is for WP7 when we get to a discussion on asynchronous programming and communication with external services.

## Using the Delegate Pattern in Objective-C

Objective-C doesn’t use events the same way that C# does, and this is often a source of confusion when programmers are trying to relate their skills from iPhone development to the .NET Framework or WP7 development.

In iOS (and virtually all other Mac-based development using Objective-C) something called the delegate pattern is utilized almost exclusively for event-driven programming. This pattern works as follows:

If a class needs to inform another class about something, or obtain information from another class, a reference to that object is stored as a delegate. This delegate isn’t like a C# delegate (which is roughly analogous to a C function pointer). Instead, this delegate is more like the dictionary definition of the word: the class is delegating functionality to another class.

For example, one of the most common control types in iOS programming is the UITableView. This control displays data arranged in vertical rows. The individual cells in these rows can be highly customized, but no matter how customized the control might be, it still performs certain core functionality the same way.

Rather than having some other class push data into the table view, the table view asks for data. This allows the table view to maintain its own optimization so that it asks only for the data it knows is going to be rendered on the screen (or will be rendered very soon). In addition to delegating the data source to another class, the UITableView also delegates the methods that respond to user events to another class, such as when a row is selected, when the view state changes into edit mode, and so on. There are even methods delegated to other classes for telling the table view how many groups there are, the style that should be used for the groupings, and for providing a custom cell to the view for each row being rendered.

For those familiar with .NET programming, this pattern might seem entirely backward. .NET programmers, especially those used to Windows Forms or ASP.NET programming, are used to gathering the data themselves and then stuffing the data into a control through some kind of data-binding mechanism. The concept of the controller being a passive participant that is invoked only when the UI control needs it often seems very strange indeed.

However strange it might seem to C# developers, this pattern is incredibly powerful and works amazingly well for iOS. Each type of delegate is required to expose a certain set of methods (some of which are optional, a very important point) so that the class utilizing the delegate can be assured that all delegated functionality is provided.

The agreement between a delegate and the class doing the delegation is very often defined explicitly in the form of a protocol. For example, the UITableViewController class is a handy controller that comes pre-equipped to conform to the two different protocols required by the UITableView control: UITableViewDelegate (the protocol that deals with handling events that occur within the control) and UITableViewDataSource (the protocol that defines how a delegate must provide rows, cells, groups, and other data for the table view).

Table 4.1 shows just a few of the methods that are part of the two delegate protocols that define the communication between the UITableView control and your application. As you will see later in this chapter, this pattern is very different from the way Silverlight controls communicate with your application in Windows Phone 7 applications.

## Table 4.1 Some Delegate Methods for iOS Table View Controllers

| Protocol | Method | Description |
|---|---|---|
| UITableViewDelegate | tableView:willSelectRowAtIndexPath: | Used to perform actions before selecting a row |
| UITableViewDelegate | tableView:didSelectRowAtIndexPath: | Invoked after a row has been selected by the user |
| UITableViewDataSource | tableView:cellForRowAtIndexPath: | Returns a configured cell to be rendered by the table view in the appropriate place |
| UITableViewDataSource | numberOfSectionsInTableView: | Returns the number of section groups in the view |
| UITableViewDataSource | tableView:numberOfRowsInSection: | Returns the number of rows in a given section |
