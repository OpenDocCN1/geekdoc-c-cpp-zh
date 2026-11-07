```
```cpp
generate(vecList.begin(), vecList.end(), nextNum);  //Line 11

cout << "Line 12: vecList after filling with "
     << "numbers: ";                              //Line 12

copy(vecList.begin(), vecList.end(), screen);       //Line 13
cout << endl;                                        //Line 14

generate_n(vecList.begin(), 3, nextNum);            //Line 15

cout << "Line 16: vecList after filling the "
     << "first three elements" << endl
     << "    with the next number: ";               //Line 16

copy(vecList.begin(), vecList.end(), screen);       //Line 17
cout << endl;                                        //Line 18

return 0;                                           //Line 18
}                                                    //Line 19

int nextNum()                                        //Line 20
{
    static int n = 1;                                //Line 22

    return n++;                                      //Line 23
}                                                    //Line 24
```
```

# Sample Run:

Line 12: vecList after filling with numbers: 1 2 3 4 5 6 7 8
Line 16: vecList after filling the first three elements
    with the next number: 9 10 11 4 5 6 7 8

This program contains a value-returning function, nextNum, which contains a static variable n initialized to 1. A call to this function returns the current value of n and then increments the value of n. Therefore, the first call of nextNum returns 1, the second call returns 2, and so on.

The statements in Lines 9 and 10 declare vecList to be a sequence container of size 8 and screen to be an ostream iterator initialized to cout with the delimiter character space. The statement in Line 11 uses the function generate to fill vecList by successively calling the function nextNum. Notice that after the statement in Line 11 executes, the value of the static variable n of nextNum is 9. The statement in Line 13 outputs the elements of vecList. The statement in Line 15 calls the function generate_n to fill the first three elements of vecList by calling the function nextNum three times. The starting position is vecList.begin(), which is the first element of vecList, and the number of elements to be filled is 3, given by the second parameter of generate_n (see Line 15). The statement in Line 17 outputs the elements of vecList.