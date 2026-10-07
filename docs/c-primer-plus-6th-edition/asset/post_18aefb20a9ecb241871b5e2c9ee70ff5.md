
# The do while Loop

You've now seen the for loop and the while loop. The third C++ loop is the do while. It's different from the other two because it's an exit-condition loop. That this devil-may-care loop first executes the body of the loop and only then evaluates the expression to see whether it should continue looping. If the condition evaluates to false, the loop terminates; otherwise, a new cycle of execution and testing begins. Such a loop always executes at least once because its program flow must pass through the body of the loop before reaching the test. Here's the syntax for the do while loop:

```
do
  body
while (test-expression);
```

The body portion can be a single statement or a brace-delimited statement block. Figure 5.4 summarizes the program flow for do while loops.

![](img/cd111a87c1db9aff4db4b18834327463_245_0.png)

Usually, an entry-condition loop is a better choice than an exit-condition loop because the entry-condition loop checks before looping. For example, suppose Listing 5.13 used

do while instead of while. In that case, the loop would print the null character and its code before finding that it had already reached the end of the string. Sometimes a do while test does make sense. For example, if you're requesting user input, the program has to obtain the input before testing. Listing 5.15 shows how to use do while in such a situation.

Listing 5.15 dumpfile.cpp

```cpp// dowhile.cpp -- exit-condition loop
#include <iostream>
int main()
{
    using namespace std;
    int n;

    cout << "Enter numbers in the range 1-10 to find *";
    cout << "*my favorite number\n";
    do
    {
        cin >> n;      // execute body
    } while (n != 7); // then test
    cout << "Yes, 7 is my favorite.\n";
    return 0;
}
```

Here's a sample run of the program in Listing 5.15:

Enter numbers in the range 1-10 to find my favorite

9

4

7

Yes, 7 is my favorite.

# Strange for loops

It's not terribly common, but you may occasionally see code that resembles the following:

```cpp
int I = 0;
for(;;) // sometimes called a "forever loop"
{
    I++;
    // do something ...
    if (30 >= I) break; // if statement and break (Chapter 6)
}
```

Or here is another variation:

```cpp
int I = 0;
for(;;I++)
{
if (30 >= I) break;
// do something ...
```

The code relies on the fact that an empty test condition in a for loop is treated as being true. Neither of these examples is easy to read, neither should be used as a general model of writing a loop. The functionality of the first example can be more clearly expressed in a do while loop:

```cpp
int I = 0;
do {
  I++;
  // do something;
} while (30 > I);
```

Similarly, the second example can be expressed more clearly as a while loop:

```cpp
while (I < 30)
{
  // do something
  I++;
}
```

In general, clearly understood code is a more useful goal than demonstrating the ability to exploit obscure features of the language.

# The Range-Based Loop (C++11)

The C++11 adds a new form of loop called the range-based loop. It simplifies its common loop task—that of doing something with each element of an array, or more generally, one of the container classes, such as vector or array. Here is an example:

```cpp
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices)
cout << x << std::endl;
```

Here x initially represents the first member of the prices array. After displaying the first element, the loop then cycles x to represent the remaining elements of the array in turn, this code would print all five members, one per line. In short, the loop displays every value included in the range of array.

To modify values, need a different syntax for the loop variable:

```cpp
for (double &x : prices)
  x = x * 0.80; //off sale
```

The symbol identifies x as a reference variable, a topic we'll discuss in Chapter 8, "Adventures in Functions.\ The significance is that this form of declaration allows the subsequent code to modify the array contents, which the first form doesn't.

The range-based loop can also be used with initialization lists:

```cpp
for (int x : {3, 5, 2, 8, 6})
cout << x << " ";
cout << '\n';
```

However, this loop likely be used most often with the various template container classes discussed in Chapter 16.

# Loops and Text Input

Now that you've seen how loops work, let's look at one of the most common and important tasks assigned to loops: reading text input. For example, you might want to write a program that counts the number of characters, lines, and words in the input. Traditionally, C++, like C, uses the while loop for this sort of task. We'll next investigate how that is done. If you already know C, don't skip through the following sections not too fast. Although the C++ while loop is the same as C's, C++s I/O facilities are different. This can give the C++ loop a somewhat different look from the C loop. In fact, the cin object supports three distinct modes of single-character input, each with a different user interface. Let's look at how to use these choices with while loops.

# Using Unadored cin for Input

If a program is going to use a loop to read text from the keyboard, it has to have some way of knowing when to stop. How can it know when to stop? One way is to choose some special character, sometimes called a sentinel character, to act as a stop sign. For example, Listing 5.16 reads input when the program encounters a # character. The program counts the number of characters and reads them then, it redis-plays the characters that have been read. (Pressing a keyboard key doesn't automatically place a character onscreen; programs have to do that work by echoing the input character. Typically, the operating system handles that task. In this case, both the operating system and the test program echo the input.) When it is finished, the program reports the total number of characters processed. Listing 5.16 shows the program.

Listing 5.16 textint.cpp

```cpp// textint.cpp reading chars with a while loop
#include <iostream>
int main()
{
    using namespace std;
    char ch;
    int count = 0; // use basic input
    cout << "Enter characters; enter # to quit:\n"
    cin >> ch; // get a character
    while (ch != '#') // test the character
    {
        cout << ch; // echo the character
        ++count; // count the character
        cin >> ch; // get the next character
    }
}
```

# Loops and Text Input

```cpp
cout << endl << count << " characters read\n";nreturn 0;
}
```

Here's a sample run of the program in Listing 5.16.

Enter characters; enter # to quit:
see ken#really fast
seek
9 characters read

Apparently, Ken runs so fast he obliterates itself—at least the spaces in the input.

# Program Notes

Note the structure of the program in Listing 5.16. The program reads the first character before it reaches the loop. That way, the first character can be tested when the program reaches the loop statement. This is important because the first character must be #. Because textinicpp uses an entry-condition, the program skips the loop in that case. Because the variable count was previously set to 0, count has the correct value.

Suppose the first character is not #. In that case, the program enters the loop, displays the character, increments the count, and reads the next character. This last step is vital. Without it, the loop repeats processes the first character.With the last step, the program advances to the next character.

Note that the loop design follows the guidelines mentioned earlier. The condition that terminates the loop is if the last character is not #. That condition is initialized by reading a character before the loop starts. The condition is updated by reading a new character at the end of the loop.

This sounds reasonable. Why does the program omit the spaces on output? Blame cin. When reading char values, just as reading basic types, cin skips over spaces and newlines. The spaces in the input are not echoed, so they are not counted.

# cin.get(char) to the Rescue

Usually, programs that read input character-by-character examine every character, including spaces, tabs, and newlines.The istream class (defined in iostream),to cin belongs, includes member functions that meet this need. In particular, the member function cin.get(ch) reads the next character, even if it is a space, from the input and
