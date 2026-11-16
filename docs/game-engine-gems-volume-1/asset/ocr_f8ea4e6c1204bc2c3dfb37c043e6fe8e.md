# ## 6.2 Design Patterns: Model View Controller (MVC)

A common problem, particularly evident with GUI systems, is that over time, last minute hacks and "temporary" bug fixes lead to strongly coupled code, leaving changes to one area of the system to cause unintended effects elsewhere and also making it difficult to refactor. The model-view-controller (MVC) design pattern aims to ensure only a loose coupling of elements by separating the framework into three distinct constituent parts to be maintained independently:

+   - The *model* refers to the actual data that we represent on the screen. For example, this could be the game time or the number of lives remaining.
+   - The *view* concerns itself only with the visual representation and rendering of that object. In our previous example, perhaps we might display an analogue clock to represent the time remaining or an icon for every life remaining.
+   - The *controller* refers to how the object interacts with the game, user input, and general state, system, or game logic.

MVC has gained popularity, now being a major contributing concept in many of the larger GUI and system frameworks, from Cocoa to Qt, MFC, and the current Windows Presentation Foundation.

Taking our previous timer example, the *controller* would refer to our game update loop; being responsible for determining the current time and passing a `TimerUpdate` message to the timer *model* object, which in turn updates its internal representation. The *view* will typically have its own internal description, but will update that based on information inside the *model* itself.