
In PHP, data input is accomplished using the PHP statement

```
$var_name = trim(fgets(STDIN));
```

where

- $var_name can be any variable.
- STDIN stands for STANDARD INPUT (this is usually the keyboard).
- function trim() is discussed later in this book.

The following code fragment lets the user enter his or her name and age.

```
$name = trim(fgets(STDIN));
$age = trim(fgets(STDIN));
echo "Wow, you are already", age, "years old,", name, "!";
```

It could be even better if, before each data input, a “prompt” message is displayed. This makes the script more user-friendly. For example, look at the following script.

```
echo "What is your name?";
$name = trim(fgets(STDIN));

echo "What is your age?";
$age = trim(fgets(STDIN));

echo "Wow, you are already", age, "years old,", name, "!";
```

The corresponding flowchart fragment looks like this.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_80_0.png)

Now when a user executes your script he or she knows exactly what to enter.

# 6.4 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

1. In PHP, the word `fgets` is a reserved word.
2. The `echo` statement can be used to display a message or the content of a variable.
3. When the `trim(fgets(STDIN))` statement is executed, the flow of execution is interrupted until the user has entered a value.
4. One single statement, `trim(fgets(STDIN))`, can be used to enter multiple data values.
5. Before data input, a prompt message must always be displayed.

# 6.5 Review Questions: Multiple Choice

Select the correct answer for each of the following statements.

1. The statement `echo "Hello"` displays
   - a. the word `Hello` (without the double quotes).
   - b. the word "Hello" (including the double quotes).
   - c. the content of the variable `Hello`.
   - d. none of the above

2. The statement `echo "Hello\nHermes"` displays
   - a. the message `Hello Hermes`.
   - b. the word `Hello` in one line and the word `Hermes` in the next one.
   - c. the message `HelloHermes`.
   - d. the message `Hello\nHermes`.
   - e. none of the above

3. The statement `$data1_data2 = trim(fgets(STDIN))`
   - a. lets the user enter a value and assigns it to variable `$data1`. Variable `$data2` remains empty.
   - b. lets the user enter a value and assigns it to variable `$data1_data2`.
   - c. lets the user enter two values and assigns them to variables `$data1` and `$data2`.
   - d. none of the above

# Chapter 7
Operators

# 7.1 The Value Assignment Operator

The most commonly used operator in PHP is the value assignment operator ( = ). For example, the PHP statement

```
$x = 5;
```

assigns a value of 5 to variable $x.

As you read in Chapter 5, this is equivalent to the left arrow used in flowcharts.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_83_0.png)

Probably the left arrow used in a flowchart is more convenient and clearer than the value assignment operator ( = ) sign because it shows in a more graphical way that the value or the result of an expression on the right is assigned to a variable on the left.

Be careful! The ( = ) sign is not equivalent to the one used in mathematics. In mathematics, the expression x = 5 is read as “x is equal to 5.” However, in PHP the expression $x = 5 is read as “assign the value 5 to x” or “set x equal to 5.” They look the same but they act differently!

In mathematics, the following two lines are equivalent:

```
x = y + z
y + z = x
```

The first one can be read as “x is equal to the sum of y and z” and the second one as “the sum of y and z is equal to x.”

On the other hand, in PHP, the following two statements are definitely not equivalent. In fact, the second one is considered wrong!

```
$x = $y + $z;
$y + $z = $x;
```

The first statement seems quite correct. It can be read as “Set x equal to the sum of y and z” or “Assign the sum of y and z to x.”

But what about the second one? Think! Is it possible to assign the value of x to y + z? The answer is obviously a big “NO!”

> Remember! In PHP, the variable on the left side of the ( = ) sign represents a region in main memory (RAM) where a value can be stored. Thus, on the left side only one single variable must exist! However, on the right side there can be a number, a variable, a string, or even a complex mathematical expression.

In Table 7–1 you can find some examples of value assignments.

# Table 7-1 Examples of Value Assignments

