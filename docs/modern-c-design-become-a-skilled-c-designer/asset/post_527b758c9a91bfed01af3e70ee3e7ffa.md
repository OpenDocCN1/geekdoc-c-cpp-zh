
The point of having an abstract interface for the UI is to enable the rest of the program to interact with the user interface without regard to whether the current interface is graphical, command line, or something else entirely. Ideally, we will be able to factor the abstract interface to the minimum number of functions required to use each concrete interface. Any functions sharing an implementation can be defined in the base class, while any functions requiring unique implementations based on the concrete type can be declared as virtual in the abstract base class and defined in the derived classes. The concept is fairly straightforward, but, as usual, the devil is in the details.

Consider the hierarchy depicted in Figure 5-1. Our goal is to design a minimal but complete interface, consistent with the Liskov Substitutability Principle, for pdCalc’s UserInterface class that will work for both the CLI and the GUI. As previously discussed, we already defined a high-level interface for this UI in Chapter 2. Let’s start from this predefined interface and refactor as necessary.

## Figure 5-1. A minimal interface hierarchy

Referring to Table 2-2 in Chapter 2, you see that the complete interface for the UserInterface class consists of two event handling functions, postMessage() and stackChanged(), and one UserInterface raised event, commandEntered(). Interestingly, the UserInterface class is a publisher, an observer, and an abstract user interface.

The two event handling functions, postMessage() and stackChanged(), are straightforward at the interface level. As we have done with previous observers, we will simply add these two functions to the public interface of the UserInterface class and create proxy observer classes to broker the communication by the publisher and the actual observer. These proxies are discussed in detail in Section 5.1.2.2 below. Concrete user interfaces must handle the implementations for event handling uniquely based on how the individual UI interacts with the user. Hence, postMessage() and stackChanged() must both be pure virtual. Because there is no need for the UserInterface class to interject during event handling, I chose, for simplicity, to forgo the NVI pattern. However, as was discussed in Chapter 4, one could instead use the NVI pattern with trivial forwarding nonvirtual interface functions.

The UserInterface class’s role as a publisher is slightly more complicated than its role as an observer. As you saw in Chapter 3 when designing the Stack class, the Stack implemented the publisher interface rather than substituted as a publisher. We therefore concluded that inheritance from the Publisher class should be private. For the UserInterface class, the relationship to the Publisher class is similar except the UserInterface class itself is not the publisher. The UserInterface class is an abstract interface for user interfaces in the system and is inheriting from the Publisher class only to enforce the notion that user interfaces must implement the publisher interface themselves. Both the CLI and the GUI classes will need to access public functions from Publisher (for example, to raise events). Thus, the protected mode of inheritance is appropriate in this instance.

Further recall from Chapter 3 that in order for the Stack class to implement the publisher interface, once we used private inheritance, we needed to hoist the Publisher class’s attach() and detach() functions into the Stack’s public interface. The same is true here using protected inheritance. The question, however, is should the hoisting occur in the UserInterface class or in its derived classes? To answer this question, we need to ask how particular user interfaces will be used by pdCalc. Clearly, either a CLI or a GUI “is-a” UserInterface. Therefore, concrete user interfaces will publicly inherit from UserInterface and be expected to obey the LSP. Attaching or detaching events to or from a particular user interface must therefore be able to be accomplished without knowing the underlying UI type. Thus, the attach() and detach() functions must be visible as part of UserInterface’s public interface.

Interestingly, in a rather unique implementation of the observer pattern, part of the publisher interface is implemented at the UserInterface level, while another part of the publisher interface is implemented at the derived class level.

Combining all of the above points, we can finally define the UserInterface class as shown in Listing 5-1.

## Listing 5-1. The UserInterface Class

```
class UserInterface : protected Publisher {
public:

UserInterface();
virtual ~UserInterface();
virtual void postMessage(const string& m) = 0; virtual void stackChanged() = 0;
using Publisher::attach;
using Publisher::detach;
static const string CommandEntered;
};
```

The CommandEntered string is the name of the command entered event. It is needed for attaching or detaching this event and can be given any name unique to events in the UserInterface class.

For completeness, I show the final user interface hierarchy in Figure 5-2. The class diagram illustrates the relationship between the CLI, the GUI, the abstract UserInterface class, and the publisher interface. Remember that the inheritance between the UserInterface class and the Publisher class is protected, so a UserInterface (or subsequent derived class) cannot be used as a Publisher. As previously stated, however, the intent for the inheritances between the concrete CLI and GUI classes and the abstract UserInterface class are public, allowing an instantiation of either concrete type to be substituted as a UserInterface.

Publisher
UserInterface
CLI GUI Figure 5-2. The user interface hierarchy

## 5.1.2 User Interface Events

Defining the UserInterface class does not complete the interface for the UI. Because the UserInterface class is an event publisher, we must also define the event data class that corresponds to the commandEntered() event. Additionally, defining the UserInterface class finally completes a publisher/observer pair, so we are finally ready to design and implement event proxy classes to broker events between the user interface and both the command dispatcher and the stack.

In Chapter 4, you saw that all commands are delivered to the command dispatcher via events. Specifically, the UI raises an event containing a specific command encoded as a string argument, the CommandDispatcher receives this event, and the string argument is passed to the CommandRepository, where a concrete command is retrieved for processing. As far as the command dispatcher is concerned, handling commandEntered() events is the same, irrespective of whether the encoded command string derives from the CLI or the GUI.

Likewise, when the Stack class raises a stackChanged() event, the Stack is indifferent to the particular UserInterface that handles this event. We are therefore motivated to treat the issuing of commandEntered() events and the handling of stackChanged() events uniformly at the UserInterface class level in the user interface hierarchy.

We begin by examining the common infrastructure for raising commandEntered() events. The commandEntered() event is registered for all user interfaces in the constructor of the UserInterface class. Therefore, any derived user interface class can simply raise this event by calling the raises() function defined by the Publisher interface, which, by protected inheritance, is part of any concrete UI’s implementation. The signature of the raises() function requires the name of the event and the event’s data. Because the event’s name is predefined in the UserInterface’s constructor, the only additional functionality required to raise a command entered event is a common CommandData class. Let’s now look at its design.

### 5.1.2.1 Command Data

In Chapter 3, we designed our event system to use push semantics for passing event data. Recall that push semantics simply means that the publisher creates an object containing the necessary information to handle an event and pushes that object to the observers when an event is raised. The event data object must publicly inherit from the abstract EventData class. Observers receive the event data through the abstract interface when the event is raised, and they retrieve the data by downcasting the event data to the appropriate derived class.

For command entered events, the event data is trivially a string containing either a number to be entered on the stack or the name of a command to be issued. The CommandData class simply needs to accept a string
