```
b.Click += new EventHandler(...);
```

which appends a delegate to the invocation list of the Click event, and

```
Click -= new EventHandler(...);
```

which removes a delegate from the invocation list of the Click event.

*end example*

When compiling a field-like event, the compiler automatically creates storage to hold the delegate, and creates accessors for the event that add or remove event handlers to the delegate field. The addition and removal operations are thread safe, and may (but are not required to) be done while holding the lock (§9.4.4.19) in the containing object for an instance event, or the type object (§11.7.15.7) for a static event.

*Note:* Thus, an instance event declaration of the form:

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
    public event D Ev
    {
        add
        {
            /* Add the delegate in a thread safe way */
        }
        remove
        {
            /* Remove the delegate in a thread safe way */
        }
    }
}
```

Within the class X, references to Ev on the left-hand side of the += and -= operators cause the add and remove accessors to be invoked. All other references to Ev are compiled to reference the hidden field __Ev instead (§11.7.6). The name "__Ev" is arbitrary; the hidden field could have any name or no name at all.

*end note*

# 14.8.3 Event accessors

*Note:* Event declarations typically omit event_accessor_declarations, as in the Button example above. For example, they might be included if the storage cost of one field per event is not acceptable. In such cases, a class can include event_accessor_declarations and use a private mechanism for storing the list of event handlers. *end note*

The event_accessor_declarations of an event specify the executable statements associated with adding and removing event handlers.