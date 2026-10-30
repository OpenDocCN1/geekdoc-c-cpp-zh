
still contain some value, only you dont know what value. If an unknown value is used in a computation, the result will of course be unpredictable in general.

Note that the operator = is used somewhat differently in C++ than in mathematics. In mathematics a statement r = x*y + p*q; asserts that the left hand side and right hand side are equal. In C++ however, it is a command to evaluate the expression on the right and put the resulting value into the variable named on the left. After the assignment the values of the expressions on either side of the = operator are indeed equal if we consider r on the left hand side to be a trivial expression.

Note however, that we cannot write x*y + p*q = r; because we require the left hand side to be a variable, into which the value of the expression on the right hand side must be stored.

The rule described above makes it perfectly natural to write a statement such as:

```
p = p + 1;
```

This is meaningless in mathematics; in C++ however it just says: evaluate the expression on the right hand side and put the resulting value into the variable named on the left. Assuming p is as in the code fragment given earlier, its value is 4. Thus in this case the value 4+1=5 would be put in p. Note that a statement such as p + 1 = p; is illegal – the left hand side p + 1 does not denote a variable.

## 3.2.1 Integer division and the modulo operator %

In C++, when one integer value is divided by another, the result is defined to also be the largest integer no larger than the quotient. Thus if you write

```
int m=100, n=7, p, q;
 p = m/n;
 q = 35/200;
```

the variables p and q would respectively get the values 14 and 0. In other words, we only get the integer part of the quotient.

If you wish to get the remainder resulting when one integer divides another you use the % operator. Thus the expression m % n evaluates to the remainder of m when divided by n, where m,n must have an integral type. The operator % has the same precedence as *, /.

Here is a code fragment that reads in a duration given in seconds and prints out the equivalent duration in hours, minutes, and seconds.

```
cout <<"Give the duration in seconds: ";
int duration; cin >> duration;
int hours, minutes, seconds;
hours = duration/3600;
minutes = (duration - hours*3600)/60;
seconds = duration % 60;
cout <<"Hours: "<< hours <<", Minutes: "
<< minutes <<", Seconds: "<< seconds << endl;
```

If you run this code, and type 5000 when asked, you would get the following output as expected:

```
Hours: 1, Minutes: 23, Seconds: 20
```

## 3.2.2 Subtleties

The assignment statement is somewhat tricky. The first point concerns the floating point representations. Both, float and double are imprecise representations, where the significand is correct only to a fixed number of bits. So if an arithmetic operation affects less significant bits, then the operation will have no effect. As an example, consider the following code.

```
float w, y=1.5, avogadro=6.022E23 ;
w = avogadro + y;
```

What is the value of w? Suppose for a moment that we precisely calculate the sum avogadro + y. The sum will be

60220000000000000000001.5

We will have a problem when we try to store this into a float type variable. This is because a float type variable can only stores significands of 24 bits, or about 7 digits. So in order to store, we would treat everything beyond the most significant 7 digits as 0. If so we would get

602200000000000000000000

This loss of digits is called round-off error. After the round off, this can now fit in a float, because it can be written exactly as 6.022E23. Net effect of the addition: nothing! The variable w gets the value avogadro even though you assigned it the value avogadro + 1.5. This example shows the inherent problem in adding a very small float value to a very large float value.

Some subtleties arise when we perform an arithmetic operation in which the operands have different types, or even simply if you store one type of number into a variable of another type. C++ allows such operations, and could be said to perform such actions reasonably well. However, it is worth knowing what exactly happens.

precision could be lost when you store a value from a double (53 bits of precision) into a float (24 bits of precision). Overflow is also possible, as discussed later.

