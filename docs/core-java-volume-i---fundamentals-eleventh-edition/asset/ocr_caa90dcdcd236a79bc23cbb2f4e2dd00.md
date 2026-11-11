Similar to clicking a mouse button, key events occur as a key is pressed or released. When pressing and releasing one or more keys yields text input, a “key typed” event is generated. For example, if the user presses the Shift key, then presses and releases the A key, an uppercase “A” is typed.

```
```java
source.setOnKeyTyped(event ->
{
  String input = event.getCharacter();
  . . .
});
```
```

The `getCharacter` method gets the input as a string (in case some keyboard produces emoji that require two UTF-16 code units, or decomposed accents, or some other input that doesn’t fit in a single `char` value).

However, if you process cursor or function keys, you want to listen to “key pressed” events and call the `getCode` method. You get a value of the `KeyCode` enumeration, which has over 200 values with every imaginable key that can appear on someone’s keyboard, such as `KeyCode.A`, `KeyCode.DELETE`, and `KeyCode.EURO_SIGN`.

```
```java
source.setOnKeyPressed(event ->
{
  KeyCode code = event.getCode();
  if (code == KeyCode.DELETE) . . .;
});
```
```

The program in Listing 13.5 demonstrates mouse and key events. Use the mouse to click on an empty space to add a new dot, or drag an existing dot to a new location. If you double-click on a dot, it is erased. The dot with keyboard focus is colored red. You can delete it with the Delete key and move it with the cursor keys. If you hold down the Shift key, it moves by a greater distance.

Note that each dot listens to “mouse entered/exited/pressed/dragged” and “key pressed” events. We simply rely on the JavaFX framework to deliver the events to the affected nodes. The “mouse pressed” event is also handled by the root pane so that we can add new dots.

A mouse event is first presented to child nodes and then to parent nodes. To avoid creating another dot, the “mouse pressed” handler of the dot consumes the event.

Alternatively, we could have implemented a single “mouse pressed” handler for the root pane. But then we would have had to check if a node is under the mouse pointer. The JavaFX way is to work as much as possible with the “scene graph” (the nodes and their parent/child relationships).