| $a = 9 | Assign a value of 9 to variable $a. |
| $b = $c | Assign the content of variable $c to variable $b. |
| $d = "Hello Zeus" | Assign the string Hello Zeus to variable $d. |
| $d = $a + $b | Calculate the sum of the contents of variables $a and $b and assign the result to variable $d. |
| $b = $a + 1 | Calculate the sum of the content of variable $a and 1 and assign the result to variable $b. Please note that the content of variable $a is not altered. |
| $a = $a + 1 | Calculate the sum of the content of variable $a and 1 and assign the result back to variable $a. In other words, increase variable $a by one. |

Confused about the last one? Are you thinking about your math teacher right now? What would he/she say if you had written a = a + 1 on the blackboard? Can you personally think of a number that is equal to the number itself plus one? Are you nuts? This means that 5 is equal to 6 and 10 is equal to 11!

Obviously, things are different in computer science. The statement $a = $a + 1 is absolutely acceptable! It instructs the CPU to retrieve the value of variable $a from main memory (RAM), to increase the value by one, and to assign the result back to variable $a. The old value of variable $a is replaced by the new one.

Still don’t get it? Let’s take a look at how the CPU and main memory (RAM) cooperate with each other in order to execute the statement A ← A + 1 (this is the same as the statement $a = $a + 1 in PHP).

Let’s say that there is a region in memory, named A and it contains the number 13

![](img/4d9a992abc5da7946ac44f9e6bf1d032_84_0.png)

When a program instructs the CPU to execute the statement
A ← A + 1

the following procedure is executed:

- the number 13 is transferred from the RAM’s region named A to the CPU;
- the CPU calculates the sum of 13 and 1; and
- the result, 14, is transferred from the CPU to the RAM’s region named A replacing the existing number, 13.

After execution, the RAM looks like this.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_85_0.png)

# 7.2 Arithmetic Operators

Just like every high-level programming language, PHP supports almost all types of arithmetic operators.

| Arithmetic Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus (remainder after integer division) |

The first four operators are straightforward and need no further explanation.

The modulus operator (%) returns the remainder of an integer division, which means that

```
$a = 13 % 3
```

assigns a value of 1 to variable $a.

The modulus operator (%) can be used with floating-point numbers as well, but the result is always an integer. For example, the operation

```
$b = 13.4 % 3
```

assigns a value of 1 (and not 1.4, as you may mistakenly expect) to variable $b.

> **Notice:** Please keep in mind that flowcharts are a loose method used to represent an algorithm. Although the use of the modulus (%) operator is allowed in flowcharts, this book uses the commonly accepted MOD operator instead! For example, the PHP statement `$b = 13 % 3` is represented in a flowchart as

![](img/4d9a992abc5da7946ac44f9e6bf1d032_85_1.png)

The order of operations can be summarized as follows:

1. Any operations enclosed in parentheses are performed first.
2. Next, any multiplication and division operations are performed from left to right.
3. In the end, any addition and subtraction operations are performed from left to right.

So, in statement $y = (20 + 3) + 12 + 8 / 4 * 3;

the operations are performed as follows:

1. 20 is added to 3, yielding a result of 23.
2. 8 is divided by 4, yielding a result of 2. This result is then multiplied by 3, yielding a result of 6.
3. 23 is added to 12, yielding a result of 35. This result is then added to 6, yielding a final result of 41.

Next is the same sequence of operations presented in a more graphical way.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_87_0.png)

# 7.4 Compound Assignment Operators

PHP offers a special set of operators known as compound assignment operators, which can help you write code faster.

| Operator | Description | Example | Equivalent to |
|---|---|---|---|
| += | Addition assignment | $a += $b | $a = $a + $b |
| -= | Subtraction assignment | $a -= $b | $a = $a - $b |
| *= | Multiplication assignment | $a *= $b | $a = $a * $b |
| /= | Division assignment | $a /= $b | $a = $a / $b |
| %= | Modulus assignment | $a %= $b | $a = $a % $b |

Looking at the “Equivalent to” column, it becomes clear that same result can be achieved by just using the classic assignment ( = ) operator. So the question that arises here is why do these operators exist?
