```
```cpp
cout << "Line 12: isEqual = " << isEqual << endl; //Line 12

greater<string> greaterStr;                          //Line 13

string str1 = "Hello";                               //Line 14
string str2 = "There";                               //Line 15

if (greaterStr(str1, str2))                           //Line 16
    cout << "Line 17: \"" << str1 << "\" is "
         << "greater than \"" << str2
         << "\"" << endl;                            //Line 17
else                                                   //Line 18
    cout << "Line 19: \"" << str1 << "\" is "
         << "not greater than \"" << str2
         << "\"" << endl;                            //Line 19

int temp[8] = {2, 3, 4, 5, 1, 7, 8, 9};              //Line 20

vector<int> vecList(temp, temp + 8);                  //Line 21
vector<int>::iterator intItr1, intItr2;              //Line 22
ostream_iterator<int> screen(cout, " ");             //Line 23

cout << "Line 24: vecList: ";                        //Line 24
copy(vecList.begin(), vecList.end(), screen);        //Line 25
cout << endl;                                         //Line 26

intItr1 = adjacent_find(vecList.begin(),
                        vecList.end(),
                        greater<int>());              //Line 27

intItr2 = intItr1 + 1;                                 //Line 28

cout << "Line 29: In vecList, the first set of "
     << "out-of-order elements is: " << *intItr1
     << " " << *intItr2 << endl;                      //Line 29
cout << "Line 30: In vecList, the first out-of-"
     << "order element is at position "
     << vecList.end() - intItr2 << endl;               //Line 30

return 0;                                              //Line 31
}                                                      //Line 32
```
```

# Sample Run:

Line 12: isEqual = 1
Line 19: "Hello" is not greater than "There"
Line 24: vecList: 2 3 4 5 1 7 8 9
Line 29: In vecList, the first set of out-of-order elements is: 5 1
Line 30: In vecList, the first out-of-order element is at position 4