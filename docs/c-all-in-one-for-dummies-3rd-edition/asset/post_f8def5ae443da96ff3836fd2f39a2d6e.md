
Notice that, in this line, we have covered two of the three aspects of variables: We have given the variable a name, and we have told the computer what type of thing we want the variable to hold. The order seems a little odd — in C++, we first say the type and then the name. That’s just the way it’s done in C++, and a good reason stands behind it, which you can read about in “Naming multiple variables,” later in this chapter.

The next line looks like this:

```cpp
mynumber = 10;
```

This line puts something in the variable. It puts the number 10 in it. Because we already said that the variable can hold an integer, you’re allowed to put in a 10 because it is an integer. If you had tried to put something other than an integer in the variable, the compiler would have given you an error. The compiler makes sure that you put into a variable only the type of thing that you said you would. The compiler is good at keeping you in line. And of course you noticed that the statement ends with a semicolon. In C++, every statement ends with a semicolon.

![](img/6ba99460b0feb3585671a4612ff5fabb_67_0.png)

To put something in a variable, you type the variable’s name, an equal sign (surrounded by optional spaces), and the value. You then end the line with a semicolon. This line of code is an assignment. Or you can say that you are setting the variable to the value.

The next line is this:

```cpp
cout << mynumber << endl;
```

Book I, Chapter 2 describes what this line does. It’s a cout statement, which means that it writes something on the console. As you can probably guess, this code tells the computer to write the value of mynumber on the console. It does not write the string mynumber. Rather, it writes whatever happens to be stored in the storage bin. The previous line of code puts a 10 in the storage bin, and so this line prints a 10 on the console. When you run the application, you see this:

```
10
```

![](img/6ba99460b0feb3585671a4612ff5fabb_67_1.png)

Think of it like this: When you type the variable’s name, you are accessing the variable. The exception to this is when the variable’s name appears to the left of an equal sign. In that case, you are setting the variable.

You can do two things with a variable:

- **Set the variable:** You can set a variable, which means that you can put something inside the storage bin.
- **Retrieve the value:** You can get back the value that is inside the variable. When you do so, the value stays inside it; you are not, so to speak, *taking it out*.

![](img/6ba99460b0feb3585671a4612ff5fabb_68_0.png)

When you retrieve the value that is in a variable, you are not removing it from the variable. The value is still inside the variable.

## Book 1, Chapter 3: Storing Data in C++

### Declaring multiple variables

Many years ago, when we first learned the original C programming language (which was the language that served as the predecessor to C++), we thought it odd that we had to first say the type of the variable and then the name. But this actually works out well because it makes declaring multiple variables of the same type easy. If you want to declare three integer variables in a row, you can do it all in one shot, like this:

```cpp
int tom, dick, harry;
```

This statement declares three separate variables. The first is called tom; the second is called dick; and the third is called harry. Each of these three variables holds an integer. You have not put anything in any of them, so you may follow that with some code to stuff each of them full with a number. For example, this code puts the number 10 in tom, the number 20 in dick, and the number 3254 in harry.

```cpp
tom = 10;
dick = 20;
harry = 3254;
```

![](img/6ba99460b0feb3585671a4612ff5fabb_68_1.png)

When you run your applications, the computer executes the statements in the order that they appear in your code. Therefore, in the preceding code, the computer first creates the three storage bins. Then it puts a 10 inside tom. (Now doesn't that sound yummy?) Next, dick gets a 20. And finally, harry consumes a 3254.

### Changing values

Although a variable can hold only one thing at a time, you can still change what the variable holds. After you put something else in a variable, it forgets what it originally had. So when people accuse us of being forgetful, we can just say, 'Yes, but you should see that computer we work with all day long!'

You put something new in the variable in the same way you originally put something in it.

Look closely at the code for the `ChangeVariable` example in Listing 3-2. Notice that the first part of the application is just like Listing 3-1. But then we added two more lines (shown in bold) that look pretty much like the previous two: The first one sticks something (20) in the same variable as before, and the next one writes this new value out to the console.

**Listing 3-2: Changing a Variable**

```cpp
#include <iostream>

using namespace std;

int main()
{
    int mynumber;
    mynumber = 10;
    cout << mynumber << endl;
    mynumber = 20;
    cout << mynumber << endl;
    return 0;
}
```

As before, the line where you put something new in the variable follows the same format: There’s an equal sign, with the variable on the left and the new value on the right. As described earlier in this chapter, this statement is an *assignment* statement.

When you see a single equal sign by itself, the item on the left side is the variable or item that receives the information that is on the right side.

![](img/6ba99460b0feb3585671a4612ff5fabb_69_0.png)

### Setting one variable equal to another

Because you can do only two direct things with variables — put something in and retrieve the value — setting one variable equal to another is a simple process of retrieving the value of one variable and putting it in the other. This process is often referred to as *copying* the variable from one to another.

For example, if you have two integer variables — say, `start` and `finish` — and you want to copy the value of `start` into `finish`, you would use a line of code like the following:

```cpp
finish = start;
```

Don’t let the language confuse you. Although we said “copy the value of `start` into `finish`,” notice that the first thing we typed was `finish`, and then the equal sign, and then `start`. The left side of the equal sign is what *receives* the value; it is an *assignment* statement.

![](img/6ba99460b0feb3585671a4612ff5fabb_69_1.png)

When you copy the value of one variable to another, the two variables must be the same type. You cannot, for instance, copy the value from a string variable into an integer variable. If you try, the compiler issues an error message and stops.

![](img/6ba99460b0feb3585671a4612ff5fabb_69_2.png)

After the computer runs this copy statement, the two variables hold the same thing. The code for `CopyVariable`, shown in Listing 3-3, is an example of copying one variable to another.

**Listing 3-3: Copying a Value from One Variable to Another**

```cpp
#include <iostream>

using namespace std;

int main()
{
    int start = 50;
    int finish;
    finish = start;
    cout << finish << endl;
    return 0;
}
```

### Initializing a variable

When you create a variable, it starts out as an empty storage bin. Before it can be of much use, you need to put something in it.

![](img/6ba99460b0feb3585671a4612ff5fabb_70_0.png)

If you try to retrieve the contents of a variable before you actually put anything in it, you end up with what computer people fondly call “unpredictable results.” What they really mean to say is, “Don’t do this because who knows what’s in it.” It’s kind of like if you go in the attic and you discover that the former owners left behind a big, ominous box. Do you *really* want to look inside it? With variables, the problem you run into is that the computer memory has something stored in that particular place where the variable now sits, and that stored item is probably just some number left over from something else. But you can’t know in advance what it is. So always make sure that you place a value inside a variable before you try to retrieve its contents, a process called *initializing the variable*.

You can initialize a variable in two ways. The first way is by declaring the variable and then assigning something into it, which takes two lines of code:

```cpp
int mynumber;
mynumber = 153;
```

But the other way is a bit quicker. It looks like this:

```cpp
int mynumber = 153;
```

This method combines both strategies into one neat little package that is available for you to use whenever you want. You see us initializing variables both ways in this book, depending on how we feel at the moment.

### Creating a great name for yourself

Every variable needs to have a name. But what names can you use? Although you are free to use names such as Fred or Zanzibar or Supercount1000M, there are limits to what you are allowed to use.
