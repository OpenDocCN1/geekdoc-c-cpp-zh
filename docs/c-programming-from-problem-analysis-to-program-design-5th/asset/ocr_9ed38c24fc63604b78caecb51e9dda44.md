```
```cpp
cout << "The number you entered is " << num
     << endl;                                      //Line 4
switch(num)                                        //Line 5
{
case 0:                                            //Line 6
case 1:                                            //Line 7
    cout << "Learning to use ";                   //Line 8
case 2:                                            //Line 9
    cout << "C++'s ";                             //Line 10
case 3:                                            //Line 11
    cout << "switch structure." << endl;          //Line 12
    break;                                         //Line 13
case 4:                                            //Line 14
    break;                                         //Line 15
case 5:                                            //Line 16
    cout << "This program shows the effect ";     //Line 17
case 6:                                            //Line 18
case 7:                                            //Line 19
    cout << "of the break statement." << endl;    //Line 20
    break;                                         //Line 21
default:                                           //Line 22
    cout << "The number is out of range." << endl;//Line 23
}

cout << "Out of the switch structure." << endl;   //Line 24

return 0;                                          //Line 25
}
```
```

**Sample Runs:** These outputs were obtained by executing the preceding program several times. In each of these sample runs, the user input is shaded.

# **Sample Run 1:**

```
Enter an integer between 0 and 7: 0
The number you entered is 0
Learning to use C++'s switch structure.
Out of the switch structure.
```

# **Sample Run 2:**

```
Enter an integer between 0 and 7: 2
The number you entered is 2
C++'s switch structure.
Out of the switch structure.
```

# **Sample Run 3:**

```
Enter an integer between 0 and 7: 4
Out of the switch structure.
```