cohesion implies that each class should only do one thing, and, presumably, do it well. At the topmost decomposition level, the command dispatcher indeed does only one thing: it interprets commands. At the task level, however, from our list of functionality above, it clearly must execute multiple tasks. Therefore, we decompose the command dispatcher into several distinct classes, one for each major task it must perform. Hence, we have the following classes:

+   1. CommandRepository: Stores the list of available commands
+   2. CommandDispatcher: Receives and interprets requests to execute commands
+   3. CommandManager: Dispatches commands and manages undo and redo
+   4. Command hierarchy: Executes commands

The remainder of this chapter is devoted to describing the design and salient implementation details for the above list of classes and class hierarchies.