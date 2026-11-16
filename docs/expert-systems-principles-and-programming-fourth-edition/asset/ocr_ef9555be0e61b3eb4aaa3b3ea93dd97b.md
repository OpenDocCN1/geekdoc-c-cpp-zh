```
MSG >> compute-area ED:1 (<Instance-circle-1>)
HND >> compute-area primary in class CIRCLE
ED:1 (<Instance-circle-1>)
HND << compute-area primary in class CIRCLE
ED:1 (<Instance-circle-1>)
MSG << compute-area ED:1 (<Instance-circle-1>)
28 .2743338823081
CLIPS> (send [rectangle-1] compute-area.)
MSG >> compute-area ED:1 (<Instance-rectangle-1>)
HND >> compute-area primary in class RECTANGLE
ED:1 (<Instance-rectangle-1>)
HND << compute-area primary in class RECTANGLE
ED:1 (<Instance-rectangle-1>)
MSG << compute-area ED:1 (<Instance-rectangle-1>)
8
CLIPS>
```

Watching messages prints debugging information when a message is sent to an instance and when the execution of that message has been totally completed. Watching message-handlers prints debugging information when a specific message-handler begins and ends execution. Watching message-handlers provides all of the information provided by watching messages, along with additional information. In the preceding dialog, the information printed by watching messages is prefaced with MSG and the information printed by watching message-handlers is prefaced with HND. The >> symbol indicates message-handler initiation and the << symbol indicates message-handler completion. This is followed by the name of the message or message-handler. For message-handlers some additional information is now printed: the handle type (before, after, primary, or around) followed by the class associated with the specific message-handler being executed. A single message is capable of causing the execution of multiple message-handlers of different types or classes, so this information allows you to determine which one is actually executed. The final information printed is the evaluation depth denoted by the symbol ED followed by the arguments to the message-handler. As with defunctions, the evaluation depth is an indication of the nesting of defunction and message-handler calls. It starts at zero and then each time a defunction/message-handler is entered it increases by one. Each time a defunction/message-handler exits, it decreases by one. In the argument list, the first argument listed is always the value of the ?self variable. The explicit arguments of the message-handler are then listed next.

It's also possible to watch all of the message-handlers of a specific class by just specifying the class; to watch a specific message-handler by specifying just the class and message-handler name; or to watch a specific message-handler and a specific type by specifying the class, message-handler name, and then the type (before, after, primary, or around);

```
CLIPS> (unwatch all)
CLIPS> (watch message-handlers CIRCLE)
```