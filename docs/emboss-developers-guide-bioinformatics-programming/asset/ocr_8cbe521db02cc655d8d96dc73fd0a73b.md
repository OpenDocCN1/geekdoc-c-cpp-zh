```
]
array: values
[
  standard: "Y"
  size: "$(subwindow)"
]
```

sequence.length is a calculated attribute and is the length of the sequence. The $(sequence.length) value is calculated during ACD processing once the input sequence has been read in. In contrast window.maximum simply refers to the maximum: attribute of the window data definition.

Of course you need to be careful that the type of retrieved value matches that of the attribute which is being calculated. For instance, if you have defined a toggle datatype:

```
toggle: dovalues
[
  standard: "Y"
]
```

then the following definition is perfectly valid because the standard: global attribute has a boolean value, which is the same type as the toggle datatype.

```
array: values
[
  standard: "$(toggle)"
  size: "$(subwindow)"
]
```

The following definition is *not* valid and an error will be generated during ACD processing:

```
array: values
[
  standard: "Y"
  size: "$(toggle)"    /* This is not valid ! */
]
```

It is invalid because the size: attribute of the array datatype has an integer value, whereas the toggle datatype has a boolean value.

# 4.4.4 Calculations and tests

Calculations can be performed in ACD using the @ syntax. A rather silly, but legal, calculation would be:

```
@ (5 + 9)
```

which equates to the value 14. Calculations can be used to add, subtract, multiply or divide, or test for equality, inequality, “greater than” or “less than”. The test values can be integers,