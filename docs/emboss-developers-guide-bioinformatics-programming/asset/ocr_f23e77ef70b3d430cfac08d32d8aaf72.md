# 4.4.5 Conditional statements

There are three kinds of conditional statements in ACD: unary, ternary and case-type.

# 4.4.5.1 Unary conditional statements

A typical use for unary conditionals is to switch prompts on or off. Assume that a window size should only be prompted for if the sequence turns out to be a protein. The ACD to achieve this would look as follows:

```
```
sequence: sequence
[
  parameter: "Y"
  type: gapany
]

integer: window
[
  standard: "$(sequence.protein)"
  etc
]
```
```

If the sequence is a protein then the required statement is equivalent to:

```
```
standard: "Y"
```
```

and the prompt is switched on. If the sequence is nucleic the statement is equivalent to:

```
```
standard: "N"
```
```

This will effectively disable the prompt. Controlling prompting is described in detail elsewhere (Section 4.5, 'Controlling the prompt').

# 4.4.5.2 Ternary conditional statements

Ternary conditional statements have the general form:

```
```
@(conditional ? value-if-true : value-if-false)
```
```

They are useful when setting up the application for two distinct modes of usage, for example when setting gap penalty values differently for proteins and nucleic acids in alignment programs. The example below will set the penalty to 14 for proteins and 16 for nucleic acids:

```
```
integer: penalty
[
  standard: "N"
  default: "@($(sequence.protein) ? 14 : 16)"
  etc
]
```
```