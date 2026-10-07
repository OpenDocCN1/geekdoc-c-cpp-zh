In each case, the hidden first operand is a pointer to the object being subscribed, the object a.

Note that the operator[] () function passes back a reference to a character. We do this so we can use it on both sides of an assignment statement.

Note also that the subscript operator must be able to appear on both the right and the left hand side of an expression. In order to appear on the left-hand side, its return value must be an Ivalue. This is achieved by specifying the return value as a reference type:

```
char& String255::operator[](int i) {
  return buf[i];
}
```

The return value of the subscript operator is the Ivalue of the indexed element. That's why it can appear as the target off an assignment.

C++ has reference declarations, and such type modifiers produce Ivalue's (stands for location value).

Note: on the right side of an assignment expression, an Ivalue is automatically dereferenced. On the left side of an expression, an Ivalue specifies where an appropriate value is to be stored.

# One Last Example

```
// phone.h

#ifndef PHONE_H
#define PHONE_H

typed struct {
  char *name;
  long number;
} ENTRY;
```