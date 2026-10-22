Notice how integer division does not round to the nearest integer, but always truncates (that is, discards the entire fractional part). When you mixed integers with floating point, the answer came out the same as floating point. Actually, the computer is not really capable of dividing a floating-point type by an integer type, so the compiler converts both operands to a single type. In this case, the integer is converted to floating point before division.

Until the C99 standard, C gave language implementers some leeway in deciding how integer division with negative numbers worked. One could take the view that the rounding procedure consists of finding the largest integer smaller than or equal to the floating-point number. Certainly, 3 fits that description when compared to 3.8. But what about −3.8? The largest integer method would suggest rounding to −4 because −4 is less than −3.8. But another way of looking at the rounding process is that it just dumps the fractional part; that interpretation, called truncating toward zero, suggests converting −3.8 to −3. Before C99, some implementations used one approach, some the other. But C99 says to truncate toward zero, so −3.8 is converted to −3.

The properties of integer division turn out to be handy for some problems, and you’ll see an example fairly soon. First, there is another important matter: What happens when you combine more than one operation into one statement? That is the next topic.

# Operator Precedence

Consider the following line of code:

```
butter = 25.0 + 60.0 * n / SCALE;
```

This statement has an addition, a multiplication, and a division operation. Which operation takes place first? Is 25.0 added to 60.0, the result of 85.0 then multiplied by n, and that result then divided by SCALE? Is 60.0 multiplied by n, the result added to 25.0, and that answer then divided by SCALE? Is it some other order? Let’s take n to be 6.0 and SCALE to be 2.0. If you work through the statement using these values, you will find that the first approach yields a value of 255. The second approach yields 192.5. A C program must have some other order in mind, because it would give a value of 205.0 for butter.

Clearly, the order of executing the various operations can make a difference, so C needs unambiguous rules for choosing what to do first. C does this by setting up an operator pecking order. Each operator is assigned a precedence level. As in ordinary arithmetic, multiplication and division have a higher precedence than addition and subtraction, so they are performed first. What if two operators have the same precedence? If they share an operand, they are executed according to the order in which they occur in the statement. For most operators, the order is from left to right. (The = operator was an exception to this.) Therefore, in the statement

```
butter = 25.0 + 60.0 * n / SCALE;
```

the order of operations is as follows:

60.0 * n    The first * or / in the expression (assuming n is 6 so that 60.0 * n is 360.0)