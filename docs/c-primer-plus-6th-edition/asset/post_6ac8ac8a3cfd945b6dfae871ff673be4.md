
# Chapter 8 Adventures in Functions

```cpp
set_pc(four);
// ill-advised assignment
accumulate(dup, five) = four;
std::cout << "Displaying dup after ill-advised assignment:\n";
display(dup);
return 0;
}

void display(const free_throws & ft)
{
    using std::cout;
    cout << "Name: " << ft.name << '\n';
    cout << "Made: " << ft.made << '\t';
    cout << "Attempts: " << ft.attempts << '\t';
    cout << "Percent: " << ft.percent << '\n';
}
void set_pc(const free_throws & ft)
{
    if (ft.attempts != 0)
        ft.percent = 100.0*float(ft.made)/float(ft.attempts);
    else
        ft.percent = 0;
}
```

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source)
{
    target.attempts += source.attempts;
    target.made += source.made;
    set_pc(target);
    return target;
}
```

Here is the program output:

Name: Ifelsa Branch
Made: 13 Attempts: 14 Percent: 92.8571
Name: Throwgoods
Made: 13 Attempts: 14 Percent: 92.8571
Name: Throwgoods
Made: 23 Attempts: 30 Percent: 76.6667
Name: Throwgoods
Made: 35 Attempts: 48 Percent: 72.9167
Displaying team:
Name: Throwgoods
Made: 41 Attempts: 62 Percent: 66.1290
Displaying dup after assignment:
Name: Throwgoods
Made: 41 Attempts: 62 Percent: 66.129
Displaying up after ill-advised assignment:
Name: Whily Looper
Made: 5 Attempts: 9 Percent: 55.5526

# Program Notes

The program begins by initializing several structure objects. Recall that if there are fewer initializers than many, the remaining members (just the percent members in this case) are set to 0. The first function calls this:

```cpp
set_pc(one);
```

Because the formal parameter ft in set_pc() is a reference, ft refers to one, and the code in set_pc() sets the one->percent member. Passing by value would not work in this case as that would result in setting the percent member of a temporary copy of one. The alternative, as you may recall from the previous chapter, is using a pointer parameter and passing the address, but the former is slightly more complicated:

```cpp
set_pc(&one);    // using pointers instead    &one instead of one
```

```cpp
void set_pc(free_throws * pt)
{
    if (pt->attempts != 0)
        pt->percent = 100.0f*float(pt->made)/float(pt->attempts);
    else
        pt->percent = 0;
}
```

The next function calls this:

```cpp
display(one);
```

Because display() displays the contents of the structure without altering them, the function uses a const reference parameter. In this case, one could have passed the structure by value, but using a reference is more economical in time and memory than making a copy of the original structure.
The next function calls this:

```cpp
accumulate(team, one);
```

The accumulate() function takes two structure arguments. It adds data from the attempts and made members of the second structure to the corresponding members of the first. Only the first structure is modified, so the first parameter is a reference, whereas the second parameter is a const reference:

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source);
```

# Chapter 8 Adventures in Functions

What about the return value? The function call we just discussed didn't use it; as far as we use, the function could have been type void. But look at this function call:

```cpp
display(accumulate(team, two));
```

What's going on here? Let's follow the structure object team. First, team is passed to accumulate() as its first argument. That means the target object in accumulate (really team). The accumulate() function modifies team, then it returns it as a reference. Note that the actual return statement looks like this:

```cpp
return target;
```

Nothing in this statement indicates that a reference is being returned. That information comes from the function header (and, also, from the prototype):
free_throws & accumulate(free_throws & target, const free_throws & source)

If the return type was declared free_throws instead of free_throws &, the same return statement would return a copy of target (and hence a copy of team). But the return type is a reference, so that means the return value is the original team object passed to accumulate().

What happens next? The accumulate() return value is the first argument to display(), so that means team is the first argument to display(). Because the display() parameter is a reference, that means the ft object in display() is really the team. Therefore, the contents of team get displayed. The net effect of

```cpp
display(accumulate(team, two));
```

is the same as that of the following:

```cpp
accumulate(team, two);
display(team);
```

The same logic applies to this statement:

```cpp
accumulate(team, three);
```

