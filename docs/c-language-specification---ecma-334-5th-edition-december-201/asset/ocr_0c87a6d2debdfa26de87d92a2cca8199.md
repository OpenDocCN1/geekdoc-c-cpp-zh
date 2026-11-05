($10.4.4.19) on the containing object for an instance event, or the type object (§12.7.11.7) for a static event.

[Note: Thus, an instance event declaration of the form:

```
class X
{
    public event D Ev;
}
```

shall be compiled to something equivalent to:

```
class X
{
    private D __Ev; // field to hold the delegate
    public event D Ev {
        add {
            /* add the delegate in a thread safe way */
        }
        remove {
            /* remove the delegate in a thread safe way */
        }
    }
}
```

Within the class X, references to Ev on the left-hand side of the += and -= operators cause the add and remove accessors to be invoked. All other references to Ev are compiled to reference the hidden field __Ev instead (§12.7.5). The name "__Ev" is arbitrary; the hidden field could have any name or no name at all. end note

# 15.8.3 Event accessors

[Note: Event declarations typically omit event-accessor-declarations, as in the Button example above. For example, they might be included if the storage cost of one field per event is not acceptable. In such cases, a class can include event-accessor-declarations and use a private mechanism for storing the list of event handlers. end note]

The event-accessor-declarations of an event specify the executable statements associated with adding and removing event handlers.

The accessor declarations consist of an add-accessor-declaration and a remove-accessor-declaration. Each accessor declaration consists of the token add or remove followed by a block. The block associated with an add-accessor-declaration specifies the statements to execute when an event handler is added, and the block associated with a remove-accessor-declaration specifies the statements to execute when an event handler is removed.

Each add-accessor-declaration and remove-accessor-declaration corresponds to a method with a single value parameter of the event type, and a void return type. The implicit parameter of an event accessor is named value. When an event is used in an event assignment, the appropriate event accessor is used. Specifically, if the assignment operator is += then the add accessor is used, and if the assignment operator is -= then the remove accessor is used. In either case, the right-hand operand of the assignment operator is used as the argument to the event accessor. The block of an add-accessor-declaration or a remove-accessor-declaration shall conform to the rules for void methods described in §15.6.9. In particular, return statements in such a block are not permitted to specify an expression.

Since an event accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declared in an event accessor to have that name.

[Example: In the following code