# 3.6.7 Displaying the sum with string Interpolation

After the calculation has been performed, line 24

```
Console.WriteLine("Sum is {sum}"); // display sum
```

uses Console.WriteLine to display the sum. C# replaces the interpolation expres-
{sum} with the calculated sum from line 22. So WriteLine displays "Sum is ",nfollowed by the value and a newline.

# 3.6.8 Performing Calculations in Output Statements

Calculations can also be performed in interpolation expressions. We could have combined
the statements in lines 22 and 24 into the statement

```
Console.WriteLine("Sum is {number1 + number2}");
```

# 3.7 Memory Concepts

Variable names as number1,number2 and sum actually correspond to locations in the
computer's memory. Every variable has a name, type, and size (determined by the type)
and a value.
In the addition app of Fig. 3.14, when the statement (line 16)

```
number1 = int.Parse(Console.ReadLine());
```

executes, the number by the user is placed into a memory location to which the
name1 has been assigned by the runtime. Suppose that the user enters 45. The
computer places that integer value into location number, as shown in Fig. 3.15. Whenever-
er value is placed in a memory location, the value replaces the previous value in that lo-
cation—the previous value is destroyed.

| number1 | 45 |

Fig. 3.15 | Memory location showing the name and value of variable number1.

When the statement (line 20)

```
number2 = int.Parse(Console.ReadLine());
```

executes, suppose that the user enters 72. The computer places that integer value into lo-
cationnumber2. The memory now appears as shown in Fig. 3.16.

| number1 | 45 |
| number2 | 72 |

Fig. 3.16 | Memory locations after storing values for number1 and number2.