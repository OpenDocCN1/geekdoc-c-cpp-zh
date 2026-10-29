
D as 1, and E as 2. Product B was not rated. The third customer rated C as 5, D as 1, and E as 3. The third customer did not rate A or B.

Create a text file in this format with sample ratings. Then write a program that reads in the text file and uses the first line to determine the number of products. The program should output the average rating for each product. Customers that did not rate a product should not be considered when computing the average rating for that product. The easiest solution to process the data may be to use the getline function with a comma as a delimiter and to create vectors or dynamic arrays to store the count and sum of the ratings. Your program should work with an arbitrary number of products and customer ratings.

![](img/c76bba8c1d927f399768ffe2ab5f5bee_604_0.png)

# 25.

One problem using cin to read directly into a variable such as an int is that if the user enters non-integer data then the program will continue with erroneous data and usually crash. A solution to this problem is to input data as a string, perform input validation, and then convert the string to an integer. Write a function that prompts the user to enter an integer. The program should use getline to read the user's input into a string. Then use the stringstream class to extract an integer from the string. If an integer cannot be extracted then the user should be prompted to try again. The function should return the extracted integer.

> After a lecture on cosmology and the structure of the solar system, William James was accosted by a little old lady.
> "Your theory that the sun is the center of the solar system, and the earth is a ball which rotates around it has a very convincing ring to it, Mr. James, but it's wrong. I've got a better theory," said the little old lady.
> "And what is that, madam?" inquired James politely.
> "That we live on a crust of earth which is on the back of a giant turtle."
> Not wishing to demolish this absurd little theory by bringing to bear the masses of scientific evidence he had at his command, James decided to gently dissuade his opponent by making her see some of the inadequacies of her position.
> "If your theory is correct, madam," he asked, "what does this turtle stand on?"
> "You're a very clever man, Mr. James, and that's a very good question" replied the little old lady, "but I have an answer to it. And it is this: the first turtle stands on the back of a second, far larger, turtle, who stands directly under him."
> "But what does this second turtle stand on?" persisted James patiently.
> To this the little old lady crowed triumphantly. "It's no use, Mr. James — it's turtles all the way down."
> J. R. R. TOSS, Constraints on Variables in Syntax. MIT Press, 1967

## Introduction

A function definition that includes a call to itself is said to be recursive. Like most modern programming languages, C++ allows functions to be recursive. If used with a little care, recursion can be a useful programming technique. This chapter introduces the basic techniques needed for defining successful recursive functions. There is nothing in this chapter that is truly unique to C++. If you are already familiar with recursion, you can safely skip this chapter.

This chapter uses material from Chapters 1 to 5 only. Sections 13.1 and 13.2 do not use any material from Chapter 5, so you can cover recursion any time after Chapter 4. If you have not read Chapter 11, you may find it helpful to review the section of Chapter 1 on namespaces.

## 13.1 Recursive void Functions

> I remembered too that night which is at the middle of the Thousand and One Nights when Scheherazade (through a magical oversight of the copyist) begins to relate word for word the story of the Thousand and One Nights, establishing the risk of coming once again to the night when she must repeat it, and thus to infinity.

> JORGE LUIS BORGES, "The Garden of Forking Paths" Trans. Anthony Boucher, 1948

When you are writing a function to solve a task, one basic design technique is to break the task into subtasks. Sometimes it turns out that at least one of the subtasks is a smaller example of the same task. For example, if the task is to search a list for a particular value, you might divide this into the subtask of searching the first half of the list and the subtask of searching the second half of the list. The subtasks of searching the halves of the list are "smaller" versions of the original task. Whenever one subtask is a smaller version of the original task to be accomplished, you can solve the original task using a recursive function. We begin with a simple example to illustrate this technique.

## Recursion

In C++ a function definition may contain a call to the function being defined. In such cases the function is said to be recursive.

## EXAMPLE: Vertical Numbers

