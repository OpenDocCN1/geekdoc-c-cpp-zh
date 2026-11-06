```
```cpp
Duck d8 = {"Ornery", 8, 8};
extras.push_back(d8);

Duck d9 = {"Goofy", 8, 8};
extras.push_back(d9);

cout << "**********" << endl;
cout << "extras:" << endl;
DumpDucks(extras);

list<Duck>::iterator first =
    MoveToPosition(extras, 1);

list<Duck>::iterator last =
    MoveToPosition(extras, 3);

list<Duck>::iterator into =
    MoveToPosition(inarrow, 2);

inarrow.splice(into, extras, first, last);

cout << "**********" << endl;
cout << "extras after splice:" << endl;
DumpDucks(extras);

cout << "**********" << endl;
cout << "inarrow after splice:" << endl;
DumpDucks(inarrow);

    return 0;
}
```
```

We made a function, MoveToPosition(), that moves to a position in the list. This may seem counterproductive because the list template doesn't allow random access. But we needed three iterators to perform the splice: Two to target the start and end position of the second list (the one we're splicing members from) and one to target the position in the first list where we want to put the spliced members. For that last bit of business, we needed the third iterator, which MoveToPosition() finds for us.

The function we created, MoveToPosition(), is a template function. But when we called the function, we didn't provide the typename in angle brackets. The compiler can figure out which class version we need; the compiler knows that it can look at what we pass into the function as a parameter and use its type to decide the template parameter. (Without the template type in the function parameter, the compiler can't figure it out.) Here's the application output:

![](bbox=[0.092, 0.638, 0.203, 0.711])

Book IV

Chapter 6

Programming with the Standard Library

```
```
----------------
(Sneaky,12,13)
(Trumper,19,26)
(Squoke,13,25)
(Sally,15,15)
(Jim,20,15)
```
```