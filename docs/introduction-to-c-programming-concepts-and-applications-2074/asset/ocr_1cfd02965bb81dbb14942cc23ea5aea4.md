# STEP 2: NARROW

Now that you have an error that you can use to debug your program, the next step in the debugging process is to hone in on where the failure is occurring in the code. This is where the debugger in Visual Studio (on a PC) or Xcode (on a Mac) can come in handy.

A debugger can only help you follow what’s going on in the program; it’s not going to solve your issues for you or even tell you where the error occurred.

Your goal is to find the first line of the program that gives a result that’s incorrect. Usually, this will mean that some variable in memory has the wrong value.

![](bbox=[0.036, 0.5, 0.324, 0.621])

If you don’t have a debugger, you can always use output statements to print out data along the way.

To hone in on an error, you should start at a point in the program where you know everything is OK and one where you know things have gone wrong. In the worst case, that’ll be the first and last lines of the program! But in many cases, you have a better idea—often right before calling some new function you wrote and right after it.

Then, you’ll want to gradually narrow down the scope of the program where the error could be occurring. Pick another point in the program, somewhere between the last-known OK point and the first-known bad point and analyze whether the variables in memory are correct there. If everything looks good, then you can move your OK point to there. If there’s a problem at that point, then move your bad point to there. The goal is to narrow down the location of the error where things first go wrong as much as possible.

In this case, you know that things are good at the beginning of the program and that there’s a problem at the end, so you should check a point in the middle.

You could do this with just print statements by using a print-debug approach: inserting one line after the remove_spaces function has returned in order to output the result there.

```
19    string no_spaces =
    remove_spaces(s);
20    cout << "String with no spaces is:" << no_spaces << endl;
21    bool could_be_palindrome = true;
```

When you run the program, it appears that the data is correct to that point. This indicates that you did indeed read in the string and calling remove_spaces did not introduce any obvious errors. So, you can assume that up until that point, things are good.

You could likewise check the value that you are going to return right before returning. If you add another output line there, printing out the value you will return right before the return statement, you can check if the problem is before or after the return from the is_palindrome function.

```
26    cout << "About to return:" << could_be_palindrome<<endl
27    return could_be_palindrome;
```

Sure enough, when you run the program, it’s returning 0, or false, which is not correct. So, you know that things seem good before the for loop and are wrong afterward. You need to hone in further.