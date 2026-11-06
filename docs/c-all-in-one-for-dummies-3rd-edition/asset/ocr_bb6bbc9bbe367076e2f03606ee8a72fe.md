# Listing 1-1 (continued)

```
```cpp
    cout << "first: " << first << endl;
    cout << "middle: " << middle << endl;
    cout << "last: " << last << endl;
    cout << endl;
}

int main()
{
    string name;

    name = "   Washington, George Zeus   ";
    ProcessName(name);

    name = "Washington, George Z.";
    ProcessName(name);

    name = "George Z. Washington";
    ProcessName(name);

    name = "George Zeus Washington";
    ProcessName(name);

    name = "George Washington";
    ProcessName(name);

    return 0;
}
```
```

Listing 1-1 is rather bug-proof, but it still does not handle some situations properly. For example, if somebody tries to process a string with a middle name, such as *Zeus*. (notice the period after the name), the application does not remove the period. But is that correct? Who knows, but people don’t normally format names that way. And so here are some improvements you might make to this application:

+   - **Eliminate improper characters:** You might make sure that no improper characters appear in the names. We would probably do this after we found the first, middle, and last names; that way, we wouldn’t kill the attempt to find the data based on the presence of a single comma that might be needed to specify the name order. You can use various if statements to do this kind of thing.
+   - **Handle more names than three:** We would probably add a special precaution for the case of more than three names. Some people have lots of names (like 10 or 11, especially if they’re members of British royalty). But if this application is to be used, for example, in an oil change operation, we don’t think you’ll see Charles Philip Arthur George, Prince of Wales coming through (although it’s possible). And so, as usual, how you handle the names depends on your particular situation.
+   - **Perform initial processing:** We would also do some initial processing. Right after the user enters the names, we would make sure that the names are not empty strings — that is, “ ” (one pair of quotation marks with no space between them).