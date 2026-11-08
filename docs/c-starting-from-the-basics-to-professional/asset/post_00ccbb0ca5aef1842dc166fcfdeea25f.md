
The variable x will be assigned a value from the values array on each iteration. It will be assigned values 2, 3, 5, and so on, in succession. Thus, the loop will accumulate the sum of all the elements in the values array in total. The variable x is local to the loop and does not exist outside of it.

A braced initializer list itself is a valid range, so you could write the previous code even more compactly as follows:

```cpp
int total {};
for (int x : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29})
    total += x;
```

Of course, the compiler knows the type of the elements in the values array, so you could also let the compiler determine the type for x by writing the former loop like this:

```cpp
for (auto x : values)
    total += x;
```

Using the auto keyword causes the compiler to deduce the correct type for x. The auto keyword is used often with the range-based for loop. This is a nice way of iterating over all the elements in an array or other kind of range. You don’t need to be aware of the number of elements. The loop mechanism takes care of that.

Note that the values from the range are assigned to the range variable, x. This means you cannot modify the elements of values by modifying the value of x. For example, this doesn’t change the elements in the values array:

```cpp
for (auto x : values)
    x += 2;
```

This just adds 2 to the local variable, x, not to the array element. The value stored in x is overwritten by the value of the next element from values on the next iteration. In the next chapter, you’ll learn how you can change values within a range-based for loop by using a reference variable.

## The while Loop

The while loop uses a logical expression to control execution of the loop body. Figure 5-3 shows the general form of the while loop.

```cpp
// Output column headings
std::cout << std::format(table_format, "integer", "sum", "factorial");

unsigned int n {};
unsigned int sum {};
unsigned long long factorial {1ULL};

while (++n <= limit)
{
    sum += n;                         // Accumulate sum to current n
    factorial *= n;                   // Calculate n! for current n
    std::cout << std::format(table_format, n, sum, factorial);
}
```

The output from this program is the same as Ex5_04.cpp. The variables n, sum, and factorial are defined before the loop. Here the types of the variables can be different, so n and sum are defined as unsigned int. The maximum value that can be stored in factorial is limited, so this remains as type unsigned long long. Because of the way the calculation is implemented, the counter n is initialized to zero. The while loop condition increments n and then compares the new value with limit. The loop continues as long as the condition is true, so the loop executes with values of n from 1 up to limit. When n reaches limit+1, the loop ends. The statements within the loop body are the same as in Ex5_04.cpp.

> **Note**  Any for loop can be written as an equivalent while loop, and vice versa. For instance, a for loop has the following generic form:

```cpp
for (initialization; condition; iteration)
    body
```

This can typically be written using a while loop as follows:

```cpp
{
    initialization;
    while (condition)
    {
        body
        iteration;
    }
}
```

The while loop needs to be surrounded by an extra pair of curly braces to emulate the way the variables declared in the initialization code are scoped by the original for loop.

```cpp
// Make sure table size is within the limits
if (table < table_min || table > table_max)
{
    std::cout << "Invalid table size entered. Program terminated." << std::endl;
    return 1;
}

// Create the top line of the table
std::cout << std::format("{:>6}", '|');
for (size_t i {1}; i <= table; ++i)
{
    std::cout << std::format("{:3} |", i);
}
std::cout << std::endl;

// Create the separator row
for (size_t i {}; i <= table; ++i)
{
    std::cout << "------";
}
std::cout << std::endl;

for (size_t i {1}; i <= table; ++i)
{
    // Iterate over rows
    std::cout << std::format("{:3} |", i);       // Start the row

    // Output the values in a row
    for (size_t j {1}; j <= table; ++j)
    {
        std::cout << std::format("{:3} |", i*j); // For each column
    }
    std::cout << std::endl;                       // End the row
}

// Check if another table is required
std::cout << "\nDo you want another table (y or n)? ";
std::cin >> reply;

} while (std::tolower(reply) == 'y');
}
```

Here's an example of the output:

```text
What size table would you like (2 to 12)? 4
     |  1 |  2 |  3 |  4 |
-----+----+----+----+----
  1  |  1 |  2 |  3 |  4 |
  2  |  2 |  4 |  6 |  8 |
  3  |  3 |  6 |  9 | 12 |
  4  |  4 |  8 | 12 | 16 |
```

## Skipping Loop Iterations

