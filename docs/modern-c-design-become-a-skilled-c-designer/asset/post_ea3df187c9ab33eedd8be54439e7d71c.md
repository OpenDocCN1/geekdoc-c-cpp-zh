
![](img/7aac03e344e518d9d0db5131f6619db9_108_0.png)

Figure 3-1. A simplified version of the class diagram for the observer pattern as it is implemented for pdCalc. The diagram illustrates push semantics for event data.

## Enhancing the Observer Pattern Implementation

In the actual implementation for our calculator, several additional features have been added beyond the abstraction depicted in Figure 3-1. First, in the figure, each publisher owns a single list of observers that are all notified when an event occurs. However, this implementation implies either

that publishers have only one event or that publishers have multiple events, but no way of disambiguating which observers get called for each event. A better publisher implementation instead holds an associative array to lists of observers. In this manner, each publisher can have multiple distinct events, each of which only notifies observers interested in watching that particular event. While the key in the associative array can technically be any suitable data type that the designer chooses, I chose to use strings for the calculator. That is, the publisher distinguishes individual events by a name. This choice enhances readability and enables runtime flexibility to add events (versus, say, choosing enumeration values as keys).

Once the publisher class can contain multiple events, the programmer needs the ability to specify the event by name when attach() or detach() is called. These method signatures must therefore be modified appropriately from how they appear in Figure 3-1 to include an event name. For attachment, the method signature is completed by adding the

name of the event. The caller simply calls the attach() method with the concrete observer instance and the name of the event to which this observer is attaching. Detaching an observer from a publisher, however, requires slightly more sophisticated mechanics. Since each event within a publisher can contain multiple observers, the programmer requires the ability to differentiate observers for detachment. Naturally, this

requirement leads to naming observers, as well, and the detach() function signature must be modified to accommodate both the observer’s and event’s names.

In order to facilitate detaching observers, observers on each event should be stored indirectly and referenced by their names. Thus, rather than storing an associative array of lists of observers, we instead choose to use an associative array of associative arrays of observers.

In modern C++, the programmer has a choice of using either a map or an unordered_map

for a standard library implementation of an associative array. The canonical implementation of these two data structures are the red-black tree and the hash table, respectively. Since the ordering of the elements in the associative array is not important, I selected the unordered_map for pdCalc’s Publisher class. However, for the likely small number of observers subscribing to each event, either data structure would have been an equally valid choice.

To this point, we have not specified precisely how observers are stored in the publisher, only that they are somehow stored in associative arrays. Because observers are used polymorphically, language rules require them to be held by either pointer or reference. The question then becomes, should publishers own the observers or simply refer to observers owned by some other class? If we choose the reference route (by either reference or raw pointer), a class other than the publisher would be required to own the memory for the observers. This situation is problematic because it is not clear who

should own the observers in any particular instance. Therefore, every developer would probably choose a different option, and the maintenance of the observers over the long term would descend into chaos. Even worse, if the owner of an observer released the observer’s memory without also detaching the observer from the publisher, triggering the publisher’s event would cause a crash because the publisher would hold an invalid reference to the observer. For these reasons, I prefer having the publisher own the memory for its observers.

Having eschewed referencing, we must use owning semantics, and, because of the C++ mechanics of polymorphism, we must implement ownership via pointers. In modern C++, unique ownership of a pointer type is achieved via the unique_ptr (see the “Modern C++ Design Note” sidebar on owning semantics to understand the design implications). Putting all of the above advice together, we are able to design the final public interface for the Publisher class, as shown in Listing 3-3.

## Listing 3-3. The Final Public Interface for the Publisher Class
// Publisher.h
class Observer;
class Publisher
{
class PublisherImpl
public:
void attach(const string& eventName,
unique_ptr<Observer> observer);
unique_ptr<Observer> detach(const string&
eventName, const string& observerName);
//
...
private:
unique_ptr<PublisherImpl> publisherImpl_;
};
```

The implementation details of event storage become

```
// Publisher.cpp
class Publisher::PublisherImpl {

// ...
private :
using ObserversList =
unordered_map<string,
unique_ptr<Observer>>;
using Events = unordered_map<string,
ObserversList>;
Events events_;
};
```

The interface for the Observer class is quite a bit simpler than the interface for the Publisher class. However, because I have not yet described how to handle event data, we are not yet ready to design the Observer’s interface. I will address both event data and the Observer class’s interface in Section 3.3.1.2 below.

## MODERN C++ DESIGN NOTE:
OWNING SEMANTICS AND
UNIQUE_PTR

In C++, the notion of owning an object implies the responsibility for deleting its memory when the object is no longer required. prior to C++11, although anyone could implement his own smart pointer (and many did), the language itself expressed no standard semantics for pointer ownership

(excepting auto_ptr, which has since been deprecated). passing memory by native pointers was more of a trust issue. that is, if you "newed" a pointer and passed it via raw pointer to a library, you hoped the library deleted the memory when it was finished with it. alternatively, the documentation for the library might inform you to delete the memory after certain operations were performed. Without a standard smart pointer, in the worst case scenario, your program leaked memory. In the best case scenario, you had to interface to a library using a nonstandard smart pointer.

C++11 corrected the problem of unknown pointer ownership by standardizing a set of smart pointers largely borrowed from the boost libraries. the unique_ptr finally allows programmers to implement unique ownership correctly (hence the deprecation of auto_ptr). essentially, the unique_ptr ensures that only one instance of a pointer exists at any one time. For the language to enforce these rules, copy and non-moving assignment for unique_ptrs are not implemented. Instead,

move semantics are employed to ensure transfer of ownership (explicit function calls can also be used to manage the memory manually). Josuttis [8] provides an excellent detailed description of the mechanics of using the unique_ptr. an important point to remember is not to mix pointer types between unique_ptrs and raw pointers.

From a design perspective, the unique_ptr implies that we can write interfaces, using standard C++, that unambiguously express unique ownership semantics. as was seen in the discussion of the observer pattern, unique ownership semantics are important in any design where one class creates memory to be owned by another class. For example, in the calculator’s eventing system, while the publisher of an event should own its observers, a publisher will rarely have enough information to create its observers. It is therefore important to be able to create the memory for the observers in one location but be able to pass ownership of that memory to another location, the publisher. the unique_ptr provides that service. Because
