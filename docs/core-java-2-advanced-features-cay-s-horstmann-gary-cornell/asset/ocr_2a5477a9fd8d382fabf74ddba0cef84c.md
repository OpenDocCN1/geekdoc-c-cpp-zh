Typically, users will supply inputs in multiple text fields and then click a button to read all values. When the button is clicked, you can get the user-supplied value with the `getValue` method. That method returns an `Object` result, and you need to cast it into the appropriate type. The `JFormattedTextField` returns an object of type `Long` if the user edited the value. However, if the user made no changes, the original `Integer` object is returned. Therefore, you should cast the return value to the common superclass `Number`:

```
Number value = (Number) intField.getValue();
int v = value.intValue();
```

The formatted text field is not very interesting until you consider what happens when a user provides illegal input. That is the topic of the next section.

# 10.4.2 Behavior on Loss of Focus

Consider what happens when a user supplies input to a text field. The user types input and eventually decides to leave the field, perhaps by clicking on another component with the mouse. Then the text field *loses focus*. The I-beam cursor is no longer visible in the text field, and keystrokes are directed toward a different component.

When the formatted text field loses focus, the formatter looks at the text string that the user produced. If the formatter knows how to convert the text string to an object, the text is valid. Otherwise it is invalid. You can use the `isEditValid` method to check whether the current content of the text field is valid.

The default behavior on loss of focus is called “commit or revert.” If the text string is valid, it is *committed*. The formatter converts it to an object. That object becomes the current value of the field (that is, the return value of the `getValue` method that you saw in the preceding section). The value is then converted back to a string, which becomes the text string visible in the field. For example, the integer formatter recognizes the input `1729` as valid, sets the current value to `new Long(1729)`, and converts it back into a string with a decimal comma: `1,729`.

Conversely, if the text string is invalid, the current value is not changed and the text field *reverts* to the string that represents the old value. For example, if the user enters a bad value, such as `x1`, the old value is restored when the text field loses focus.

> **NOTE:** The integer formatter regards a text string as valid if it starts with an integer. For example, `1729x` is a valid string. It is converted to the number 1729, which is then formatted as the string `1,729`.