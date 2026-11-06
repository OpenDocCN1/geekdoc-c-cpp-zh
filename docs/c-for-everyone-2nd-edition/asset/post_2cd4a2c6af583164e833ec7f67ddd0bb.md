
**Practice It** Now you can try these exercises at the end of the chapter: R4.10, P4.6, P4.7.

## Special Topic 4.1: Clearing the Failure State

![](img/23fb3582e93ebc95909e1de029c3d388_180_0.png)

When an input operation has failed, all further input operations also fail. If you want to read two number sequences and use a letter as a sentinel, you need to clear the failure state after reading the first sentinel. Call the `clear` function:

```cpp
cout << "Enter values, Q to quit.\n";
while (cin >> values)
{
   Process input.
}
cin.clear();
```

Suppose the user has entered 30 10 5 Q. The input of Q has caused the failure. Because only successfully processed characters are removed from the input, the Q character is still present. Read it into a dummy variable:

```cpp
string sentinel;
cin >> sentinel;
```

Now you can go on and read more inputs.

## Special Topic 4.2: The Loop-and-a-Half Problem and the break Statement

![](img/23fb3582e93ebc95909e1de029c3d388_180_1.png)

Some programmers dislike loops that are controlled by a Boolean variable, such as:

```cpp
bool more = true;
while (more)
{
   cin >> value;
   if (cin.fail())
   {
      more = false;
   }
   else
   {
      Process value.
   }
}
```

The actual test for loop termination is in the middle of the loop, not at the top. This is called a **loop and a half** because one must go halfway into the loop before knowing whether one needs to terminate.

As an alternative, you can use the `break` reserved word.

```cpp
while (true)
{
   cin >> value;
   if (cin.fail()) { break; }
   Process value.
}
```

The `break` statement breaks out of the enclosing loop, independent of the loop condition.

In the loop-and-a-half case, `break` statements can be beneficial. But it is difficult to lay down clear rules as to when they are safe and when they should be avoided. We do not use the `break` statement in this book.

Figure 6 Storyboard for the Design of a Web Application

![](img/23fb3582e93ebc95909e1de029c3d388_182_0.png)

What if there is more than one quantity? A user may have a whole table of centimeter values that should be converted into inches.

What if the user enters units that our program doesn't know how to handle, such as angstrom?

What if the user asks for impossible conversions, such as inches to gallons?

Let's get started with a storyboard panel. It is a good idea to write the user inputs in a different color. (Underline them if you don't have a color pen handy.)

```
Converting a Sequence of Values

What unit do you want to convert from? cm
What unit do you want to convert to? in
Enter values, terminated by zero        — Allows conversion of multiple values
30
30 cm = 11.81 in
100
100 cm = 39.37 in                          — Format makes clear what got converted
0
What unit do you want to convert from?
```

The storyboard shows how we deal with a potential confusion. A user who wants to know how many inches are 30 centimeters may not read the first prompt carefully and specify inches. But then the output is “30 in = 76.2 cm”, alerting the user to the problem.

The storyboard also raises an issue. How is the user supposed to know that “cm” and “in” are valid units? Would “centimeter” and “inches” also work? What happens

- 27. Google has a simple interface for converting units. You just type the question, and you get the answer.

  ![](img/23fb3582e93ebc95909e1de029c3d388_184_0.png)

  Make storyboards for an equivalent interface in a C++ program. Show the “happy day” scenario in which all goes well, and show the handling of two kinds of errors.

- 28. Consider a modification of the program in Self Check 26. Drop the lowest score before computing the average. Provide a storyboard for the situation in which a user only provides one score.

- 29. What is the problem with implementing the following storyboard in C++?

  ```
  Computing Multiple Averages
  Enter scores: 90 80 90 100 80
  The average is 88
  Enter scores: 100 70 70 100 80
  The average is 88
  Enter scores: -1        -1 is used as a sentinel to exit the program
  (Program exits)
  ```

- 30. Produce a storyboard for a program that compares the growth of a $10,000 investment for a given number of years under two interest rates.

**Practice It** Now you can try these exercises at the end of the chapter: R4.17, R4.18, R4.19.

## 4.7 Common Loop Algorithms

In the following sections, we discuss some of the most common algorithms that are implemented as loops. You can use them as starting points for your loop designs.

### 4.7.1 Sum and Average Value

Computing the sum of a number of inputs is a very common task. Keep a *running total*: a variable to which you add each input value. Of course, the total should be initialized with 0.

```cpp
double total = 0;
double input;
while (cin >> input)
{
    total = total + input;
}
```

To compute an average, keep a total and a count of all values. To compute an average, count how many values you have, and divide by the count. Be sure to check that the count is not zero.

```cpp
double total = 0;
int count = 0;
double input;
while (cin >> input)
{
    total = total + input;
    count++;
}
double average = 0;
if (count > 0) average = total / count;
```

### 4.7.2 Counting Matches

To count values that fulfill a condition, check all values and increment a counter for each match.

You often want to know how many values fulfill a particular condition. For example, you may want to count how many spaces are in a string. Keep a counter, a variable that is initialized with 0 and incremented whenever there is a match.

```cpp
int spaces = 0;
for (int i = 0; i < str.length(); i++)
{
    string ch = str.substr(i, 1);
    if (ch == " ")
    {
        spaces++;
    }
}
```

For example, if str is the string "My Fair Lady", spaces is incremented twice (when i is 2 and 7).

Note that the spaces variable is declared outside the loop. We want the loop to update a single variable. The ch variable is declared inside the loop. A separate variable is created for each iteration and removed at the end of each loop iteration.

This loop can also be used for scanning inputs. The following loop reads text, a word at a time, and counts the number of words with at most three letters:

```cpp
int short_words = 0;
string input;
while (cin >> input)
{
    if (input.length() <= 3)
    {
        short_words++;
    }
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_185_0.png)

In a loop that counts matches, a counter is incremented whenever a match is found.

*To find the height of the tallest bus rider, remember the largest value so far, and update it whenever you see a taller one.*

![](img/23fb3582e93ebc95909e1de029c3d388_187_0.png)

To compute the smallest value, simply reverse the comparison:

```cpp
double smallest;
cin >> smallest;
double input;
while (cin >> input)
{
    if (input < smallest)
    {
        smallest = input;
    }
}
```

### 4.7.5 Comparing Adjacent Values

When processing a sequence of values in a loop, you sometimes need to compare a value with the value that just preceded it. For example, suppose you want to check whether a sequence of inputs contains adjacent duplicates such as 1 7 2 9 9 4 9. Now you face a challenge. Consider the typical loop for reading a value:

```cpp
double input;
while (cin >> input)
{
    // Now input contains the current input
    ...
}
```

To compare adjacent inputs, store the preceding input in a variable.

How can you compare the current input with the preceding one? At any time, input contains the current input, overwriting the previous one. The answer is to store the previous input, like this:

```cpp
double input;
double previous;
while (cin >> input)
{
    if (input == previous) { cout << "Duplicate input" << endl; }
    previous = input;
}
```
