Remember, the test covers inherited methods, not just one that is directly defined in the class definition.

The performSelector: method and its variants (not shown in Table 9.1) enable you to send a message to an object, where the message can be a selector stored inside a variable. For example, consider this code sequence:

```
SEL action;
id graphicObject;
...
action = @selector (draw:);
...
[graphicObject performSelector:action];
```

In this example, the method indicated by the SEL variable action is sent to whatever object is stored in graphicObject. Presumably, the action may vary during program execution—perhaps based on the user's input—even though we've shown the action as draw. To first ensure that the object can respond to the action, you might want to use something like this:

```
if ([graphicObject respondsToSelector:action]
== YES)
    [graphicObject performSelector:action];
else
    // error handling code here
```

# Note

The respondsToSelector: method is used extensively in iOS for implementing the concept of delegation. You'll learn in Chapter 10, "More on Variables and Data Types," the system will give you the option to implement one or more methods in your class to handle certain events or provide certain information (such as the number of sections