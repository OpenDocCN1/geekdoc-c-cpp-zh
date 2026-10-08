
errors, but it is not always easy to know what to do with an error once you catch it at run time. Consider:

```C
int area(int length, int width)        // calculate area of a rectangle
{
    return length*width;
}

int framed_area(int x, int y)           // calculate area within frame
{
    return area(x-2,y-2);
}

int main()
{
    int x = -1;
    int y = 2;
    int z = 4;
    // ...

    int area1 = area(x,y);
    int area2 = framed_area(1,z);
    int area3 = framed_area(y,z);
    double ratio = double(area1)/area3;  // convert to double to get
                                          // floating-point division
}
```

We used the variables **x, y, z** (rather than using the values directly as arguments) to make the problems less obvious to the human reader and harder for the compiler to detect. However, these calls lead to negative values, representing areas, being assigned to **area1** and **area2**. Should we accept such erroneous results, which violate most notions of math and physics? If not, who should detect the errors: the caller of area() or the function itself? And how should such errors be reported?

Before answering those questions, look at the calculation of the **ratio** in the code above. It looks innocent enough. Did you notice something wrong with it? If not, look again: **area3** will be **0**, so that **double(area1)/area3** divides by zero. This leads to a hardware-detected error that terminates the program with some cryptic message relating to hardware. This is the kind of error that you – or your users – will have to deal with if you don't detect and deal sensibly with run-time errors. Most people have low tolerance for such “hardware violations” because to anyone not intimately familiar with the program all the information provided is “Something went wrong somewhere!” That's insufficient for any constructive action, so we feel angry and would like to yell at whoever supplied the program.

So, let's tackle the problem of argument errors with **area()**. We have two obvious alternatives:

- a. Let the caller of **area()** deal with bad arguments.
- b. Let **area()** (the called function) deal with bad arguments.

### 5.5.1 The caller deals with errors

Let's try the first alternative (“Let the user beware!”) first. That's the one we'd have to choose if **area()** was a function in a library where we couldn't modify it. For better or worse, this is the most common approach.

Protecting the call of **area(x, y)** in **main()** is relatively easy:

```C
if (x<=0) error("non-positive x");
if (y<=0) error("non-positive y");
int area1 = area(x, y);
```

Really, the only question is what to do if we find an error. Here, we have called a function **error()** which we assume will do something sensible. In fact, in **std_lib_facilities.h** we supply an **error()** function that by default terminates the program with a system error message plus the string we passed as an argument to **error()**. If you prefer to write out your own error message or take other actions, you catch **runtime_error** (§5.6.2, §7.3, §7.8, §B.2.1). This approach suffices for most student programs and is an example of a style that can be used for more sophisticated error handling.

If we didn't need separate error messages about each argument, we would simplify:

```C
if (x<=0 || y<=0) error("non-positive area() argument");
int area1 = area(x, y);
```

To complete protecting **area()** from bad arguments, we have to deal with the calls through **framed_area()**. We could write

```C
if (z<=2)
    error("non-positive 2nd area() argument called by framed_area()");
int area2 = framed_area(1, z);
if (y<=2 || z<=2)
    error("non-positive area() argument called by framed_area()");
int area3 = framed_area(y, z);
```

This is messy, but there is also something fundamentally wrong. We could write this only by knowing exactly how **framed_area()** used **area()**. We had to know that **framed_area()** subtracted **2** from each argument. We shouldn't have to know such details! What if someone modified **framed_area()** to use **1** instead of **2**? Someone doing that would have to look at every call of `framed_area()` and modify the error-checking code correspondingly. Such code is called “brittle” because it breaks easily. This is also an example of a “magic constant” (§4.3.1). We could make the code less brittle by giving the value subtracted by `framed_area()` a name:

```C
constexpr int frame_width = 2;

int framed_area(int x, int y)    // calculate area within frame
{
    return area(x-frame_width, y-frame_width);
}
```

That name could be used by code calling `framed_area()`:

```C
if (1-frame_width<=0 || z-frame_width<=0)
    error("non-positive argument for area() called by framed_area()");
int area2 = framed_area(1,z);
if (y-frame_width<=0 || z-frame_width<=0)
    error("non-positive argument for area() called by framed_area()");
int area3 = framed_area(y,z);
```

Look at that code! Are you sure it is correct? Do you find it pretty? Is it easy to read? Actually, we find it ugly (and therefore error-prone). We have more than trebled the size of the code and exposed an implementation detail of `framed_area()`. There has to be a better way!

Look at the original code:

```C
int area2 = framed_area(1,z);
int area3 = framed_area(y,z);
```

It may be wrong, but at least we can see what it is supposed to do. We can keep this code if we put the check inside `framed_area()`.

### 5.5.2 The callee deals with errors

Checking for valid arguments within `framed_area()` is easy, and `error()` can still be used to report a problem:

```C
int framed_area(int x, int y)    // calculate area within frame
{
    constexpr int frame_width = 2;
    if (x-frame_width<=0 || y-frame_width<=0)
        error("non-positive area() argument called by framed_area()");
    return area(x-frame_width, y-frame_width);
}
```

This is rather nice, and we no longer have to write a test for each call of **framed_area()**. For a useful function that we call 500 times in a large program, that can be a huge advantage. Furthermore, if anything to do with the error handling changes, we only have to modify the code in one place.

Note something interesting: we almost unconsciously slid from the “caller must check the arguments” approach to the “function must check its own arguments” approach (also called “the callee checks” because a called function is often called “a callee”). One benefit of the latter approach is that the argument-checking code is in one place. We don’t have to search the whole program for calls. Furthermore, that one place is exactly where the arguments are to be used, so all the information we need is easily available for us to do the check.

Let’s apply this solution to **area()**:

```C
int area(int length, int width)        // calculate area of a rectangle
{
    if (length<=0 || width <=0) error("non-positive area() argument");
    return length*width;
}
```

This will catch all errors in calls to **area()**, so we no longer need to check in **framed_area()**. We might want to, though, to get a better – more specific – error message.

Checking arguments in the function seems so simple, so why don’t people do that always? Inattention to error handling is one answer, sloppiness is another, but there are also respectable reasons:

- **We can’t modify the function definition:** The function is in a library that for some reason can’t be changed. Maybe it’s used by others who don’t share your notions of what constitutes good error handling. Maybe it’s owned by someone else and you don’t have the source code. Maybe it’s in a library where new versions come regularly so that if you made a change, you’d have to change it again for each new release of the library.
- **The called function doesn’t know what to do in case of error:** This is typically the case for library functions. The library writer can detect the error, but only you know what is to be done when an error occurs.
- **The called function doesn’t know where it was called from:** When you get an error message, it tells you that something is wrong, but not how the executing program got to that point. Sometimes, you want an error message to be more specific.
- **Performance:** For a small function the cost of a check can be more than the cost of calculating the result. For example, that’s the case with **area()**, where the check also more than doubles the *size* of the function (that is,
