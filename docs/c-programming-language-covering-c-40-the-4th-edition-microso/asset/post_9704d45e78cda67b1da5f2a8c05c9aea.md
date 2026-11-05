
Click is used as a field within the Button class. As the example demonstrates, the field can be examined, modified, and used in delegate invocation expressions. The OnClick method in the Button class “raises” the Click event. The notion of raising an event is precisely equivalent to invoking the delegate represented by the event—thus there are no special language constructs for raising events. Note that the delegate invocation is preceded by a check that ensures the delegate is non-null.

Outside the declaration of the Button class, the Click member can be used only on the left-hand side of the += and -= operators, as in

```
    b.Click += new EventHandler(...);
```

which appends a delegate to the invocation list of the Click event, and

```
    b.Click -= new EventHandler(...);
```

which removes a delegate from the invocation list of the Click event.

When compiling a field-like event, the compiler automatically creates storage to hold the delegate, and creates accessors for the event that add or remove event handlers to the delegate field. The addition and removal operations are thread safe, and may (but are not required to) be done while holding the lock (§8.12) on the containing object for an instance event, or the type object (§7.6.10.6) for a static event.

Thus an instance event declaration of the form

```
    class X
    {
        public event D Ev;
    }
```

will be compiled to something equivalent to

```
    class X
    {
        private D __Ev;  // Field to hold the delegate
        public event D Ev {
            add {
                /* Add the delegate in a thread-safe way */
            }
            remove {
                /* Remove the delegate in a thread-safe way */
            }
        }
    }
```

Within the class X, references to Ev on the left-hand side of the += and -= operators cause the add and remove accessors to be invoked. All other references to Ev are compiled to reference the hidden field __Ev instead. The name "__Ev" is arbitrary; the hidden field could have any name or no name at all.

## 10.8.2 Event Accessors

Event declarations typically omit event-accessor-declarations, as in the Button example above. One situation for doing so involves the case in which the storage cost of one field per event is not acceptable. In such cases, a class can include event-accessor-declarations and use a private mechanism for storing the list of event handlers.

The event-accessor-declarations of an event specify the executable statements associated with adding and removing event handlers.

The accessor declarations consist of an add-accessor-declaration and a remove-accessor-declaration. Each accessor declaration consists of the token add or remove followed by a block. The block associated with an add-accessor-declaration specifies the statements to execute when an event handler is added, and the block associated with a remove-accessor-declaration specifies the statements to execute when an event handler is removed.

Each add-accessor-declaration and remove-accessor-declaration corresponds to a method with a single value parameter of the event type and a void return type. The implicit parameter of an event accessor is named value. When an event is used in an event assignment, the appropriate event accessor is used. Specifically, if the assignment operator is +=, then the add accessor is used; if the assignment operator is -=, then the remove accessor is used. In either case, the right-hand operand of the assignment operator is used as the argument to the event accessor. The block of an add-accessor-declaration or a remove-accessor-declaration must conform to the rules for void methods described in §10.6.10. In particular, return statements in such a block are not permitted to specify an expression.

Since an event accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declared in an event accessor to have that name.

In the example

```
class Control : Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}

    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}

    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}
    // MouseDown event
    public event MouseEventHandler MouseDown {
      add { AddEventHandler(mouseDownEventKey, value); }
      remove { RemoveEventHandler(mouseDownEventKey, value); }
    }
    // MouseUp event
    public event MouseEventHandler MouseUp {
      add { AddEventHandler(mouseUpEventKey, value); }
      remove { RemoveEventHandler(mouseUpEventKey, value); }
    }
    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
      MouseEventHandler handler;
      handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
      if (handler != null)
        handler(this, args);
    }
}
```

the Control class implements an internal storage mechanism for events. The AddEventHandler method associates a delegate value with a key, the GetEventHandler method returns the delegate currently associated with a key, and the RemoveEventHandler method removes a delegate as an event handler for the specified event. Presumably, the underlying storage mechanism is designed such that there is no cost for associating a null delegate value with a key, and thus unhandled events consume no storage.

## 10.8.3 Static and Instance Events

When an event declaration includes a static modifier, the event is said to be a static event. When no static modifier is present, the event is said to be an instance event.

A static event is not associated with a specific instance, and it is a compile-time error to refer to this in the accessors of a static event.

An instance event is associated with a given instance of a class, and this instance can be accessed as this (§7.6.7) in the accessors of that event.

When an event is referenced in a member-access (§7.6.4) of the form E.M, if M is a static event, E must denote a type containing M; if M is an instance event, E must denote an instance of a type containing M.

The differences between static and instance members are discussed further in §10.3.7.

## 10.8.4 Virtual, Sealed, Override, and Abstract Accessors

A virtual event declaration specifies that the accessors of that event are virtual. The virtual modifier applies to both accessors of an event.

An abstract event declaration specifies that the accessors of the event are virtual, but does not provide an actual implementation of the accessors. Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the event. Because an abstract event declaration provides no actual implementation, it cannot provide brace-delimited event-accessor-declarations.

An event declaration that includes both the abstract and override modifiers specifies that the event is abstract and overrides a base event. The accessors of such an event are also abstract.

Abstract event declarations are permitted only in abstract classes (§10.1.1.1).

The accessors of an inherited virtual event can be overridden in a derived class by including an event declaration that specifies an override modifier. This is known as an overriding event declaration. An overriding event declaration does not declare a new event. Instead, it simply specializes the implementations of the accessors of an existing virtual event.

An overriding event declaration must specify the exact same accessibility modifiers, type, and name as the overridden event.

An overriding event declaration may include the sealed modifier. Use of this modifier prevents a derived class from further overriding the event. The accessors of a sealed event are also sealed.

It is a compile-time error for an overriding event declaration to include a new modifier.

Except for differences in declaration and invocation syntax, virtual, sealed, override, and abstract accessors behave exactly like virtual, sealed, override, and abstract methods. Specifically, the rules described in §10.6.3, §10.6.4, §10.6.5, and §10.6.6 apply as if accessors were methods of a corresponding form. Each accessor corresponds to a method with a single value parameter of the event type, a void return type, and the same modifiers as the containing event.

## 10.9 Indexers

An indexer is a member that enables an object to be indexed in the same way as an array. Indexers are declared using indexer-declarations:
