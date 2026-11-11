As we demonstrate in the next chapter, it is just as easy to add the same action to a menu.

Finally, we want to add the action objects to keystrokes so that an action is carried out when the user types a keyboard command. To associate actions with keystrokes, you first need to generate objects of the `Keystroke` class. This convenience class encapsulates the description of a key. To generate a `Keystroke` object, don't call a constructor but instead use the static `getKeystroke` method of the `Keystroke` class.

```
```java
Keystroke ctrlBKey = Keystroke.getKeystroke("ctrl B");
```
```

To understand the next step, you need to understand the concept of *keyboard focus*. A user interface can have many buttons, menus, scrollbars, and other components. When you hit a key, it is sent to the component that has focus. That component is usually (but not always) visually distinguished. For example, in the Java look-and-feel, a button with focus has a thin rectangular border around the button text. You can use the Tab key to move the focus between components. When you press the space bar, the button with focus is clicked. Other keys carry out different actions; for example, the arrow keys can move a scrollbar.

However, in our case, we do not want to send the keystroke to the component that has focus. Otherwise, each of the buttons would need to know how to handle the Ctrl+Y, Ctrl+B, and Ctrl+R keys.

This is a common problem, and the Swing designers came up with a convenient solution. Every `JComponent` has three *input maps*, each mapping `Keystroke` objects to associated actions. The three input maps correspond to three different conditions (see Table 10.2).

**Table 10.2** Input Map Conditions

| Flag | Invoke Action |
|---|---|
| WHEN_FOCUSED | When this component has keyboard focus |
| WHEN_ANCESTOR_OF_FOCUSED_COMPONENT | When this component contains the component that has keyboard focus |
| WHEN_IN_FOCUSED_WINDOW | When this component is contained in the same window as the component that has keyboard focus |