
![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_104_0.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_104_1.png)

**Figure 1**  
Flowchart for if Statement

**Figure 2**  
Flowchart for if Statement with No else Branch

There is nothing to do in the else branch of the statement. In that case, you can omit it entirely, such as in this example:

```cpp
int actual_floor = floor;

if (floor > 13)
{
    actual_floor--;
}  // No else needed
```

See Figure 2 for the flowchart.

The following program puts the if statement to work. This program asks for the desired floor and then prints out the actual floor.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_104_2.png)

*An if statement is like a fork in the road. Depending upon a decision, different parts of the program are executed.*

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_106_0.png)

- 1. In some Asian countries, the number 14 is considered unlucky. Some building owners play it safe and skip *both* the thirteenth and the fourteenth floor. How would you modify the sample program to handle such a building?
- 2. Consider the following if statement to compute a discounted price:

    ```cpp
    if (original_price > 100)
    {
        discounted_price = original_price - 20;
    }
    else
    {
        discounted_price = original_price - 10;
    }
    ```

    What is the discounted price if the original price is 95? 100? 105?
- 3. Compare this if statement with the one in Self Check 2:

    ```cpp
    if (original_price < 100)
    {
        discounted_price = original_price - 10;
    }
    else
    {
        discounted_price = original_price - 20;
    }
    ```

    Do the two statements always compute the same value? If not, when do the values differ?
- 4. Consider the following statements to compute a discounted price:

    ```cpp
    discounted_price = original_price;
    if (original_price > 100)
    {
        discounted_price = original_price - 10;
    }
    ```

    What is the discounted price if the original price is 95? 100? 105?
- 5. The variables `fuel_amount` and `fuel_capacity` hold the actual amount of fuel and the size of the fuel tank of a vehicle. If less than 10 percent is remaining in the tank, a status light should show a red color; otherwise it shows a green color. Simulate this process by printing out either "red" or "green".

### Practice It

Now you can try these exercises at the end of the chapter: R3.3, R3.4, P3.16.

### Programming Tip 3.1: Brace Layout

Programmers vary in how they align braces in their code. In this book, we follow the simple rule of making { and } line up.

```cpp
if (floor > 13)
{
   floor--;
}
```

This style makes it easy to spot matching braces.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_106_1.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_106_2.png)

*Properly lining up your code makes your programs easier to read.*

Some programmers put the opening brace on the same line as the if:

```cpp
if (floor > 13) {
    floor--;
}
```

This style makes it harder to match the braces, but it saves a line of code, allowing you to view more code on the screen without scrolling. There are passionate advocates of both styles.

It is important that you pick a layout style and stick with it consistently within a given programming project. Which style you choose may depend on your personal preference or a coding style guide that you need to follow.

### Programming Tip 3.2: Always Use Braces

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_107_0.png)

When the body of an if statement consists of a single statement, you need not use braces. For example, the following is legal:

```cpp
if (floor > 13)
    floor--;
```

However, it is a good idea to always include the braces:

```cpp
if (floor > 13)
{
    floor--;
}
```

The braces make your code easier to read, and you are less likely to make errors such as the one described in Common Error 3.1.

### Common Error 3.1: A Semicolon After the if Condition

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_107_1.png)

The following code fragment has an unfortunate error:

```cpp
if (floor > 13) ; // ERROR
{
    floor--;
}
```

There should be no semicolon after the if condition. The compiler interprets this statement as follows: If floor is greater than 13, execute the statement that is denoted by a single semicolon, that is, the do-nothing statement. The statement enclosed in braces is no longer a part of the if statement. It is always executed. Even if the value of floor is not above 13, it is decremented.

Placing a semicolon after the else reserved word is also wrong:

```cpp
if (floor > 13)
{
    actual_floor = floor - 1;
}
else ;
{
    actual_floor = floor;
}
```

In this case, the do-nothing statement is executed if floor > 13 is not fulfilled. This is the end of the if statement. The next statement, enclosed in braces, is executed in both cases; that is, actual_floor is always set to floor.

### Programming Tip 3.3: Tabs

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_108_0.png)

Block-structured code has the property that nested statements are indented by one or more levels:

```cpp
int main()
{
    int floor;
    ...
    if (floor > 13)
    {
        floor--;
    }
    ...
    return 0;
}
```

0 1 2  Indentation level

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_108_1.png)

How do you move the cursor from the leftmost column to the appropriate indentation level? A perfectly reasonable strategy is to hit the space bar a sufficient number of times. However, many programmers use the Tab key instead. A tab moves the cursor to the next indentation level.

While the Tab key is nice, some editors use tab characters for alignment, which is not so nice. Tab characters can lead to problems when you send your file to another person or a printer. There is no universal agreement on the width of a tab character, and some software will ignore tabs altogether. It is therefore best to save your files with spaces instead of tabs. Most editors have a setting to automatically convert all tabs to spaces. Look at the documentation of your development environment to find out how to activate this useful setting.

### Special Topic 3.1: The Selection Operator

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_108_2.png)

C++ has a selection operator of the form

```cpp
condition ? value1 : value2
```

The value of that expression is either *value1* if the test passes or *value2* if it fails. For example, we can compute the actual floor number as

```cpp
actual_floor = floor > 13 ? floor - 1 : floor;
```

which is equivalent to

```cpp
if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}
```

You can use the selection operator anywhere that a value is expected, for example:

```cpp
cout << "Actual floor: " << (floor > 13 ? floor - 1 : floor);
```

We don't use the selection operator in this book, but it is a convenient construct that you will find in many C++ programs.

### Programming Tip 3.4: Avoid Duplication in Branches

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_109_0.png)

Look to see whether you duplicate code in each branch. If so, move it out of the if statement. Here is an example of such duplication:

```cpp
if (floor > 13)
{
   actual_floor = floor - 1;
   cout << "Actual floor: " << actual_floor << endl;
}
else
{
   actual_floor = floor;
   cout << "Actual floor: " << actual_floor << endl;
}
```

The output statement is exactly the same in both branches. This is not an error—the program will run correctly. However, you can simplify the program by moving the duplicated statement, like this:

```cpp
if (floor > 13)
{
   actual_floor = floor - 1;
}
else
{
   actual_floor = floor;
}
cout << "Actual floor: " << actual_floor << endl;
```

Removing duplication is particularly important when programs are maintained for a long time. When there are two sets of statements with the same effect, it can easily happen that a programmer modifies one set but not the other.

## 3.2 Comparing Numbers and Strings

Relational operators (`< > <= >= == !=`) are used to compare numbers and strings.

Every if statement contains a condition. In many cases, the condition involves comparing two values. For example, in the previous examples we tested `floor > 13`. The comparison `>` is called a relational operator. C++ has six relational operators (see Table 1).

As you can see, only two C++ relational operators (`>` and `<`) look as you would expect from the mathematical notation. Computer keyboards do not have keys for ≥, ≤, or ≠, but the `>=`, `<=`, and `!=` operators are easy to remember because they look similar. The `==` operator is initially confusing to most newcomers to C++. In C++, `=` already has a meaning, namely assignment.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_109_1.png)

In C++, you use a relational operator to check whether one value is greater than another.
