
You can also do something similar with characters. The following code snippet adds a single character to a string:

```cpp
string mystring;
mystring = "abcdef";
mystring += 'g';
cout << mystring << endl;
```

This code creates a string with "abcdef" and then adds a 'g' character to the end to get "abcdefg". Then it writes the full "abcdefg" to the console.

## Adding two strings

You can take two strings and add them together by using a + sign, just as you can do with integers. The final result is a string that is simply the two strings pushed together, side by side. For example, the following code adds first to second to get a string called third:

```cpp
string first = "hello ";
string second = "there";
string third = first + second;
cout << third << endl;
```

This code prints the value of third, which is simply the two strings pushed together — in other words, "hello there". (Notice that the string called first has a space at its end, which is inside quotes and, therefore, part of the string.) You can also add a string constant (that is, an actual string in your application surrounded by quotes) to an existing string variable, as shown here:

```cpp
string first = "hello ";
string third = first + "there";
cout << third << endl;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_116_0.png)

You may be tempted to try to add two string constants together, like so:

```cpp
string bigstring = "hello " + "there";
cout << bigstring << endl;
```

Unfortunately, this won't work. The reason is that (deep down inside its heart) the compiler just wants to believe that a string constant and a string are fundamentally different. But really, you don’t have a good reason to do this, because you can accomplish the same thing with this code:

```cpp
string bigstring = "hello there";
cout << bigstring << endl;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_117_0.png)

You can do a lot more with strings. But first, you need to understand something called a function. If you’re curious about functions, read Book 1, Chapter 6, which covers all the nitty-gritty details.

## Making Decisions Using Conditional Operators

One of the most important features of computers, besides allowing you to surf the web and allowing telemarketers to dial your telephone automatically while you’re eating, is the capability to make comparisons. Although this topic may not seem like a big deal, computer technology did not start to take off until the engineers realized that computers could become much more powerful if they could test a situation and do one task or another task, depending on the situation.

You can use many ways to write a C++ application that can make decisions; see Book 1, Chapter 5, for a discussion about this topic. But one way that is quite handy is the use of the *conditional operator*.

Think about this process: If two integer variables are equal, set a string variable to the string "equal". Otherwise, set it to the string "not equal". In other words, suppose that you have two integer variables, called first and second. first has the value 10 in it, and second has the value 20 in it. You also have a string variable called result. Now, to follow the little process just described: Are the two variables equal? No, they are not, so you set result to the string "not equal".

Now do this in C++. Look carefully at the following code. First, you declare the variables first, second, and result:

```cpp
int first = 10;
int second = 20;
string result;
```

So far, so good. Notice that you didn’t yet initialize the string variable result. But now you’re going to write a single line of code that performs the process just described. First, look over the following example, and see whether you can figure out what it’s doing. Look carefully at the variables and what they may do, based on the process described earlier. Then the text explains what the code does.

```cpp
result = (first == second) ? "equal" : "not equal";
```

The preceding line is probably one of the more bizarre-looking lines of C++ code that you’ll see in this book. First, you discover what it means. Then you break it into parts to understand why it means what it does.

In English, this means result gets "equal" if first is equal to second; otherwise, it gets "not equal".

Now break it into two parts. A single equals sign indicates that the left side, result, receives what is on the right side. So you need to figure out that crazy business on the right side:

```cpp
(first == second) ? "equal" : "not equal"
```

When you see this strange setup, consider the question mark to be the divider. The stuff on the left of the question mark is usually put in parentheses, as shown in the following:

```cpp
(first == second)
```

This line actually compares first to second and determines whether they are equal. Yes, the code shows two equals signs. In C++, that’s how you test whether two things are equal. Now move to the part on the right of the question mark:

```cpp
"equal" : "not equal"
```

This is, itself, two pieces divided by a colon, so if first is indeed equal to second, result gets the string "equal". Otherwise, it gets the string "not equal". Take a look at the whole thing one more time:

```cpp
result = (first == second) ? "equal" : "not equal";
```

Once again, consider what it means: If first is equal to second, result gets "equal"; otherwise, it gets "not equal".

Remember that the storage bin on the left side of the single equals sign receives what is on the right side. The right side is an expression, which comes out to be a string of either "equal" or "not equal". The whole EqualityCheck example is shown in Listing 4-8.

## Boolean Variables and Conditional Operators

You can use Boolean variables with conditional operators. In a conditional operator such as

```cpp
result = (first == second) ? "equal" : "not equal";
```

the item `(first == second)` actually works out to be a Boolean value — either true or false. Therefore, you can break up this code into several lines. Even though breaking something into several lines seems a little backward, developers do it all the time. The reason for breaking code into lines is that sometimes, when you are programming, you may have an expression that is extremely complex — much more complex than `first == second`. As you grow in your C++ programming ability, you start to build more complex expressions and then start to realize just how complex they can become. Often, breaking expressions into multiple smaller pieces is more manageable. To break this example into multiple lines, you can do this (as shown in the `EqualityCheck2` example):

```cpp
string result;
bool isequal;
isequal = (first == second);
result = isequal ? "equal" : "not equal";
```

The second line declares a Boolean variable called `isequal`. The third line sets it to the value `first == second`. In other words, if `first` is equal to `second`, then `isequal` gets the value true. Otherwise, `isequal` gets the value false. In the fourth line, `result` gets the value `"equal"` if `isequal` is true; or `result` gets the value `"not equal"` if `isequal` is false.

The reason that this code works is that the item on the left side of the question mark is a *Boolean expression*, which is just a fancy way of saying that the code requires a Boolean value. Therefore, you can throw in a Boolean variable if you prefer, because a *Boolean variable* holds a *Boolean value*.

When you print the value of a Boolean variable by using code like this:

```cpp
cout << finished << endl;
```

you see either a `1` for true or a `0` for false. The reason is that, deep down inside, the computer stores a `1` to represent true and a `0` to represent false.

## Reading from the Console

Throughout this chapter and the preceding chapter, you see many examples of how to write information to the console. But just writing information is sort of like holding a conversation where one person does all the talking and no listening. Getting some feedback from the users of your applications would be nice. Fortunately, getting feedback is easy in C++. Writing to the console involves the use of `cout` in a form like this:

```cpp
cout << "hi there" << endl;
```

Reading from the console (that is, getting a response from the user of your application) uses the `cin` object. (It’s pronounced “see-in”.) Next, instead of using the goofy-looking `<<` operator, you use the equally but backwardly goofy `>>` operator.

![](img/128ab511de4e7360e167e3b15cdd5dd0_121_0.png)

The `<<` operator is often called an *insertion operator* because you are writing to (or *inserting into*) a stream. A *stream* is nothing more than a bunch of characters going out somewhere. In the case of `cout`, those characters are going out to the console. The `>>` operator, on the other hand, is often called the *extraction operator*. The idea here is that you are extracting stuff from the stream. In the case of `cin`, you are pulling letters from the stream that the user is, in a sense, sending into your application through the console.

The ReadString example, shown in Listing 4-9, demonstrates how you can read a string from the console.

### LISTING 4-9: Using the Conditional Operator to Make Comparisons

```cpp
#include <iostream>

using namespace std;

int main()
{
    string name;
    cout << "Type your name: ";
    cin >> name;
    cout << "Your name is " << name << endl;
    return 0;
}
```
