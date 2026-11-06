# **Listing 3-3: Copying a Value from One Variable to Another**

```
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
```

# **Initializing a variable**

When you create a variable, it starts out as an empty storage bin. Before it can be of much use, you need to put something in it.

![](bbox=[0.112, 0.423, 0.212, 0.491])

If you try to retrieve the contents of a variable before you actually put anything in it, you end up with what computer people fondly call “unpredictable results.” What they really mean to say is, “Don’t do this because who knows what’s in it.” It’s kind of like if you go in the attic and you discover that the former owners left behind a big, ominous box. Do you *really* want to look inside it? With variables, the problem you run into is that the computer memory has something stored in that particular place where the variable now sits, and that stored item is probably just some number left over from something else. But you can’t know in advance what it is. So always make sure that you place a value inside a variable before you try to retrieve its contents, a process called *initializing the variable*.

You can initialize a variable in two ways. The first way is by declaring the variable and then assigning something into it, which takes two lines of code:

```
```cpp
int mynumber;
mynumber = 153;
```
```

But the other way is a bit quicker. It looks like this:

```
```cpp
int mynumber = 153;
```
```

This method combines both strategies into one neat little package that is available for you to use whenever you want. You see us initializing variables both ways in this book, depending on how we feel at the moment.

# **Creating a great name for yourself**

Every variable needs to have a name. But what names can you use? Although you are free to use names such as Fred or Zanzibar or Supercount1000M, there are limits to what you are allowed to use.