
As a concrete example, suppose an error is triggered because an empty stack is popped. In order to raise this event, theStack calls the following code (the actual implementation is slightly different because theStack is wrapped in a pimpl):

```
parent_..raise(Stack::StackError,
make_shared<StackEventData>(
StackEventData::ErrorConditions::Empty));
```

The first argument to the raise() function is a static string that resolves to"error". Recall that in order to handle multiple events, the publisher names each event. Here, theStack::StackError static variable holds the name of this event. A variable is used instead of directly using the string to prevent runtime errors being caused by mistyping the event name. The second argument to theraise() function creates the StackEventData instance and initializes it with the empty stack error condition. Note that the implementation passes event data using ashared_ptr. This decision is discussed below in the sidebar concerning sharing semantics. Although

theStackObserver class has not yet been introduced, I note for completeness that an event can be interpreted with code typified by the following:

```
StackObserver::notify(shared_ptr<EventData> d)
{
shared_ptr<StackEventData> p =
dynamic_pointer_cast<StackEventData>(d);
if(p) {

// do something with the data }
else
{

// uh oh, what event did we just catch?! }
}
```

## MODERN C++ DESIGN NOTE:
SHARING SEMANTICS AND
SHARED_PTR

Whereas unique_ptr enables the programmer to express, safely, unique ownership, shared_ptr enables the programmer to express, safely, shared ownership. prior to theC++11

standard, C++ enabled data sharing by either raw pointer or reference. Because references for class data could only be initialized during construction, for late binding data, only raw pointers could be used. therefore, often two classes shared a single piece of data by each containing a raw pointer to a common object. the problem with that scenario is, of course, that it is unclear which object owns the shared object. In particular, this ambiguity implies uncertainty about when such a shared object can safely be deleted and which owning object ultimately should free the memory.shared_ptrs rectify this dilemma at the standard library level. shared_ptr implements sharing semantics via reference counting. as new objects point to ashared_ptr, theinternal reference count increases (enforced via constructors and assignment). When ashared_ptr goes out of scope, its destructor is called, which decrements theinternal reference count. When thecount goes to zero, the destruction of the finalshared_ ptr triggers reclamation of the underlying memory. as withunique_ptr, explicit member function calls can also

thememory aftercompletion of event handling, the publisher cannot simply deallocate the memory after the event has been handled. Moreover, because multiple observers can be called for any given event, neither can the publisher transfer unique ownership of the data to any given observer. therefore, theshared_ptr standardized in C++11 offers the ideal semantics for handling this situation.

Now that you understand event data, let’s finally write the abstractObserver interface. It is, unsurprisingly, exactly what you might have been expecting. See Listing 3-5.

## Listing 3-5. The Abstract Observer Interface

```
class Observer
{
public :

explicit Observer(const string& name);
virtual ~Observer();
virtual void notify(shared_ptr<EventData>) = 0;
```

## The Stack as an Event Publisher

The final step in constructing the Stack is simply to put all of the pieces together. Listing 3-1 shows theStack as a singleton. In order to implement events, we simply modify this code to inherit from thePublisher base class. We now must ask ourselves, should this inheritance be public or private?

Typically, in object-oriented programming, one uses public inheritance to indicate the is-a relationship. That is, public inheritance expresses the relationship that a derived class is a type of or specialization of a base class. More precisely, the is-a relationship obeys the Liskov Substitutability Principle (LSP) [29], which states that (via polymorphism) a function that takes a base class pointer (reference) as an argument must be able to accept a derived class pointer (reference) without knowing it. Succinctly, a derived class must be usable wherever a base class can be used, interchangeably. When people refer to inheritance, they are generally referring to public inheritance.

Private inheritance is used to express the implements-a relationship. Private inheritance, simply, is used to embed the implementation of one class into the private implementation of another. It does not obey the LSP, and, in fact, the C++ language does not permit substitution of a derived class for a base class if the inheritance relationship is private. For completeness, the closely related protected inheritance is semantically the same as private inheritance. The only difference is that in private inheritance, the base class implementation becomes private in the derived class while in protected inheritance, the base class implementation becomes protected in the derived class.

Our question has now been refined to, is theStack aPublisher or does theStack implement aPublisher? The answer is yes and yes. That was unhelpful, so how do we choose?

In order to disambiguate whether we should use public or private inheritance in this instance, we must delve deeper into the usage

of theStack class. Public inheritance, or the is-a relationship, would indicate our intent to use the stack polymorphically as a publisher. However, this is not the case. While theStack class is a publisher, it is not a publisher in the context that it could be substituted for aPublisher in an LSP sense. Therefore, we should use private inheritance to indicate the intent to use the implementation of thePublisher within theStack. Equivalently, we can state that the Stack provides thePublisher service. If you’ve been following along with the repository source code, you might have noticed a big hint that private inheritance was the answer. ThePublisher class was implemented with a nonvirtual, protected destructor, making it unusable for public inheritance.

Readers familiar with object-oriented design may wonder why I didn’t ask the ubiquitous has-a question, which indicates ownership or the aggregation relationship. That is, why shouldn’t theStack simply own aPublisher and reuse its implementation instead of privately inheriting from it? Many designers

prefer almost exclusively to use aggregation in place of private inheritance, arguing that when given an equivalent choice between these two, one should always prefer the language feature leading to looser coupling (inheritance is a stronger relationship than aggregation). This opinion has merit. Personally, though, I simply prefer to accept the technique that trades off stronger coupling for greater clarity. I believe that private inheritance more clearly states the design intent of implementing the Publisher service than does aggregation. This decision has no right or wrong answer. In your code, you should prefer the style that suits your tastes.

An additional consequence of privately inheriting from the Publisher class is that theattach() anddetach() methods of thePublisher become private. However, they need to be part of the public interface for theStack if any other class intends to subscribe to theStack’s events. Thus, the implementer must choose to utilize either using statements or forwarding member functions to hoistattach() anddetach() into the

public interface of theStack. Either approach is acceptable in this context, and the implementer is free to use his or her personal preference.

## The Complete Stack Interface

We are finally ready to write the complete Stack public interface. See Listing 3-6.

**Listing 3-6.** The Complete Stack Public Interface

```
class Stack : private Publisher
{
public:

static Stack& Instance();

void push(double, bool suppressChangeEvent = false); double pop(bool suppressChangeEvent = false);
void swapTop();
vector<double> getElements(size_t n) const;

using Publisher::attach;
using Publisher::detach;
```
