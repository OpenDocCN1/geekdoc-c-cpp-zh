```
// Try to find a box containing glasses
{
    foundBox = findBox(myBoxes, 5, "glasses");
}
catch(logic_error logErr) {
    cout << logErr.what() << endl; // Display error message to user
    foundBox = PlainBox<string>("nothing"); // Fix problem
} // end-catch
// Because we catch the exception and fix the problem, the following
// statement should work even if the target is not found
cout << foundBox.getItem();
```

Output
Target not found in a box!
nothing

# D3.4.1 Multiple catch Blocks

A single statement in a try block might cause more than one type of exception. Thus, a try block can have many catch blocks associated with it. When more than one catch follows a try block, the catch block that executes is the first—in order of appearance—parameter matches the thrown exception in type. Thus, the catch blocks must be ordered so the most specific exception classes are caught before the most general exception classes. For example, the following catch blocks are in the wrong order:

```
string str = "Sarah";
try {
    str.substr(9, 1);
    // <other statements appear here...>
}
catch (exception e) // WRONG ORDER!!
{
    cout << "Something else was caught" << endl;
}
catch (out_of_range e) {
    cout << "out_of_range exception caught" << endl;
} // end-catch
```

The compiler issues a warning message like the following:
'class std::out_of_range' is caught by base class ('class exception') on line n
This warning means that any out_of_range exception thrown in the try block will be caught by the first catch block—with the parameter of type exception—so the second catch block will never be reached. To get the code to compile without warnings, you must interchange the two catch blocks.