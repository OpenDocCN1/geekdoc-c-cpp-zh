```
add-accessor-declaration:
    attributes_opt add block
remove-accessor-declaration:
    attributes_opt remove block
```

An event-declaration may include a set of attributes (§22) and a valid combination of the four access modifiers (§15.3.6), the new (§15.3.5), static (§15.6.3, §15.8.4), virtual (§15.6.4, §15.8.5), override (§15.6.5, §15.8.5), sealed (§15.6.6), abstract (§15.6.7, §15.8.5), and extern (§15.6.8) modifiers.

Event declarations are subject to the same rules as method declarations (§15.6) with regard to valid combinations of modifiers.

The type of an event declaration shall be a delegate-type (§9.2.8), and that delegate-type shall be at least as accessible as the event itself (§8.5.5).

An event declaration can include event-accessor-declarations. However, if it does not, for non-extern, non-abstract events, the compiler shall supply them automatically (§15.8.2); for extern events, the accessors are provided externally.

An event declaration that omits event-accessor-declarations defines one or more events—one for each of the variable-declarators. The attributes and modifiers apply to all of the members declared by such an event-declaration.

It is a compile-time error for an event-declaration to include both the abstract modifier and event-accessor-declarations.

When an event declaration includes an extern modifier, the event is said to be an external event. Because an external event declaration provides no actual implementation, it is an error for it to include both the extern modifier and event-accessor-declarations.

It is a compile-time error for a variable-declarator of an event declaration with an abstract or external modifier to include a variable-initializer.

An event can be used as the left-hand operand of the += and -= operators. These operators are used, respectively, to attach event handlers to, or to remove event handlers from an event, and the access modifiers of the event control the contexts in which such operations are permitted.

The only operations that are permitted on an event by code that is outside the type in which that event is declared, are += and -=. Therefore, while such code can add and remove handlers for an event, it cannot directly obtain or modify the underlying list of event handlers.

In an operation of the form x += y or x -= y, when x is an event the result of the operation has type void (§12.18.4) (as opposed to having the type of x, with the value of x after the assignment, as for other the += and -= operators defined on non-event types). This prevents external code from indirectly examining the underlying delegate of an event.

[Example: The following example shows how event handlers are attached to instances of the Button class:]

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
}
public class LoginDialog: Form
{
    Button okButton;
    Button cancelButton;
```