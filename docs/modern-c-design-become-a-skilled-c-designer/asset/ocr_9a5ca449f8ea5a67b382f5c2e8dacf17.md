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

# MODERN C++ DESIGN NOTE:
SHARING SEMANTICS AND
SHARED_PTR

W hereas unique_ptr enables the programmer to express, safely, unique ownership, shared_ptr enables the programmer to express, safely, shared ownership. prior to theC++11