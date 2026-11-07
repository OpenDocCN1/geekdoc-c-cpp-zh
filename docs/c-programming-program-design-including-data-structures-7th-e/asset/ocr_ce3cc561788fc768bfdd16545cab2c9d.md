```
cout << "Line 4: After first cin.get(ch); "
     << "ch = " << ch << endl;                 //Line 4

cin.get(ch);                                      //Line 5
cout << "Line 6: After second cin.get(ch); "
     << "ch = " << ch << endl;                 //Line 6

cin.putback(ch);                                  //Line 7
cin.get(ch);                                      //Line 8
cout << "Line 9: After putback and then "
     << "cin.get(ch); ch = " << ch << endl;    //Line 9

ch = cin.peek();                                  //Line 10
cout << "Line 11: After cin.peek(); ch = "
     << ch << endl;                               //Line 11

cin.get(ch);                                      //Line 12
cout << "Line 13: After cin.get(ch); ch = "
     << ch << endl;                               //Line 13

return 0;
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 1: Enter a string: abcd

Line 4: After first cin.get(ch); ch = a
Line 6: After second cin.get(ch); ch = b
Line 9: After putback and then cin.get(ch); ch = b
Line 11: After cin.peek(); ch = c
Line 13: After cin.get(ch); ch = c
```

The user input, abcd, allows you to see the effect of the functions get, putback, and peek in the preceding program. The statement in Line 1 prompts the user to enter a string. In Line 2, the statement `cin.get(ch);` extracts the first character from the input stream and stores it in the variable ch. So after Line 2 executes, the value of ch is 'a'.

The cout statement in Line 4 outputs the value of ch. The statement `cin.get(ch);` in Line 5 extracts the next character from the input stream, which is 'b', and stores it in ch. At this point, the value of ch is 'b'.

The cout statement in Line 6 outputs the value of ch. The `cin.putback(ch);` statement in Line 7 puts the previous character extracted by the get function, which is 'b', back into the input stream. Therefore, the next character to be extracted from the input stream is 'b'.

The `cin.get(ch);` statement in Line 8 extracts the next character from the input stream, which is still 'b', and stores it in ch. Now the value of ch is 'b'. The cout statement in Line 9 outputs the value of ch as 'b'.

In Line 10, the statement `ch = cin.peek();` checks the next character in the input stream, which is 'c', and stores it in ch. The value of ch is now 'c'. The cout statement in Line