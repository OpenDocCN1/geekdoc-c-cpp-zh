```
```cpp
cout << "Line 19: list after a call to "
     << "for_each function:\n        ";                 //Line 19
copy(list, list + 7, screenout);                         //Line 20
cout << endl;                                             //Line 21

return 0;
}

void doubleNum(int& num)
{
    num = 2 * num;

    cout << num << " ";
}
```
```

# Sample Run:

```
```text
Line 4: cList: a b c d e
Line 8: cList after changing all lowercase letters to
         uppercase: A B C D E
Line 13: list: 2 8 5 1 7 11 3
Line 16: The effect of for each function:
         4 16 10 2 14 22 6
Line 19: list after a call to for_each function:
         4 16 10 2 14 22 6
```
```

The statement in Line 7 uses the function transform to change every lowercase letter of charList into its uppercase counterpart. The statement in Line 9 outputs the elements of charList. In the output, the line marked Line 8 contains the output of the statements in Lines 8 through 10 in the program. Note that the fourth parameter of the function transform (in Line 7) is the function toupper from the header file cctype.

The statement in Line 17 calls the function for_each to process each element in the list using the function doubleNum. The function doubleNum has a reference parameter, num, of type int. Moreover, this function doubles the value of num and then outputs the value of num. Because num is a reference parameter, the value of the actual parameter is changed. In the output, the line marked Line 16 contains the output produced by the cout statement in the function doubleNum, which is passed as the third parameter of the function for_each (see Line 17). The statement in Line 20 outputs the values of the elements of list. In the output, Line 19 contains the output of the statements in Lines 19 through 20.