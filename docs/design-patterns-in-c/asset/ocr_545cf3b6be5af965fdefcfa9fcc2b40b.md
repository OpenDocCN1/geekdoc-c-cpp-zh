![](bbox=[0.18, 0.08, 0.82, 0.42])

So this concludes our application implementing Memento pattern.

# Comparing Command and Memento Patterns

The Command pattern also provides the Undo / Redo functionality by converting actions to commands. The difference would be that the Command pattern stores each action but the Memento pattern saves the state only on request. Additionally, the Command pattern has Undo and Redo operations for each action, but the Memento does not need that.

Depending on the scenario, Command / Memento pattern could be used.

# Summary

In this chapter we have explore the Memento pattern. The attached source code contains the example we discussed.