
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
            Console.WriteLine(y + " ");
        }
        Console.WriteLine();

        x = 1;
        Console.WriteLine("Series generated using y = x + ++x;");
        for(i = 0; i < 10; i++) {
            y = x + ++x; // prefix ++
            Console.WriteLine(y + " ");
        }
        Console.WriteLine();
    }
}
```

The output is shown here:

```
Series generated using y = x + x++;
2
4
6
8
10
12
14
16
18
20
```

```
Series generated using y = x + ++x;
3
5
7
9
11
13
15
17
19
21
```

As the output confirms, the statement

```
y = x + x++;
```

adds the original value of x to x and assigns this result to y. The value of x is incremented after its value has been obtained. However, the statement

```
y = x + ++x;
```

obtains the value of x, increments x, and then adds that value to the original value of x. The result is assigned to y. As the output shows, simply changing ++x to x++ changes the number series from even to odd.

One other point about the preceding example: Don't let expressions like

```
x + ++x
```

intimidate you. Although having two operators back-to-back is a bit unsettling at first glance, the compiler keeps it all straight. Just remember, this expression simply adds the value of x to the value of x incremented.

## Relational and Logical Operators

In the terms relational operator and logical operator, relational refers to the relationships that values can have with one another, and logical refers to the ways in which true and false values can be connected together. Since the relational operators produce true or false results, they often work with the logical operators. For this reason they will be discussed together here.

The relational operators are as follows:

| Operator | Meaning |
|---|---|
| == | Equal to |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

The logical operators are shown next:

| Operator | Meaning |
|---|---|
| & | AND |
| \| | OR |
| ^ | XOR (exclusive OR) |
| \|\| | Short-circuit OR |
| && | Short-circuit AND |
| ! | NOT |

The outcome of the relational and logical operators is a bool value.

In general, objects can be compared for equality or inequality using == and !=. However, the comparison operators, <, >, <=, or >=, can be applied only to those types that support an ordering relationship. Therefore, all of the relational operators can be applied to all numeric types. However, values of type bool can only be compared for equality or inequality since the true and false values are not ordered. For example, true > false has no meaning in C#.

For the logical operators, the operands must be of type bool, and the result of a logical operation is of type bool. The logical operators, &, &&, |, ||, ^, and !, support the basic logical operations AND, OR, XOR, and NOT, according to the following truth table:

| p | q | p & q | p \| q | p ^ q | !p |
|---|---|---|---|---|---|
| False | False | False | False | False | True |
| True | False | False | True | True | False |
| False | True | False | True | True | True |
| True | True | True | True | False | False |

As the table shows, the outcome of an exclusive OR operation is true when one and only one operand is true.

Here is a program that demonstrates several of the relational and logical operators:

```
// Demonstrate the relational and logical operators.

using System;

class RelLogOps {
  static void Main() {
    int i, j;
    bool b1, b2;

    i = 10;
    j = 11;
    if(i < j) Console.WriteLine("i < j");
    if(i <= j) Console.WriteLine("i <= j");
    if(i == j) Console.WriteLine("this won't execute");
    if(i != j) Console.WriteLine("i != j");
    if(i > j) Console.WriteLine("this won't execute");
    if(i >= j) Console.WriteLine("this won't execute");

    b1 = true;
    b2 = false;
    if(b1 & b2) Console.WriteLine("this won't execute");
    if(!(b1 & b2)) Console.WriteLine("!(b1 & b2) is true");
    if(b1 | b2) Console.WriteLine("b1 | b2 is true");
    if(b1 ^ b2) Console.WriteLine("b1 ^ b2 is true");
  }
}
```

The output from the program is shown here:

```
i < j
i <= j
i != j
!(b1 & b2) is true
b1 | b2 is true
b1 ^ b2 is true
```

The logical operators provided by C# perform the most commonly used logical operations. However, several other operations are defined by the rules for formal logic. These other logical operations can be constructed using the logical operators supported by C#. Thus, C# supplies a set of logical operators sufficient to construct any other logical operation. For example, another logical operation is implication. Implication is a binary operation in which the outcome is false only when the left operand is true and the right operand is false. (The implication operation reflects the idea that true cannot imply false.) Thus, the truth table for the implication operator is shown here:

| p | q | p implies q |
|---|---|---|
| True | True | True |
| True | False | False |
| False | False | True |
| False | True | True |

The implication operation can be constructed using a combination of the ! and the | operator, as shown here:

```
!p | q
```

The following program demonstrates this implementation:

```
// Create an implication operator in C#.

using System;

class Implication {
    static void Main() {
        bool p=false, q=false;
        int i, j;

        for(i = 0; i < 2; i++) {
            for(j = 0; j < 2; j++) {
                if(i==0) p = true;
                if(i==1) p = false;
                if(j==0) q = true;
                if(j==1) q = false;

                Console.WriteLine("p is " + p + ", q is " + q);
                if(!p | q) Console.WriteLine(p + " implies " + q + " is " + true);
                Console.WriteLine();
            }
        }
    }
}
```

The output is shown here:

```
p is True, q is True
True implies True is True

p is True, q is False

p is False, q is True
False implies True is True

p is False, q is False
False implies False is True
```

## Short-Circuit Logical Operators

C# supplies special short-circuit versions of its AND and OR logical operators that can be used to produce more efficient code. To understand why, consider the following. In an AND operation, if the first operand is false, then the outcome is false no matter what value the second operand has. In an OR operation, if the first operand is true, then the outcome of the operation is true no matter what the value of the second operand. Thus, in these two cases there is no need to evaluate the second operand. By not evaluating the second operand, time is saved and more efficient code is produced.

The short-circuit AND operator is && and the short-circuit OR operator is ||. As described earlier, their normal counterparts are & and |. The only difference between the normal and short-circuit versions is that the normal operators will always evaluate each operand, but short-circuit versions will evaluate the second operand only when necessary.

Here is a program that demonstrates the short-circuit AND operator. The program determines if the value in d is a factor of n. It does this by performing a modulus operation. If the remainder of n / d is zero, then d is a factor. However, since the modulus operation involves a division, the short-circuit form of the AND is used to prevent a divide-by-zero error.

```
// Demonstrate the short-circuit operators.

using System;

class SCops {
    static void Main() {
        int n, d;

        n = 10;
        d = 2;
        if(d != 0 && (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);

        d = 0; // now, set d to zero

        // Since d is zero, the second operand is not evaluated.
        if(d != 0 && (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);

        // Now, try the same thing without short-circuit operator.
        // This will cause a divide-by-zero error.
        if(d != 0 & (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);
    }
}
```

To prevent a divide-by-zero error, the if statement first checks to see if d is equal to zero. If it is, then the short-circuit AND stops at that point and does not perform the modulus
