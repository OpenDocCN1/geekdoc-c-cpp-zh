This is a common problem, and the Swing designers came up with a convenient solution. Every `JComponent` has three *input maps*, each mapping keystroke objects to associated *actions*. The three input maps correspond to three different conditions (see **Table 10.2**).

# **Table 10.2** Input Map Conditions

| Flag | Invoke Action |
|---|---|
| `WHEN_FOCUSED` | When this component has keyboard focus |
| `WHEN_ANCESTOR_OF_FOCUSED_COMPONENT` | When this component contains the component that has keyboard focus |
| `WHEN_IN_FOCUSED_WINDOW` | When this component is contained in the same window as the component that has keyboard focus |

Keystroke processing checks these maps in the following order:

+   1. Check the `WHEN_FOCUSED` map of the component with input focus. If the keystroke exists and its corresponding action is enabled, execute the action and stop processing.
+   2. Starting from the component with input focus, check the `WHEN_ANCESTOR_OF_FOCUSED_COMPONENT` maps of its parent components. As soon as a map with the keystroke and a corresponding enabled action is found, execute the action and stop processing.
+   3. Look at all *visible* and *enabled* components, in the window with input focus, that have this keystroke registered in a `WHEN_IN_FOCUSED_WINDOW` map. Give these components (in the order of their keystroke registration) a chance to execute the corresponding action. As soon as the first enabled action is executed, stop processing.

To obtain an input map from the component, use the `getInputMap` method. Here is an example:

```
InputMap imap = panel.getInputMap(JComponent.WHEN_FOCUSED);
```