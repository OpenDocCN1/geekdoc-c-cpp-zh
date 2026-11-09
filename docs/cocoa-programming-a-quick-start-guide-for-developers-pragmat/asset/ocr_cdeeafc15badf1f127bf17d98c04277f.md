```
    windowDidEndSheet:
    windowDidExpose:
    windowDidMiniaturize:
    windowDidMove:
    windowDidResignKey:
    windowDidResignMain:
    windowDidResize:
    windowDidUpdate:
    windowShouldClose:
    windowShouldZoom:toFrame:
    windowWillBeginSheet:
    windowWillClose:
    windowWillMiniaturize:
    windowWillMove:
    windowWillResize:toSize:
    windowWillReturnFieldEditor:toObject:
    windowWillReturnUndoManager:
    windowWillUseStandardFrame:defaultFrame:
```

The delegate methods come in three flavors: something will happen, something did happen, and something should happen. You implement the will version to change the behavior before an action happens and the did version to respond after the action happens. The should version returns a BOOL that allows you to cancel an action if you determine it shouldn’t happen.

Just like the game shows where a contestant can “call a friend,” each window object gets to designate a single friend that can be called when any of these methods is called. That friend is the delegate.

We don’t really expect one friend to be able to respond to all of these messages, but our window must choose only one delegate ahead of time. Unfortunately, the window can’t say, “I know who would know how to answer that question” and decide who will be called at runtime. The delegate is chosen before the question is asked.

Before the game begins, we preinterview the delegate. This way, we know which messages the delegate can handle and which ones it can’t. In Cocoa terms, the delegate may implement none, any, or all of the delegate methods for an object. If a delegate has not implemented a method, it will not be called to handle that message. The window will have to come up with its own answer.

These rules might seem complicated—but a quick example should clarify the situation.