This has the same effect as the following:

```cpp
accumulate(team, three);
accumulate(team, four);
```

Next, the program uses an assignment statement:

```cpp
dup = accumulate(team, five);
```

As you might expect, this copies the values in team. Finally, the program uses accumulate() in a manner for which it was not intended:

```cpp
accumulate(dup, five) = four;
```

This statement—that is, assigning a value to a function call—works because the return value is a reference. The code won't compile if accumulate() returns by value. Because the return value is a reference to dup, this code has the same effect as the following:

```cpp
accumulate(dup, five); // add five's data to dup
dup = four; // overwrite the contents of dup with four
```

The second statement wipes the work accomplished by the first, so the assignment statement was not a good use of accumulate().

# Reference Variables

Let's look a bit further at why returning a reference is different from the traditional return mechanism. The latter works like passing by value parameters. The expression following the return is evaluated, and the value is passed back to the calling function. Conceptually, this value is copied to a temporary location and the program uses the value. Consider the following:

```cpp
double m = sqrt(4.0);
cout = sqrt(5.0);
```

In the first statement, the value 4.0 is copied to a temporary location and the value in that location is copied to m. In the second statement, the value 5.0 is copied to a temporary location, then the contents of that location are passed out (This is the conceptual description. In practice, an optimizing compiler might consolidate some of the steps). Now consider this statement:

```cpp
dup = accumulate(team, five);
```

If accumulate() returns a structure instead of a reference to a structure, this could involve copying the entire structure to a temporary location and then copying that copy of dup. With a reference return, team is copied directly to dup. A function that returns a reference is actually an alias for the variable.

# Being Careful About What Return Refers To

The single most important point to remember when returning a reference is to avoid returning a reference to a memory location that ceases to exist when the function terminates. What you want to avoid is code like these:

```cpp
free_throws clone(free_throws & ft)
{
    free_throws newguy; // first step to big
    guy = ft; // copy info
    return newguy; // return reference to copy
}
```

This has the unfortunate effect of returning a reference to a temporary variable (newguy) passes from existence as soon as the function terminates. (Chapter 9, "Memory Models and Namespaces," discusses the persistence of various kinds of variables.) Similarly, you should avoid returning pointers to such temporary variables.

The simplest way to avoid this problem is to return a reference that was passed as an argument to the function; reference will refer to data used by the calling function; however, the returned reference will refer to that same data. This, for example, is what accumulate() does in Listing 8.6.

A second method is to use new to create new storage. You've already seen examples in which new creates space for a string and the function returns a pointer to that. Here's how you could do something similar with a reference:

```cpp
const free_throws & clone(free_throws & ft)
{
    free_throws * pt;
    *pt = ft; // copy info
    return *pt; // return reference to copy
}
```

The first statement creates a nameless free_throws structure. The pointer pt points to the structure, so *pt is the structure. The code appears to return the structure, but the function declaration indicates that the function really returns a reference to this structure. You could then use the function this way:

```cpp
free_throws & jolly = clone(three);
```

This makes jolly a reference to the new structure. There is a problem with this approach: You use to delete memory allocated when the memory is no longer needed. A call to clone() conceals the call to new, making it simpler to forget to use delete later. The auto_ptr template or, better, the C++11 unique_ptr discussed in Chapter 16, "The String Class and the Standard Template Library," can help automate the deletion process.

# Why use with a Reference Return?

Listing 8.6, as you will recall, this statement:
accumulate(dup, five) = four;

It had the effect of first adding data from five to dup, overwriting the contents of dup with the contents of four. Why does this statement compile? Assignment requires a modifiable lvalue on the left. That is, the subexpression on the left should identify a block of memory that can be modified. In this case, the function returned a reference to dup, which does identify such a block of memory. So the statement is valid.

Regular (non reference) return types, the other hand, are values, values that can't be accessed by address. Such expressions can appear on the right side of an assignment statement but not the left. Other examples of rvalues include literals, such as 10.0, and expressions such as x + y. Clearly, it doesn't make sense to try to take the address of a literal as 10.0, but why is a normal function return value an rvalue? It's the return value, which you recall, resides in a temporary memory location that doesn't necessarily persist even until the next statement.
