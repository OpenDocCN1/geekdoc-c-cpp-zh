```
// Prompt user for input
cout << "Enter the floating point rate of pay "
     << "and hours worked: ";
cin >> rate >> hours;
cout << "Enter the employee's integer id: ";
cin >> id;
cout << "Enter the tax code (h,r,l): "
cin >> code;
cout << rate << endl << hours << endl
     << id << endl << code << endl;
return 0;
}
```

If the input stream from the keyboard contained the three lines of input

```
10.5 40
556
r
```

the objects in the input statement would be assigned values as shown in the following memory snapshot:

| double rate | 10.5 | double hours | 40 |
|---|---|---|---|
| int id | 556 | char code | 'r' |

The cout statement would print the following output to the screen:

```
10.5
40
556
r
```

The >> operator discards whitespace and interprets the input value according to the data type of the identifier that follows. For some applications requiring character data, it may not be desirable to discard whitespace. The function get() is a member function of the istream class and can be called by cin to get a single character from the input stream. The statements

```
char ch;
cin.get(ch);
```

will read the next character from the keyboard and assign the character to variable ch. The get() function does not discard whitespace, but rather treats whitespace as valid character data, as illustrated in the following example:

```
char ch1, ch2, ch3;
cout << "Enter three characters: ";
cin.get(ch1);
cin.get(ch2);
cin.get(ch3);
cout << ch1 << ch2 << ch3;
```

If the input stream from the keyboard contained the two lines

```
a
1
```