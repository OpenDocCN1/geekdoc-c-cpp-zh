Understand, however, that in the increment or decrement forms, x is evaluated only once, not twice. This can improve efficiency in some cases.

Both the increment and decrement operators can either precede (prefix) or follow (postfix) the operand. For example

```
x = x + 1;
```

can be written as

```
++x; // prefix form
```

or as

```
x++; // postfix form
```

In the foregoing example, there is no difference whether the increment is applied as a prefix or a postfix. However, when an increment or decrement is used as part of a larger expression, there is an important difference. When an increment or decrement operator precedes its operand, the result of the operation is the value of the operand after the increment. If the operator follows its operand, the result of the operation is the value of the operand before the increment. Consider the following:

```
x = 10;
y = ++x;
```

In this case, y will be set to 11. This is because x is first incremented and then its value is returned. However, if the code is written as

```
x = 10;
y = x++;
```

then y will be set to 10. In this case, the value of x is first obtained, x is incremented, and then the original value of x is returned. In both cases, x is still set to 11. The difference is what is returned by the operation.

There are significant advantages in being able to control when the increment or decrement operation takes place. Consider the following program, which generates a series of numbers:

```
// Demonstrate the difference between prefix and
// postfix forms of ++.

using System;

class PrePostDemo {
    static void Main() {
        int x, y;
        int i;

        x = 1;
        Console.WriteLine("Series generated using y = x + x++;");
        for(i = 0; i < 10; i++) {

            y = x + x++; // postfix ++
```