Situations arise where you want to skip one loop iteration and press on with the next. The continue statement does this:

```cpp
continue;      // Go to the next iteration
```

When this statement executes within a loop, execution transfers immediately to the end of the current iteration. As long as the loop control expression allows it, execution continues with the next iteration. This is best understood in an example. Let’s suppose you want to output a table of characters with their character codes in hexadecimal and decimal formats. Of course, you don’t want to output characters that don’t have a graphical representation—some of these, such as tabs and newline, would mess up the output. So, the program should output just the printable characters. Here’s the code:

```cpp
// Ex5_08.cpp
// Using the continue statement to display ASCII character codes
import <iostream>;
import <format>;
#include <cctype>

int main()
{
  const auto header_format = "{:^11}{:^11}{:^11}\n";     // 3 cols., 11 wide, centered (^)
  const auto body_format = "{:^11}{:0^11X}{:0^11d}\n";   // Print same argument three times

  std::cout << std::format(header_format, "Character", "Hexadecimal", "Decimal");

  // Output 7-bit ASCII characters and corresponding codes
  char ch{};
  do
  {
    if (!std::isprint(ch))  // If it's not printable...
      continue;             // ...skip this iteration
    std::cout << std::format(body_format, ch);
  } while (ch++ < 127);
}
```

This displays a handy table of the codes for all 95 printable ASCII characters. From Chapter 1 you may recall that ASCII is a 7-bit encoding, meaning all ASCII code values lie between 0 and 127 (both inclusive).

| Character | Hexadecimal | Decimal |
|---|---|---|
|  | 20 | 32 |
| ! | 21 | 33 |
| " | 22 | 34 |
| # | 23 | 35 |
| ⋮ |  |  |
| } | 7D | 125 |
| ~ | 7E | 126 |

The format strings at the top of the main() function are used to generate a table with three columns, each of width 11 and each with their values centered (as dictated by the ^ alignment options). Note that even though the table has three columns, we pass only one single argument to the std::format() expression in the do-while loop. In body_format, we use the positional argument identifier 0 (to the left of the columns) to print out this one argument three times: once as a letter, once as an uppercase hexadecimal number (thanks to the X suffix), and once as a decimal number (thanks to the d suffix, which could be omitted, as decimal output is the default).

The interesting bit here, however, is of course the (conditional) continue statement. You don't want to output details of characters that do not have printable representations. The isprint() function declared in <cctype> can help with that: it only returns true for printable characters. Thus, the expression in the if statement will be true when ch contains the code for a character that is not printable. In this case, the continue statement executes, which skips the rest of the code in the current loop iteration.

It is worth noting that the straightforward for loop isn't suitable here. That is: a natural first attempt at the program's loop would be this for loop:

```cpp
for (char ch {}; ch <= 127; ++ch)
{
    // Output character and code...
}
```

Sadly, this naïve loop never ends on systems where char is a signed type. After all, for signed char, 127 is the largest possible value, so ch <= 127 will always be true. In the original do-while loop, the condition was checked after the loop's body executed, and before incrementing ch (thanks to the post-increment expression). The condition of the naïve for loop, however, is checked before the body executes, and after incrementing ch.

Nevertheless, it's very tempting to write a for loop like this. Believe us, you'll fall into this trap (or one similar to it) at least once in your career. So take care not to write stop conditions that are always true!

You could alternatively make the for loop work by using type int for the control variable and then casting that value to type char when passing it to std::format().

### Breaking Out of a Loop

Sometimes, you need to end a loop prematurely; something might arise within the loop statement that indicates there is no point in continuing. In this case, you can use the break statement. Its effect in a loop is much the same as it is in a switch statement: executing a break statement within a loop ends the loop immediately, and execution continues with the statement following the loop. The break statement is often used with an indefinite loop, so let's look next at what one of those looks like.

### Indefinite Loops

An indefinite loop can potentially run forever. Omitting the second control expression in a for loop results in a loop that potentially executes an unlimited number of iterations. There has to be some way to end the loop within the loop block itself; otherwise, the loop repeats indefinitely.

Indefinite loops have many practical uses, such as programs that monitor some kind of alarm indicator, for instance, or that collect data from sensors in an industrial plant. An indefinite loop can be useful when you don't know in advance how many loop iterations will be required, such as when you are reading a variable quantity of input data. In these circumstances, you code the exit from the loop within the loop block, not within the loop control expression.