Display 13.1 contains a demonstration program for a recursive function named writeVertical that takes one (nonnegative) int argument and writes that int to the screen, with the digits going down the screen one per line. For example, the invocation

```
writeVertical(1234);
```

would produce the output

```
1
2
3
4
```

The task to be performed by writeVertical may be broken down into the following two cases:

- Simple case: If n < 10, then write the number n to the screen. After all, if the number is only one digit long, the task is trivial.

## Display 13.1 A Recursive void Function

```
1 //Program to demonstrate the recursive function writeVertical.
2 #include <iostream>
3 using std::cout;
4 using std::endl;
5 
6 void writeVertical(int n);
7 //Precondition: n >= 0.
8 //Postcondition: The number n is written to the screen vertically,
9 //with each digit on a separate line.
10 
11 int main()
12 {
13     cout << "writeVertical(3):" << endl;
14     writeVertical(3);
15 
16     cout << "writeVertical(12):" << endl;
17     writeVertical(12);
18 
19     cout << "writeVertical(123):" << endl;
20     writeVertical(123);
21 
22     return 0;
23 }
24 
25 //uses iostream:
26 void writeVertical(int n)
27 {
28     if (n < 10)
29     {
30         cout << n << endl;
31     }
32     else //n is two or more digits long:
33     {
34         writeVertical(n / 10);
35         cout << (n % 10) << endl;
36     }
37 }
```

## Sample Dialogue

```
writeVertical(3):
3
writeVertical(12):
1
2
writeVertical(123):
1
2
3
```

## Tracing a Recursive Call

Let's see exactly what happens when the following function call is made (as in Display 13.1):

```
writeVertical(123);
```

When this function call is executed, the computer proceeds just as it would with any function call. The argument 123 is substituted for the parameter n, and the body of the function is executed. After the substitution of 123 for n, the code to be executed is equivalent to the following:

```
if (123 < 10)
{
    cout << 123 << endl;
}
else //n is two or more digits long:
{
    writeVertical(123 / 10);
    cout << (123 % 10) << endl;
}
```

Since 123 is not less than 10, the else part is executed. However, the else part begins with the function call

```
writeVertical(n / 10);
```

which (since n is equal to 123) is the call

```
writeVertical(123 / 10);
```

which is equivalent to

```
writeVertical(12);
```

When execution reaches this recursive call, the current function computation is placed in suspended animation and the recursive call is executed. When this recursive call is finished, the execution of the suspended computation will return to this point and the suspended computation will continue from there.

The recursive call

```
writeVertical(12);
```

is handled just like any other function call. The argument 12 is substituted for the parameter n, and the body of the function is executed. After substituting 12 for n, there are two computations, one suspended and one active, as follows:

```
if (123 < 10)
{
    cout <<
}
else // n i
{
    writeV
    cout <<
}

if (12 < 10)
{
    cout << 12 << endl;
}
else // n is two or more digits long:
{
    writeVertical(12 / 10);
    cout << (12 % 10) << endl;
}
```

Computation will stop here until the recursive call returns.

Since 12 is not less than 10, the else part is executed. However, as you already saw, the else part begins with a recursive call. The argument for the recursive call is n / 10, which in this case is equivalent to 12 / 10. So this second computation of the function writeVertical is suspended and the following recursive call is executed:

writeVertical(12 / 10);

which is equivalent to

writeVertical(1);

At this point there are two suspended computations waiting to resume, and the computer begins to execute this new recursive call, which is handled just like all the previous recursive calls. The argument 1 is substituted for the parameter n, and the body of the function is executed. At this point, the computation looks like the following:

```
if (123 < 10)
{
    c
}
else
{
    w
    c
}

if (12 < 10)
{
}
else
{
}

if (1 < 10)
{
    cout << 1 << endl;
}
else // n is two or more digits long:
{
    writeVertical(1 / 10);
    cout << (1 % 10) << endl;
}
```

No recursive call this time