When we perform an arithmetic operation on operands of the same type the result is also computed to be of the same type. If your program asks to perform arithmetic operations on operands of different types, then the operands are first converted by C++ so that they have the same type. The rules for this are fairly natural. C++ always converts less expressive types to more expressive ones, where unsigned integral types are deemed less expressive than signed integral types, which in turn are deemed less expressive than the floating types. If the two types differ in size, then the smaller is converted to have a larger size. As an example, suppose we have an arithmetic expression var1 op var2, where var1 is int and var2 is float. Then var1 will be converted to float, and the result will also be float. If var1, var2 are long, int, then var2 will be converted to long. If the operands are of type float, long long then both will be converted to double, and so on. After the expression is evaluated, it may either itself form an operand in a bigger expression, or it might have to be stored into a variable. In both cases, there may have to be a further type conversion.

Literals also have a type associated with them. An integer literal like 35 is considered to be of type int, and a floating literal like 100.0 is by default considered to be of type double. You can specify literals of specific types by attaching the suffixes L,F,U which respectively stand for long, float, unsigned. Thus if you write 100LU, it will be interpreted as a literal of type long unsigned, having the value 100.

It is important to be careful with division.

```
int x=100, w;
float y,z;
y = 360/x;
z = 360.0/x;
w = 360.0/x;
```

As per the rules stated, 360/x will be evaluated to have an integer value since both operands are integer. Thus the exact quotient 3.6 will be truncated to give 3. This value will be stored (after conversion to the floating point format) into y. In the next statement, 360.0/x the first operand is double, hence the result will be evaluated as a double, i.e. 3.6. This value will be stored in z. In the final statement, the value of the expression will indeed be 3.6, however because w is of type int, there will have to be a type conversion, and as a result the value stored in w will be just 3.

Note finally that if the dividend and the divisor are of integral types, and the divisor is 0, then an error will be reported when such an operation happens during execution, and the program will stop with a message. Something different happens for floating types, as discussed in Section 3.2.4.

## 3.2.3 Overflow and arithmetic errors

For each numerical data type, we have mentioned a certain largest possible and smallest possible value that can be represented. While performing calculations, the results can go outside this allowed range. In this case, what exactly happens is handled differently for different types.

```
```cpp
int x,y,z;
x = y = z = 1;
```
```

This will end up assigning 1 to all the variables. This has a systematic explanation as follows. Any assignment, say `z = 1`, is also an expression in C++. Not only is the assignment made, but the expression stands for the value that got assigned. Further, the *associativity* of `=` is right-to-left, i.e. given an expression `x = y = z = 1`, the rightmost assignment operator is evaluated first. This is different from the other operators you have seen so far, such as the arithmetic operators, in which the evaluation order is left to right. Thus, the our statement `x = y = z = 1;` is really to be read as

```
```cpp
x = (y = (z = 1));
```
```

Now the expression inside the innermost parentheses, `z = 1` is required to be evaluated first. This not only puts the value 1 into z, but itself evaluates to 1. Now the statement effectively becomes

```
```cpp
x = (y = 1);
```
```

The execution continues by setting y to 1, and then x to 1.

## 3.3 Examples

We consider some simple examples of using the data-types and assignment statements. These do not include the `bool` type which is considered in Section 6.7. Here is a program that reads in the temperature in Centigrade and prints out the equivalent temperature in Fahrenheit.

```
```cpp
main_program{
  double centigrade, fahrenheit;

  cout << "Give temperature in Centigrade: ";
  cin >> centigrade;

  fahrenheit = 32.0 + centigrade * 9.0/5.0;
  cout << "Temperature in Fahrenheit: " << fahrenheit << endl;
}
```
```

Note that the operator `+` is executed last because it has lower precedence than `*` and `/`. The operator `*` executes before `/` because it appears to the left. Note we could have written 9 instead of 9.0. This is because that while multiplying centigrade, it would get converted to a double value anyway, since centigrade is double. Similarly we could have written 5 and 32 instead of 5.0 and 32.0. But what we have written is preferable because it makes it very clear that we are engaging in floating point arithmetic. In the next program you are expected to type in any lowercase letter, and it prints out the same letter in the upper case.
